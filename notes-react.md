# ES6

    -variable
        var:
            scope là global(trừ khi khai bao trong fn thì là fn scope)
            có tinh hoisting: biến sẻ được đưa lên đầu scope trươc khi thực hiện( giá trị là undefined)
        let:
            scope là block
            cho phep cập nhật giá trị của biến, ko cho tái khai báo lại biến
            có tinh hoisting: (gia trị là Reference Error)
        const:
            scope là block
            có hoisting (gia trị là Reference Error)
            đôi với kiểu là primitive(string, number, boolean,null,undefined) thì ko thể tái tạo biến hay cập nhật
            đôi vơi kiểu là reference(object, array, fn) co thể cập nhật giá trị
    - default parameter
    - Spread
        lặp lại các p/tử của mãng or object
    -  rest
    - destructuring
    - arrow fn
    - classes
    - import & export

# virtual DOM

    - xây dựng dựa trên DOM thật
    - khi render 1 jsx element ->cập nhật virtual DOM(kiểm tra sựu thay đổi với virtual DOM trươc đó =>cập nhật)-> cập nhật DOM thật
    - tại sao dùng?
        - khi 1 nodes thay đổi thì cac nodes cũng thay đổi trên DOM thật -> chậm khi xây dựng ứng dụng lớn.

# jsx

    + là js XML: cho phép viết mã html trong React

    + gán 1 biểu thức trong jsx = cách bọc nó trong {}
        + <h1>Welcome to {name}</h1>

    + là object sau khi compile

    + phần tử con trong jsx
        + nếu chỉ co 1 tag thì đóng = />
        + có nhiều p/tử con => bọc bằng jsx tag(<div></div>)

    + compile 1 jsx object -> jsx
        + dùng React.createElement(type,props)
            + type: "p","h1",...
            + props:
                + className
                + children

    + cung cấp cú pháp đặc biệt cho hàm React.createElement(component,props,...children)
        <MyButton color="blue" shadowSize={2}>Click Me</MyButton>

        ==> React.createElement(
            MyButton,
            {color:'blue', shadowSize:2},
            'Click Me'
        )

# components

    + bên trong return luôn tồn tại tag bao ngoài tất cả

    + dùng React.DOM để render 1 component
    + phải có cấu trúc XML <Ten/> or <Ten></Ten>
    + chia nhỏ các thành phần trong UI thành nhiều component

## Fn vs class Component

### Fn Component

    function Wle(props){
        return <h1>{props.name}</h1>
    }

### class Component

    class Wle extends React.Component{
        render(){
            return <h1>{this.props.name}</h1>
        }
    }

### Convert a Fn to a Class

    + tạo es6 class( extends React.Component )
    + add method render()
    + move body of fn into render()
    + replace props with this.props

### render Component

    // code
    ...
    const element = <Wle name="Huy" />
    root.render(element)
        // step: call root.render with element
                call Wel Component with props
                our Wle Component return a result
                React DOM update DOM


    + component API

        + setState : update status state
            + this.setState({...})
            + this.setState((prevState, props) => {
                return newState;
            })

        + forceUpdate : re-render ko cần sự thay đổi của state

## lifecycle

    + khi render 1 component thì react thực hiện nhiều tiến trình # nhau

### mounting

    component render lần đầu

### unmounting

    khi removed component

### các giai đoạn

    + Initialization
        + khởi tạo state và props(thường trong constructor)

        + Mounting
            + thực hiện sau khi khởi tạo hoàn thành
            + nv: chuyển virtual DOM thành DOM và hiển thị
            + component render đầu tiên
            + có 2 p/thức:

                + componentWillMount():
                    + chạy khi component chuẩn bị được mount(trước khi render)-> component được mount
                    + không nên thực hiện bất cứ thay đổi nào liên quan đến state, props hay call API ở trong hàm này (vì thời gian chuẩn bị mount -> mount rất ngắn nên các tác vụ đó không thể hoàn thành kịp)

                + componentDidMount():
                    + run after component render to DOM
                    + gọi sau khi đã mount, xảy ra sau khi componentWillMount thực hiện xong.
                    + có thể gọi API, thay đổi state, props

            + Updating
                + data của props & state sẽ được update -> đáp ứng event của user -> re-render component
                + các p/thức:
                    + shouldComponentUpdate():
                        + xác định component có nên được render (default-> return true)
                        nhận vào 2 tham số : nextState, nextProps

                    + componentWillUpdate():
                        + gọi trước khi tiến hành re-render
                        + action: update state, props trước khi re-render
                        nhận vào 2 tham số : nextState, nextProps

                    + componentDidUpdate():
                        + gọi khi component đã re-render xong
                        2 tham số (prevProps, prevState)

            + unmounting
                + tiến hành unmountDOM
                    + componentWillUnmount()

# props

## props chỉ có thể đọc

    + props là tham số, là 1 object
    + component nhận vào 1 props và trả về 1 react element
    + Cha(props) -> Con(props): Con only read
    + truyền props:
        + truyền 1 g/trị bên trong 1 tags thì nó có thuộc tính children trong object props
        + vi dụ :
            const app = () => <Welcome name="Huy" age=18>hello</Welcome>
            + bên trong component : giá trị là 1 object
                {
                    name: "Huy",
                    age: 18,
                    children:"hello"
                }
    + nhận props:
        + class component: dùng this.props
        + fn component: chỉ định tham số trong fn

    + props validation
        + kiểm soát vấn đề của props, kiểm tra đầu vào của props trước khi component được render.

        + dùng propTypes.

            fn component
                fnComponent.propTypes = {
                    ....//
                }
            class component
                clComponent.propTypes = {
                    ...//
                }

            static propType
                class clCompoment extends React.Component {
                    .....
                    static propTypes = {
                        ...
                    }
                }

    + render props
        + tái sử dụng logic trên nhiều component
        + cách dùng
            + truyền vào component là 1 fn
                <Component render={(data)=>(
                    <p>{data.value}</p>
                )}>

                bên trong Component
                    const Component = (props) => {
                        return (
                            <div>
                                {props.render({
                                    value:'string'
                                })}
                            </div>
                        )
                    }

# state

    + state là 1 object lưu trữ giá trị của các thuộc tính bên trong component, scope là component đó
    + giá trị của 1 state thay đổi-> component render lại.

    + khởi tạo:
        this.state = {name:"Huy"};
        + nên khởi tạo state trong hàm constructor(hàm chạy đầu tiên khi component được gọi)

    + lấy g/trị
        + gọi this.state
            this.state.name// log "Huy"

    + cập nhật state
            dùng this.setState({
                name: "HuyRua"
            })

    + lấy g/trị state trước khi update
        this.setState((state)=>{
            return newState;
        })

## add local state to a class

    + tiếp theo của convert fn to class
    + replace this.props with this.state
    + add constructor để assign init this.state

## using state correctly

    + ko sửa state trực tiếp
        -> dùng useState()
            => this.state.name = 'Huy'      //Wrong
               this.setState({name:'Huy'})  // Correct

    + gộp nhiều setState thành 1 -> tăng hiệu suất

        //Wrong
        this.SetState({
            name: this.state.name + this.props.age
        })

        // Correct
        this.setState((state,props)=>({
            name: state.name + props.age
        }))

        dùng setState thứ 2 trong setState nhận vào fn thay vỉ object:
            argument1 là prev state
            argument2 là props

## state update and merged

    + khi call setState, react merge object được provide into current state
        add thêm state mới vào current state
        ...
        this.state = {
            ....
            like:[]
        }

        call setState
            setState({like:response.like})

    + việc merge là shallow -> giữ nguyên các thành phần trước và thay thế hoàn toàn thành phần khi setState

## data flows down

# handling eventslllllllllllllllll

        các event viết trong {}
        dùng preventDefault(): chặn các hành động mặc định

            fn handleSubmit(e){
                e.preventDefault()
            }
                e: event ảo

## this trong callback jsx

    method của class default ko bị bound
        nếu ko bind thì this là undefined
            constructor...
                this.handleClick = this.handleClick.bind(this) // true
                this.handleClick = this.handleClick(this) // wrong

    khi refer method mà ko có () theo sau [onClick={this.handleClick}] thì nên bind method đó

    các cách khác khi ko dùng bind
        class field syntax
            class .... extends React.Component
                handleClick = () => {
                    ....
                }
            .... onClick={this.handleClick}

        arrow fn
            class .... extends React.Component
                handleClick() {
                    ....
                }
            .... onClick={() => this.handleClick()}

## passing argument to Event Handles

    onCkick= {(e) => this.deleteRow(id,e)}
        e: event React

    onCkick= {this.deleteRow.bind(this,id)}

# xử lý form

    controller component
        component thực hiện render 1 form element sẻ kiểm soát được điều gì đang xảy ra với form element khi user nhập vào.
        + 1 input form element mà g/trị của nó được đk bởi react bằng pp nêu trên -> controlled component

    + thẻ textarea
        dùng attr value lưu trữ
    + thẻ select
        dùng value thay cho selected
    + input, select,textarea nhận vào 1 value -> controlled component
    + input file(value của file chặn quyền ghi/ read-only ) -> uncontrolled component
    + handle nhiều thẻ input
        + thêm name vào từng element để handle fn chọn chính xác thông qua (event.target.name)

# render với điều kiện

    &&
    condition ? true : false
    bọc trong {}

    ngăn chặn component render
        khi muốn ẩn 1 component khi nó được render bởi 1 component khác -> return null
        [khi return null trong render của component ko ảnh hưởng đến method của lifecycle]

# List and Key

    lists:
        khởi tạo giống js
        const list = ['a','b','c'];

    basic list component

    keys:
        + là duy nhất khi ss với anh/chị của nó trong lists chứa chúng
        + xác định mục nào changed,add,remove
        + tránh lấy index làm key(sắp xếp mảng thì index thay đổi-> xác định lại key 1 lần nữa-> giảm hiệu xuất làm việc)
            dùng index làm key khi
                là list tĩnh, ko thay đổi
                ko sắp xếp lại
                ko được lọc
                ko có id cho mục trong list

# Lifting State Up

    khi 1 component thay đổi(re-render) thì các component quan hệ phía trên nó phải nhận được sự thay đổi(cha/con)
    truyền xuống Component con 1 props có dạng là 1 fn
        component con thực hiện gọi props đó để đưa state lên component cha
        A{
            fn handleChange(val){
                this.setState({data: val})
            }
        }
        truyền fn vào component con B
        <B handleChange = {handleChange}>

        trong component B gọi fn để up state lên cha
            B{
                <input onChange={(e)=> handleChange(e.target.value)}>
            }

    + trong A
        + truyền xuống B 1 fn để change state

    + trong B
        + call fn khi được truyền xuống khi cần thay đổi state ở cha

# composition && inhert

## limitlll

    + nhiều khi component ko biết về các component children của nó trước thời hạn [Sidebar & Dialog là component chung]
    + dùng props.children để truyền trực tiếp element
        function ComponentA(props){
            ...
            return(
                ...
                {props.children} // xuất hiện ở đây
                ...
                {props.left}
                {props.right} // custom
            )
        }
        function ComponentB(){
            return(
                ....
                <ComponentA left = {<ComponentC />} right={<ComponentD />}>
                    // những gì ở đây là children được gửi đi như 1 children props

                </ComponentA>
            )
        }           // ComponentC, ComponentD là các object -> có thể truyền như các props thông thường

    + ngoại lệ
        kết hợp 2 TH trên lại [vừa có props vừa có children]

# === ADV ===

# Accessibility

## react Fragment

## Accessible form

# code splitting

## bundling

## splitting

    import() dynamic
        import("./math").then(math => {
            console.log(math.add(16, 26));
        });

    lazy load
        render 1 import động như 1 component normal

        const OtherComponent = React.lazy(() => import('./OtherComponent'));

# Refs

    + chuyển 1 ref qua 1 component đến 1 trong các component con của nó

    + ref to DOM components

    cách dùng:
        khởi tạo: thường trong constructor(class component) hay biến(fn component) -> gán vào 1 element trong hàm render()
            ....
            constructor(props){
                ...
                this.myRefs = React.createRef();
            }
            render(){
                return(
                    ....
                    ref = {this.myRefs}
                )
            }
            //khởi tạo 1 ref(dùng React.createRef()) -> gán g/trị vào thuôc tính myRef trong class/fn component -> gán refs vào element input(element có thể được truy cập/sửa thông qua ref)
        uses:
            ...
            handleClick = () => {
                ...
                this.myRef.current.focus();
                ....
            }
            //current: chứa g/trị element được tham chiếu khi element đó được render -> focus vào input(ko dùng đến state or props->ko re-render)

    Forwarding Refs:
        chuyển 1 ref từ 1 component tới component con, cho phép component cha tham chiếu tới các element của component con để đọc/chỉnh sửa
        - cách dùng:
            bao component con trong React.forwardRef()
    + quá trình
        + tạo ref = useRef
        + truyền ref vào <Component ref={ref} />
        + Component nhận 2 argument là ref và props
        + dùng React.forwardRef(Component) để forwarding ref vào Component
        + sau khi ref được forward --> dùng ref.current trong element
    + use case
        + animation, text selection, focus, media playback
        + refs trỏ trực tiếp vào DOM thật

# Context

    + chia sẻ dữ liệu tới các component trong cây mà ko cần truyền dữ liệu qua props theo từng cấp bậc

## when

    khi data là global của toàn app(info user, theme,...)

## before uses

    + chủ yếu dùng khi data cần được truy cập bởi nhiều component ở nhiều tầng # nhau

    + dùng component composition để truyền 1 số props qua nhiều level đơn giản hơn

        function Page(props) {
            const user = props.user;
            const userLink = (
                <Link href={user.permalink}>
                <Avatar user={user} size={props.avatarSize} />
                </Link>
            );
            return <PageLayout userLink={userLink} />;
        }

        <Page user={user} avatarSize={avatarSize} />
        // ... được renders ...
        <PageLayout userLink={...} />
        // ... được renders ...
        <NavigationBar userLink={...} />
        // ... được renders ...
        {props.userLink}

        khi composition như trên thì chỉ tầng tên cùng Page mới biết được Link và Avatar sử dụng user và avatarSize

## API

    .createContext
        const MyContext = React.createContext(defaultValue)

        + khi render 1 component -> dọc value current từ Provider gần nhất
        + khi component ko có provider nào thì sẻ lấy defaultValue
        NOTE: truyền undefined như 1 value Provider sẽ ko khiến consuming component sử dụng defaultValue

    .Provider
        + mỗi context phải đi kèm 1 provider
        + nhận vào 1 value prop -> truyền đến consuming component (con) của Provider
        + 1 provider có thể kết nối nhiều consumers
        + có thể lồng Provider

        + consumers con của provider sẽ re-render khi value của provider thay đổi
        + sự lan truyền từ Provider đến consumers ko lện thuộc vào shouldComponentUpdate -> consumer update ngay cả khi 1 component cha thoát ra vòng update đó

    Class.contextType
    .Consumer
    .displayName
    update context tứ 1  nested component
    consuming nhiều context
    caveats



    khởi tạo:

            //context object
        mỗi context object phải đi kèm 1 provider(nhận về sự thay đổi của context)
        <MyContext.Provider value={}>
        <MyContext.Consumer>
            //khởi chạy khi giá trị context thay đổi -> nhận về g/trị của context đó
        .displayName
            // hiển thị trong devTools
        .contextType: được tạo bởi .createContext -> lấy g/trị của context
    cách dùng:
        - khởi tạo(.createContext) -> nhận 1 object các thuộc tính: provider, consumer
        - dùng provider bọc quanh component, truyền g/trị vào props value
        - thêm consumer ở bên trong provider để chia sẻ context(lấy g/trị thông qua props.children)
        vd

# error boundary

# Fragments

    bao bọc các element jsx -> triển khai element theo mong muốn
    cach viết:
        React.Fragment key={}//chỉ định key vào fragment(triển khai lists..)
        <></>

# Render props

    + share code giữa các component = props[là fn]
        <Component render={data => (<h1>{data.target}</h1>)}>
    + Component được tái sử dụng chỉ chứa logic
    + Component nào gọi nó sẽ quyết định nó render như thế nào

        có 1 componentA chỉ cò logic fetch data từ url, gán vào init state và truyền nó ra bên ngoài
        componentB sử dụng componentA thì sẽ quyết định sẽ render [name,age]
        componentC sử dụng componentA thì sẽ quyết định sẽ render [name,age,salary]

## render props cho cross-cutting concerns

# higher other component

## basic

    + là 1 fn nhận vào 1 component và trả về 1 component
        + tái sử dụng logic của component
        + chuyển đổi 1 component thành 1 component khác
        + làm khuôn mẫu cho các Component tương tự

    + HOC ko chỉnh sửa, thay đổi component đầu vào mà chỉ kế thừa hành vi của component đó
        + HOC là fn ko có side-effect

## ko thay đổi Component gốc mà dùng composition

    + fn ...(Component){
        Component.prototype.componentDidUpdate = fn(prevProps){
            console.log('Current props:', this.props);
            console.log('Prev props:', prevProps);
        }
        // việc component được trả về chứng tỏ nó đã được mutate
        return Component;
    }
    // thay vì mutate -> dùng composition
        [gói component đầu vào bên trong 1 container]
            fn ComponentA(ComponentB)
                return class extends React.Component{
                    componentDidUpdate(prev){
                        log this props
                        log prev props
                    }
                    render(){
                        return <ComponentB {...this.props}/>
                    }
                }
    // điểm giống nhau giữa HOCs và container component
        + container component là 1 phần của strategy of separating responsibility high và low concerns
        + container quản lý state và subscriptions, truyền props đến component
        + HOC là container component có thể truyền tham số

## Convention

### truyền props ko liên quan đến component con

            + HOC thêm tính năng vào component, ko nên thay đổi cấu trúc, component return từ HOC nên có chung interface với component con
            + HOC nên truyền qua các props mà ko liên quan đến những quan tâm đặc thù thì có dạng( chỉ chứa 1 hàm render)
                render(){
                    // lọc props mà chỉ liên quan đến HOC này mà ko cần truyền xuống
                    const {extraProps, ...passThroughProps} = this.props

                    // truyền props vào component con.[state or method]
                    const injectedProp = someStateOrInstanceMethod;

                    return (
                        <ComponentCon injectedProp = {injectedProp} {...passThroughProps} />
                    )
                }
            + HOC trở nên linh hoạt và có thể tái sử dụng

### composition maximizing

            + accept only a single argument
                const NavbarWithRouter = whitRouter(Navbar)

            + accept multi argument
                const ComponentA = Relay.createContainer(ComponentB, config)

            + điển hình nhất
                // redux connect
                const ConnectedComment = connect(commentSelector,commentActions)(CommentList);

                    // phân tách ra ta được
                    // connect là fn return other fn
                    const enhance = connect(commentListSelector, commentListActions)
                    // fn return là 1 HOC, HOC return 1 component connect vs Redux store
                    const ConnectedComment = enhance(CommentList)

                connect là HOC return HOC

## NOTE

### ko dùng HOC bên trong hàm render

            nếu 1 component return từ render === component từ lần render trước => react sẽ đệ qui update substree = ss(diffing) với mới. if ko giống nhau substree được unmount hoàn tất

            + ko thề áp dụng HOC cho 1 component bên trong fn render của component khác
                render(){

                    const EnhancedComponent = enhance(MyComponent)
                    return <EnhancedComponent />
                        // khi render tạo ra 1 bản mới
                        // EnhancedComponent1 != EnhancedComponent2
                        // mount/unmount substree mỗi lần
                }
                 + remount 1 component -> state và children đều lost
            + áp dụng HOC bên ngoài definition của component để component chỉ tạo 1 lần(ko thay đổi qua mỗi lần render)

            + you need to apply a HOC dynamically:
                use in fn lifecycle or constructor của component

### static method phải được copy qua

### refs ko được truyền xuống

    + ref ko phải là 1 prop
    + nếu thêm ref vào 1 element mà component là k từ HOC, ref là của container ngoài cùng nhất - ko phải component được bao bọc

# React ko dùng es6

    + set init state
        gán this.state bên trong constructor
            class ComponentA extends React.Component{
                constructor(props){
                    super(props);
                    this.state = {count: props.init}
                }
            }

    + auto binding
        + react khai báo như es6 class -> ko tự bind this đến instance mà phải dùng .bind(this) trong constructor
            class ComponentA extends React.Component{
                constructor(props){
                    super(props);
                    ...
                    this.handleClick = this.handleClick.bind(this);
                }
                handleClick(){
                    ....
                }
                render(){
                    return(
                        <button onClick = {this.handleClick} />
                    )
                }
            }

# Reconciliation

# ref & DOM

## ref

    + ref là cách truy cập đến những nút DOM or element được tạo ra trong method render

### when??

        + quản lý focus, text selection, media playback
        + trigger animation của 1 element khác
        + tích hợp những thư viện DOM từ bên thứ 3

    + ko dùng refs khi có thể khai báo

### tạo refs

        class ComponentA extends React.Component{
            constructor(props){
                super(props);
                this.myRef = React.createRef();
            }
            render(){
                return <div ref={this.myRef} />
            }
        }
        // tạo = .createRef(), gán vào các element thông qua attr 'ref'
        // tại đó có thể tham chiếu đến all thành phần bên trong

### truy cập refs

        const node = this.myRef.current

### ref dùng trong html element -> ref nhận DOM element bên dưới làm attr 'current'

            class ComponentA ...{
                constructor(){
                    ...
                    this.textInput = React.createRef();
                    this.focusTextInput = this.focusTextInput.bind(this)
                    ...
                }
                focusTextInput(){
                    this.textInput.current.focus();
                }
                render(){
                    return(
                        <div>
                            <input
                                type='text'
                                ref={this.textInput} />
                            <input
                                type='button'
                                value='....'
                                onClick={this.focusTextInput}
                            />
                        </div>
                    )
                }
            }
            // current được gán cho DOM element khi component mounts
            // current = null khi unmounts
            // ref được cập nhật trước componentDidMount or componentDidUpdate

### ref trong class component

            class ....{
                constructor...{
                    ....
                    this.textInput = React.createRef();
                }
                componentDidMount(){
                    ths.textInput.current.focusTextInput();
                }
                render(){
                    return(
                        <Component ref={this.textInput} />
                    )
                }
            }
            // chỉ hoạt động khi khai báo component dưới dạng class

### không dùng 'ref' trong fn component vì ko có instances

            fn Name(){
                return <input />
            }
            class ...{
                constructor...{
                    this.textInput = React.createRef();
                }
                render(){
                    return (
                        // NOT WORK
                        <Name ref=[this.textInput] />
                    )
                }
            }
            dùng forwardRef[ kết hợp useImperativeHandle]

            có thể dùng trong fn nếu tham chiếu đến p/tử DOM or class component
                fn Name(props){
                    const textInput = useRef(null)

                    fn handleClick(){
                        textInput.current.focus()
                    }
                    return (
                        <div>
                            <input
                                type='text'
                                ref = {textInput} />
                            <input
                                type='button'
                                onClick={handleClick} />
                        </div>
                    )
                }

### hiển thị DOM ref cho component cha

    + mượn quyền truy cập vao DOM node của element con từ component cha

    + thêm ref vào component con [ref trong class component]
        => cái nhận được là 1 component instance [ko phải DOM node]

    + ref forwarding cho phép các component tham gia hiển thị bất kì bản tham chiếu nào của component là con của nó

    + callback refs

# strict mode

# propTypes

    import PropTypes from 'prop-types'
        class ComponentA ...{
            render(){
                return(
                    <h1>{this.props.name}</h1>
                )
            }
        }
        ComponentA.propTypes = {
            name: PropTypes.string
        }

    // PropType sẻ export 1 loạt các validator nhằm đảm bảo data nhập vào valid

    // các propTypes
        + PropTypes.array
        + PropTypes.bool
        + PropTypes.func
        + PropTypes.number
        + PropTypes.object
        + PropTypes.string
        + PropTypes.symbol
        + PropTypes.node
        + PropTypes.element
        + PropTypes.elementType
        + PropTypes.instanceOf(Message)
        + PropTypes.oneOf(['New','Photo'])
        + PropTypes.oneOf([
            PropTypes.array
            PropTypes.string
            ...
        ])
        + PropTypes.objectOf(ProTypes.number)
        + PropTypes.shape({
            name: ProTypes.string,
            quantity: ProTypes.number
        })
        + PropTypes.func.isRequired

    // requiring single child
        proTypes.element -> chỉ có duy nhất 1 child có thể truyền đến component
            children: PropTypes.element.isRequired

    // default props
        + ComponentA.defaultProps = {
            name: 'Huy'
        }

# uncontrolled components

#

======= API ==========

# component

    + chia UI -> thành phần nhỏ độc lập, tái sử dụng
        class ComponentA extends React.Component{
            render(){
                return <h1>{this.props.name}</h1>
            }
        }

## life cycle

### mounting

    + gọi theo thứ tự:
        + constructor
        + static getDerivedStateFromProps
        + render
        + componentDidMount

### updating

    khi có sự thao đổi props & state, gọi theo thứ tự
        + static getDerivedStateFromProps
        + shouldComponentUpdate
        + render
        + getSnapshotBeforeUpdate
        + componentDidUpdate

### unmounting

    gọi khi component được xóa khỏi DOM
        + componentWillUnmount

## API khác

    + setState
    + forceUpdate
    + defaultProps
    + displayName
    + props
    + state

### detail API

#### render()

    là method bắt buộc trong class component
    khi được gọi, sẽ check this.props và this.state sau đó return:
        + react element [<div /> or <MyComponent />]
        + array và fragment [cho phép return nhiều element từ render]
        + portal [render children vào 1 DOM subtree khác]
        + string và number [ dạng text node trong DOM]
        + boolean or null [ko render]
    + fn render nên là pure[ko làm thay đổi component state]
    + render ko được gọi khi shouldComponentUpdate return false

#### constructor

    + if ko khởi tạo state và ko bind các method -> ko cần implement 1 constructor cho component
    + được gọi trước khi component đó được mount
    + gọi super(props) trước tiên [nếu ko thì this.props sẽ bị undefined trong constructor]
    + mục đích:
        + khởi tạo local state = gán 1 object cho this.state
        + binding các method event handle cho 1 instance
    + ko gọi setState trong constructor
    + constructor là mơi duy nhất gán this.state, mọi chỗ khác dùng this.setState
    + ko đặt side-effect or subscription nào trong constructor
    + ko copy props vào state
        //WRONG
        this.state = {color: props.color}

#### componentDidMount

    + được gọi ngay sau khi component được mount
    + quá trình khởi tạo mà yêu vầu các DOM node sẽ thực hiện tại đây
    + thực hiện network request để tải data từ 1 remote endpoint
    + thích hợp subscriptions tại đây [unsubscribe trong componentWillUnmount]
    + gọi setState tại đây [kích hoạt 1 lần render bổ sung, xảy ra trước khi browser update screen],

#### componentDidUpdate(prevProps, prevState, snapshot)

    + gọi khi quá trình update diễn ra [ko gọi cho lần render đầu tiên]
    + used để thao tác với DOM khi component update xong
    + thực hiện network request để tải data từ 1 remote endpoint [miễn là so sánh currentProps và prevProps (network request ko cần thiết nếu props ko thay đổi)]
        componentDidUpdate(prevProps){
            if(this.props.userID !== prevProps.userID){
                this.fetchData(this.props.userID)
            }
        }
    + gọi setState ngay lập tức [phải được đặt trong 1 điều kiện (if ko thì tạo ra vòng lặp vô hạn)], gây ra 1 lần render bổ sung
    + componentDidUpdate sẽ ko gọi nếu shouldComponentUpdate return false

#### componentWillUnmount

    + được gọi ngay trước khi 1 component bị unmount va destroy
    + thực hiện mọi thao tác cleanup [invalidating timers, cancel network request, destroy subscription]
    + ko gọi setState tại đây [ sẽ ko render lại, component instance bị unmount nó sẽ ko bao giờ được mount lại]

#### shouldComponentUpdate

    + output của 1 component ko bị ảnh hưởng bởi sự thay đổi của state or props
    + được gọi trước render khi nhận props or state mới [true]
    + ko được gọi ở lần render đầu or forceUpdate được dùng
    + tác dụng chính: tối ưu hóa hiệu suất
    + ss this.props vs nextProps và this.state vs nextState sau đó return false [bỏ qua việc cập nhật]

#### static getDerivedStateFromProps(props, state)

    + gọi trước method render, mount lần đầu, update tiếp theo
    + return object -> update state, null -> ko update
    + dùng khi state phụ thuộc vào sự thay đổi của props theo thời gian [implement 1 <Component> mà ss children trước và sau của component để quyết định children nào sẽ in/out]
    + các thay thế
        + thực hiện 1 side effect[data fetching, animation] để đáp ứng thay đổi props -> componentDidUpdate
        + tính toán lại 1 số data chỉ khi 1 prop thay đổi -> memoization helper
        + reset 1 số state khi 1 prop thay đổi
            -> component fully controlled
            -> fully uncontrolled với 1 key
    + ko có quyền truy cập vào component instance
    + được kích hoạt ở mọi lần render

#### getSnapshotBeforeUpdate()

    + gọi trước khi output của lần render gần nhất commit với DOM
    + component lấy 1 số thông tin từ DOM[vị trí thanh cuộn] trước khi thông tin bị thay đổi
    + value được return ở dạng tham số cho componentDidUpdate

        class ComponentA extends React.Component{
            constructor(props){
                super(props);
                this.listRef = React.createRef();
            }
            getSnapshotBeforeUpdate(prevProps, prevState){
                //
                if(prevProps.list.length < this.props.list.length){
                    const list = this.listRef.current
                    return list.scrollHeight - list.scrollTop
                }
                return null;
            }
            componentDidUpdate(prevProps, prevState, snapshot){

                // snapshot là return của getSnapshotBeforeUpdate
                if(snapshot !== null){
                    const list = this.listRef.current;
                    list.scrollTop = list.scrollHeight- snapshot;
                }
            }
            render(){
                return(
                    <div ref={this.listRef}>....</div>
                )
            }
        }
        // có đọc được scrollHeight trong getSnapshotBeforeUpdate hay ko -> có độ trễ giữa các render và commit

#### error boundaries

#### static getDerivedStateFromError

#### componentDidCatch

#### setState(update, callback)

    + tạo ra hàng đợi tới component state
    + thông báo component này cùng children của nó cần phải được render lại với state đã update
    + method chính để update UI response eventHandle và server response
    + setState là request
        + ko phải lúc nào cũng update component ngay lập tức
        + gộp nhóm or trì hoãn update
        + việc đọc this.state ngay sau gọi setState là BIG TRAP
            + dùng componentDidUpdate or setState callback [setState(updater, callback)] sẽ đảm bảo đọc this.state diễn ra sau khi update được áp dụng
                + updater: (state, props) => stateChange
                    + state tham chiếu tới component state tại thời điểm thay đổi đang được áp dụng
                    + những sự thay đổi nên được thực hiện = cách tạo ra 1 object mới dựa trên input từ state và props
                        this.setState((state, props) => {
                            return {counter: state.counter + props.step}
                        })
                    state, props sẽ đảm bảo update tới trạng thái mới nhất
        + cần đặt state dựa vào state trước đó
            + setState luôn render lại trừ khi shouldComponentUpdate return false
    + callback sẽ thực thi sau khi setState hoàn thành và component được render lại
    + có thể truyền 1 object làm đối số đầu tiên thay vì 1 fn
        setState(stateChange, callback)
                setState sẽ shallow merge stateChange và state mới
            + điều chỉnh sl mặt hàng trong giỏ hàng
                this.setState({quantity: 2})

                // setState là async và nhiều lời gọi trong cùng 1 chu kì -> gộp nhóm lại
                    // tăng sl 1 mặt hàng lên nhiều hơn 1 lần trong 1 chu kì
                        Object.assign(
                            prevState,
                            {quantity: state.quantity +1},
                            {quantity: state.quantity +1},
                            ...
                        )
                        // các lời gọi next sẽ override value của lời gọi trước trong cùng 1 chu kì -> sl chỉ tăng 1 lần
                        // nếu nextState phụ thuộc prevState
                            this.setState((state) => {
                                return {quantity: state.quantity + 1}
                            })

#### forceUpdate(callback)

    + if render phụ thuộc vào các data khác, thông báo với react rằng component cần được render lại = cách gọi forceUpdate
    + gọi forceUpdate -> method render được gọi, bỏ qua shouldComponentUpdate.
    + kích hoạt các method lifecycle cho các child component [kể cả shouldComponentUpdate của mỗi child]
    + react chỉ update DOM nếu markup thay đổi
    + tránh dùng forceUpdate [chỉ đọc this.props và this.state trong render]

#### defaultProps

    + được đ/n như là 1 thuộc tính của component class
    + đặt props default cho class
    + dùng cho các undefined prop [trừ null prop]
        class ComponentA ...{...}
        ComponentA.defaultProps = {color: 'blue'}
        // nếu props.color ko được cung cấp -> dùng default

        <ComponentA color={null}> // props.color vẫn là null

#### displayName

#### props

#### state

## React.PureComponent

    + giống react.component
    + có thực hiện shouldComponentUpdate
    + ss nông (shallow) state, props -> có nên update ko
    + để show kq với cùng props và state -> dùng react.PureComponent để tăng hiệu suất
    + chỉ dùng pureComponent khi có props và state đơn giản

## React.memo

    + là 1 HOC
    + if fn component biểu diễn cùng kq với cùng props -> gói lại và gọi đến React.memo -> tăng hiệu suất = ghi nhớ kq
        [bỏ qua việc render component, sử dụng lại kq đã render lần cuối]
    + chỉ check các thay đổi của props
    + if fn component được wrap với React.memo [có useState, useReducer, useContext] vân render lại khi state or context thay đổi
    + if want control all ss -> cung cấp fn ss ở đối số thứ 2
        fn MyComponent(props){...}
        fn areEqual(prevProps, nextProps){

        }
        export default React.memo(MyComponent, areEqual)
    +

# React element

    + ko cần dùng method sau khi dùng JSX
    + React.createElement(
        type,
        [props],
        [...children]
    )
        type: 'div'... / component class,fn / fragment

## crElement

## createFactory

    + return về 1 fn tạo ra các react element theo kiểu truyền vào
    + ko dùng nữa

# chuyển đổi các element

## cloneElement

    + copy và return về 1 react element = cách dùng element làm điểm start
    + React.cloneElement(
        element,
        [config],
        [...children]
    )
    + element kq là các props của element gốc kết hợp với các props mới.
    + thành phần con mới thay thế thành phần con hiện tại
    + key và ref từ element gốc sẽ được giữ nguyên

## isValidElement

    + React.isValidElement(object)
        xác định object là 1 react element [return true or false]

## React.Children

    cung cấp các tiện ích để tương tác với data structure ẩn
    + .map
    + .forEach
    + .count
    + .only
    + .toArray

# Fragments

## React.Fragment

# Refs

## React.createRef

    tạo ra 1 ref có thể được gán vào các element thông qua attr ref

## React.forwardRef

    tạo ra component giúp forwards attr ref mà nó nhận được cho các component khác bên dưới tree
    + forward refs tới các component DOM
    + forward refs trong các HOC

# Suspense

    + giúp component chờ để sử lý trước khi rendering

## React.lazy

    định nghĩa component được load 1 cách dynamically
    + giảm kích thước bundle để delay việc load component mà nó ko dùng trong lúc render ban đầu

## React.Suspense

# Hook

- cho phép sử dụng state, life cycle trong fn component

## quy tắt dùng hook

### call hook ở trên cùng

    + ko gọi hook từ fn Js
        + gọi trong React fn component
        + gọi từ custom Hook

### ESLint Plugin

    npm i eslint-plugin-react-hooks --save-dev
    + setup file
        {
            "plugins": [
                ...
                "react-hook"
            ],
            "rules":{
                ...
                "react-hooks/rules-of-hooks": "error" // check rule hook
                "react-hooks/exhaustive-deps":"warn" // check effect deps
            }
        }

### used nhiều state or nhiều effect trên một component

    + HOW REACT BIẾT STATE NÀO ỨNG VỚI LÚC GỌI USESTATE
        dựa trên thứ tự hook được gọi

    + ko đặt hook trong câu đk [trong hook có dk thì được]

## useState

    + làm việc với state trong fn component mà ko chuyển về class component

    + const [state, setState] = useState(init)
        state: value hiện tại
        setState: value update
        init: value ban đầu (string, number, object, array)

    + return cặp value dạng array

    + fn ComponentA(){
        const [count, setCount] = useState(0);
        return (
            <>
                <button onClick={()=> setCount(count + 1)}></button>
            </button>
        )
    }

    + nếu nextState được tính dựa vào prevState -> có thể dùng fn trong setState [nhận prev value và return value đã update]

    + if fn update return giống với value hiện tại, rerender tiếp theo được bỏ qua hoàn toàn

    + useState ko auto merge object
        có thể dùng spread
            setState(prevState=> {
                return {...prevState, ...updateValues}
            })

## useEffect

    + chạy khi g/trị của 1 biến nào đó thay đổi or component được render (thay thế lifecycle trong class component)

    + useEffect(fn,[deps])
        + re-run khi deps thay đổi
        + effect 1 lần duy nhất[lúc mount và unmount] thì dùng arr empty []
            props và state sẽ luôn có init value của nó

    + là componentDidMount, componentDidUpdate, componentWillUnmount kết hợp lại

    + nếu component render nhiều lần, effect trước đó sẽ bị loại bỏ trước khi effect mới thực thi

### effect ko cần cleanup

    + chạy 1 vài đoạn code sau khi đã update DOM
        network request tự ý thay đổi DOM và logging -> ko cần cleanup

    + trong class:
        + render ko được tạo side effect
        + đặt side effect trong componentDidMount và componentDidUpdate
            class ...{
                constructor(){
                    ....
                    this.state = {
                        count: 0
                    }
                }
                componentDidMount(){
                    document.title =  `${this.state.count}`
                }
                componentDidUpdate(){
                    document.title =  `${this.state.count}`
                }
                render(){
                    <>
                        <button onClick={() => this.setState({
                            count: this.state.count + 1
                        })}>
                    </button>
                }
            }
            // có 2 thao tác tương tự nhau
            //      vì muốn thực hiện cùng 1 side effect khi component đã mount hay update
    + cách hoạt động:
        + cần thực hiện 1 việc gi đó sau khi render
        + React ghi nhớ fn truyền vào
        + gọi lại fn này sau khi DOM đã update

    + fn truyền vào cho useEffect khác nhau cho tất cả các lần render
        + mỗi lần re-render, có 1 effect khác thay thế cái trước
        + mỗi effect thuộc về 1 render cụ thể

### Effect cần Cleanup

    + khi cần thiết lập các subscription cho data source bên ngoài -> clean up là cần thiết [memory leak]
        + trong class, đặt subscription trong componentDidMount và clean up trong componentWillUnmount

        + trong fn[hook] : useEffect khởi tạo và subscription cùng 1 chỗ
            + effect return fn, react chạy fn đó, đưa clean up vào bên trong fn
            ////////////////////
            useEffect(() => {
                const subscription = props.source.subscribe();
                return () => {
                    subscription.unsubscribe();
                }
            })
            ///////////////////
            const [isOnline, setIsOnline] = useState(null);
            useEffect(() =>{
                fn handleChange(status){
                    setIsOnline(status.isOnline)
                }
                ChatAPI.subscribeStatus(props.friend.id,handleChange)
                return fn cleanup(){
                    ChatAPI.unsubscribeStatus(props.friend.id, handleChange)
                }
            })
            // return fn trong effect?
                là 1 optional để chạy cleanup cho effect [tạo và xóa subscription trong cùng 1 effect]

            // when cleanup effect?
                khi component unmount

            // return fn trong effect ko cần có tên [arrow fn]

### TIP

#### used effect tách biệt

#### why Effect chạy trên mỗi update

#### tối ưu hiệu suất = bỏ qua Effect

        - sử dụng useEffect như componentDidMount
            - useEffect(effectFn, [])
            - dùng để gọi API khi component được render

        - sử dụng useEffect như componentDidUpdate
            - useEffect(effectFn)

        - sử dụng useEffect như componentUnWillMount
            - chỉ cần return về 1 fn trong effectFn, fn được return đóng vai trò như componentUnWillMount

## custom Hook

    + tách logic của component thành 1 fn có thể tái sử dụng

## useContext

    + const value = useContext(MyContext)
        + nhận vào 1 contextObject -> return value context hiện tại

        + value context được xác định = value prop của <MyContext.Provider> gần nhất ở bên trên component trong tree

        + khi <MyContext.Provider> gần nhất update, hook này trigger render lại với context value mới nhất đã truyền vào MyContext provider

        + cả khi dùng React.memo or shouldComponentUpdate thì việc re-render vẫn diễn ra khi component đó dùng useContext

        + argument của useContext là context object của nó
            useContext(MyContext)
            useContext(MyContext.Consumer)  //WRONG
            useContext(MyContext.Provider)  //WRONG

        + 1 component gọi useContext luôn render lại khi value của context thay đổi

    + useContext(MyContext) tương đương
        static contextType = MyContext trong 1 class
        or <MyContext.Consumer>

    + useContext(MyContext) chỉ giúp đọc context và subscribe sự thay đổi, vẫn cần <MyContext.Provider> ở bên trên 'tree' để provide value cho context này
        const themes ={
            light:{
                bg:...
            },
            dark:{
                bg:...
            }
        }
        const ThemeContext = React.createContext(themes.light)
        fn App(){
            return(
                <ThemeContext.Provider value={theme.dark}>
                    <ToolBar />
                </ThemeContext.Provider>
            )
        }
        fn ToolBar(){
            return (
                <ThemeButton />
            )
        }
        fn ThemeButton(){
            const theme = useContext(ThemeContext)
            return(
                <button style={{bg: theme.bg}} />
            )
        }

## useReducer

    + const [state, dispatch] = useReducer(reducer, initArg, init)
        + thay thế cho useState
        + reducer: (state,action) => newState
        + dùng khi có state phức tạp [nhiều logic, nextState phụ thuộc prevState]

        const initState = {count: 0}
        fn reducer(state,action){
            switch(action.type){
                case 'increment':
                    return {count: state.count +1}
                case 'decrement':
                    return {count: state.count -1}
                default:
                    throw new Error();
            }
        }
        fn Counter(){
            const [state, dispatch] = useReducer(reducer, initState);
            return(
                <>
                    {state.count}
                    <button onClick={()=> dispatch({type:'decrement'})} />
                    <button onClick={()=> dispatch({type:'increment'})} />
                </>
            )
        }

        NOTE: dispatch là stable và ko thay đổi khi re-render

    + chỉ định initState
        + const [state, dispatch] = useReducer(reducer,{count: init})

        NOTE: react ko dùng state = initState [redux]
        init đôi khi phụ thuộc vào props

        + lazy init
            để fn init ở argu 3
            fn init(initCount){
                return {count: initCount}
            }
            const [state,dispatch] = useReducer(reducer, initCount, init)

    + bỏ qua dispatch
        if return về cùng value với state hiện tại từ reducer hook, react bỏ qua mà ko render lại children hay bắn ra effect

## useCallback

    const memoCallback = useCallback(
        () => {
            doSomething(a,b);
        },[a,b];
    )
    // return 1 callback memoried
    + bỏ vào 1 callback và 1 array [deps] -> return 1 bản đã ghi nhớ của callback mà nó chỉ thay đổi khi có 1 phụ thuộc trong array [] thay đổi
    + hữu ích khi để 1 component con mà chỉ render lại phụ thuộc vào 1 số value nhất định để tránh việc render ko cần thiết

    + useCallback(fn, deps) tương đương useMemo(() => fn, deps)

## useMemo

    const memoized = useMemo(() => computeExpensiveValue(a,b),[a,b]);

    + bỏ vào 1 fn và [deps]
    + calculator lại value đã nhớ khi 1 trong những deps thay đổi
    + fn truyền vào useMemo chỉ chạy khi render
    + if ko có deps, new value luôn được calculator mỗi lần render

## useRef

    const refCon - useRef(init)
    + useRef return object ref có thể thay đổi nơi mà .current được khởi tạo và thêm vào value init
    + object return kiên định cho cả lifecycle của component
        fn ComponentA(){
            const inputRef = useREf()
            const buttonClick = () =>{
                inputRef.current.focus()
            }
            return (
                <>
                    <input ref ={inputRef} />
                    <button onClick ={buttonClick} />
                </input>
            )
        }

    + useREf lưu trữ 1 value có thể thay đổi (mutable value) bên trong .current
    + dùng để giữ mọi mutable value
        + khác nhau giữa useRef và tạo 1 object {current:...}
            useRef đưa cùng 1 object ref trong mọi lần render

## useImperativeHandle

## useLayoutEffect

## useDebugValue

## NOTE

Hook có thay thế prop và higher-order component?

Các phương thức lifecycle tương ứng với Hook như thế nào?
Làm thế nào tôi có thể fetching data với Hook?
Tôi nên sử dụng 1 hay nhiều biến state?
Làm sao để lấy được prop và state trước đó?
Tại sao tôi có thể thấy prop và state bên trong function?

# ReactDOM

## render

    ReactDOM.render(element, container [,callback])
        + render element vào DOM trong container và return về 1 ref đến Component [null if stateless component]
        + if element đã được render vào container, thì element này update element đó và mutate DOM khi cần thiết
        + if optional có, nó sẽ thực thi sau khi component render or update

    ko

## hydrate

## unmountComponentAtNode

## findDOMNode

## createPortal

# ReactDOMSever

## renderToString

## renderToStaticMarkup

## renderToNodeStream

## renderToStaticNodeStream

# DOM Element

## khác biệt trong Attr

# SyntheticEvent

# NOTE

# redux

- là libraly và là template dùng quản lý state bằng cách dùng các event(actions)
- là store lưu trữ tập trung cho state cần được dùng trên toàn bộ app

## dùng khi nào

- có nhiều state cần thiết ở nhiều nơi
- state update theo thời gian
- logic update phức tạp

- dùng kiến trúc uni - directional data flow

  - View
  - Actions
  - Store :
    - Dispatcher
      - Middlewares: call API, log
    - Reducer:
      - nhận vào state và action
    - State

- khi nào dùng?

  - data được dùng ở nhiều nơi
  - chức năng undo/redo
    - cùng state, cùng action cho ra stae mới giống nhau
  - cần cache data để tái sử dụng cho những lần sau

- redux có phải chỉ dùng cho reactjs
  - ko, dùng cho js apps
    +reactjs, angular, vuejs, pure js app,...

# Router

# NOTE

onClick={handleClick} ko có () ở cuối
-> ko cần gọi fn [react tự gọi khi có action xảy ra]

mỗi lần render thì có state khác nhau
[khi render thì component có state
unique ]

lifting state up -> share state between components
Component cha(state)
componentConA(state)
componentConB(state)

https://devdocs.io/

# mutate(biến đổi)

    + mutate object trong js
        const person1 = {name: "Huy"}
        const person2 = person1
        person2.name = "Rua"
        console.log(person1) //{name:"Rua"}

        + khai báo const vs object thì chỉ có hiệu nghiệm trên person1 chứ ko có hiệu nghiệm trên các thuộc tính bên trong nó
            person1 = {name: "Rua"}     //WRONG

        + khi gán person1 = person2 thi địa chỉ của 2 biến cùng vùng nhớ và chia sẻ thuộc tính

    + mutate state trong react
        + export fault fn App(){
            const [info, setInfo] = useState({
                name: "Huy",
                ability: {
                    dance:"hiphop",
                    sing:"Opera"
                }
            })
            const changeName = () => ({...info, name:"Rua"})
            return (
                <Header info={info} />
                <button>Change Name</button>
            )
        }
        function Header({info}){
            const [infoH, setInfoH] = useState(null);
            useEffect(() =>{
                setInfoH(info)
            },[info])

            const changeNormal = () => {
                infoH.ability.dance = "Run"
                setInfoH({...infoH});
            }
            return(
                <p>{infoH?.name}</p>
                <p>{infoH?.ability?.dance}</p>
                <button onClick={changeNormal}>change</button>
            )
        }
        // attr ability.dance của info cũng thay đổi mà ko hề setState -> UI ko update

        // khi truyền props từ App vào Header và gán state infoH = info thì infoH và info cùng tham chiếu đến vùng nhớ như nhau (mutate object)
            + khi changeNormal -> thay đổi value của attr dance (chung của infoH và info) và setState lại infoH (UI bên App chưa update vì chưa setState)
            + khi changeName -> thay đổi state info và update UI(ability đã thay đổi trước đó)

        // hướng giải quyết
            + shallow clone
                object.assign
                    changeAssign = () => {
                        const infoA = Object.assign({}, infoH)
                        infoA.ability.dance = 'Run'
                        setInfoH(infoA)
                    }
                    // khi changeAssign -> ability.dance ở info vẫn bị thay đổi mặc dù chưa setState

                dùng spread operator
                    changeOperator = () =>{
                        const infoO = {...infoH}
                        infoO.ability.dance = 'Run'
                        setInfoH(infoO)
                    }
                    // vẫn bị thay đổi info ở App

            cloneDeep Lodash
                const changeCloneDeep = () => {
                    let infoD = cloneDeep(infoH)
                    infoD.ability.dance = 'Run'
                    setInfoH(infoD)
                }
                //cloneDeep là fn của lodash
                // ko bị thay đổi info ở App vì cloneDeep sẽ trở thành object mới tách biệt với object cũ
                // vấn đề về hiệu suất [cloneDeep dùng loop nhiều]
                // parse và stringify -> clone deep [mất giá trị NAN, fn, undefined]

            immutability Helper
                làm thay đổi data của 1 clone object mà ko thay đổi object gốc
                const changeImmu = () => {
                    let infoImmu = update(infoH, {
                        ability: {dance:{$set:'Run'}}
                    })
                    setInfoH({...infoImmu})
                }
                // cách hoạt động của update
                    các attr là giống nhau
                    chỉ có attr cần thay đổi thì vùng nhớ bị thay đổi

        // RECAP
            hạn chế mutate object
