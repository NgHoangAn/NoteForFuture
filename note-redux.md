# Redux

## what

    + library quản lý và update state, dùng các event là 'actions'
    + là 1 center store (state) có các quy tắc đảm bảo state chỉ có thể update theo cách dự đoán được

## why

    + quản lý global state
    + các pattern và tool giúp dễ hiểu hơn khi nào, ở đâu, tạo sao và cách state update như thế nào

## when

    + xử lí việc quản lý state
    + có nhiều state cần ở nhiều nơi
    + state update theo thời gian
    + logic update phức tạp

# redux terms and concepts

## state management

    state: state tại thời điểm cụ thể
    view: UI dựa trên state
    action: dựa trên action của user

    one-way-data flow:
        state -> view -> action -> state -> ...
            khi có nhiều component cần share và used cùng 1 state [component nằm ở các component khác nhau] -> dùng lifting-state-up cho các main component

            => solution: trích xuất state được share từ các component và đặt nó vào 1 vị trí center ở bên ngoài component tree. component tree trở thành big view và bất kì component nào cũng có thể truy cập state or trigger action

## immutability

    + ko thể bị thay đổi
    + object và array default là mutable
    + để update object or array mà cho chúng tính immutability thì copy ra rồi update

## actions

    const actionEvent = {
        type: 'todos/todoAdded',
        payload: 'Buy something'
    }
    + mô tả event nào đó
        + type: string [domain/eventName]
        + payload: info what happen on action

## action creator

    + fn tạo và return action object
        const addTodos = text => {
            return {
                type: 'todos/todoAdded',
                payload: text
            }
        }
    + tái sử dụng actions (gán action vào 1 biến và gọi khi cần)

## reducer

    + reducer(InitialState, action) => newState
    + xử lý event khi nhận loại action

    RULE:
        + chỉ nên calculate newState dựa tên state và action
        + ko được phép sửa state đã tồn tại => immutable update by copy state[sao chép state hiện có và thực hiện thay đổi trên bản copy]
        + ko async logic, tính toán random, thực hiện side effect

    logic fn
        check reducer có cares action này ko
            if có, copy state và update copy state and return it
            if ko, return state cũ
        fn reducer(state, action){
            if(action.type === 'counter/increment'){
                return {
                    ...state,
                    value: state.value + 1
                }
            }
            return state
        }

    array.reduce xảy ra cùng lúc
    redux, reducer xảy ra all lifetime app

    + reducer never allow mutate original/ current state

## store

    + nơi chứa state

```javascript
import { configureStore } from "@reduxjs/toolkit";
const store = configureStore({ reducer: counterReducer });
console.log(store.getState());
// {value: 0}
```

## dispatch

    + cách duy nhất để update state là gọi store.dispatch() và truyền vào action object
    + reducer chạy và save [newState] -> call getState để lấy value update

```javascript
store.dispatch({ type: "counter/increment" });
console.log(store.getState());
// { value: 1}
```

    + dispatch action giống như trigger[kích hoạt] event

## selectors

    + là các fn biết cách extract info cụ thể từ value state của store

```javascript
const selectCounterValue = (state) => state.value;
const currentValue = selectCounterValue(store.getState());
console.log(currentValue);
```

# Data flow

    'one way flow'
        + state mô tả condition của app tại thời điểm cụ thể
        + UI render với state mặc định
        + khi có event -> state được update
        + UI render với newState

    redux flow
        + init setup
            + redux store create với root reducer fn
            + store call reducer once, save value [init state]
            + UI render lần đầu, UI chấp nhận current state [quyết định render cái gì]. subscribe nhận bất kì store update để biết state có thay đổi hay ko

        + update
            when something happen
                + dispatch action đến store
                + store run reducer[prevState, current action] save-> return value newState
                + store thông báo với all UI đã subscribe rằng store đã update
                + UI[cần data từ store] check xem data nó cần có thay đổi hay ko
                    if data thay đổi thì re-render[new data] -> update screen

# NOTE Part 1

    + redux là library quản lý global state
        + dùng với react-redux
        + redux toolkit dùng để viết logic redux
    + redux dùng 'one-way-data flow'
    + type of code
        + action
        + reducers
        + store run root reducer bất cứ khi nào action dispatched

# redux app

## create redux store

```javascript
import { configureStore } from "@reduxjs/toolkit";
import counterReducer from "../features/counter/counterSlice";
export default configureStore({
  reducer: {
    counter: counterReducer,
  },
});
```

    // counterReducer fn quyết định và cách update state.counter bất cứ khi nào khi 1 action được dispatch

## redux slice

    slice : collection reducer action and logic, name tạo ra từ việc splitting up [root state object] into multi slices state

```javascript
    export default configureStore({
        reducer: {
            users: usersReducer,
            posts: postReducer,
            ...
        }
    })
```

    + 1 store cần có root reducer được truyền vào khi nó được tạo.
    + if có nhiều slide reducer fn:

```javascript
    fn rootReducer(state = {}, action){
        return {
            users: usersReducer(state.users, action)
            ....
        }
    }
```

        => dùng combineReducers: nhận vào 1 object chứa full slide -> return fn gọi slice khi có action dispatch -> all result từ slice được combine lại với nhau thành 1 object duy nhất làm final result

```javascript
    const rootReducer = combineReducers({
        users: usersReducer,
        ...
    })
    // pass vào store
    const store = configureStore({
        reducer: rootReducer
    })
```

## create slide and action

    + createSlide: tạo string action, action creator fn, action object
        + name: tên slide
        + reducer: action
            [type: 'name/reducer']
        + initState:

```javascript
export const counterSlide = createSlide({
    name:'counter',
    initState:{
        value: 0
    },
    reducers{
        increment: state => { state.value += 1 },
        decrement: state => { state.value -= 1 },
        incrementByAmount: (state,action) => { state.value += action.payload }

    }
})
```

    + createSlice auto tạo các action creator cùng tên với reducer

```javascript
console.log(counterSlide.action.increment());
// { type: 'counter/increment' }
```

    + chỉ có thể viết mutate logic tong createSlice and createReducer

## write async with thunk

    + thunk là redux fn có thể chứa async logic
        + inside thunk fn, lấy dispatch và getState làm argument
        + outside creator fn, create and return thunk fn

```javascript
export const incrementAsync = (amount) => (dispatch) => {
  setTimeout(() => {
    dispatch(incrementByAmount(amount));
  }, 1000);
};

store.dispatch(incrementAsync(5));
```

```javascript
//outside 'thunk creator' fn
const fetchUserById = (userId) => {
  // inside 'thunk fn'
  return async (dispatch, getState) => {
    try {
      const user = await userAPI.fetchById(userId);
      dispatch(userLoaded(user));
    } catch (err) {}
  };
};
```

```javascript
const thunkMiddleware =
  ({ dispatch, getState }) =>
  (next) =>
  (action) => {
    if (typeof action === "function") {
      return action(dispatch, getState);
    }
    return next(action);
  };
```

## read data with useSelector

    + component có thể extract bất kì data nào từ store state
    + đảm nhận talk với store

## dispatch action with useDispatch

## provider the store

```javascript

```

# combineReducer

    + biến object có value là các fn reducing khác nhau thành 1 fn reducing và có thể pass to createStore[https://redux.js.org/api/createstore]

```javascript
rootReducer = combineReducers({
  potato: potatoReducer,
  tomato: tomatoReducer,
});
```

    + RULE:[reducer pass to combineReducers]
        + https://redux.js.org/api/combinereducers
    + exp

```javascript
reducers/todos.js
export default function todos(state = [], action) {
  switch (action.type) {
    case 'ADD_TODO':
      return state.concat([action.text])
    default:
      return state
  }
}

reducers/counter.js
export default function counter(state = 0, action) {
  switch (action.type) {
    case 'INCREMENT':
      return state + 1
    case 'DECREMENT':
      return state - 1
    default:
      return state
  }
}

reducers/index.js
import { combineReducers } from 'redux'
import todos from './todos'
import counter from './counter'

export default combineReducers({
  todos,
  counter
})

App.js
import { createStore } from 'redux'
import reducer from './reducers/index'

const store = createStore(reducer)
console.log(store.getState())
// {
//   counter: 0,
//   todos: []
// }

store.dispatch({
  type: 'ADD_TODO',
  text: 'Use Redux'
})
console.log(store.getState())
// {
//   counter: 0,
//   todos: [ 'Use Redux' ]
// }

```
# store
redux store : lưu trữ state của app

state read-only
cách duy nhất để update state là emit[bắn] ra 1 action với object mô tả những gì xảy ra
action luôn có 1 type mô tả hành động
dispatch một action: chuyển action đến reducer để lấy về state mới

tạo redux store [quản lý state]

```javascript
import { createStore } from "redux";
const store = createStore();
// khi tạo 1 store với createStore thì có 3 hàm để dùng
//  getState: luôn trả về state hiện tại
```

- Redux là một container chứa state có thể dự đoán được, dành cho các ứng dụng Javascript.
- Hàm createStore của Redux là hàm factory được dùng để tạo ra một STORE
- Reducer là tham số yêu cầu duy nhất cần truyền vào hàm createStore()
- Reducer chỉ là một hàm, nhận HAI tham số. Tham số đầu tiên là STATE của ứng dụng, và một tham số là ACTION
- Một Reducer luôn luôn trả về state mới của ứng dụng
  State khởi tạo của ứng dụng được gọi là initialState và có thể tuỳ chọn truyền vào tham số thứ 2 khi gọi hàm createStore
- Store.getState() sẽ trả về state hiện tại của ứng dụng. (trong đó STORE là một STORE của Redux)

action
{
type: '',
payload:{}
}

define initialState

    const initialState = {
        value: 0
    }

define reducer [counterReducer]

    function couterReducer(state, action){
        switch(action.type){
            case 'counter/incremented':
                return {...state, value:state.value + 1}
            ....
            default:
                return state
        }
    }

create Store

    const store = Redux.createStore(counterReducer)

in UI
function render(){
const state = store.getState()
}

    render()
    store.subscribe(render) // [gọi mỗi khi store thay đổi][truyền vào render để update UI mỗi khi store update
    ]

dispatch action

    store.dispatch({ type: 'counter/decremented})

data flow
action send
store run reducer -> new state
new state -> UI

NOTE 1:
redux: library manage global state
action:
reducer: tính toán state mới dựa trên old state + action
store: run root reducer khi actions dispatch

===============================================
state management
state
view
action

    one-way data flow
        state là current State
        UI render [current State]
        when actions, update state-> new state
        UI re-render [ref: newState]

        khi có multi component share and used one state [thường dùng lifiting state up]

actions
hành động là một sự kiện mô tả điều gì đó đã xảy ra trong ứng dụng

    const add = {
        type: domain/eventName
        payload
    }

reducers
(state, action) => newState

    tính toán giá trị trạng thái mới dựa trên các đối số 'state và action'

    không được phép sửa đổi tệp state [cập nhật bất biến bằng cách sao chép giá trị hiện có statevà thực hiện các thay đổi đối với giá trị đã sao chép]

    không được thực hiện bất kỳ logic không đồng bộ nào, tính toán các giá trị ngẫu nhiên hoặc gây ra "tác dụng phụ" khác

    step
        if(Kiểm tra xem bộ giảm tốc có quan tâm đến hành động này không)
            tạo một bản sao của trạng thái, cập nhật bản sao với các giá trị mới và gửi lại
        else
            trả lại trạng thái hiện tại không thay đổi

store
const store = configureStore({ reducer: counterReducer })

dispatch
Cách duy nhất để cập nhật trạng thái là gọi store.dispatch() và chuyển vào một đối tượng hành động

selector
là các hàm biết cách trích xuất các phần thông tin cụ thể từ giá trị trạng thái cửa hàng

    const selectCounterValue = state => state.value
    const currentValue = selectCounterValue(store.getState())

# Core concept

    Single Source
        State của ứng dụng của bạn được lưu trữ dưới dạng một object bên trong một store duy nhất

    state read-only
        only-way change state -> dispatch action

    change made with pure reducer fn
        reducers(state,action) -> nextState

    data flow
        currentState
        render UI (currentState)
        action -> update -> newState
        re-render UI(newState)

        specifically
            made store (root reducer)
            store call root reducer once -> state
            render UI (state), subcribe store (update)

            update
                click button
                dispatch({type: 'counter/incremented'})
                store run reducer(state,action) -> newState
                store noti UI

NOTE 2:
state global (store I')
state(store) read-only
reducer -> update state follow actions

    use one way data-flow

===================================================================

khi viết vanilla

    import todosReducer from './features/todos/todosSlice'
    import filtersReducer from './features/filters/filtersSlice'

    export default function rootReducer(state = {}, action) {
    return {
        todos: todosReducer(state.todos, action),
        filters: filtersReducer(state.filters, action)
    }
    }

khi dùng combineReducers

    import { combineReducers } from 'redux'

    import todosReducer from './features/todos/todosSlice'
    import filtersReducer from './features/filters/filtersSlice'

    const rootReducer = combineReducers({
    todos: todosReducer,
    filters: filtersReducer
    })

    export default rootReducer

===============================================================
create store
Mỗi cửa hàng Redux có một chức năng root reducer duy nhất
default:

    import { createStore } from 'redux'
    import rootReducer from './reducer'

    const store = createStore(rootReducer)

    export default store

options
preloadedState: thêm dữ liệu ban đầu khi cửa hàng được tạo [localStorage] đọc lại khi người dùng truy cập lại trang

        let preloadedState
        const persistedTodosString = localStorage.getItem('todos')

        if (persistedTodosString) {
        preloadedState = {
            todos: JSON.parse(persistedTodosString)
        }
        }

        const store = createStore(rootReducer, preloadedState)

dispatch actions

    call subscribe
        const unsubscribe = store.subscribe()
    call store.dispatch(action)
    store call rootReducer(state,action)
    call todosReducers(state.todos,action)

    call unsubscribe
        unsubscribe()
    =================================
    // every time state change, log it
    const unsubscribe = store.subscribe(()=>
        console.log('State after dispatch:', store.getState())
    )

    store.dispatch({type:'todos/todoAdded', payload: ''Learn about actions})

    //stop listening to state updates
    unsubscribe()
    ==========================================
    cấu tạo createStore cơ bản [full: https://github.com/reduxjs/redux/blob/v4.0.5/src/createStore.js]
        fn createStore(reducer, preloadedState){
            let state = preloadedState
            const listeners = []

            fn getState(){
                return state
            }

            fn subscribe(listener){
                listeners.psh(listener)
                return fn unsubscribe(){
                    const index = listeners.indexOf(listener)
                    listeners.splice(index,1)
                }
            }
            fn dispatch(action){
                state = reducer(state, action)
                listeners.forEach(listener => listener())
            }
            dispatch({type: '@@redux/INIT'})
            return {dispatch, subscribe, getState}
        }

    ===========================================================
    createStore nhận enhancer làm đối số thứ 3
        createStore(reducer,preloadedState,enhancer)

        nếu có 2 enhancer trở lên thì dùng compose
            const rootEnhancer = compose(part1,part2)

            createStore(reducer,preloadedState,rootEnhancer)

middleware
thực chất là 1 enhancer
có thể có các side effect bên trong(timer,logic async)

    basic
        fn logMiddleware(storeAPI){
            return fn wrapDispatch(next){
                return fn handle(action){
                    ...
                    return next(action)
                }
            }
        }

        logMiddleware: được gọi bởi applyMiddleware [nhận 1 storeAPI{dispatch,getState}]. call once
        wrapDispatch: chuyển đổi giữa các middleware thông qua next

    es6: const logMiddleware = storeAPI => next => action => {
        ...
        return next(action)
    }

    EX: const logMiddleware = storeAPI => next => action => {
        console.log('dispatching', action)
        let result = next(action)
        console.log('next state', storeAPI.getState())
        return result
    }
        //LOG:
        // dispatching
        // chuyển action cho next [other middleware or real store.dispatch]
        // reducer run, updated state, return next
        // log newState
        // return result từ middleware next

    dùng middleware khi:
        log something to the console
        timer
        call async API
        fix action
        => chứa logic với side effect

NOTE 3:
only one store
createStore has single root reducer
in store:
getState
dispatch
subscribe

=========================================================================
useSelector
lấy all state [store] làm đối số. read 1 số value từ state và return it

    auto subscribe store
    ss result [===] component re-render when result là tham chiếu mới

    const todos = useSelector(state => state.todos)

useDispatch
bình thường thì dùng store.dispatch(action)
[ko có quyền truy cập store trong component]
dùng useDispatch [là cách khác của return store.dispatch]

Provider
bọc App trong Provider

react-redux với react
useSelector -> đọc data trong component
useDispatch -> send action trong component
<Provider store={store}> <App/> </Provider>

template react-redux
có thể gọi useSelector nhiều lần trong 1 component
[useSelector phải luôn return về lượng state nhỏ nhất]

    react render lại component theo default [có 1 vài component ko cần re-render lại]
        solution: dùng React.memo() bọc bên trong 1 component -> chỉ render khi các props có sự thay đổi [cải thiện perform]

    dùng shallowEqual[react-redux] để ss trong useSelector [value nếu khác nhau thì re-render component]
        const todoIds = useSelector(state => state.todos.map(todo => todo.id), shallowEqual)

=====================================================
store ko biết về async logic [ only send sync action, update state[call reducer], subscribe/unsubscribe]

bất kì async nào đều được xảy ra bên ngoài store

side effect: bất kì thay đổi nào với state or behavior có thể được nhìn thấy từ bên ngoài việc return value từ fn
log on the console
save file
timer
ajax http
modify state outside of a fn
make number or id random

async middleware
basic:
// chuyển 1 fn tới dispatch

    const asyncMiddleware = storeAPI => next => action => {
        if(typeof action === 'function'){
            return action(storeAPI.dispatch, storeAPI.getState)
        }
        return next(action)
    }

    thunk:
     - chứa async logic có thể tái sử dụng mà ko cần biết trước store nào
     - triển khai:
        const composed = composeWithDevTools(applyMiddleware(thunkMiddleware))

        const store = createStore(reducer, composed)

    - used thunk call async
        in todosSlice.js

            export async function fetchTodos(dispatch, getState){
                const response = await client.get('/fakeApi/todos')
                dispatch({type: 'todos/todosLoaded', payload:response.todos})
            }

        gọi ở đâu [App(useEffect) / component(useEffect) / index.js]
            store.dispatch(fetchTodos)

====================================================
standard redux patterns
action creators để đóng gói các action object
memories selector cải thiện perform
tracking request status thông qua loading enums
normal state for managing collection of items
promise thunk

action creators

    viết object action trực tiếp

        dispatch({
            type: 'todos/todoAdded',
            payload: trimmedText
        })

    creator action là 1 fn tạo và return 1 object action

        const todoAdded = text => {
            return {
                type: 'todos/todoAdded',
                payload: text
            }
        }

        used: gọi creator action, chuyển trực tiếp result object action tới dispatch

            store.dispatch(todoAdded('Buy milk'))
            console.log(store.getState().todos)
            // [ {id: 0, text: 'Buy milk', completed: false}]

memories selector

    basic:

        const selectTodoIds = state => state.todos.map(todo => todo.id)

            [map luôn return new array ref]
            [useSelector re-run sau mỗi dispatch action, if result selector -> component re-render]
            [dùng shallowEqual cho useSelector]

    memories: lưu result của 1 phép tính tốn kém và dùng lại cac result nếu thấy các đầu vào tương tự

    memories selector fn: selector lưu value gần nhất, gọi nhiều lần với cùng 1 input -> return về cùng 1 result. if input khác -> calc new result -> save temp -> return new result

        createSelector:
            accept 1 or multi input selector làm đối số
            1 output selector -> return 1 fn selector

            export const selectTodoIds = createSelector(
                state => state.todos,
                todos => todos.map(todo => todo.id)
            )

            const todoIds = useSelector(selectTodoIds)

=====================================================
redux toolkit

    configureStore
        const store = configureStore({
            reducer:{
                todos: todoReducer,
                filters: filtersReducer,
            }
        })
        export default store

        [ - compose todoReducer và filtersReducer vào rootReducer]
        [ - create store từ rootReducer]
        [ - auto add middleware thunk]
        [ - auto setup redux devtools extension]

    createSlice
        name
        initialState
        reducers

        [immer]

    createAsyncThunk
        string,
        payload creator [return Promise [async/await]]

        extraReducers: builder => {
            builder.addCase(something.pending, caseReducer)
            .addCase(something.fulfilled, caseReducer)
            .addCase(something.rejected, caseReducer)
        }

    normalizing state
        createEntityAdapter
            addOne/addMany: add item to state
            upsertOne/upsertMany: add multi or update item
            updateOne
            removeOne
            setAll

            getInitialState: return { ids: [], entities: {} }
            getSelectors

=====================================================

create store(index.js)

    const store = createStore(rootReducer)
        // return object store

    move store vào react-redux Provider
        <Provider store ={store}>
            <App />
        </Provider>

extending redux function

    logger middleware(logger.js)

        const logger = store => next => action {
            console.group(action.type)
            console.info('dispatching', action)
            let result = next(action)
            console.log('next state', store.getState())
            console.groupEnd()
            return result
        }
        export default logger

    enhancer (monitorReducer.js)
        monitorReducerEnhancer = createStore => (reduce, initialState, enhancer) => {
            const monitoredReduce = (state, action) => {
                const start = performance.now()
                const newState = reducer(state, action)
                const end = performance.now()
                const diff = round( end - start)

                console.log('reducer process time:', diff)
                return newState
            }
            return createStore(monitoredReducer, initialState, enhancer)
        }
        export default monitorReducerEnhance

    (index.js)
        const middlewareEnhancer = applyMiddleware(logger, thunkMiddleware)
        const composeEnhancer = compose(middlewareEnhancer, monitorReducer)

        const store = createStore(rootReducer, undefined, composeEnhancer)

solution configureStore

- gói gọn logic tạo store

  - index.js

        const store = configureStore()

  - configureStore.js

        export default function configureStore(preloadedState){
            const middleware = [logger, thunkMiddleware]
            const middlewareEnhancer = applyMiddleware(...middleware)
            const enhancer = [middlewareEnhancer, monitorReducerEnhancer]
            const composeEnhancer = compose(...enhancer)

            const store = createStore(rootReducer, preloadedState, composeEnhancer)

            return store
        }


=======================================================
createStore(reducer, [preloadedState], [enhancer])

store

    getState
    dispatch
    subscribe
    replaceReducer

combineReducers(reducers)

applyMiddleware(...middleware)

bindActionCreators(actionCreators, dispatch)

compose(...functions)
