
OOP
1. Class and Object
1.1 what
```py
# define a class
class Person:

    # class attribute. share by all instance of the class
    counter = 0

    # define instance attributes
    def __init__(self, nme, age):
        self.name = name
        self.age = age

    # instance method
    def greet(self):
        return f"Hi, it's {self.name}"
    
    # class method. share by all instance of the class
    #  first parameter is cls which represent current class object
    @classmethod
    def create_anonym(cls):
        return Person('Anonym', 22)
    
    # static method
    @staticmethod
    def calculate_sum(a, b):
        return a + b


person = Person('Huy', 25)
anonym = Person.create_anonym()
f = Person.calculate_sum(1,2)

# single inheritance (kế thừa)
## child class can access the attribute and method of the parent class
class Employee(Person):
    def __init__ (self, name, age,job_tile):
        super().__init__(name,age)
        self.job_title= job_tile
    
    # override the greet() class
    def greet(self):
        return super().greet() + f"I'm a {self.job_title}"
```
1.2 Class
```py
# object chứa data à functionality
## data đại diện cho object tại 1 thời điểm. data của object => state. dùng attribute để mô hình hóa state của object
## Functionality đại diện cho behaviors(hành vi) của object. dùng fn để mô hình hóa. fn được kiên kết với object => method của object
## ==> object chứa state và method

# object của class là các instances của class
class Person:
    pass    # thêm vào sau

person = Person()
print(person)

# get an identity of an object
## id is unique
## return a  number that represents the memory address of this object
print(id(person))       # 1943155787760
print(hex(id(person)))  # 0x1c46d1c47f0
```
1.3 Class variable
```py
class HtmlDocument:
    extension = 'html'
    version = '5'

# get value of class variable
print(HtmlDocument.extension) # html
print(HtmlDocument.version) # 5

# using getattr()
extension = getattr(HtmlDocument, 'extension')
version = getattr(HtmlDocument, 'version')

print(extension)  # html
print(version)  # 5

# set values
HtmlDocument.version = 10

setattr(HtmlDocument, 'version', 10)

# can add class variable after create

# delete class variable
delattr(HtmlDocument, 'version')

del HtmlDocument.version

# class variable storage
## store in __dict__. it mapping proxy
## can't change __dict__ directly
from pprint import pprint

class HtmlDocument:
    extension = 'html'
    version = '5'
HtmlDocument.media_type = 'text/html'
pprint(HtmlDocument.__dict__)
# mappingproxy({'__dict__': <attribute '__dict__' of 'HtmlDocument' objects>,
#               '__doc__': None,
#               '__module__': '__main__',
#               '__weakref__': <attribute '__weakref__' of 'HtmlDocument' objects>,
#               'extension': 'html',
#               'media_type': 'text/html',
#               'version': '5'})

```

1.4 class method
```py
class Request:
    def send():
        print('Sent')

Request.send() # Sent
print(Request.send) # <function Request.send at 0x00000276F9E00310>

print(type(Request.send)) # <class 'function'>

# create new instance of Request
http_request = Request()
print(http_request.send) # <bound method Request.send of <__main__.Request object at 0x00000104B6C3D580>>

## http_request.send is not a fn like Request.send
print(type(http_request.send))  # <class 'method'>
print(type(Request.send))  # <class 'function'>

http_request.send() # TypeError. 
## Because the http_request.send is a method that is bound to the http_request object, Python always implicitly passes the object to the method as the first argument

class Request:
    def send(*args):
        print('Sent', args)

Request.send() # Sent ()
## send() fn ko nhận bất kì argument(đối số) nào

http_request.send() # Sent (<__main__.Request object at 0x000001374AF4D580>,)

print(hex(id(http_request)))
http_request.send()
# output:
0x1ee3a74d580
Sent (<__main__.Request object at 0x000001EE3A74D580>,)

http_request.send()
# bằng với
Request.send(http_request)

# method của 1 object luôn có object làm argument đầu tiên. call 'self'
class Request:
    def send(self):
        print('Sent', self)

# 'self' like 'this' in other language
```
1.5 __init__
```py
# __init__ auto call when create a new object of a class
class Person:
    def __init__(self, name, age = 25):
        self.name = name
        self.age = age


if __name__ == '__main__':
    person = Person('John', 25)
    print(f"I'm {person.name}. I'm {person.age} years old.")

```
1.5 instance variable
```py
from pprint import pprint

class HtmlDocument:
    version = 5
    extension = 'html'      # instance variable

pprint(HtmlDocument.__dict__)

print(HtmlDocument.extension)
print(HtmlDocument.version)

# store in __dict__
mappingproxy({'__dict__': <attribute '__dict__' of 'HtmlDocument' objects>,
              '__doc__': None,
              '__module__': '__main__',
              '__weakref__': <attribute '__weakref__' of 'HtmlDocument' objects>,
              'extension': 'html',
              'version': 5})

# create new instance of HtmlDocument class
home = HtmlDocument() # có __dict__ riêng

home.version = 6
print(home.__dict__)    #  {'version': 6}

```
2. special method
3. property
4. single inheritance
5. enumeration
6. solid principles
7. multiple inheritance
8. descriptors
9. meta programming
10. exceptions


