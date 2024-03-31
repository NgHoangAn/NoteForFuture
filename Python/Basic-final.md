1. variable
```py

variable_name = value
# biến luôn được đi kèm với g/trị

message = 'Hello, World!'
print(message)      # Hello, World!

# variable có thể chứa nhiều g/trị khác nhau tại các thời điểm khác nhau
# value có thể thay đổi trong suốt quá trình

# value có thể là string, number...
# RULE đặt tên:
- tên chỉ chứa chữ cái, số, _. có thể bắt đầu bằng chử, dấu _ mà KHÔNG PHẢI BẰNG SỐ

```
2.  string
```py
# NHỮNG GÌ BÊN TRONG DẤU '' ĐỀU LÀ STRING
message = 'This is a string in Python'
message = "This is also a string"

message = "It's a string"

# escape the quotes: \' or \"
message = 'It\'s also a valid string'

# multiline string
help_message = '''
Usage: mysql command
    -h hostname     
    -d database name
    -u username
    -p password 
'''

# sử dụng value của variable trong string: f' Hi {name}'
name = 'John'
message = f'Hi {name}'
print(message)      # Hi John

# auto concat string: 'hi' 'huy' // hi huy
greeting = 'Good ' 'Morning!'
print(greeting)      # Good Morning!

# concat two string : use +
greeting = 'Good '
time = 'Afternoon'

greeting = greeting + time + '!'
print(greeting)        # Good Afternoon!

# [0] nếu xuôi | [-1] nếu ngược

# lenght string
len(str)

# slicing:
string[start:end]
str = "Python String"
print(str[0:2])        # Py

# string là bất biến [ko thể update 1 char trong string] -> tạo string mới xong sửa trên đó
```

3. number
```py
# integer [-1,0,1,2...] type "int"
"+, -, *, /"

"**": số mủ (2**3) => 8


# floats
## division integer always return 'float'

count = 10_000_000_000
print(count)              # 10000000000
```
4. Boolean
```py
# True/False
# Bool()
>>> bool('Hi')
True
>>> bool('')
False
>>> bool(100)
True
>>> bool(0)
False

# Falsy, Truthy
## Falsy: 0, '', False, None, [], (), {}
```
5. Constants
```py
# Python doesn't support constants

# use chữ cái viết hoa đặt tên cho biến. 
FILE_SIZE = 1000
```
## 6. Type Conversion
```py
# nhập từ bàn phím:
input('nhập vào:') => return string

value = input('Enter a value:') # nhập 5
print(value) 5 có type là string

int(str)
int(value)  # 5 có type là int

float(str), 
bool(val), 
str(val),

type(val): type(100) => int
```