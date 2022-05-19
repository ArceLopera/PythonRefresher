
The location where we can find a variable and also access it if required is called the scope of a variable. Python resolves names using the so-called LEGB rule, which is named after the Python scope for names. The letters in LEGB stand for Local, Enclosing, Global, and Built-in. When you use nested functions, names are resolved by first checking the local scope or the innermost function’s local scope. Then, Python looks at all enclosing scopes of outer functions from the innermost scope to the outermost scope. If no match is found, then Python looks at the global and built-in scopes. If it can’t find the name, then you’ll get an error.
### Global Keyword
Global variables are the ones that are defined and declared outside any function and are not specified to any function. They can be used by any part of the program.

We only need to use the global keyword in a function if we want to do assignments or change the global variable. global is not needed for printing and accessing. Python “assumes” that we want a local variable due to the assignment to s inside of f(), so the first statement throws the error message. Any variable which is changed or created inside of a function is local if it hasn’t been declared as a global variable. To tell Python, that we want to use the global variable, we have to use the keyword “global”

``` py
a = 1

# Uses global because there is no local 'a'
def f():
	print('Inside f() : ', a)

# Variable 'a' is redefined as a local
def g():
	a = 2
	print('Inside g() : ', a)

# Uses global keyword to modify global 'a'
def h():
	global a
	a = 3
	print('Inside h() : ', a)


# Global scope
print('global : ', a)
f()
print('global : ', a)
g()
print('global : ', a)
h()
print('global : ', a)
```
```
global :  1
Inside f() :  1
global :  1
Inside g() :  2
global :  1
Inside h() :  3
global :  3
```
###Nonlocal Keyword
In Python, nonlocal keyword is used in the case of nested functions. This keyword works similar to the global, but rather than global, this keyword declares a variable to point to the variable of outside enclosing function, in case of nested functions.

``` py
# Python program to demonstrate
# nonlocal keyword

print ("Value of a using nonlocal is : ", end ="")
def outer():
	a = 5
	def inner():
		nonlocal a
		a = 10
	inner()
	print (a)

outer()

# demonstrating without non local
# inner loop not changing the value of outer a
# prints 5
print ("Value of a without using nonlocal is : ", end ="")
def outer():
	a = 5
	def inner():
		a = 10
	inner()
	print (a)

outer()
```

```
Value of a using nonlocal is : 10
Value of a without using nonlocal is : 5
```