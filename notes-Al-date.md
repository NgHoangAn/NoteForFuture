# Linear Search
    - tìm kiếm p/tử cho trước trong 1 danh sách = duyệt lần lượt từng p/tử của danh sách -> tìm được or hết
    - cách:
        băt đầu duyệt từ đầu đến cuối mảng với x
        p/tử  đang duyệt = x thì return vị trí
        ko tìm thấy or hết -> return -1
        độ phức tạp là O(1) -> O(n) 
# Binary Search
    - tìm kiếm vị trí trongn mảng đã sắp xếp
    - chia khoảng tìm kiếm thành 1/2 -> ss x với giá trị ở giữa
        - nếu g/trị nhỏ hơn g/trị ở giữa thì tìm bên trái, ngược lại
         
# Interpolation Search
    - có xu hướng tiến đến gần vị trí, giá trị tìm kiếm.
    - tìm ra phần tử gần với giá trị tìm kiếm  nhất và bắt đầu từ đó để tìm
    - cách tìm:
        - x là số cần tìm, t là tập
        - s = left +(right-left) * 1/2
        - thay 1/2 = (x - t[left]) / (t[right] - t[left])
        - ta được:
            s = left + (x - t[left]) * (right - left) / (t[right] - t[left])
        - nếu t[s] === x thì return, ko thì có 2 trường hợp:
            - t[s] < x ==> left = s + 1
            - t[s] > x ==> right = s - 1
# Bubble Sort
# Insertion Sort
# Selection Sort
# Merge Sort
# Quick Sort



# phân tích tiệp cận
    - phân tích tiệp cận

        + ước lượng được thời gian chạy
        + kết luận tốt nhất
            + trường hợp tốt nhất
            + trường hợp trung bình
            + trường hợp xấu nhất

        + là tiệm cận dữ liệu đầu vào 
            + nếu giải thuật không có Input -> giải thuật sẽ chạy trong một lượng thời gian cụ thể và là hằng số

        + exp:
            - thời gian chạy của một phép tính nào đó
                + là một hàm f(n)
                + với một phép tính khác là hàm g(n<sup>2</sup>)
                ==> thời gian chạy của phép tính đầu tiên sẽ tăng tuyến tính với sự tăng lên của n
                ==> thời gian chạy của phép tính thứ hai sẽ tăng theo hàm mũ khi n tăng lên
                ==> khi n là khá nhỏ thì thời gian chạy của hai phép tính là gần như nhau
        
        + Big Oh Notation
            + Ο(n) là một cách để biểu diễn tiệm cận trên của thời gian chạy của một thuật toán
            + ước lượng độ phức tạp thời gian trường hợp xấu nhất
            + O(f(n)) = {g(n)}
                if: c > 0
                    n(0): g(n) <= c*f(n) // [n > n(0)]
        
        + Omega Notation
            + Ω(n) là một cách để biểu diễn tiệm cận dưới của thời gian chạy của một giải thuật
            + ước lượng độ phức tạp thời gian trường hợp tốt nhất
            + Ω(f(n)) ≥ { g(n) }
                if: c > 0
                    n(0): g(n) <= c*f(n) // [n > n(0)]

        + Theta Notation
            + biểu diễn cả tiệm cận trên và tiệm cận dưới của thời gian chạy của một giải thuật
            + θ(f(n)) = { g(n) }
                if: g(n) = O(f(n))
                    g(n) = Ω(f(n)) // [n > n(0)]


# giai thuat tham lam (Greedy)
    + là giải thuật tối ưu hóa tổ hợp

    + tìm kiếm, lựa chọn giải pháp tối ưu địa phương ở mỗi bước
    => hi vọng tìm được giải pháp tối ưu toàn cục

    + lựa chọn giải pháp nào được cho là tốt nhất ở thời điểm hiện tại
    => giải bài toán con nảy sinh từ việc thực hiện lựa chọn đó

    + Lựa chọn có thể phụ thuộc vào lựa chọn trước đó

    + quyết định sớm và thay đổi hướng đi của giải thuật
    + không bao giờ xét lại các quyết định cũ
    ==> không tối ưu để tìm giải pháp toàn cục

    + exp:
        + 1, 2, 5, và 10 xu 
        + chọn ra 18 xu
            - áp dụng tham lam:     + chọn 10 xu (còn 8 xu)
                                    + chọn 5 xu (còn 3 xu)
                                    + chọn 2 xu (còn 1 xu)
                                    + chọn 1 xu
        ==> chọn 4 lần

        + 1, 7, 10 xu
        + chon 15 xu
            - áp dụng tham lam:     + 10
                                    + 1
                                    + 1
                                    + 1
                                    + 1
                                    + 1
        => chọn 6 lần (trong khi có thể chọn 3 lần: 7 + 7 + 1)

        ==> giải thuật tham lam:    + tìm kiếm giải pháp tôi ưu ở mỗi bước
                                    + thất bại trong việc tìm ra giải pháp tối ưu toàn cục


# chia để trị (divide & conquer)

    + chia bài toán đó thành các bài toán con nhỏ hơn
    + chia cho đến khi các bài toán nhỏ này không thể chia thêm nữa
    + giải quyết các bài toán nhỏ nhất
    + kết hợp giải pháp của tất cả các bài toán nhỏ để tìm ra giải pháp của bài toán ban đầu

    + tiến trình
        + divide/beak
            + chia bài toán ban đầu thành các bài toán con
            + sử dụng phương pháp đệ qui
            + các bài toán con được gọi là "atomic – nguyên tử"
        
        + Conquer/Solve
            + giải các bài toán con
        
        + Merge/Combine
            + kết hợp chúng một cách đệ qui để tìm ra giải pháp cho bài toán ban đầu
    
    + Hạn chế
        + Làm thế nào để chia tách bài toán một cách hợp lý thành các bài toán con
        + Việc kết hợp lời giải các bài toán con được thực hiện như thế nào

    Giải thuật sắp xếp trộn (Merge Sort)
    Giải thuật sắp xếp nhanh (Quick Sort)
    Giải thuật tìm kiếm nhị phân (Binary Search)
    Nhân ma trận của Strassen

# Quy hoạch động ( Dynamic Programming )
    + chia nhỏ bài toán thành các bài toán con nhỏ hơn
    + kết quả của các bài toán con này được lưu lại => được sử dụng cho các bài toán con tương tự hoặc các bài toán con gối nhau (Overlapping Sub-problems)

    + dùng khi
        + được chia thành các bài toán con tương tự nhau -> tái sử dụng kq
        + tối ưu hóa
        
    + 
        Dãy Fibonacci
        Bài toán tháp Hà Nội (Tower of Hanoi)
        Bài toán ba lô

# data array
    + 
    + ưu điểm:
        Truy câp phàn tử vơi thời gian hằng số O(1)
        Sử dụng bộ nhớ hiệu quả
        Tính cục bộ về bộ nhớ

# Linked List
    + một dãy các cấu trúc dữ liệu được kết nối với nhau thông qua các liên kết
    + là một cấu trúc dữ liệu bao gồm một nhóm các nút tạo thành một chuỗi
    + Mỗi nút gồm dữ liệu ở nút đó và tham chiếu đến nút kế tiếp trong chuỗi
        + Link: có thể lưu giữ một dữ liệu được gọi là một phần tử
        + Next: Mỗi liên kết chứa một link tới next link được gọi là Next
        + First: một Danh sách liên kết bao gồm các link kết nối tới first link được gọi là First

    + Biểu diễn Ds Liên kết
    
    + Danh sách liên kết chứa một phần tử link thì được gọi là First
    + Mỗi link mang một trường dữ liệu, một trường link được gọi là Next
    + Mỗi link được liên kết với link kế tiếp bởi sử dụng link kế tiếp của nó.
    + Link cuối cùng mang một link là null để đánh dấu điểm cuối của danh sách

    + các loại dslk:
        + Danh sách liên kết đơn: hỉ duyệt các phần tử theo chiều về trước
        + Danh sách liên kết đôi: các phần tử có thể được duyệt theo chiều về trước hoặc về sau
        + Danh sách liên kết vòng:  + phần tử cuối cùng chứa link của phần tử đầu tiên như là next
                                    + phần tử đầu tiên có link tới phần tử cuối cùng như là prev
    
    + Các hoạt động của dslk:
        + Hoạt động chèn
            + khi đặt một nút vào vị trí cuối của danh sách, thìnút thứ hai tính từ nút cuối cùng của danh sách sẽ trỏ tới nút mới và nút mới sẽ trỏ tới NULL
        + Hoạt động xóa (phần tử đầu)
        + Hiển thị
        + Hoạt động tìm kiếm
        + Hoạt động xóa (bởi sử dụng khóa)

    + lk đôi:
        + link : mỗi link của một Danh sách liên kết có thể lưu giữ một dữ liệu
        + next : mỗi link của một Danh sách liên kết có thể chứa một link tới next link
        + Prev : mỗi link của một Danh sách liên kết có thể chứa một link tới previous link
        + first & last : một Danh sách liên kết chứa link kết nối tới first link được gọi là First và tới last link được gọi là Last

        + các hoạt động:
            + chèn:
                + đầu
                + cuối
                + sau
            + xóa
                + đầu
                + cuối
                + key
            + hiển thị
                + về phía trước
                + về phía sau




 