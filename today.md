OOP
1. Class and Object
2. special method
3. property
4. single inheritance
5. enumerations
6. SOLID Principles(nguyên tắc)
7. multiple inheritance
8. descriptors
8.1 Descriptors
```py
## first_name and last_name attributes to be non-empty strings
# define a descriptor class
class RequiredString:
    def __set_name__(self, owner, name):
        self.property_name = name

    def __get__(self, instance, owner):
        if instance is None:
            return self

        return instance.__dict__[self.property_name] or None

    def __set__(self, instance, value):
        if not isinstance(value, str):
            raise ValueError(f'The {self.property_name} must be a string')

        if len(value) == 0:
            raise ValueError(f'The {self.property_name} cannot be empty')

        instance.__dict__[self.property_name] = value

class Person:
    first_name = RequiredString()
    last_name = RequiredString()

try:
    person = Person()
    person.first_name = ''
except ValueError as e:
    print(e)    #  The first_name must be a string

# DESCRIPTOR PROTOCOL
## method: __get__, __set__, __delete__
## is an object of class that implements(thực hiện) one of the method(1 trong các method) specified in the descriptor protocol
## type: data descriptor & non-data descriptor
### data descriptor: implements __set__ and/or __delete__
### non-data descriptor: implement __get__ only
## HOW WORK?
class RequiredString:
    def __set_name__(self, owner, name):
        print(f'__set_name__ was called with owner={owner} and name={name}')
        self.property_name = name

    def __get__(self, instance, owner):
        print(f'__get__ was called with instance={instance} and owner={owner}')
        if instance is None:
            return self

        return instance.__dict__[self.property_name] or None

    def __set__(self, instance, value):
        print(f'__set__ was called with instance={instance} and value={value}')

        if not isinstance(value, str):
            raise ValueError(f'The {self.property_name} must a string')

        if len(value) == 0:
            raise ValueError(f'The {self.property_name} cannot be empty')

        instance.__dict__[self.property_name] = value


class Person:
    first_name = RequiredString()
    last_name = RequiredString()
### OUTPUT:
__set_name__ was called with owner=<class '__main__.Person'> and name=first_name
__set_name__ was called with owner=<class '__main__.Person'> and name=last_name

### Python automatically calls the __set_name__ when the owning class Person is created

first_name = RequiredString()
### EQUIVALENT
first_name.__set_name__(Person, 'first_name')

from pprint import pprint

pprint(Person.__dict__)
### OUTPUT
mappingproxy({'__dict__': <attribute '__dict__' of 'Person' objects>,
            '__doc__': None,
            '__module__': '__main__',
            '__weakref__': <attribute '__weakref__' of 'Person' objects>,
            'first_name': <__main__.RequiredString object at 0x0000019D6AB947F0>,
            'last_name': <__main__.RequiredString object at 0x0000019D6ACFBE80>})

# assign the new value to a descriptor, Python calls __set__ method to set the attribute on an instance of the owner class to the new value
person = Person()
person.first_name = 'John'
### OUTPUT: __set__ was called with instance=<__main__.Person object at 0x000001F85F7167F0> and value=John

# Python uses instance.__dict__ dictionary to store instance attributes of the instance object.
person = Person()
print(person.__dict__)  # {}

person.first_name = 'John'
person.last_name = 'Doe'

print(person.__dict__) # {'first_name': 'John', 'last_name': 'Doe'}

# __GET__
person = Person()

person.first_name = 'John'
print(person.first_name)
### OUTPUT: 
__set__ was called with instance=<__main__.Person object at 0x000001F85F7167F0> and value=John
__get__ was called with instance=<__main__.Person object at 0x000001F85F7167F0> and owner=<class '__main__.Person'>

# The __get__ method returns the descriptor if the instance is None
print(Person.first_name) # <__main__.RequiredString object at 0x000001AF1DA147F0>

# If the instance is not None, the __get__() method returns the value of the attribute with the name property_name of the instance object

```
8.2 DATA VS NON-DATA DESCRIPTOR
```py
# Both descriptor types can optionally implement the __set_name__ method. The __set_name__ method doesn’t affect the classification of the descriptors

# If a class uses a non-data descriptor, Python will search the attribute in instance attributes first (instance.__dict__)
## If Python doesn’t find the attribute in the instance attributes, it’ll use the data descriptor.
class FileCount:
    def __get__(self, instance, owner):
        print('The __get__ was called')
        return len(os.listdir(instance.path))

class Folder:
    count = FileCount()

    def __init__(self, path):
        self.path = path

folder = Folder('/')
print('file count: ', folder.count)
# Python called the __get__ descriptor
## output:
The __get__ was called
file count:  32

folder.__dict__['count'] = 100
print('file count: ', folder.count)
## output: file count:  100
## Python can find the count attribute in the instance dictionary __dict__. Therefore, it does not use data descriptors.

# chưa hiểu gì hết
```
9. meta programming
10. exceptions

====CONCURRENCY====

1. Multithreading
2. Thread Synchronization Techniques
3. Sharing Data Between Threads
4. Multiprocessing
5. Async I/O

====ADVanced====
1. Variables & Memory Management
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

https://react-tutorial.app/app.html

https://www.tutorialspoint.com/reactjs/reactjs_pagination.htm