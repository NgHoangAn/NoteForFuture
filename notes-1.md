cấu trúc file html
các thẻ meta
thẻ html
    h1 - h6
    p
    img
    a
    ul, li, ol
    table
        thead(th), tbody(tr - td),
    input
    button
    div
thuộc tính trong html
css trong html
    internal
        viết css trong cặp thẻ style
    external
        link css vào
    inline
        viết css trong attribute style
css selectors
    id, class
priority - do uu tien
    internal va external ko co phan biet, ai viet sau thi lấy
    inline->id->class->tag
    equal specificity
    universal selector and inherited

    =============================================================================

    
# 1. phép so sánh trong JavaScript
    - so sánh nghiêm ngặt
        - sử dụng ba dấu bằng ===
        - Cả kiểu và giá trị phải giống nhau
        - không cho phép ép kiểu dữ liệu  (coercion)
            - ép kiểu tường minh
            - ép kiểu ngầm định
    - So sánh trừu tượng
        - sử dụng Dấu bằng kép
        - là so sánh giá trị bình đẳng và được phép ép kiểu dữ liệu
        - được so sánh sau khi chuyển đổi chúng thành cùng một kiểu dữ liệu
![](1-ep%20kieu%20tuong%20minh.png)
![](2-ep%20kieu%20ngam%20dinh.png)


![](3-callback.png)




# 4. && là?
    - tìm giá trị falsy đầu tiên và trả về
    - trả về giá trị cuối nếu không tìm thấy

# 5. || là?
    - tìm giá tị truthy đầu tiên và trả về

# 6. Falsy và truthy
    - Falsy
        0, 0n, undefined, null, NaN, false, ""
    - Truthy
        còn lại

# 7. Undefined và null?
    - Null
        - một giá trị rỗng hoặc không tồn tại
        - là 1 object
    - Undefined
        - một biến đã được khai báo
        - giá trị chưa xác định

# 8. IIFEs?
   - Một Immediately Invoked Function Express  được thực thi ngay sau khi nó được tạo


# 10. Ba giai đoạn của sự lan truyền sự kiện
    -  capturing trước sau đó bubbling
        - Trong giai đoạn capturing các sự kiện truyền từ Window qua  DOM tree cho đến khi nó đến nút đích
    - Bubbling ngược lại với giai đoạn capturing
        - các sự kiện nổi bong bóng (buble up) lên cây DOM


# 12.Number.MIN_VALUE > 0 ??
    - True
    - Number.MIN_VALUE là 5e-234
    - giá trị nhỏ nhất là Number.NEGATIVE_INFINITY

# 13. Math.max() nhỏ hơn Math.min()?
    - Math.min () trả về infinity và Math.max () trả về -infinity



# 15. Sự khác nhau giữa var, let và const
    - let và var có thể được gán lại (re-assigned) trong khi const thì không
    - const cho phép biến thay đổi (variable mutation), có nghĩa là nếu nó đại diện cho một mảng hoặc một đối tượng, nó có thể thay đổi. Bạn chỉ không thể chỉ định lại chính biến đó
    - let có những lợi thế đáng kể so với var, khiến nó trở thành lựa chọn tốt hơn trong hầu hết, nếu không phải là tất cả các trường hợp mà một biến cần thay đổi

    - các biến được khai báo bằng var luôn được đưa lên đầu phạm vi tương ứng của chúng
    - các biến được khai báo bằng const và let được cũng được đưa lên, nhưng nếu bạn cố gắng truy cập chúng trước khi chúng đã khai báo, bạn sẽ gặp lỗi ‘vùng chết tạm thời’ (temporal dead zone).  Đây là hành vi hữu ích, vì var có thể dễ bị lỗi hơn, chẳng hạn như tình cờ bị gán lại

    - var là phạm vi chức năng (function-scoped), let và const là phạm vi khối (block-scoped)

# 16. xác định một biến mà không có từ khóa?
    - nếu x chưa được xác định, thì x = 1 là viết tắt của window.x = 1
    sử dụng strict mode (use strict):
        - gặp lỗi khi khai bao biến ko có từ khóa:
            - Uncaught SyntaxError: Unexpected indentifier

# 17. event delegation?
    - sử dụng để phản hồi các sự kiện (event) của người dùng thông qua một node cha thay vì mỗi node con



# 19. Prototype chain?
    - trong js là kế thừa nguyên mẫu
        - truy cập thuộc tính của 1 đối tượng
            - tìm trong đối tượng
            - tìm kiếm trong nguyên mẫu của đối tượng
            - ...cho đến khi tìm thấy
    - mọi thứ đều được kế thừa từ Object

# 20. DOM?
    - là 1 API liên kết các p/tử tài liệu HTML và XML -(node)- thành 1 cấu trúc cây
    - chứa thông tin về các mối quan hệ cha-con giữa các nút
        - node là các đối tượng co thể thao tác:
            - styles
            - contentt
            - placement changes

# 26. map và forEach()
    forEach thay đổi các mục gốc trong mảng
    map trả về một mảng đã biến đổi trong khi vẫn giữ nguyên bản gốc


palindrome?
    là một từ hoặc một cụm từ mà khi ta đọc xuôi hoặc đọc ngược thì nó cũng như nhau

https://viblo.asia/p/co-che-bat-dong-bo-trong-javascript-jvElaO1zKkw

for-in
    lặp qua tất cả các thuộc tính của đối tượng theo cách thức từng bước

xử lý ngoại lệ
    dùng try...catch


Currying?
    có nghĩa là biến đổi một hàm có n đối số, thành n hàm của một hoặc ít đối số
    Currying không thay đổi hành vi của một hàm. Nó chỉ thay đổi cách nó được gọi

Phương thức PreventDefault ()
    dùng để hủy bỏ một phương thức
    ngăn không cho sự kiện thực hiện hành vi mặc định

    

# 1. khác nhau giữa undefined và not defined
    https://stackoverflow.com/questions/20822022/whats-the-difference-between-variable-definition-and-declaration-in-javascript



    
