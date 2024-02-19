1. use strict
- khi ccó thêm tính năng mới và sửa đổi một số tính năng cũ. để giử cho mã cũ được hoạt động nên các sửa đổi như vậy đều bị tắt theo mặc định. nên  là muốn dùng thì kích hoạt nó bằng cách thêm "use strict"
- thêm vào đầu script
- khi sử dụng mà có class và module thì không cần khai báo 'use strict' vì nó đã tự động thêm rồi.

2. Variable
- là nơi lưu trữ có tên cho dữ liệu
>- [var] : không bị giới hạn trong pham vi
hàm, lưu trữ toàn cục (global scope)

>- [let] (từ ES6): bị giới hạn trong phạm vi
hàm [tránh viết đè lên giá trị biến bên
ngoài hàm]

>- [const] (từ ES6): biến không thể gán lại
giá trị sau khi được khởi tạo [đảm bảo an
toàn dữ liệu]

>=> [kết luận]: 
> - Nên dùng let, const thay cho var [tránh các vấn đề liên quan đến phạm vi biến và vòng đời biến]

>Nâng cao: sử dụng các quy tắc cam kết như
Immutable Infrastructure để đảm bảo tính
ổn định và dễ bảo trì

***
3. Data types
- PART-1
> có 8 loại data type
 - dynamic type: tồn tại data type nhưng các biến không bị ràng buộc với bất kì kiểu nào

- NUmber: ngoài các kiều số bình thường ra còn có Infinity,  Infinity và NaN
    + (1/0) infinity
    + NaN thì là lỗi tính toán, kq của phép toán không xác định 

- BigInt: số nguyên có độ dài tùy ý
- String: 0 or nhiều kí tự, ko có đơn lẻ. ''/""/``
- Boolean: true, false
- Null: tham chiếu đến 1 đối tượng không tốn tại[con trỏ rỗng]
- Undefined: giá trị không được gán
- object
- symbol: mã định danh duy nhất
- typeOf

- PART-2
1. Methods of primitives
2. Number
    - toString(base)--> string  
        base: 2 to 36. default 10
        base = 16: hex color,character encodings, digit 0..9 or A..F.
        base = 2: bitwise operations (0 or 1)
        base = 36: 0..9 and a..z
    
    - Rounding
        .floor: 3.1 -> 3 ||| -1.1 -> -2 (down)
        .ceil: 3.1 -> 4 ||| -1.1 -> -1  (up)
        .round: 3.1 -> 3 ||| 3.6 -> 4  (nearest)
    
    - isFinite and isNaN
    - parseInt and parseFloat

3. String
    - special character
    - string are immutable
    - indexOf ||| lastIndexOf
    - includes  ||| startsWith ||| endsWith
    - slice  |||  substr  ||| substring
    - codePointAt ||| fromCodePoint
    - locateCompare

4. Array
    - lưu trữ có thứ tự
    - Declaration; 2 cách
    - pop ||| push, shift ||| unshift
    - for ||| for..in
    - method
        + add/remove items: 
            + splice[start, deleteCount, ele1...eleN]: xóa deleteCount p/tử từ start và thêm vào ele1..eleN
        
            + slice[start, end]: copy vào array mới từ start --> end( not include end)

            + concat(arg1, arg2,...): tạo ra arr mới từ arr cũ và có thêm arg1,arg2,...
        
        + Search in array
            + indexOf/lastIndexOf/includes
            + find/findIndex/findLastIndex
            + filter
        
        + transform an array
            + map
            + sort(n)
            + reverse
            + split / join
            + reduce / reduceRight

5. Iterables
- Symbol.iterator
    
6. Map and Set
- khác nhau của Map và Object: Map có thể sử dụng bất kì loại key nào(string,number,boolean)
- method
    + new Map()
    + set(key, value)
    + get(key) --> value of key / undefined
    + has(key) --> true / false
    + delete(key)
    + clear()
    + size()

- loop Map:
    + keys()
    + values()
    +  entries()

7. WeakMap and WeakSet
8. Object.keys, value, entries
9. Destructuring
- Array Destructuring
- Object Destructuring
- Nested Destructuring
10. Date and time
11. JSON method

4. Interaction: alert, prompt, confirm
- alert: show ra thông báo có nút ok

-prompt: result = prompt(title,[default]);
    + show window có message, input và ok/cancel
    + [default]: tham số tùy chọn, ko bắt buộc
    + return về value trong input(ok), null(cancel)

- result = confirm(question)
    + return true(ok)/ false(cancel) 

5. type conversion
- string conversion: dùng khi cần 1 string từ 1 value nào đó
        + alert(value) ko được, mà phải đổi sang string

- number conversion: tự động đổi trong toán và biểu thức
    + rule:
        undefined   --> NaN
        nul         --> 0
        true,false  --> 1,0
        string      --> bỏ k/trắng ở đầu-cuối, nếu chuỗi trống là 0, còn lại là NaN
- boolean
    + "", 0, null, undefined, NaN ==> false
    + còn lại ==> true

6. comparisons
-   null === undefined // false
-   null == undefined // true
-  

7. function
- declaration: tạo 1 fn mới

        let message = 'Hello' //outlet variable
    + function name(para1, para2,.... paraN){
        let message = 'Hi'; // local variable
    }
    + outlet variable chỉ được dùng khi không có local variable
    + tham số là biến được liệt kê bên trong () trong phần khai báo hàm
    + đối số là g/tri được truyền cho hàm khi nó được gọi
    + nếu 1 hàm được gọi mà không cò đối số thì g/trị là undefined

- fn expressions
    + let name = function(a,b){};
    + fn là 1 value
    + callback fn: 
            function ask(question, yes, no){
                if(confirm(question)) yes()
                else no();
            }
            function yes(){}
            function no(){}
            ask("Are you sure?",yes,no);
        - arguments "showOk" và "showCancel" của "ask" là callback fn hay callback

        - declaration fn được khai báo dưới dạng 1 câu lệnh riêng biệt. Còn expression được tạo bên trong 1 biểu thức or bẹn trong 1 cấu trúc syntax khác

        - expression fn được tạo khi quá trình thực thi đến nó và có thể sử dụng từ đó về sau. Còn Declaration fn thì có thể được gọi trước khi nó được defined

        - trong strict mode thì khi có declaration fn trong code block thì nó sẽ khả dụng trong mọi nơi miễn là còn trong code block

- arrow fn
    + let func = (arg1, arg2,...) => expression;
                (...args) => {body}

8. Objects
    - empty object:
        let user = new Object(); // Object constructor
        let user = {}; // object literal
    - square brackets
        let user = {};
        // set
        user["likes birds"] = true;
        // get
        alert(user["likes birds"]); // true
        // delete
        delete user["likes birds"];

+ object references
    + object thì lưu trữ và copy theo them chiếu còn g/tri nguyen thủy thì copy toàn bộ g/trị
    + 2 object = nhau khi chúng là cùng 1 object
    + 2 object độc lập riêng biệt thì ko = nhau, mặc dù chúng nhìn giống nhau
    + object mà khai bao bằng "const" thì CÓ THỂ SỬA
    + clone object
        dùng assign
        object.assign(clone, ...source)
        nếu tên thuộc tính sao chép đã tồn tại thì sẽ ghi đè lên
        structuredClone

+ garbage collection
+ constructor fn
    -   function User(name){
        this.name = name;
        this.isAdmin = false;}

        let user = new User(“John”);

    - Test coi có phải là fn được gọi tù "new" hay không
        "new.target"
        function User(){
            alert(new.target)
        }
        without "new" -> undefined
        ngược lại -> return fn đang gọi
    - không có câu lệnh return --> đã được tự động return ẩn(return this)

+ chaining '?.'
    - dùng để truy cập các thuộc tính lồng nhau kể cả khi thuộc tính trung gian không tồn tại
        if value trong value.prop là null or undefined --> undefined

///////MAI LÀM//////
+ Symbol
+ Object to primitive conversion
    - string
    - number
