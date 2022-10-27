Properties provide a way of customizing access to instance attributes. They are created by putting the property decorator above a method, which means when the instance attribute with the same name as the method is accessed, the method will be called instead. One common use of a property is to make an attribute read-only.

``` py
class Pizza:
  def __init__(self,toppings):
    self.toppings=toppings
  @property
  def pinapple_allowed(self):
    return False
pizza=Pizza(["cheese","tomato"])
print(pizza.pinapple_allowed)
#pizza.pinapple_allowed=True #Read_only
```
```
False
```

Properties can also be set by defining setter/getter functions. The setter function sets the corresponding property's value. The getter gets the value. To define a setter, you need to use a decorator of the same name as the property, followed by a dot and the setter keyword. The same applies to defining getter functions.

``` py
class Pizza:
  def __init__(self,toppings):
    self.toppings=toppings
    self._pinapple_allowed=False
  @property
  def pinapple_allowed(self):
    return self._pinapple_allowed
  @pinapple_allowed.setter
  def pinapple_allowed(self,value):
    if value:
      password=input("Enter password: ")
      if password == "Sword":
        self._pinapple_allowed=value
      else:
        raise ValueError("Intruder")

pizza=Pizza(["cheese","tomato"])
print(pizza.pinapple_allowed)
pizza.pinapple_allowed=True
print(pizza.pinapple_allowed)
```
```
False
Enter password: Sword
True
```