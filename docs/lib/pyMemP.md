Managing memory is important in any programming logic but this becomes necessary for python. As python is used in Ml and AI where vast data are used which needs to be managed. Memory leaks, i.e. the program is out of memory after running for several hours. To manage these memory leaks memory monitoring is essential. Monitoring memory is also called profiling. As a developer, it’s a necessity that we profile our program and use less memory allocation as much as possible.

## Using Tracemalloc

Tracemalloc is a library module that traces every memory block in python. The tracing starts by using the start() during runtime. This library module can also give information about the total size, number, and average size of allocated memory blocks.

``` py
# importing the module
import tracemalloc

# code or function for which memory
# has to be monitored
def app():
	lt = []
	for i in range(0, 100000):
		lt.append(i)

# starting the monitoring
tracemalloc.start()

# function call
app()

# displaying the memory
print(tracemalloc.get_traced_memory())

# stopping the library
tracemalloc.stop()

```
```
(729, 3617551)
```

The output is given in form of (current, peak), i.e. current memory is the memory the code is currently using and peak memory is the maximum space the program used while executing.

## Using Psutil

Psutil is a python system library used to keep track of various resources in the system and their utilization. The library is used for profiling, limiting, and management of process resources.

``` py
import os
import psutil

p = psutil.Process(os.getpid())
for i in range(10):
    print(i)
    for j in range(5):
        mem_usage = p.memory_info().rss / 1024 / 1024
        print("{} {} MB".format(j, mem_usage))
```
``` py
def memory_usage_psutil():
    # return the memory usage in MB
    import psutil
    process = psutil.Process(os.getpid())
    mem = process.get_memory_info()[0] / float(2 ** 20)
    return mem
```
The above function returns the memory usage of the current Python process in MiB. Depending on the platform it will choose the most accurate and fastest way to get this information. For example, in Windows it will use the C++ Win32 API while in Linux it will read from /proc, hiding the implementation details and proving on each platform a fast and accurate measurement.

If you are looking for an easy way to get the memory consumption within Python this in my opinion your best shot.

## Using Memory Profiler

``` py
!pip install memory-profiler 
```
Notice the @profile this is a decorator. Any function which is decorated by this decorator, that function will be tracked.

``` py
%%file sos.py
"""memory_profiler example"""

@profile
def sum_of_diffs(vals):
    """Compute sum of diffs"""
    vals2 = vals[1:]

    total = 0
    for v1, v2 in zip(vals, vals2):
        total += v2 - v1

    return total


if __name__ == '__main__':
    vals = list(range(1, 1_000_000, 3))
    print(sum_of_diffs(vals))
```
```
Writing sos.py
```

``` py
!python -m memory_profiler sos
```
```
999996
Filename: /content/sos.py

Line #    Mem usage    Increment  Occurrences   Line Contents
=============================================================
     3   52.160 MiB   52.160 MiB           1   @profile
     4                                         def sum_of_diffs(vals):
     5                                             """Compute sum of diffs"""
     6   54.738 MiB    2.578 MiB           1       vals2 = vals[1:]
     7                                         
     8   54.738 MiB    0.000 MiB           1       total = 0
     9   54.738 MiB    0.000 MiB      333333       for v1, v2 in zip(vals, vals2):
    10   54.738 MiB    0.000 MiB      333332           total += v2 - v1
    11                                         
    12   54.738 MiB    0.000 MiB           1       return total
```

``` py
%%file sos1.py
"""memory_profiler example"""

def sum_of_diffs(vals):
    """Compute sum of diffs"""
    vals2 = vals[1:]

    total = 0
    for v1, v2 in zip(vals, vals2):
        total += v2 - v1

    return total


if __name__ == '__main__':
    vals = list(range(1, 100_000_000, 3))
    print(sum_of_diffs(vals))
```
```
Writing sos1.py
```

mprof generates profile data

``` py
!mprof run sos1.py
```
```
mprof: Sampling memory every 0.1s
running new process
running as a Python program...
99999996
```

``` py
!mprof plot mprofile_20211225174100.dat
```
```
<Figure size 1260x540 with 1 Axes>
```

## Reducing Memory Consumption with Slots

Slots in Python is a special mechanism that is used to reduce memory of the objects. In Python, all the objects use a dynamic dictionary for adding an attribute. Slots is a static type method in this no dynamic dictionary are required for allocating attribute.
``` py
# defining the class.
class myCourse:
	
	# defining the slots.
	__slots__ =('course', 'price')
	
	def __init__(self):
		
		# initializing the values
		self.course ='MAth'
		self.price = 300

# create an object of gfg class
a = myCourse()

# print the slot
print(a.__slots__)

# print the slot variable
print(a.course, a.price)

```
```
('course', 'price')
MAth 300
```
When we create objects for classes, it requires memory and the attribute are stored in the form of a dictionary. In case if we need to allocate thousands of objects, it will take a lot of memory space. slots provide a special mechanism to reduce the size of objects.It is a concept of memory optimisation on objects. As every object in Python contains a dynamic dictionary that allows adding attributes. For every instance object, we will have an instance of a dictionary that consumes more space and wastes a lot of RAM. In Python, there is no default functionality to allocate a static amount of memory while creating the object to store all its attributes. Usage of slots reduce the wastage of space and speed up the program by allocating space for a fixed amount of attributes.

``` py
#Example of python object without slots
class MFT(object):
	def __init__(self, *args, **kwargs):
				self.a = 1
				self.b = 2

if __name__ == "__main__":
	instance = MFT()
	print(instance.__dict__)
```
```
{'a': 1, 'b': 2}
```

``` py
#Example of python object with slots 
class MFT(object):
	__slots__=['a', 'b']
	def __init__(self, *args, **kwargs):
				self.a = 1
				self.b = 2

if __name__ == "__main__":
	instance = MFT()
	print(instance.__slots__)
```
```
['a', 'b']
```

**Result of using slots:**

+ Fast access to attributes
+ Saves memory space