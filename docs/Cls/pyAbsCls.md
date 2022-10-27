An abstract class can be considered as a blueprint for other classes. It allows you to create a set of methods that must be created within any child classes built from the abstract class. A class which contains one or more abstract methods is called an abstract class. An abstract method is a method that has a declaration but does not have an implementation. While we are designing large functional units we use an abstract class. When we want to provide a common interface for different implementations of a component, we use an abstract class.

**Why use Abstract Base Classes :**

By defining an abstract base class, you can define a common Application Program Interface(API) for a set of subclasses. This capability is especially useful in situations where a third-party is going to provide implementations, such as with plugins, but can also help you when working in a large team or with a large code-base where keeping all classes in your mind is difficult or not possible. 
  
**How Abstract Base classes work:**

By default, Python does not provide abstract classes. Python comes with a module that provides the base for defining Abstract Base classes(ABC) and that module name is ABC. ABC works by decorating methods of the base class as abstract and then registering concrete classes as implementations of the abstract base. A method becomes abstract when decorated with the keyword @abstractmethod.

``` py
# Using Abstract Base Classes to enforce class constraints

from abc import ABC, abstractmethod


class GraphicShape(ABC):
    # Inheriting from ABC indicates that this is an abstract base class
    def __init__(self):
        super().__init__()

    # declaring a method as abstract requires a subclass to implement it
    @abstractmethod
    def calcArea(self):
        pass


class Circle(GraphicShape):
    def __init__(self, radius):
        self.radius = radius

    def calcArea(self):
        return 3.14 * (self.radius ** 2)


class Square(GraphicShape):
    def __init__(self, side):
        self.side = side

    def calcArea(self):
        return self.side * self.side


# Abstract classes can't be instantiated themselves
# g = GraphicShape() # this will error

c = Circle(10)
print(c.calcArea())
s = Square(12)
print(s.calcArea())

```
```
314.0
144
```