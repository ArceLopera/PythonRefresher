A Decorator is a callable that takes another function as an argument, extending the behavior of that function without explicitly modifying that function.

Decorators provide a way to modify functions using other functions. This is ideal when you need to extend the functionality of functions that you don't want to modify.

## Functions within functions

``` py
def fib_3(a, b, c):
  def get_3():
    return a, b ,c
  return get_3

fib_3(1,1,2)
```
```
<function __main__.fib_3.<locals>.get_3>
```

``` py
f=fib_3(1,1,2)
f()
```
```
(1, 1, 2)
```
We defined a function named decor that has a single parameter func. Inside decor, we defined a nested function named wrap. The wrap function will print a string, then call func(), and print another string. The decor function returns the wrap function as its result. We could say that the variable decorated is a decorated version of print_text - it's print_text plus something.

``` py
def decor(func):
  def wrap():
    '''This is the wrapper'''
    #Do something before
    print("***************")
    func()
    #Do something after
    print("***************")
  return wrap

def print_text():
  '''Prints Hello'''
  print("Hello")

decorated = decor(print_text)
decorated()
```
```
***************
Hello
***************
```


``` py
print_text.__name__
```
```
print_text
```

``` py
print_text.__doc__
```
```
 Prints Hello
```
Python provides support to wrap a function in a decorator by pre-pending the function definition with a decorator name and the @ symbol. If we are defining a function we can "decorate" it with the @ symbol like. A single function can have multiple decorators.



``` py
def print_text():
  print("Hello")

print_text=decor(print_text)
print_text()
```
```
***************
Hello
***************
```
Is equivalent to:

``` py
@decor
def print_text():
  '''Prints Hello'''
  print("Hello")

print_text()
```
```
***************
Hello
***************
```


``` py
print_text.__name__
```
```
wrap
```


``` py
print_text.__doc__
```
```
This is the wrapper
```
To avoid this problem use functools

``` py
from functools import wraps 
def decor(func):
  @wraps(func)
  def wrap():
    '''This is the wrapper'''
    #Do something before
    print("***************")
    func()
    #Do something after
    print("***************")
  return wrap

@decor
def print_text():
  '''Prints Hello'''
  print("Hello")

print_text()
```
```
***************
Hello
***************
```

``` py
print_text.__name__
```
```
print_text
```

``` py
print_text.__doc__
```
```
Prints Hello
```
## Decorators with arguments

``` py
def pfib(a, b, c):
  print(a,b,c)

pfib(1,1,2)
```
```
1 1 2
```
If I dont want only 3 args but more

``` py
def pfib(a, *args):
  print(a)
  print(args)

pfib(1,1,2, 3)
```
```
1
(1, 2, 3)
```


``` py
def pfib(a, **kwargs):
  print(a)
  print(kwargs)

pfib(1,se=1,th=2, fo=3, fi=5)
```
```
1
{'se': 1, 'th': 2, 'fo': 3, 'fi': 5}
```


``` py
def pfib(*args, **kwargs):
  print(args)
  print(kwargs)

pfib(1,2,2,se=1,th=2, fo=3, fi=5)
```
```
(1, 2, 2)
{'se': 1, 'th': 2, 'fo': 3, 'fi': 5}
```


``` py
def wrapper(*args, **kwargs):
  print(*args)
  print('Leaving wrapper')
  pfib(*args, **kwargs)
  print(kwargs)

wrapper(1,1, th=2)
```
```
1 1
Leaving wrapper
(1, 1)
{'th': 2}
{'th': 2}
```

The template is:

``` py
from functools import wraps

def decorator(func):
  @wraps(func)
  def wrapper(*args, **kwargs):
    #Do something before
    result = func(*args, **kwargs)
    #Do something after
    return result
  return wrapper

@decorator
def func():
  pass
```
## Decorators with classes

We can define a decorator as a class in order to do that, we have to use a call method of classes.

``` py
# Python program showing
# use of __call__() method

class MyDecorator:
	def __init__(self, function):
		self.function = function
	
	def __call__(self):

		# We can add some code
		# before function call

		self.function()

		# We can also add some code
		# after function call.


# adding class decorator to the function
@MyDecorator
def function():
	print("Meps3")

function()
```
```
Meps3
```


``` py
# Python program showing
# class decorator with *args
# and **kwargs

class MyDecorator:
	def __init__(self, function):
		self.function = function
	
	def __call__(self, *args, **kwargs):

		# We can add some code
		# before function call

		self.function(*args, **kwargs)

		# We can also add some code
		# after function call.
	

# adding class decorator to the function
@MyDecorator
def function(name, message ='Hello'):
	print("{}, {}".format(message, name))

function("gpes3", "hello")

```
```
hello, gpes3
```


``` py
# Python program to execute
# time of a program

# importing time module
from time import time
class Timer:

	def __init__(self, func):
		self.function = func

	def __call__(self, *args, **kwargs):
		start_time = time()
		result = self.function(*args, **kwargs)
		end_time = time()
		print("Execution took {} seconds".format(end_time-start_time))
		return result


# adding a decorator to the function
@Timer
def some_function(delay):
	from time import sleep

	# Introducing some time delay to
	# simulate a time taking function.
	sleep(delay)

some_function(3)

```
```
Execution took 3.003098487854004 seconds
```
## Decorators as a cache: Memoization

LRU is the cache replacement algorithm that removes the least recently used data and stores the new data. Suppose we have a cache space of 10 memory frames. And each frame is filled with a file. Now if we want to store the new file, we need to remove the oldest file in the cache and add the new file. This is how LRU works. LRU cache consists of Queue and Dictionary data structures.

Queue: to store the most recently used to least recently used files

Hash table: to store the file and its position in the cache

lru_cache() is one such function in functools module which helps in reducing the execution time of the function by using memoization technique.

``` py
from functools import lru_cache
import time


# Function that computes Fibonacci
# numbers without lru_cache
def fib_without_cache(n):
	if n < 2:
		return n
	return fib_without_cache(n-1) + fib_without_cache(n-2)
	
# Execution start time
begin = time.time()
fib_without_cache(30)

# Execution end time
end = time.time()

print("Time taken to execute the\
 function without lru_cache is", end-begin)

# Function that computes Fibonacci
# numbers with lru_cache
@lru_cache(maxsize = 128)
def fib_with_cache(n):
	if n < 2:
		return n
	return fib_with_cache(n-1) + fib_with_cache(n-2)
	
begin = time.time()
fib_with_cache(30)
end = time.time()

print("Time taken to execute the \
function with lru_cache is", end-begin)

```
```
Time taken to execute the function without lru_cache is 0.3661181926727295
Time taken to execute the function with lru_cache is 7.653236389160156e-05
```