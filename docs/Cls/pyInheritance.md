Inheritance provides a way to share functionality between classes.

To inherit a class from another class, put the superclass name in parentheses after the class name. A class that inherits from another class is called a subclass. A class that is inherited from is called a superclass. If a class inherits from another with the same attributes or methods, it overrides them. One class can inherit from another, and that class can inherit from a third class. However, circular inheritance is not possible.

The function super is a useful inheritance-related function that refers to the parent class. It can be used to find the method with a certain name in an object's superclass.

``` py
class Animal:
  def __init__(self,name,color):
    self.name=name
    self.color=color 
  def walk(self):
    print("walking...")
class Cat(Animal):
  def purr(self):
    print("prrrr")
class Dog(Animal):
  def bark(self):
    print("woof!")
    super().walk()
fido = Dog("fido","brown")
print(fido.color)
fido.bark()
```
```
brown
woof!
walking...
```

``` py
class RevStr(str):
  def __str__(self):
    return self[::-1]

hello = RevStr('Hello, World!')
print(hello)
```
```
!dlroW ,olleH
```

## Multiple Inheritance

**Method resolution order:**
In Python, every class whether built-in or user-defined is derived from the object class and all the objects are instances of the class object. Hence, the object class is the base class for all the other classes.
In the case of multiple inheritance, a given attribute is first searched in the current class if it’s not found then it’s searched in the parent classes. The parent classes are searched in a depth-first, left-right fashion and each class is searched once.
If we see the above example then the order of search for the attributes will be Derived, Base1, Base2, object. The order that is followed is known as a linearization of the class Derived and this order is found out using a set of rules called Method Resolution Order (MRO).

**To view the MRO of a class:** 
 

Use the mro() method, it returns a list 
Eg. Class4.mro()
Use the _mro_ attribute, it returns a tuple 
Eg. Class4.__mro__

``` py
# Understanding multiple inheritance
class A:
    def __init__(self):
        super().__init__()
        self.foo = "foo"
        self.name = "Class A"

class B:
    def __init__(self):
        super().__init__()
        self.bar = "bar"
        self.name = "Class B"

class C(B, A):
    def __init__(self):
        super().__init__()

    def showprops(self):
        print(self.foo)
        print(self.bar)
        print(self.name)


# create the class and call showname()
c = C()
print(C.mro())
print(C.__mro__) #Method resolution order
c.showprops()

```
```
[<class '__main__.C'>, <class '__main__.B'>, <class '__main__.A'>, <class 'object'>]
(<class '__main__.C'>, <class '__main__.B'>, <class '__main__.A'>, <class 'object'>)
foo
bar
Class B
```

## Interfaces

Interfaces are not necessary in Python. This is because Python has proper multiple inheritance, and also ducktyping, which means that the places where you must have interfaces in Java, you don't have to have them in Python.

That said, there are still several uses for interfaces. Some of them are covered by Pythons Abstract Base Classes, introduced in Python 2.6. They are useful, if you want to make base classes that cannot be instantiated, but provide a specific interface or part of an implementation.

Another usage is if you somehow want to specify that an object implements a specific interface, and you can use ABC's for that too by subclassing from them. Another way is zope.interface, a module that is a part of the Zope Component Architecture, a really awesomely cool component framework. Here you don't subclass from the interfaces, but instead mark classes (or even instances) as implementing an interface. This can also be used to look up components from a component registry.

Interface acts as a blueprint for designing classes, so interfaces are implemented using implementer decorator on class. If a class implements an interface, then the instances of the class provide the interface. Objects can provide interfaces directly, in addition to what their classes implement.

``` py
pip install zope.interface
```
```
Collecting zope.interface
  Downloading zope.interface-5.4.0-cp37-cp37m-manylinux2010_x86_64.whl (251 kB)
     |████████████████████████████████| 251 kB 9.9 MB/s 
Requirement already satisfied: setuptools in /usr/local/lib/python3.7/dist-packages (from zope.interface) (57.4.0)
Installing collected packages: zope.interface
Successfully installed zope.interface-5.4.0
```

``` py
import zope.interface


class MyInterface(zope.interface.Interface):
	x = zope.interface.Attribute('foo')
	def method1(self, x, y, z):
		pass
	def method2(self):
		pass

@zope.interface.implementer(MyInterface)
class MyClass:
	def method1(self, x):
		return x**2
	def method2(self):
		return "foo"
obj = MyClass()

# ask an interface whether it
# is implemented by a class:
print(MyInterface.implementedBy(MyClass))

# MyClass does not provide
# MyInterface but implements it:
print(MyInterface.providedBy(MyClass))

# ask whether an interface
# is provided by an object:
print(MyInterface.providedBy(obj))

# ask what interfaces are
# implemented by a class:
print(list(zope.interface.implementedBy(MyClass)))

# ask what interfaces are
# provided by an object:
print(list(zope.interface.providedBy(obj)))

# class does not provide interface
print(list(zope.interface.providedBy(MyClass)))

```
```
True
False
True
[<InterfaceClass __main__.MyInterface>]
[<InterfaceClass __main__.MyInterface>]
[]
```