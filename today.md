python
39. Unpacking Tuple
```py

```

DSA

25. Array

        - lưu trữ 1 số phần tử có cùng type data
        - array = [element[index], ...]
        - time: O(1)
        - memory: local
        - ko thể thay đổi kích thước mảng khi đang chạy

        - dynamic array:
        - NHẬP VÀO N(NGUYÊN DƯƠNG) VÀ N P/TỬ TRONG DÃY A => TỔNG CỦA DÃY

```py
n = (int)(input())
a = []
for i in range(n):
        a.append((int)(input()))
Sum = 0
for i in range(n):
        Sum+ = a[i]
print(Sum)
```

        - NHẬP VÀO N(NGUYÊN DƯƠNG), N P/TỬ TRONG DÃY A. THAY ĐỔI G/TRỊ CỦA P/TỬ THÀNH BÌNH PHƯƠNG CỦA NÓ.

```PY
n = int(input())
a = []
for i in range(n):
        a.append(int(input()))
for i in range(n):
        a[i] *= a[i]
for i in range(n):
        print(a[i], end = ' ')
```
