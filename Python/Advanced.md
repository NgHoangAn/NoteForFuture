# 1. Variables & Memory Management
## 1.1 References
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
## 1.2 Garbage Collection
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
## 1.3 Dynamic Typing 
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
## 1.4 Mutable and immutable
```py
# immutable
## numbers(int, float, bool), Strings, Tuples

# mutable
## Lists, Sets, Dictionaries

# EX: immutables
counter = 100
print(id(counter))  # 140717671523072
print(hex(id(100))) # 0x7ffb62d32300

counter = 200
print(counter)  # 200   
print(hex(id(counter))) # 0x7ffb62d32f80

## reassignment doesn’t change the value of the first integer object
## just reassigns the reference.

# Ex: mutable
ratings = [1, 2, 3]
print(hex(id(ratings)))  # 0x1840f97a340

ratings.append(4)
print(ratings)  # [1, 2, 3, 4]
print(hex(id(ratings)))  # 0x1840f97a340

# Ex:
low = [1, 2, 3]
high = [4, 5]

rankings = (low, high)  # tuple: immutables

high.append(6)
print(rankings)     # ([1, 2, 3], [4, 5, 6])

```
## 1.5 operator
```py
`is` compare two variable => return True if they reference the same object
# Ex:
a = 100
b = a
result = a is b
print(result)   # True

a = 100
b = 100

result = a is b
print(result)   # True

ranks = [1, 2, 3]
rates = [1, 2, 3]

result = ranks is rates
print(result)   # False

# '==' OPERATOR
## compare two variable for equality => return True if they are equal
## Ex:
a = 100
b = a

is_identical = a is b
is_equal = a == b

print(is_identical)     # True
print(is_equal)         # True

## Ex:
ranks = [1, 2, 3]
rates = [1, 2, 3]

is_identical = ranks is rates
is_equal = ranks == rates

print(is_identical)     # False
print(is_equal)         # True

```
## 1.6 None
```py
# a special object of the NoneType class
print(type(None))       # <class 'NoneType'>

# The None is a singleton object of the NoneType class => creates one and only one None object at runtime

print(None == None) # True
print(None is None) # True

# NOTE
## None is not zero
## None is not same as False
## None is not the same as an empty string('')
## compare None to any value will return False (except None)

## EX:
colors = ['red', 'green']
append('blue', colors)

print(colors)   # ['red', 'green', 'blue']

### problem: The issue is that the function creates the list once defined and uses the same list in each successive call
hsl = append('hue')
print(hsl)          # ['hue']

rgb = append('red')
print(rgb)          # ['hue', 'red']

### FIX:
def append(color, colors=None):
    if colors is None:
        colors = []
    colors.append(color)
    return colors

hsl = append('hue')
print(hsl)          # ['hue']

rgb = append('red')
print(rgb)          # ['red']
```
# 2. Integer types
## 2.1 Integer
```py
# Computers can’t store integers directly. Instead, they only can store binary numbers such as 0 and 1
# Python uses a variable number of bits to store integers
counter = 10
print(type(counter))    <class 'int'>

# GET SIZE OF INTEGER TYPE
from sys import getsizeof

counter = 0
size = getsizeof(counter)

print(size)  # 24 bytes
```
## 2.2 Floor Division
```py
# The // is called the floor division operator or div. And the % is called the modulo operator or mod.
n // d = floor(n/d)

a = 10
b = 3
print(a//b)  # 3

a = -10
b = -3
print(a//b)  # 3

a = 10
b = -3
print(a//b)  # -4

a = -10
b = 3
print(a//b)  # -4

# math.floor() function
from math import floor

a = 10
b = 3
print(a//b)  # 3
print(floor(a/b))  # 3

```
## 2.3 Modulo
```py
# n % d gives the remainder of the division between n and d, it's also known as the "mod" operation.

a = 16
b = 5

m = a % b
f = a // b

print(f'{a} % {b} = {m}')  # 1
print(f'{a} // {b} = {f}')  # 3

## EX: Using the modulo operator to check if a number is even or odd
def is_even(num):
    return num % 2 == 0

def is_odd(num):
    return num % 2 != 0

# Using the modulo operator to convert units
from math import floor

def get_time(total_seconds):
    return {
        'days': floor(total_seconds / 60 / 60 / 24),
        'hours': floor(total_seconds / 60 / 60) % 24,
        'minutes': floor(total_seconds / 60) % 60,
        'seconds': total_seconds % 60,
    }


print(get_time(93750))  # {'days': 1, 'hours': 2, 'minutes': 2, 'seconds': 30}
```
## 2.4 bool
```py
# The bool class is the subclass of the int class
is_child_class = issubclass(bool, int)
print(is_child_class)   # True

# True and False are singleton objects of the bool class
isinstance(True, bool)  # True
isinstance(False, bool) # True

# Comparing boolean values
a = True
b = True
print(a == b)   # True
print(a is b)   # True

```
## 2.5 and
## 2.6 or
# 3. Float
## 3.1 float
```py
>>> float(0.1)
0.1
>>> float('1.25')
1.25

>>> format(0.1, '.20f')
'0.10000000000000000555'

# EX:
x = 0.1 + 0.1 + 0.1
y = 0.3

print(x == y)   # False
print(format(x, '.20f'))    # 0.30000000000000004441
print(format(y, '.20f'))    # 0.29999999999999998890

print(round(x, 3) == round(y, 3))   # True

## OR
from math import isclose

x = 0.1 + 0.1 + 0.1
y = 0.3

print(isclose(x,y))      # True
```
## 3.2 Float to Int
```py
# Truncation
## The trunc(x) function returns the integer part of the number x. It ignores everything after the decimal point
from math import trunc

print(trunc(12.2))  # 12
print(trunc(12.5))  # 12
print(trunc(12.7))  # 12

# Floor
from math import floor

print(floor(12.2))  # 12
print(floor(12.5))  # 12
print(floor(12.7))  # 12

# Ceiling
## returns the smallest integer greater than or equal to x
from math import ceil

print(ceil(12.7)) # 13
```
## 3.3 Rounding
```py
# the round() function returns the number rounded to ndigits precision after the decimal point
round(number [, ndigits])

round(1.25) # 1
round(1.25, 0)  # 1.0

round(15.5, -1) # 20

round(1.25, 1)  # 1.2
round(1.35, 1)  # 1.4

```
# 4. Decimal
```py

```
# 5. Variable scopes
## 5.1 variable scope
```py
# global scopes
## The global scope is basically the module scope
## Python doesn’t have a truly global scope that spans across all modules except for the built-in scope.
## The built-in scope is a special scope that provides globally available objects such as print, len, None, True, and False
## The built-in scope is a special scope that provides globally available objects such as print, len, None, True, and False

print('Hello')
## In this app.py module, Python looks for the print function in the module scope (app.py).
## Since Python doesn’t find the definition of the print function in the app.py module scope, Python goes up to the enclosing scope, which is the built-in scope, and looks for the print function there

# local scopes
def increment(counter, by=1):
    result = counter + by
    return result

## When Python compiles the file, it adds the increment function to the global scope
## determines that the counter, by, and result variables inside the increment() function will be local to the increment() function
## Every time you call a function, Python creates a new scope =>  function local scope or local scope.

## When the function completes, Python will delete the local scope
##  all the local variables such as counter, by, and result variables are out of scope

# Variable lookups
## scopes are nested
##  access an object bound to a variable, Python tries to find the object => in the current local scope first => goes up the chain of enclosing scopes if Python doesn’t find the object in the current scope.

# The global keyword
## When you retrieve the value of a global variable from inside a function, Python automatically searches the local scope’s namespace and up the chain of all enclosing scope namespaces

counter = 10

def current():
    print(counter)

current()

## If you want to access a global variable from inside a function, you can use the global keyword

counter = 10

def reset():
    global counter
    counter = 0
    print(counter) # 0

reset()
print(counter) # 0

```
## 5.2 nonlocal
```py
def outer():
    print('outer function')

    def inner():
        print('inner function')
    inner()

outer() # outer function inner function

## inner fn được lòng vào outer fn => dùng trong TH khi không muốn cán fn này mang tính global 
## cả 2 fn đều có thể truy cập vào global, built-in scope, local scope của chúng
## inner fn cũng có thể truy cập vào phạm vi của enclosing scope [outer fn scope]
## nhìn tù inner fn thì enclosing của nó không phải là local hay global scope => nonlocal

# nonlocal keyword
def outer():
    message = 'outer scope'
    print(message)          

    def inner():
        nonlocal message
        message = 'inner scope'
        print(message)

    inner()

    print(message)


outer()     # outer scope
            # inner scope
            # inner scope
## khi dùng nonlocal cho biến thì nó sẻ tìm trong pham vi enclosing local gần nó cho tới khi gặp biến lần đầu tiên
## nó sẽ không tìm ở phạm vi global

message = 'outer scope'
def outer():
    print(message)
    def inner():
        nonlocal message
        message = 'inner scope'
        print(message)
    inner()
    print(message)

outer() # SyntaxError: no binding for nonlocal 'message' found
## => tìm trong enclosing scope(là outer scope) => ko có báo lỗi (ko tìm trong global scope nữa)
```
6. Closures
```py

def say():

    ## start closure
    greeting = 'Hello'

    def display():
        print(greeting)
    ## end closure

    return display()

## display fn là nested fn, có thể truy cập biến 'greeting' từ nonlocal scope
## 'greeting' là free variable
## => closure là nested fn mà nó tham chiếu đến 1 hay nhiều biến từ enclosing scope

fn = say()
fn()
## say() fn executes and return function.
## fn () fn executes thì say() đã hoàn thành
## ==> scope của say() đã biến mất ngay tại thời điểm fn() thực thi
## biến 'greeting' thuộc phạm vi của say() fn, nó nê bị hủy cùng với scope của function

# cells and multi-scopes variable
## value của 'greeting' được share giữa 2 scope: say() và closure => nhưng cùng tham chiếu tới string object có value là 'hello' ==> python dùng cell làm trung gian

print(fn.__closure__)   # (<cell at 0x0000017184915C40: str object at 0x0000017186A829B0>,), return a tuple of cell

## khi truy cập biến 'greeting' thì python 'double-hop' để lấy string value ==> giả thích tại sao say() out scope mà vẫn có thể truy cập string object referenced bởi 'greeting' variable

## closure là 1 function và phần mở rộng scope có chứa free variable

## find free variable
print(fn.__code__.co_freevars) #('greeting',)

# python tạo closure khi nào
## khi fn thực thi => python tạo 1 scope mới. nếu mà fn tạo 1 closure thì python cũng tạo 1 closure

### multiplier return a closure
def multiplier(x):
    def multiply(y):
        return x * y
    return multiply

### function calls create three closures
m1 = multiplier(1)
m2 = multiplier(2)
m3 = multiplier(3)

print(m1(10))   # 10
print(m2(10))   # 20
print(m3(10))   # 30
### m1, m2, and m3 have different instances of closure.

## EX:
multipliers = []
for x in range(1, 4):
    multipliers.append(lambda y: x * y)

m1, m2, m3 = multipliers

print(m1(10))   # 30
print(m2(10))   # 30
print(m3(10))   # 30
### WHY??
### FIX
```
# 7. Decorators
## 7.1 decorators
```py
# là 1 fn lấy 1 fn khác làm argument(đối số) và extend behavior của fn mà ko thay đổi fn ban đầu

# Ex:
def net_price(price, tax):
    return price * (1 + tax)

### Decorator Function: currency fn return về wrapper fn. trong wrapper có cá tham số cho phép gọi bất kì fn function nào với bất kì sự kết hợp nào
def currency(fn):
    # wrapper thực thi hành vi của fn
    def wrapper(*args, **kwargs):
        result = fn(*args, **kwargs)
        return f'${result}'
    return wrapper
# ==> currency là 1 @decorators
net_price = currency(net_price)
print(net_price(100, 0.05))     # $105.0

# 1 hàm lấy hàm khác làm đối số và trả về hàm khác
# closure chấp nhận sự kết hợp của positional and keyword-only argument
# closure fn gọi original fn = sử dụng các đối số cho closure fn và return result của fn 

# '@'
net_price = currency(net_price)
## or
fn = decorate(fn)
@decorare
def fn():
    pass

## ex:
def currency(fn):
    def wrapper(*args, **kwargs):
        result = fn(*args, **kwargs)
        return f'${result}'
    return wrapper

@currency
def net_price(price, tax):
    return price * (1 + tax)

print(net_price(100, 0.05))

# Introspecting decorated functions
@decorate
def fn(*args,**kwargs):
    pass
## bằng với việc:
fn = decorate(fn)

## won’t see the documentation of the original function
help(net_price) # wrapper(*args, **kwargs)
                # None
print(net_price.__name__)   # wrapper

## => decorate a function, you’ll lose the original function signature and documentation

## FIX: use @wraps
from functools import wraps

def currency(fn):
    @wraps(fn)
    def wrapper(*args, **kwargs):
        result = fn(*args, **kwargs)
        return f'${result}'
    return wrapper

@currency
def net_price(price, tax):
    return price * (1 + tax)

help(net_price)
print(net_price.__name__)
## output:
# net_price(price, tax)
#     calculate the net price from price and tax
#     Arguments:
#         price: the selling price
#         tax: value added tax or sale tax
#     Return
#         the net price

# net_price    
```
## 7.2 Decorator with Arguments
```py
# hard-coded value 5
from functools import wraps

def repeat(fn):
    @wraps(fn)
    def wrapper(*args, **kwargs):
        for _ in range(5):
            result = fn(*args, **kwargs)
        return result

    return wrapper


@repeat
def say(message):
    print(message)

say('Hello')

## FIX : flexible
from functools import wraps

def repeat(times):
    ''' call a function a number of times '''
    ## decorate() tương đương với original repeat()
    def decorate(fn):
        @wraps(fn)
        def wrapper(*args, **kwargs):
            for _ in range(times):
                result = fn(*args, **kwargs)
            return result
        return wrapper
    return decorate

@repeat(10)
def say(message):
    print(message)

say('Hello')

## ==> repeat không phải decorator mà là decorator factory nó sẻ trả về 1 decorator
```
## 7.3 class decorator
```py
# can make the __call__ method as a decorator
from functools import wraps


class Star:
    def __init__(self, n):
        self.n = n

    def __call__(self, fn):
        @wraps(fn)
        def wrapper(*args, **kwargs):
            print(self.n*'*')
            result = fn(*args, **kwargs)
            print(result)
            print(self.n*'*')
            return result
        return wrapper


@Star(5)
def add(a, b):
    return a + b


add(10, 20)

# => Use callable classes as decorators by implementing the __call__ method
# => Pass the decorator arguments to the __init__ method

```
## 7.4 Monkey patching
```py
# Monkey Patching là một kỹ thuật cho phép bạn sửa đổi hoặc mở rộng hoạt động của các modules, class hoặc function hiện có trong thời gian chạy mà không thay đổi original source code
# cách làm
## xác định target 
## create patch by writing: add, modify, replace existing logic
## apply the patch. patch overwrite or extend
```
# 8. Named Tuples
## 8.1 NamedTuple
```py
# tuple + class = Named tuple [cho phép tạo tuple và gán tên có ý nghĩa cho các p/tử]
# là subclass của tuple, no thêm các property name vào vị trí element

from collections import namedtuple
## namedtuple => return new name tuple class[class factory]

Point2D = namedtuple('Point2D',['x','y'])
#or
Point2D = namedtuple('Point2D',('x','y'))
#or 
Point2D = namedtuple('Point2D',('x, y'))
# or
Point2D = namedtuple('Point2D','x y')

# Instantiating named tuples
point = Point2D(100, 200)
#or
point = Point2D(x=100, y=200)

# ex:
## unpacking
x, y = point
print(f'({x}, {y})')  # (100, 200)

## indexing
x = point[0]
y = point[1]
print(f'({x}, {y})')  # (100, 200)

## iterating

for coordinate in point:
    print(coordinate)   # 100, then 200

# The rename argument of the namedtuple function
## accepts the rename the keyword-only argument that allows you to rename invalid field names
from collections import namedtuple

Circle = namedtuple(
    'Circle',
    'center_x, center_y, _radius',
    rename=True
)
print(Circle._fields)   # ('center_x', 'center_y', '_2')
# => the namedtuple function changes the _radius field to _2 automatically

# ex:
a = Point2D(100, 200)
b = Point2D(100, 200)

print(a == b)  # True
print(a)    # Point2D(x=100, y=200)

# Named tuples are tuples whose element positions have meaningful names
# Use the namedtuple function of the collections standard library to create a named tuple class
# Named tuples are immutable
``` 
