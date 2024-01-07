
1. class:
    - là bản thiết kế thể hiện của 1 lớp (plan instance of class)
    - là khuôn mẫu logic chia sẻ các props và method
    - modifiers -> class name -> superclass -> interface -> body
        public test {}

2. object:
    - là 1 thể hiện của class
    - là thực thể (entity) có behavior và state(trạng thái)

3. method:
    - behavior của object là method

4. instance variable:
    - mỗi object có 1 tập hợp entity duy nhất của riêng nó
    - state của 1 object được tạo bởi các value được assign cho các biến instance này

//
/**/
/** .... */

5. Source name file
    - nếu là class public thì phải trùng tên

6. phân biệt hoa - thường

7. scope(class và method):
    - cho phép sửa: default, public, protected, private
    - ko cho sửa: final, abstract, static, transient, synchronized, volatile, native

8. public static void main(String [] args)
    - public: jvm có thể execute method mọi nơi
    - static: 
    - void:
    - main: 
    - string[]: method main accept 1 argument duy nhất

=== DATA TYPES ===
    - primitive types: boolean, char, int, short, byte, long, float, doubles
    - Object type(reference data type): String, array,...
        String s = "..."
        Sting s1 = new String("...")

        interface: có method và variable abstract(assign method no content)
    - cấu trúc lưu trữ:
        - primitive: trong 1 stack
        - non-primitive: reference var lưu trong stack và original object lưu trong heap
    - primitive ko có default value, non-pri có default là null

=== IDENTIFIERS === 
- [ AZ ],[ az ],[ 0-9 ]
- $
- _

=== Operator ===
- +, -, *, /, %
- ++, --, -, +, !
- ... ? ... : ...
- &, |, ^
- >>, <<

=== Variable ===
- local     :   nằm trong {}, method, constructor
                k/tạo local var là bắt buộc trước khi dùng
- instance  :   + nằm trong class và bên ngoài bất kì method, {}, constructor nào
                + được tạo khi object được tạo và hùy khi object bị hủy
                + chỉ co thể truy cập = tạo object
                + constructor là không bắt buộc. default value phụ thuộc vào type data của variable (String:null, int:0, Wrapper Integer:null)
                + mỗi object sẽ có bản sao instance var riêng
                + class Test{
                    // Instance var
                    public String geek;
                    public int i;
                    public Integer I;
                }

- static    :   + k/báo giống instance nhưng có thêm static
                + chỉ có 1 bản copy của static variable cho mỗi class
                + được tạo khi thực thi c/trình và auto hủy khi thực thi kết thúc
                + nếu truy cập static var như instance var( thông qua object) => thông báo cảnh báo và ko dừng c/trình. auto thay thế tên object = tên class

=== Scope ===
- member scope: k/báo bên trong class và bên ngoài hàm trong class
- local scope:k/báo bên trong method
- block scope: k/báo trong {} bên trong method

=== Wrapper class === **
- là class có object wrap or chứa các data type ng/thủy
- có thể gán 1 g/trị ng/thủy vào 1 object wrapper
- lợi ích:
    + cần thiết khi sửa đổi đới số được truyền vào method
    + collections chỉ cho phép data type object