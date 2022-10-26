Methods of objects we've looked at so far are called by an instance of a class, which is then passed to the self parameter of the method.
Class methods are different - they are called by a class, which is passed to the cls parameter of the method.
A common use of these are factory methods, which instantiate an instance of a class, using different parameters than those usually passed to the class constructor.

**Class methods** are marked with a classmethod decorator. Technically, the parameters self and cls are just conventions; they could be changed to anything else. However, they are universally followed, so it is wise to stick to using them.

**Static methods** behave like plain functions, except for the fact that you can call them from an instance of the class.

``` py
class Rectangle:
  def __init__(self,w,h):
    self.w=w
    self.h=h
  def area(self):
    return self.w*self.h
  @classmethod
  def new_square(cls,side_length):
    return cls(side_length,side_length)
  @staticmethod
  def spam(x):
    print("Spam and eggs"+x)

square=Rectangle.new_square(5)
print(square.area())
Rectangle.spam(" and Ham")
```
```
25
Spam and eggs and Ham
```

**Class method vs Static Method**

* A class method takes cls as the first parameter while a static method needs no specific parameters.
* A class method can access or modify the class state while a static method can’t access or modify it.
* In general, static methods know nothing about the class state. They are utility-type methods that take some parameters and work upon those parameters. On the other hand class methods must have class as a parameter.
* We use @classmethod decorator in python to create a class method and we use @staticmethod decorator to create a static method in python.

**When to use what?**

* We generally use class method to create factory methods. Factory methods return class objects ( similar to a constructor ) for different use cases.
* We generally use static methods to create utility functions.

``` py
# Python program to demonstrate
# use of class method and static method.
from datetime import date

class Person:
	def __init__(self, name, age):
		self.name = name
		self.age = age
	
	# a class method to create a Person object by birth year.
	@classmethod
	def fromBirthYear(cls, name, year):
		return cls(name, date.today().year - year)
	
	# a static method to check if a Person is adult or not.
	@staticmethod
	def isAdult(age):
		return age > 18

person1 = Person('mayank', 21)
person2 = Person.fromBirthYear('mayank', 1996)

print (person1.age)
print (person2.age)

# print the result
print (Person.isAdult(22))

```
```
21
25
True
```