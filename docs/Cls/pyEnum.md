Enumerations in Python are implemented by using the module named “enum“.Enumerations are created using classes. Enums have names and values associated with them.
Properties of enum:

1. Enums can be displayed as string or repr.
2. Enums can be checked for their types using type().
3. “name” keyword is used to display the name of the enum member.
4. Enumerations are iterable. They can be iterated using loops
5. Enumerations support hashing. Enums can be used in dictionaries or sets.

``` py
# Python code to demonstrate enumerations

# importing enum for enumerations
import enum

# creating enumerations using class
class Animal(enum.Enum):
	dog = 1
	cat = 2
	lion = 3

# printing enum member as string
print ("The string representation of enum member is : ",end="")
print (Animal.dog)

# printing enum member as repr
print ("The repr representation of enum member is : ",end="")
print (repr(Animal.dog))

# printing the type of enum member using type()
print ("The type of enum member is : ",end ="")
print (type(Animal.dog))

# printing name of enum member using "name" keyword
print ("The name of enum member is : ",end ="")
print (Animal.dog.name)

```
```
The string representation of enum member is : Animal.dog
The repr representation of enum member is : <Animal.dog: 1>
The type of enum member is : <enum 'Animal'>
The name of enum member is : dog
```

``` py
# Python code to demonstrate enumerations
# iterations and hashing
# importing enum for enumerations
import enum

# creating enumerations using class
class Animal(enum.Enum):
	dog = 1
	cat = 2
	lion = 3

# printing all enum members using loop
print ("All the enum values are : ")
for Anim in (Animal):
	print(Anim)

# Hashing enum member as dictionary
di = {}
di[Animal.dog] = 'bark'
di[Animal.lion] = 'roar'

# checking if enum values are hashed successfully
if di=={Animal.dog : 'bark',Animal.lion : 'roar'}:
	print ("Enum is hashed")
else: print ("Enum is not hashed")

```
```
All the enum values are : 
Animal.dog
Animal.cat
Animal.lion
Enum is hashed
```

**Accessing Modes**: Enum members can be accessed by two ways

1. By value :- In this method, the value of enum member is passed.
2. By name :- In this method, the name of enum member is passed.
Separate value or name can also be accessed using “name” or “value” keyword.

**Comparison**: Enumerations supports two types of comparisons

1. Identity :- These are checked using keywords “is” and “is not“.
2. Equality :- Equality comparisons of “==” and “!=” types are also supported.

``` py
# Python code to demonstrate enumerations
# Access and comparison

# importing enum for enumerations
import enum

# creating enumerations using class
class Animal(enum.Enum):
	dog = 1
	cat = 2
	lion = 3

# Accessing enum member using value
print ("The enum member associated with value 2 is : ",end="")
print (Animal(2))

# Accessing enum member using name
print ("The enum member associated with name lion is : ",end="")
print (Animal['lion'])

# Assigning enum member
mem = Animal.dog

# Displaying value
print ("The value associated with dog is : ",end="")
print (mem.value)

# Displaying name
print ("The name associated with dog is : ",end="")
print (mem.name)

# Comparison using "is"
if Animal.dog is Animal.cat:
	print ("Dog and cat are same animals")
else : print ("Dog and cat are different animals")

# Comparison using "!="
if Animal.lion != Animal.cat:
	print ("Lions and cat are different")
else : print ("Lions and cat are same")
```
```
The enum member associated with value 2 is : Animal.cat
The enum member associated with name lion is : Animal.lion
The value associated with dog is : 1
The name associated with dog is : dog
Dog and cat are different animals
Lions and cat are different
```

``` py
# define enumerations using the Enum base class

from enum import Enum, unique, auto
#Enum do not permit repeated names howewver
#To avoid repeated values the unique decorator is used
@unique
class Fruit(Enum):
    APPLE = 1
    BANANA = 2
    ORANGE = 3
    TOMATO = 4
    PEAR = auto()


def main():
    # enums have human-readable values and types
    print(Fruit.APPLE)
    print(type(Fruit.APPLE))
    print(repr(Fruit.APPLE))

    # enums have name and value properties
    print(Fruit.APPLE.name, Fruit.APPLE.value)

    # print the auto-generated value
    print(Fruit.PEAR.value)

    # enums are hashable - can be used as keys
    myFruits = {}
    myFruits[Fruit.BANANA] = "Come Mr. Tally-man"
    print(myFruits[Fruit.BANANA])


if __name__ == "__main__":
    main()
```
```
Fruit.APPLE
<enum 'Fruit'>
<Fruit.APPLE: 1>
APPLE 1
5
Come Mr. Tally-man
```