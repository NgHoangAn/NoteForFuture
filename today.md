====CONCURRENCY====

1. Multithreading

2. Thread Synchronization Techniques
3. Sharing Data Between Threads
4. Multiprocessing
5. Async I/O

====ADVanced====





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