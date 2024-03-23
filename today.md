====CONCURRENCY====

1. Multithreading

2. Thread Synchronization Techniques
3. Sharing Data Between Threads
4. Multiprocessing
5. Async I/O

====ADVanced====
1. Variables & Memory Management
1.1 References
```py
# a variable references on object that hold a value
# variable ae references

# find the memory address of an object references by a variable
counter = 100
print(id(counter)) # 14717671523072
print(hex(id(counter))) # 0x7ffb62d32300

# Reference counting
## An object in the memory address can have one or more references
counter = 100
max = counter

# Once an object doesn’t have any reference, Python Memory Manager will destroy that object and reclaim the memory
import ctypes

def ref_count(address):
    return ctypes.c_long.from_address(address).value

numbers = [1, 2, 3]
numbers_id = id(numbers)

print(ref_count(numbers_id))  # 1

ranks = numbers
print(ref_count(numbers_id))  # 2

ranks = None
print(ref_count(numbers_id))  # 1

numbers = None
print(ref_count(numbers_id))  # 0
```
1.2 Garbage Collection
```py
# khi có 1 object tham chiếu đến chính nó or 2 object tham chiếu lẫn nhau  ==> circular references[python memory manager cannot remove object with circular references] ==> use garbage collector

import gc
import ctypes

## counting ref
def ref_count(address):
    return ctypes.c_long.from_address(address).value

## check if exist
def object_exists(object_id):
    for object in gc.get_objects():
        if id(object) == object_id:
            return True
    return False

# 2 class A,B tham chiếu lẫn nhau
class A:
    def __init__(self):
        self.b = B(self)
        print(f'A: {hex(id(self))}, B: {hex(id(self.b))}')

class B:
    def __init__(self, a):
        self.a = a
        print(f'B: {hex(id(self))}, A: {hex(id(self.a))}')

gc.disable()

a = A()     # B: 0x20fccd148e0, A: 0x20fccd75c40
            # A: 0x20fccd75c40, B: 0x20fccd148e0

a_id = id(a)
b_id = id(a.b)
print(ref_count(a_id))  # 2 [the variable a and the instance of B]
print(ref_count(b_id))  # 1 [the instance of A]

## check instance
print(object_exists(a_id))  # True
print(object_exists(b_id))  # True

a = None
print(ref_count(a_id))  # 1
print(ref_count(b_id))  # 1

print(object_exists(a_id))  # True
print(object_exists(b_id))  # True

## it can detect the circular reference, destroy the objects, and reclaim the memory
gc.collect()

print(object_exists(a_id))  # False
print(object_exists(b_id))  # False

print(ref_count(a_id))  # 0
print(ref_count(b_id))  # 0

# ** Note**
## garbage collector ovoid(tránh) memory leak bằng cánh phát hiện circular references và hủy chúng
```
1.3 Dynamic Typing 
```py
# Python is a dynamically typed language
message = 'Hello'
# the message variable is just a reference to an object which is a string. There is no type associated with the message variable

message = 100
# Python creates a new integer object, and the message references to the new integer object

# determine the type of object that a variable currently references
message = 'Hello'
print(type(message))    # <class 'str'>

message = 100
print(type(message))    # <class 'int'>
```
2. Integer types
3. Float
4. Decimal
5. Variable scopes
6. Closures
7. Decorators
8. Named Tuples
9. Sequence Types
10. Iterators and Iterables
11. Generators
12. Context Managers

====Regex====
====Unit Test====
====NumPy====

====CSS====

















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

https://www.javascripttutorial.net/

https://www.mysqltutorial.org/
![sample database diagram](sample-database-diagram.png)
====BaSic====
1. Querying data
```sql
SELECT select_list, select_list1,...
FROM table_name;

```
2. Sorting data
3. Filtering data
4. Joining tables
5. Grouping data
6. Sub queries
7. Set operator
8. Managing database
9. Working with table
10. constraints
11. Data types
12. MOdifying data
13. Common table Expression
14. Locking
15. Globalization
16. User-define variable
17. import & export CSV
18. Adv techniques
====Adv====
1. Stored procedures
2. Conditional Statements
3. Loops
4. Error Handling
5. Cursors
6. Stored Function
7. Stored Program Security
8. Transaction
9. Trigger
10. Event
11. Views
12. Index
    1. Creating and Managing
    2. Index Types
    3. INdex Hints
13. Json
    1. search json document
    2. Modifying Json document
    3. querying Json document
    4. Json array
    5. Aggregating Json Data
    6. index Json data
    7. Getting attribute Json value
    8. Json table fn
    9. validation fn
    10. utility fn
14. Full-text search
====Administration====
==== Function====
====API====
1. python
2. Nodejs

https://react-tutorial.app/app.html

https://www.tutorialspoint.com/reactjs/reactjs_pagination.htm

https://www.javazerotomastery.com/