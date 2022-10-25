**Magic methods** are special methods which have double underscores at the beginning and end of their names.
They are also known as **dunders**.
So far, the only one we have encountered is **\__init__**, but there are several others.
They are used to create functionality that can't be represented as a normal method.

One common use of them is operator overloading.
This means defining operators for custom classes that allow operators such as + and * to be used on them.
An example magic method is **\__add__** for +. The **\__add__** method allows for the definition of a custom behavior for the + operator in our class.

``` py
class Vector2D:
  def __init__(self,x,y):
    self.x=x
    self.y=y
  def __add__(self, other):
    return Vector2D(self.x+other.x,self.y+other.y)
first=Vector2D(5,7)
second=Vector2D(3,9)
result=first+second
print(result.x)
print(result.y)
```
```
8
16
```
## Common OPs

More magic methods for common operators:

* \__sub__      for -
* \__mul__      for *
* \__floordiv__ for //
* \__truediv__  for /
* \__mod__      for %
* \__pow__      for **
* \__and__      for &
* \__xor__      for ^
* \__or__       for |

The expression x + y is translated into x.\__add__(y).
However, if x hasn't implemented \__add__, and x and y are of different types, then y.\__radd__(x) is called.
There are equivalent r methods for all magic methods just mentioned.

``` py
class SpecialString:
  def __init__(self, cont):
    self.cont=cont
  def __truediv__(self,other):
    line="="*len(other.cont)
    return "\n".join([self.cont,line,other.cont])

spam=SpecialString("spam")
hello=SpecialString("Hello world!")
print(spam/hello)
```
```
spam
============
Hello world!
```
## Comparisons

Python also provides magic methods for comparisons.

* \__lt__ for <
* \__le__ for <=
* \__eq__ for ==
* \__ne__ for !=
* \__gt__ for >
* \__ge__ for >=

If \__ne__ is not implemented, it returns the opposite of \__eq__.
There are no other relationships between the other operators.

``` py
class SpecialString:
  def __init__(self, cont):
    self.cont=cont
  def __gt__(self,other):
    for i in range(len(other.cont)+1):
      res = other.cont[:i]+">"+self.cont
      res += ">"+other.cont[i:]
      print(res)
spam=SpecialString("spam")
eggs=SpecialString("eggs")
spam > eggs
```
```
>spam>eggs
e>spam>ggs
eg>spam>gs
egg>spam>s
eggs>spam>
```
## String 
Magic methods for String representation:

* \__str__ :The function is used to return a user-friendly string
  representation of the object
* \__repr__

## Attribute Access

Magic methods for Attribute access:

* \__getattribute__
* \__setattr__
* \__getattr__

``` py
class Book:
    def __init__(self, title, author, price):
        super().__init__()
        self.title = title
        self.author = author
        self.price = price
        self._discount = 0.1

    # The __str__ function is used to return a user-friendly string
    # representation of the object
    def __str__(self):
        return f"{self.title} by {self.author}, costs {self.price}"

    # Called when an attribute is retrieved. Be aware that you can't
    # directly access the attr name otherwise a recursive loop is created
    def __getattribute__(self, name):
        if (name == "price"):
            p = super().__getattribute__("price")
            d = super().__getattribute__("_discount")
            return p - (p * d)
        return super().__getattribute__(name)

    # __setattr__ called when an attribute value is set. Don't set the attr
    # directly here otherwise a recursive loop causes a crash
    def __setattr__(self, name, value):
        if (name == "price"):
            if type(value) is not float:
                raise ValueError("The 'price' attribute must be a float")
        return super().__setattr__(name, value)

    # __getattr__ called when __getattribute__ lookup fails - you can
    # pretty much generate attributes on the fly with this method
    def __getattr__(self, name):
        return name + " is not here!"


b1 = Book("War and Peace", "Leo Tolstoy", 39.95)
b2 = Book("The Catcher in the Rye", "JD Salinger", 29.95)

# Try setting and accessing the price
b1.price = 38.95
print(b1)

b2.price = float(40)  # using an int will raise an exception
print(b2)

# If an attribute doesn't exist, __getattr__ will be called
print(b1.randomprop)
```
```
War and Peace by Leo Tolstoy, costs 35.055
The Catcher in the Rye by JD Salinger, costs 36.0
randomprop is not here!
```

## Callable Objects

``` py
class Book:
    def __init__(self, title, author, price):
        super().__init__()
        self.title = title
        self.author = author
        self.price = price

    def __str__(self):
        return f"{self.title} by {self.author}, costs {self.price}"

    # the __call__ method can be used to call the object like a function
    def __call__(self, title, author, price):
        self.title = title
        self.author = author
        self.price = price


b1 = Book("War and Peace", "Leo Tolstoy", 39.95)
b2 = Book("The Catcher in the Rye", "JD Salinger", 29.95)

# call the object as if it were a function
print(b1)
b1("Anna Karenina", "Leo Tolstoy", 49.95)
print(b1)

```
```
War and Peace by Leo Tolstoy, costs 39.95
Anna Karenina by Leo Tolstoy, costs 49.95
```

## Containers

There are several magic methods for making classes act like containers.

* \__len__ for len()
* \__getitem__ for indexing
* \__setitem__ for assigning to indexed values
* \__delitem__ for deleting indexed values
* \__iter__ for iteration over objects (e.g., in for loops)
* \__contains__ for in

``` py
import random
class VagueList:
  def __init__(self,cont):
    self.cont=cont
  def __getitem__(self,index):
    return self.cont[index+random.randint(-1,1)]
  def __len__(self):
    return random.randint(0,len(self.cont)*2)

vague_list=VagueList(["A","B","C","D","E"])
print(len(vague_list))
print(len(vague_list))
print(vague_list[2])
print(vague_list[2])
```
```
10
0
D
C
```

## Destructor

**Destructors** are called when an object gets destroyed. In Python, destructors are not needed as much needed in C++ because Python has a garbage collector that handles memory management automatically.
The \__del__() method is a known as a destructor method in Python. It is called when all references to the object have been deleted i.e when an object is garbage collected.


``` py
def __del__(self):
        print("Destructor called")
```