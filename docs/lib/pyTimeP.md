In Python, we have three modules that help us find the execution time of a program.

## Using Timeit Module

Python timeit module is often used to measure the execution time of small code snippets. We can also use the timeit() function which executes an anonymous function with a number of executions. It temporarily turns off garbage collection (the process of collecting unwanted variables whose use has been over and clears them by marking them as garbage values to free up the memory) during calculating the time of execution. How is the "timeit" command better than "time"? It averages results and ignores warm up.

``` py
# importing the module
import timeit


# using the timeit method and lambda
# expression to get the execution time of
# the function.
t = timeit.timeit(lambda: "print('Hello World!')")

# printing the execution time
print(t)
```
```
0.08696221099944523
```

``` py
# importing the module
import timeit

# sample function that returns square
# of the value passed
def print_square(x):
	return (x**2)

# using the timeit method and lambda
# expression to get the execution time of
# the function, number defines how many
# times we execute this function
t = timeit.timeit(lambda: print_square(3), number=10)

# printing the execution time
print(t)

```
```
4.83900021208683e-06
```

Now, practically to estimate the execution time of a program we generally do not use the value obtained once as the ultimate correct value, because the execution of a program may depend upon os and availability of hardware at a particular instant of time. So generally we take multiple values of execution time and generally the average computed gives us the best possible answer. For this, we would use the timeit.repeat() method instead of timeit.timeit() which takes a repeat parameter and saves you the trouble of creating a loop and storing the values in the array.

``` py
# importing the module
import timeit


# sample function that returns square
# of the value passed
def print_square(x):
	return (x**2)

# using the repeat method and lambda
# expression to get the execution time of
# the function, number defines how many
# times we execute this function and the
# repeat defines the number of times the
# time calculation needs to be done.
t = timeit.repeat(lambda: print_square(3), number=10, repeat=5)

# printing the execution time
print(t)

```
```
[5.1380002332734875e-06, 3.6009996620123275e-06, 3.5189996197004803e-06, 3.484999979264103e-06, 3.50700065609999e-06]
```

Also, we can use the timeit.default_timer() which basically records the time at the instant when the method is called. So we call the method just before and after the lines of the code for which we want to calculate the execution time and then basically the difference between the two times give us the result. So for finding the time we record the times using the timeit.defaultTimer() method, and then we print the difference between the two times in the last line.

``` py
# importing the module
import timeit


# sample function that returns
# square of the value passed
def print_square(x):
	return (x**2)

# records the time at this instant
# of the program
start = timeit.default_timer()

# calls the function
print_square(3)

# records the time at this instant
# of the program
end = timeit.default_timer()

# printing the execution time by subtracting
# the time before the function from
# the time after the function
print(end-start)

```
```
3.099999958067201e-05
```



``` py
"""Using "timeit"""
from timeit import timeit

items = {
    'a': 1,
    'b': 2,
}
default = -1


def use_catch(key):
    """Use try/catch to get a key with default"""
    try:
        return items[key]
    except KeyError:
        return default


def use_get(key):
    """Use dict.get to get a key with default"""
    return items.get(key, default)


if __name__ == '__main__':
    # Key is in the dictionary
    print('catch', timeit('use_catch("a")', 'from __main__ import use_catch'))
    print('get', timeit('use_get("a")', 'from __main__ import use_get'))

    # Key is missing from the dictionary
    print('catch', timeit('use_catch("x")', 'from __main__ import use_catch'))
    print('get', timeit('use_get("x")', 'from __main__ import use_get'))
```
```
catch 0.12401290399975551
get 0.16413491899947985
catch 0.32834199399985664
get 0.17250985499958915
```

## Using Time Module

We can use the time.perf_counter() method in the same way as the timeit.default_timer() method discussed above. It can use the highest possible resolution clock and gives you the most accurate result. In fact the timeit.default_timer() also uses time.perf_counter() as it’s base. This also records the time before and after the required lines of code whose execution or elapsed time needs to be calculated. Then we subtract the recorded time before the start of the lines from the recorded time after the lines of the code.

``` py
# importing the module
import time

# sample function that returns square
# of the value passed
def print_square(x):
	return (x**2)

# records the time at this instant of the
# program
start = time.perf_counter()

# calls the function
print_square(3)

# records the time at this instant of the
# program
end = time.perf_counter()

# printing the execution time by subtracting
# the time before the function from
# the time after the function
print(end-start)

```
```
2.8733999897667672e-05
```
To measure the elapsed time or execution time of a block of code in nanoseconds, we can use the time.time_ns() function. This follows the same syntax as the time.perf_counter() function, like recording the time before and after the lines of the code and then subtracting the values and then printing them to the screen, but it records in nanoseconds instead of seconds.

``` py
# importing the module
import time

# sample function that returns square
# of the value passed
def print_square(x):
	return (x**2)

# records the time in nanoseceonds at
# this instant of the program
start = time.time_ns()

# calls the function
print_square(3)

# records the time in nanoseceonds at this
# instant of the program
end = time.time_ns()

# printing the execution time by subtracting
# the time before the function from
# the time after the function
print(end-start)

```
```
50676
```

``` py
"""Measuring time"""

from time import perf_counter


def upto_for(n):
    """Sum 1...n with a for loop"""
    total = 0
    for i in range(n):
        total += i
    return total


def upto_sum(n):
    """Sum 1...n with built-in sum and range"""
    return sum(range(n))


if __name__ == '__main__':
    n = 1_000_000

    start = perf_counter()
    upto_for(n)
    duration = perf_counter() - start
    print('upto_for', duration)

    start = perf_counter()
    upto_sum(n)
    duration = perf_counter() - start
    print('upto_sum', duration)

```
```
upto_for 0.0630132690002938
upto_sum 0.018293597999218036
```

## Using Datetime Module

Datetime module can also be used to find the time elapsed or spent in a code block provided you are not looking for high precision. the datetime.now() also works the same way as the timeit.default_timer() or time.perf_counter() but lacks the same precision as those. It returns the result in HH:MM:SS format. This function is generally used for getting the current time and not a preferred use case for calculating execution time. However, these can be programs that take quite some time to execute like training ML/AI models, web scraping large websites, etc.

``` py
# importing the module
from datetime import datetime

# sample function that returns square
# of the value passed
def print_square(x):
	return (x**2)

# records the time at this instant of
# the program in HH:MM:SS format
start = datetime.now()

# calls the function
print_square(3)

# records the time at this instant of the
# program in HH:MM:SS format
end = datetime.now()

# printing the execution time by subtracting
# the time before the function from
# the time after the function
print(end-start)

```
```
0:00:00.000034
```
## [%Timeit](https://ipython.org/ipython-doc/dev/interactive/magics.html#magic-timeit) Magic inline

``` py
import numpy as np
import pandas as pd

data = pd.Series(np.random.randint(50, 60 , 10_000))

#Outliers
data[7]=3
data[1003]=100


def find_outliers(data):
    """Find outliers in data, return indices of outliers"""
    out = data[(data - data.mean()).abs() > 2 * data.std()]
    return out.index

find_outliers(data)
```
```
Int64Index([7, 1003], dtype='int64')
```

``` py
%timeit find_outliers(data)
```
```
1000 loops, best of 5: 629 µs per loop
```

```
%prun -s cumulative find_outliers(data)
```

## Using cprofile

Python includes a built in module called cProfile which is used to measure the execution time of a program.cProfiler module provides all information about how long the program is executing and how many times the function get called in a program. How does cProfile work? It records every function entry and exit.

``` py
# importing cProfile
import cProfile

cProfile.run("10 + 10")
```
```
   3 function calls in 0.000 seconds

   Ordered by: standard name

   ncalls  tottime  percall  cumtime  percall filename:lineno(function)
        1    0.000    0.000    0.000    0.000 <string>:1(<module>)
        1    0.000    0.000    0.000    0.000 {built-in method builtins.exec}
        1    0.000    0.000    0.000    0.000 {method 'disable' of '_lsprof.Profiler' objects}
```

``` py
# importing cProfile
import cProfile

def f():
	print("hello")
cProfile.run('f()')
```
```
hello
         39 function calls in 0.000 seconds

   Ordered by: standard name

   ncalls  tottime  percall  cumtime  percall filename:lineno(function)
        1    0.000    0.000    0.000    0.000 <ipython-input-46-7b34c7345cd2>:4(f)
        1    0.000    0.000    0.000    0.000 <string>:1(<module>)
        3    0.000    0.000    0.000    0.000 iostream.py:195(schedule)
        2    0.000    0.000    0.000    0.000 iostream.py:307(_is_master_process)
        2    0.000    0.000    0.000    0.000 iostream.py:320(_schedule_flush)
        2    0.000    0.000    0.000    0.000 iostream.py:382(write)
        3    0.000    0.000    0.000    0.000 iostream.py:93(_event_pipe)
        3    0.000    0.000    0.000    0.000 socket.py:480(send)
        3    0.000    0.000    0.000    0.000 threading.py:1050(_wait_for_tstate_lock)
        3    0.000    0.000    0.000    0.000 threading.py:1092(is_alive)
        3    0.000    0.000    0.000    0.000 threading.py:507(is_set)
        1    0.000    0.000    0.000    0.000 {built-in method builtins.exec}
        2    0.000    0.000    0.000    0.000 {built-in method builtins.isinstance}
        1    0.000    0.000    0.000    0.000 {built-in method builtins.print}
        2    0.000    0.000    0.000    0.000 {built-in method posix.getpid}
        3    0.000    0.000    0.000    0.000 {method 'acquire' of '_thread.lock' objects}
        3    0.000    0.000    0.000    0.000 {method 'append' of 'collections.deque' objects}
        1    0.000    0.000    0.000    0.000 {method 'disable' of '_lsprof.Profiler' objects}
```

## Using line_profiler

Python provides a built-in module to measure execution time and the module name is LineProfiler.It gives detailed report on time consumed by a program.

``` py
!pip install line_profiler
# importing line_profiler module
from line_profiler import LineProfiler

def peek(rk):
	print(rk)

rk ="risk"
profile = LineProfiler(peek(rk))
profile.print_stats()

```
```
risk
Timer unit: 1e-06 s
```

``` py
%load_ext line_profiler
```
``` py
%lprun -f find_outliers
```