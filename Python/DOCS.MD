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