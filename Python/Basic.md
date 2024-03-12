1.  variable
```py
# variable_name = value
# biến luôn được đi kèm với g/trị
```
2.  string
```py
# '' | "" | """...""" (multiline)

# escape the quotes: \' or \"

# using value of var in a string: f' Hi {name}'

# auto concat string: 'hi' 'huy' // hi huy
# concat two string : use +

# [0] nếu xuôi | [-1] nếu ngược

# lenght string
len(str)

# slicing:
string[start:end]

# string là bất biến [ko thể update 1 char trong string] -> tạo string mới xong sửa trên đó
```
3.  number
```py
# integer [-1,0,1,2...] type "int"
"+, -, *, /"

"**": số mủ (2**3) => 8

# floats
## division integer always return 'float'
```
4.  Boolean
```py
# True/False
# Bool()
# Falsy, Truthy

```
5.  Constants
```py
# Python doesn't support constants

# use chữ cái viết hoa đặt tên cho biến. 
FILE_SIZE = 1000
```
6.  Type Conversion
```py
int(str), 
float(str), 
bool(val), 
str(val),

type(val): type(100) => int
```
7.  Ternary Operator

8.  Loop
```py
for index in range(n| start,stop| start,stop,step):
    statement
    if condition:
        break|continue

while condition:
    body
        pass( implement later )
    if condition:
        break|continue
```
9.  FN
```py
def nameFN(param1, param2=value,...):
    code

nameFN(argument)

# Recursive FN
def fn():
    if condition:
        stop call
    else:
        fn()
```
10. Lambda Expressions
```py
# dùng khi viết fn dùng 1 lần
# define anonymous fn
# chứa nhiều argument mà chỉ có 1 expression(biểu thức)

lambda param: expression
        lambda fName,lName: f"{fName} {lName}"
```
11. Fn Docstring
12. list
```py
empty_list = []
todo_list = ['learn','work', 'write CV']
print(todo_list) => [learn, work, write CV]

print(todo_list[0]) => learn // first element
print(todo_list[-1]) => write CV //last element

todo_list[1] = 'home' => ['learn', 'home', 'write CV']

todo_list.append('how') =>  ['learn', 'home', 'write CV', 'how'] // add last
todo_list.insert(2, 'game') =>  ['learn', 'home', 'game', 'home', 'write CV', 'how'] // insert at index 2

del todo_list[0] =>  ['work', 'write CV'] // remove first
todo_list.pop() => 'how' //remove last
todo_list.remove('work') => [learn, write CV]
```
13. tuples
```py
# create list of items cannot be changed
# tuples is an immutable list
traffic_light = ('red', 'green', 'yellow')

# if try changed element in tuple 
=> error: tuple object does not support item assignment

number = (3,) => <class 'tuple'>
number = (3) => <class 'int'>

# can assign a new tuple to a variable that references a tuple.
traffic_light = (1,2,3,4,5) // work
```
14. sort list
```py
traffic_light.sort([,reverse = true|false])
# sort a list of string
##sort  by alphabetical order
## if reverse = 'true' => reverse alphabetical order

# sort a list numbers
## smallest -> largest
## if reverse = true => largest -> smallest

# sort a list of tuple
infos = [('huy', 20, '54kg''),
        ('an', 18, '45kg''),
        ('rua', 26, '60kg'')
        ]

# step 1: specify(chi định) a 'sort key' and pass in to the sort()
def sort_key(info):
    return info[2] //dùng vị trí[2] để ss

# step 2: 
infos.sort(key = sort_key, reverse = True) // kg lớn nhất => bé nhất

# OR use lambda
lambda argument: expression

def info(argument):
    return expression

infos.sort(key=lambda info: info[2]) // giống như trên
```
15. sorted
```py
# return new  sorted list from the original list
# doesn't modify the original list
# default  sorting is ascending
sorted(list) | sorted(list, reverse=True)

# sort a list of string
# sort a list of number
```
16. list slice
```py
sub_list = list[begin:end:step]

# begin default = 0, end = length, step = 1
# lấy từ begin đến end (trừ end)
```
17. unpack a list 
```py
red, greed, blue = colors => [red, green, blue, yellow] 
# if colors length = 3, variable length must be 3 too 

red, greed, *other = colors
print(other) // ['blue', 'yellow']
```
18. for loop to iterate over a list
```py
for item in list:
    process the item

# loop with index in
## use the 'enumerate()' 
### => return tuple // index and element
for info in enumerate(infos):
    print(info) // (0, 'John')...

for index, info in enumerate(infos):
    print(f'{index}: {info}') // 0: John...

enumerate(info,1) // default = 0, set = 1
```
19. find index of element in list
```py
# use index(element)
result = infos.index('Tom')
```
20. Iterables 
```py
# an iterable is an object that includes zero, one, many elements 

# 'range()', 'str' is an iterable 
# 'lists' and 'tuple' are also iterable 

# iterable có thể lập đi lập lại, tác nhân thực hiện lập là iterator 
## iterator' is stateful. sau khi sử dụng 1 ptử từ iterator thì nó sẽ biến mất
```
21. transform list element using map function 
```py
    iterator = map(fn, list)
# return iterator 
# fn will call on each element of list(tuple | any) 

# EX1:
numbers = [1,2,3]
iterator = map(lambda: bonus: bonus\*2, numbers)

# EX2:
carts = [['SmartPhone', 400],
        ['Tablet', 450],
        ['Laptop', 700]]

TAX = 0.1
carts = map(lambda item: [item[0], item[1], item[1] * TAX], carts)
print(list(carts))
        
```
22. filter list element
```py
filter(fn, list)
# return iterator
# only keep the element where fn returns True

# EX1:
scores = [70, 60, 80, 90, 50]
filtered = filter(lambda score: score >= 70, scores)

print(list(filtered))

#EX2:
countries = [
        ['China', 1394015977],
        ['United States', 329877505],
        ['India', 1326093247],
        ['Indonesia', 267026366],
        ['Bangladesh', 162650853],
        ['Pakistan', 233500636],
        ['Nigeria', 214028302],
        ['Brazil', 21171597],
        ['Russia', 141722205],
        ['Mexico', 128649565]
]
populated = filter(lambda c: c[1] > 300000000, countries)
print(list(populated))

```
23. reduce
```py
reduce(fn, list)

# apply a function of two arguments cumulatively to the items of iterable, from left to right, reduce the list into a single value
# reduce belong to the functools module

#EX1:
from functools import reduce

scores = [75, 65, 80, 95, 50]
total = reduce(lambda a, b: a + b, scores)

print(total)
```
24. list Comprehensions
```py
[output_expression for element in list if condition]

===equivalent===
output_list = []
for element in list:
output_list.append(output_expression)

# EX1:
numbers = [1, 2, 3, 4, 5]
squares = [number**2 for number in numbers]
print(squares)

# EX2:
mountains = [
        ['Makalu', 8485],
        ['Lhotse', 8516],
        ['Kanchenjunga', 8586],
        ['K2', 8611],
        ['Everest', 8848]
]
highest_mountains = [m for m in mountains if m[1] > 8600]
print(highest_mountains)
```
25. DICTIONARY TYPE
```PY
# uses '{}' define a dictionary
empty_dict = {}
print(type(empty_dict)) // <class 'dict'>

=> EX1:
person = {
        'first_name': 'John',
        'last_name': 'Doe',
        'age': 25,
        'favorite_colors': ['blue', 'green'],
        'active': True
}
ssn = person['ssn']                     // KeyError
ssn = person.get('ssn')                 // None[doesn't exist]
ssn = person.get('ssn','000-00')        // 000-00 cuz None

# ADD NEW KEY-VALUE
person['salary'] = 750

# MODIFYING VALUE
person['age'] = 30

# DELETING A KEY
del person['age']

# CHECKING IF A KEY EXISTS IN THE DICT
'age' in person               // False
'salary' in person            // True
```
26. LIST COMPREHENSIONS
```PY
# dictionary comprehension cho phép chạy for loop trong dictionary và return a new dictionary
{key:value for (key,value) in dict.items() if condition}

# EX1:
stocks = {
        'AAPL': 121,
        'AMZN': 3380,
        'MSFT': 219,
        'BIIB': 280,
        'QDEL': 266,
        'LVGO': 144
}
## for loop
new_stocks = {}

for symbol, price in stocks.items():
    new_stocks[symbol] = price*1.02

selected_stocks = {}

for symbol, price in stocks.items():
    if price > 200:
        selected_stocks[symbol] = price

## dictionary comprehension
new_stocks = {symbol: price * 1.02 for (symbol, price) in stocks.items()}

selected_stocks = {s: p for (s, p) in stocks.items() if p > 200}

print(new_stocks)
```
27. Set
```py
# A set is an unordered collection of unique elements
# cannot be changed. They can be numbers, string, tuples, but not lists or dictionaries

# create a set
my_set = {'apple', 'banana', 'cherry'}

# empty set
empty_set = set()

# can pass an iterable to the set()
skills = (['Python','ABC'])     // {'ABC', 'Python'}

# if an iterable duplicate element => remove them
characters = set('letter')      //  {'l', 'e', 't', 'r'}

# get size of set
len(characters)         //   4

# add elements to a set
skills.add('DEF')       // { 'ABC', 'DEF' , 'Python'}

# remove element
skills.remove(‘ABC’)   //  {'DEF' , 'Python'}

# returning an element 
# frozen a set
```

28. Set comprehension
```py

```

29. Set Union
```py
# union of two set => return a new set [element khác nhau của cả 2]
set1 = {"a", "b"}
set2 = {"b", "c"}
s = set1.union(set2)    //  s={"a","b","c"}

# "|" operator
s= set1 | set2          //  s={"a","b","c"}

# union() vs "|"
# union() accepts one or more iterables, converts the iterables to sets
rates = {1,2,3}
ranks = [2,3,4]
rating = rates.union(ranks)     // {1,2,3,4}
# "|" only accept iterables not lists
rating = rates | ranks           // TypeError:

```
30. Set Intersection
```py
new_set = set1.intersection(set2,set3)
new_set = set1 & set2 & set3

# get a new set consisting(bao gồm) of elements that exist in all sets.
rates = {1,2,3}
ranks = {2,3,4}
rating = rates.intersection(ranks)      // {2,3}

# intersection() vs "&"
## intersection() can accept any iterables[string, lists, dictionaries]
## '&' can only allows sets
rates = {1,2,3}
ranks = [2,3,4]

rates = rates.intersection(ranks)       // {2,3}

rates = rates & ranks   // TypeError

```
31. Set Difference
```py
# return new set that has element from the first set
s1 = {'Python', 'Java', 'C++'}
s2 = {'C#', 'Java', 'C++'}

s = s1.difference(s2)   // {'Python'}
s = s2.difference(s1)   // { 'C#'}

# "-"
s = s1 - s2     // {'Python'}
s = s2 - s1     // {'C#'}

# difference() method vs "-" operator
## difference() can accept one or more iterable[strings, lists, dictionaries]
## '-' only allows sets

```
32. Symmetric(đối xứng) difference
```py
# là phần không giao nhau của 2 sets
#  return a new set containing elements which are present in either of the sets but not common to both.

# symmetric_difference vs '^'
```
33. issubset(tập hợp con)
```py
set_a.issubset(set_b)   //  True if all items of set_a exist in set_b. False otherwise.

# '<='

```
34. issuperset
```py
# issuperset() v '>='

```
35. Disjoint
```py
# isdisjoint()
```
36. for...else
```py
for item iterables:
        #
else:
        #

#EX1:
people = [{'name': 'John', 'age': 25},
        {'name': 'Jane', 'age': 22},
        {'name': 'Peter', 'age': 30},
        {'name': 'Jenifer', 'age': 28}]

name = input('Enter a name:')

for person in people:
    if person['name'] == name:
        print(person)
        break
else:
    print(f'{name} not found!')
```

37. while...else
```py
while condition:
        #
else:
        #

#EX1:
basket = [
    {'fruit': 'apple', 'qty': 20},
    {'fruit': 'banana', 'qty': 30},
    {'fruit': 'orange', 'qty': 10}
]

fruit = input('Enter a fruit:')
index = 0

while index < len(basket):
    item = basket[index]
    if item['fruit'] == fruit:
        print(f"The basket has {item['qty']} {item['fruit']}(s)")
        found_it = True
        break
    index += 1
else:
    qty = int(input(f'Enter the qty for {fruit}:'))
    basket.append({'fruit': fruit, 'qty': qty})
    print(basket)

```
38. Do...while
```py
while True:
    #
    if condition
        break

#EX1:
from random import randint

# determine the range
MIN = 0
MAX = 10

# generate a secret number
secret_number = randint(MIN, MAX)

# initialize the attempt
attempt = 0

while True:
    attempt += 1

    input_number = int(input(f'Enter a number between {MIN} and {MAX}:'))

    if input_number > secret_number:
        print('It should be smaller.')
    elif input_number < secret_number:
        print('It should be bigger.')
    else:
        print(f'Bingo! {attempt} attempt(s)')
        break

```
39. Unpacking Tuple
```py
# tuple constructor
tuple()

# define tuple only one element
1, //   = (1) = (1, )

# unpacking a tuple means splitting(chia) the tuple's element into individual(riêng lẻ) variable
a, b = (1, 2) # a = 1 and b = 2

#swap values
x = 10
y = 20
print(f'x={x}, y={y}')   # x=10, y=20

x, y = y, x
print(f'x={x}, y={y}')     # x=20, y=10

x, y, _ = 10, 20, 30    # '_' is used to ignore some value that we don't care about 

# '*' operator
r, g, *other = (192, 210, 100, 0.5)     #  r = 192, g =  210, other = [100,0.5]

odd_numbers = (1, 3, 5)
even_numbers = (2, 4, 6)
numbers = (*odd_numbers, *even_numbers)   # numbers = (1, 3, 5, 2, 4,  6)

```
40. *args
```py
# parameters like *args => variadic(có tính biến đổi) parameter
def add(*args):
    print(args)
add(1,2,3)  # output: (1, 2, 3)

# unpacking argument
def point(x, y):
    return f'({x},{y})'

a = (0, 0)
origin = point(a)   # TypeError: point() missing 1 required positional argument: 'y'
origin = point(*a)  #: output: (0,0), unpacks the tuple and assigns its elements to x and y parameters
print(origin)
```
41. **kwargs
```py
# keyword arguments like **kwargs => dictionary-like(tương tự như một tập của key và value) parameter
def connect(**kwargs):
    print(kwargs)

config = {'server': 'localhost',
        'port': 3306,
        'user': 'root',
        'password': 'Py1thon!Xt12'}
connect(**config)
# need to place the **kwargs after other parameters

```

42. partial fn
```py
# partial return new partial object
partial(fn, /, *args, **kwargs)

from functools import partial

def multiply(a, b):
    return a*b

double = partial(multiply, x)

x = 2
result = double(10)
print(result)     # output: 20

x = 3
result = triple(10)
print(result)      # output:  30
```

43. Type Hints
```py
def say_hi(name: str) -> str:
    return f'Hi {name}'


greeting = say_hi('John')
print(greeting) # Hi John

# type checker tool: mypy

```
44. Module
```py
# pricing.py

def get_net_price(price, tax_rate, discount=0):
    return price * (1 + tax_rate) * (1-discount)

def get_tax(price, tax_rate=0):
    return price * tax_rate

# main.py
import pricing
# import pricing as newName
# from pricing import get_net_price
# from pricing import get_net_price as newName
# from pricing import *

net_price = pricing.get_net_price(
    price=100,
    tax_rate=0.01
)
print(net_price)           # output: 99.0
```
45. __name__
```py
# dunder name
```
46. packages
```py
# import packages
import package.module
from module import function

```
47. private Fn
```py
# create a package with the __init__.py
# do not specify the fn in the __all__ variable
# import all symbols from the module in the __init__.py file of the package and expose only the public fn by using the __all__ variable
├── mail
|  ├── email.py
|  └── __init__.py
└── main.py

# email.py
__all__ = ['send']

def send(email, message):
    print(f'Sending "{message}" to {email}')

def attach_file(filename):
    print(f'Attach {filename} to the message')

# __init__.py
from .email import * 

__all__ = email.__all__


# main.py
import mail
mail.send('test@example.com','Hello')
```
48. try...except
```py
# syntax error => write an invalid P code
# exceptions => reading a file does not exist, connecting to a remote server that is offline, bad user input
## TypeError, NameError, ect
try:
    # may cause error
except:
    # handle error
finally:
    # code that clean up
# finally block always runs even if there was an exception or no exception

```
49. try...except...else
```py
try:
    #
except:
    #
else:
    # executes when no exception occurs
# Use the Python try...except...else statement provides you with a way to control the flow of the program in case of exceptions.
# The else clause executes if no exception occurs in the try clause.
# If so, the else clause executes after the try clause and before the finally clause.
```
50. Read file text
```py
with open('readme.txt') as f:
    lines = f.readlines()

# open()
open(path_to_file, mode)
## mode: 'r': reading text, 'w': writing text, 'a': appending text
## return a file object

# READING TEXT METHOD
## read(size): return a string
## readline(): read a line from text => a string
## readlines(): read all lines => list of string

# CLOSE METHOD
# It’s important to close the file that is no longer in use
## when you open a file in your script, the file system usually locks it down so no other programs or scripts can use it until you close it
## your file system has a limited number of file descriptors that you can create before it runs out of them. Although this number might be high, it’s possible to open a lot of files and deplete your file system resources
## leaving many files open may lead to race conditions which occur when multiple processes attempt to modify one file at the same time and can cause all kinds of unexpected behaviors
f.close()

# To close the file automatically without calling the close() method
with open(path_to_file) as f:
    contents = f.readlines()

#EX1:
with open('the-zen-of-python.txt') as f:
    while True:
        line = f.readline()
        if not line:
            break
        print(line.strip()) # strip()=> remove blank line

# open() return file object (iterable object) => use a for loop
with open('the-zen-of-python.txt') as f:
    for line in f:
        print(line.strip())

# Read UTF-8 file
## use |encoding='utf-8'|
with open('quotes.txt', encoding='utf8') as f:
    for line in f:
        print(line.strip())
```
51. Write a text
```py
with open('readme.txt', 'w') as f:
    f.write('readme')
# write(): write a string to a text file
# writelines():  write a list of strings to a text file

#EX1:
lines = ['Readme', 'How to write text files in Python']
with open('readme.txt', 'w') as f:
    for line in lines:
        f.write(line)
        f.write('\n') 
# OR
lines = ['Readme', 'How to write text files in Python']
with open('readme.txt', 'w') as f:
    f.writelines(lines)

# OR
lines = ['Readme', 'How to write text files in Python']
with open('readme.txt', 'w') as f:
    f.write('\n'.join(lines))

#EX2: appending text file
more_lines = ['', 'Append text files', 'The End']

with open('readme.txt', 'a') as f:
    f.write('\n'.join(more_lines))
```
52. create text file
```py
# 'w': if file doesn't exist -> create a new file. it’ll overwrite the contents of the existing file
# 'x': if file exist -> error(FileExistError), otherwise create text file

#EX1:
with open('docs/readme.txt', 'w') as f:
    f.write('Create a new text file!')

```
53. check if file exist
```py
from os.path import exists

file_exists = exists(path_to_file)  # True|False

# OR
from pathlib import Path

path = Path(path_to_file)
path.is_file()
```
54. Read CSV file
```py
import csv

f = open('path/to/csv_file', encoding='UTF8')
csv_reader = csv.reader(f) # return a csv reader object
for line in csv_reader:
    print(line)
f.close()
#EX1:
import csv

total_area = 0

# calculate the total area of all countries
with open('country.csv', encoding="utf8") as f:
    csv_reader = csv.reader(f)

    # skip the header
    next(csv_reader)

    # calculate total
    for line in csv_reader:
        total_area += float(line[1])

print(total_area)

#EX2: using DictReader class
## The DictReader class allows you to create an object like a regular CSV reader. But it maps the information of each line to a dictionary (dict) whose keys are specified by the values of the first line
import csv

with open('country.csv', encoding="utf8") as f:
    csv_reader = csv.DictReader(f)
    # skip the header
    next(csv_reader)
    # show the data
    for line in csv_reader:
        print(f"The area of {line['name']} is {line['area']} km2")
### The area of Afghanistan is 652090.00 km2
### The area of Albania is 28748.00 km2
### The area of Algeria is 2381741.00 km2 

# OR:
import csv

fieldnames = ['country_name', 'area', 'code2', 'code3']

with open('country.csv', encoding="utf8") as f:
    csv_reader = csv.DictReader(f, fieldnames)
    next(csv_reader)
    for line in csv_reader:
        print(f"The area of {line['country_name']} is {line['area']} km2")

```
55. Write CSV file
```py
import csv

# open the file in the write mode
f = open('path/to/csv_file', 'w')

# create the csv writer
writer = csv.writer(f)

# write a row to the csv file
writer.writerow(row)

# close the file
f.close()

# OR:
import csv

# open the file in the write mode
with open('path/to/csv_file', 'w', encoding='UTF8') as f:
    # create the csv writer
    writer = csv.writer(f)

    # write a row to the csv file
    writer.writerow(row)

# Ex1:
import csv  

header = ['name', 'area', 'country_code2', 'country_code3']
data = ['Afghanistan', 652090, 'AF', 'AFG']

with open('countries.csv', 'w', encoding='UTF8', newline='') as f:
    writer = csv.writer(f)

    # write the header
    writer.writerow(header)

    # write the data
    writer.writerow(data)

# Ex2: Write multiple rows at once
import csv

header = ['name', 'area', 'country_code2', 'country_code3']
data = [
    ['Albania', 28748, 'AL', 'ALB'],
    ['Algeria', 2381741, 'DZ', 'DZA'],
    ['American Samoa', 199, 'AS', 'ASM'],
    ['Andorra', 468, 'AD', 'AND'],
    ['Angola', 1246700, 'AO', 'AGO']
]

with open('countries.csv', 'w', encoding='UTF8', newline='') as f:
    writer = csv.writer(f)

    # write the header
    writer.writerow(header)

    # write multiple rows
    writer.writerows(data)

# EX3: using DictWrite class
import csv

# csv header
fieldnames = ['name', 'area', 'country_code2', 'country_code3']

# csv data
rows = [
    {'name': 'Albania',
    'area': 28748,
    'country_code2': 'AL',
    'country_code3': 'ALB'},
    {'name': 'Algeria',
    'area': 2381741,
    'country_code2': 'DZ',
    'country_code3': 'DZA'},
    {'name': 'American Samoa',
    'area': 199,
    'country_code2': 'AS',
    'country_code3': 'ASM'}
]

with open('countries.csv', 'w', encoding='UTF8', newline='') as f:
    writer = csv.DictWriter(f, fieldnames=fieldnames)
    writer.writeheader()
    writer.writerows(rows)

```
56. Delete file
```py
import os

os.remove('readme.txt')

# or:
import os

filename = 'readme.txt'
if os.path.exists(filename):
    os.remove(filename)

# or:
import os

try:
    os.remove('readme.txt')
except FileNotFoundError as e:
    print(e)
```
57. rename file
```py
os.rename(src,dst)

import os
os.rename('readme.txt', 'notes.txt')

# or
import os

try:
    os.rename('readme.txt', 'notes.txt')
except FileNotFoundError as e:
    print(e)
except FileExistsError as e:
    print(e)
```
58. Directory
```py
# get current directory
import os
cwd = os.getcwd()
print(cwd)

# change current directory
import os

os.chdir('/script')
cwd = os.getcwd()
print(cwd)

# join and split a path
import os

fp = os.path.join('temp', 'python')
print(fp)  # temp\python (on Windows)

pc = os.path.split(fp)
print(pc)  # ('temp', 'python')

# test if path is a directory
import os

dir = os.path.join("C:\\", "temp")
print(dir)

if os.path.exists(dir) or os.path.isdir(dir):
    print(f'The {dir} is a directory')

# create , delete directories

import os
dir = os.path.join("C:\\", "temp", "python")
if not os.path.exists(dir):
    os.mkdir(dir)


import os
dir = os.path.join("C:\\","temp","python")
if os.path.exists(dir):
    os.rmdir(dir)
    print(dir + ' is removed.')

# rename 
import os

oldpath = os.path.join("C:\\", "temp", "python")
newpath = os.path.join("C:\\", "temp", "python3")

if os.path.exists(oldpath) and not os.path.exists(newpath):
    os.rename(oldpath, newpath)
    print("'{0}' was renamed to '{1}'".format(oldpath, newpath))

```
59. list file
```py
D:\web
├── assets
|  ├── css
|  |  └── style.css
|  └── js
|     └── app.js
├── blog
|  ├── read-file.html
|  └── write-file.html
├── about.html
├── contact.html
└── index.html

# EX1: list all html files
import os

path = 'D:\\web'
html_files = []

for dirpath, dirnames, filenames in os.walk(path):
    for filename in filenames:
        if filename.endswith('.html'):
            html_files.append(os.path.join(dirpath, filename))

for html_file in html_files:
    print(html_file)
## D:\web\about.html
## D:\web\contact.html
## D:\web\index.html
## D:\web\blog\write-file.html
## D:\web\blog\read-file.html

# EX2: Defining a reusable list files function
import os


def list_files(path, extentions=None):
    """ List all files in a directory specified by path
    Args:
        path - the root directory path
        extensions - a iterator of file extensions to include, pass None to get all files.
    Returns:
        A list of files specified by extensions
    """
    filepaths = []
    for root, _, files in os.walk(path):
        for file in files:
            if extentions is None:
                filepaths.append(os.path.join(root, file))
            else:
                for ext in extentions:
                    if file.endswith(ext):
                        filepaths.append(os.path.join(root, file))

    return filepaths


if __name__ == '__main__':
    filepaths = list_files(r'D:\web', ('.html', '.css'))
    for filepath in filepaths:
        print(filepath)

```
60. pip
```py
pip install <package_name>

pip install <package_name>==<version>

# list all package install
pip list

pip list --outdated

pip uninstall <package_name>

pip show <package_name>
```
61. venv
62. F-string
```py
name = 'John'
s = F'Hello, {name.upper()}!'
print(s)


first_name = 'John'
last_name = 'Doe'
s = F'Hello, {first_name} {last_name}!'
print(s)


first_name = 'John'
last_name = 'Doe'
s = F'Hello, {" ".join((first_name, last_name))}!'

print(s)


name = 'John'
website = 'PythonTutorial.net'

message = (
    f'Hello {name}. '
    f"You're learning Python at {website}." 
)

print(message)


name = 'John'
website = 'PythonTutorial.net'

message = f"""Hello {name}.
You're learning Python at {website}."""

print(message) 


s = f'{{1+2}}'
print(s) #  {{1+2}}

# Format numbers using f-strings
number = 16
s = f'{number:x}'
print(s)  # 10

number = 0.01
s = f'{number:e}'
print(s)  # 1.000000e-02

number = 9.98567
s = f'{number: .2f}'
print(s)  # 9.99

number = 200
s = f'{number: 06}'
print(s)  # 00200

number = 0.1259
s = f'{number: .2%}'
print(s)  # 12.59%

s = f'{number: .1%}'
print(s)  # 12.5%
```