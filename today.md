OOP
1. Class and Object
2. special method
3. property
4. single inheritance
4.4 __slots__
```py

```
4.5
```py

```
5. enumeration
6. solid principles
7. multiple inheritance
8. descriptors
9. meta programming
10. exceptions

1. Array
```py
# lưu trữ 1 số phần tử có cùng type data
# array = [element[index], ...]
# time: O(1)
# memory: local
# ko thể thay đổi kích thước mảng khi đang chạy

# dynamic array:

# EX1:
## NHẬP VÀO N(NGUYÊN DƯƠNG) VÀ N P/TỬ TRONG DÃY A => TỔNG CỦA DÃY
n = (int)(input())
a = []
for i in range(n):
        a.append((int)(input()))
Sum = 0
for i in range(n):
        Sum+ = a[i]
print(Sum)

# EX2: NHẬP VÀO N(NGUYÊN DƯƠNG), N P/TỬ TRONG DÃY A. THAY ĐỔI G/TRỊ CỦA P/TỬ THÀNH BÌNH PHƯƠNG CỦA NÓ.
n = int(input())
a = []
for i in range(n):
        a.append(int(input()))
for i in range(n):
        a[i] *= a[i]
for i in range(n):
        print(a[i], end = ' ')

# EX3: nhập:
## N nguyên dương
## N p/tử của dãy a
## k,x (0 <= k <= n)

##  chèn x vào dãy a [k < x < k-1]
## input                # output
4                           
1 2 3 4                     1 10 2 3 4
1 10

a = int(input())
ori_list = []
result = ""

for i in range(a):
    ori_list.append(input())

k = int(input())
x = input()

for i in range(a+1):
    if i < k:
        result = result + ori_list[i] + ' '
    elif i == k:
        result = result + x + ' '
    else:
        result = result + ori_list[i-1] + ' '
print(result)
```

