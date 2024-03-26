====CONCURRENCY====

1. Multithreading

2. Thread Synchronization Techniques
3. Sharing Data Between Threads
4. Multiprocessing
5. Async I/O

====ADVanced====

# 9. Sequence Types
## 9.1 Sequences
```py
# A sequence is a positionally ordered collection of items. And you can refer to any item in the sequence by using its index number e.g., s[0] and s[1]
# The mutable sequence types are lists and bytearrays 
#  the immutable sequence types are strings, tuples, range, and bytes.
# In a homogeneous sequence, all elements have the same type [strings are homogeneous sequences where each element is of the same type]
# heterogeneous sequences where you can store elements of different types[List: integer, strings, objects, etc]

# Sequence type vs iterable type
## an iterable may not be a sequence type [a set is iterable but it’s not a sequence]
## An iterable is a collection of objects where you can get each element one by one [a list is iterable.]

# sequence methods
len(seq)
cities = ['San Francisco', 'New York', 'Washington DC']
print(len(cities))  # 3


element in seq
cities = ['San Francisco', 'New York', 'Washington DC']
print('New York' in cities) # true
print('New York' not in cities) # false


seq.index(e)
numbers = [1, 4, 5, 3, 5, 7, 8, 5]
print(numbers.index(5))    # 2

# tìm e xuất hiện lần đầu sau i
seq.index(e, i)
numbers = [1, 4, 5, 3, 5, 7, 8, 5]
print(numbers.index(5, 3))  # 4


seq.index(e, i, j)
numbers = [1, 4, 5, 3, 5, 7, 8, 5]
print(numbers.index(5, 3, 5))   # 4

seq[i:j]
numbers = [1, 4, 5, 3, 5, 7, 8, 5]
print(numbers[2:6]) # [5, 3, 5, 7]

# slice from i too not include j by k step
seq[i:j:k]
numbers = [1, 4, 5, 3, 5, 7, 8, 5]
print(numbers[2:6:2])   # [5,5]

numbers = [1, 4, 5, 3, 5, 7, 8, 5]
print(min(numbers))  # 1
print(max(numbers))  # 8

s3 = s1 + s2
east = ['New York', 'New Jersey']
west = ['San Diego', 'San Francisco']
cities = east + west
print(cities)   # ['New York', 'New Jersey', 'San Diego', 'San Francisco']


city = [['San Francisco', 900_000]]
cities = city + city

print(cities)   # [['San Francisco', 1000000], ['San Francisco', 1000000]]
print(id(cities[0]) == id(cities[1]))  # True

city[0][1] = 1_000_000
print(cities)   # [['San Francisco', 1000000], ['San Francisco', 1000000]]


s = 'ha'
print(s*3)  # hahaha

```
## 9.2 Tuple vs List
```py
# A tuple is immutable while a list is mutable
## list
fruits = ['apple', 'orange', 'banana']
fruits[0] = 'strawberry'
print(fruits)   # ['strawberry', 'orange', 'banana']

## tuple
fruits = ('apple', 'orange', 'banana')
fruits[0] = 'strawberry'
### => TypeError: 'tuple' object does not support item assignment
### can reference a new tuple
fruits = ('apple', 'orange', 'banana')
fruits = ('strawberry', 'orange', 'banana')

fruits = ('apple', 'orange', 'banana')
print(hex(id(fruits)))  # 0x1c018286e00

fruits = ('strawberry', 'orange', 'banana')
print(hex(id(fruits)))  # 0x1c018286e40

# The storage efficiency of a tuple is greater than a list
from sys import getsizeof

fruits = ['apple', 'orange', 'banana']
print(f'The size of the list is {getsizeof(fruits)} bytes.')    # The size of the list is 80 bytes.

fruits = ('strawberry', 'orange', 'banana')
print(f'The size of the tuple is {getsizeof(fruits)} bytes.')   # The size of the tuple is 64 bytes

# Copying a tuple is faster than a list
## copy list =>create new list
## copy tuple => reuse an existing tuple => tuples are immutable
fruit_tuple = ('apple', 'orange', 'banana')
fruit_tuple2 = tuple(fruit_tuple)
print(id(fruit_tuple) == id(fruit_tuple2))  # True

fruit_list = ['apple', 'orange', 'banana']
fruit_list2 = list(fruit_list)
print(id(fruit_list) == id(fruit_list2))  # False

```
## 9.3 Slicing 
```py
```
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