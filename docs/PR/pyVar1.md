
In Python, we store all pieces of data -- numbers, characters, strings, *everything* -- as objects, and we refer to these objects using variables.  As a simple case, we can *assign* a variable a value using the assignment operator, which is the "equals" sign. Python's order of operations is the same as that of normal mathematics: parentheses first, then exponentiation, then multiplication/division, and then addition/subtraction.

``` py
x = 4
y = 5
z = x + y
print(z)
stri="Hello" # or stri='Hello' No difference in python between "" and ''
print(stri + str(z))
a=True
print(a)
b=(1==3)
print(b)
```
``` 
9
Hello9
True
False
```

##**Three tools for understanding strange objects**
### type() function
+ type() (what is this thing?) To inspect which type is a variable use type().
### dir() function
+ dir() (what can I do with it?)
### help() function
+ help() (tell me more)
``` py
print(type(z))
print(type(a))
print(type(stri))
print(dir(2))
#print(help(2))
```
```
<class 'int'>
<class 'int'>
<class 'str'>
['__abs__', '__add__', '__and__', '__bool__', '__ceil__', '__class__', '__delattr__', '__dir__', '__divmod__', '__doc__', '__eq__', '__float__', '__floor__', '__floordiv__', '__format__', '__ge__', '__getattribute__', '__getnewargs__', '__gt__', '__hash__', '__index__', '__init__', '__init_subclass__', '__int__', '__invert__', '__le__', '__lshift__', '__lt__', '__mod__', '__mul__', '__ne__', '__neg__', '__new__', '__or__', '__pos__', '__pow__', '__radd__', '__rand__', '__rdivmod__', '__reduce__', '__reduce_ex__', '__repr__', '__rfloordiv__', '__rlshift__', '__rmod__', '__rmul__', '__ror__', '__round__', '__rpow__', '__rrshift__', '__rshift__', '__rsub__', '__rtruediv__', '__rxor__', '__setattr__', '__sizeof__', '__str__', '__sub__', '__subclasshook__', '__truediv__', '__trunc__', '__xor__', 'bit_length', 'conjugate', 'denominator', 'from_bytes', 'imag', 'numerator', 'real', 'to_bytes']
```

Python supports addition (+), substraction(-), multiplication(\*), division(/),exponentiation(**), quotient (//) and remainder(%). You can chain exponentiations together. In other words, you can rise a number to multiple powers.

## id() function

The id() function returns identity (unique integer) of an object.
``` py
print('id of 5 =',id(5))

a = 5
print('id of a =',id(a))

b = a
print('id of b =',id(b))

c = 5.0
print('id of c =',id(c))
``` 
```
id of 5 = 94364870744704
id of a = 94364870744704
id of b = 94364870744704
id of c = 140097885531312
``` 

It's important to note that everything in Python is an object, even numbers, and Classes. Hence, integer 5 has a unique id. The id of the integer 5 remains constant during the lifetime. Similar is the case for float 5.5 and other objects.

## isinstance() function
To verify the type of an object, the isinstance() function checks if the object (first argument) is an instance or subclass of classinfo class (second argument).

## The None Object
The **None** object is used to represent the absence of a value. It is similar to null in other programming languages. The None object is returned by any function that doesn't explicitly return anything else.
