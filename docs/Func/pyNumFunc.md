* To find the maximum or minimum of some numbers or a list, you can use max or min.
* To find the distance of a number from zero (its absolute value), use abs.
* To round a number to a certain number of decimal places, use round.
* To find the total of a list, use sum.

## Numeric Functions

``` py
x=-47.3
y=abs(x)

print(f'x is {type(x)}')
print(f'x is {x}')
print(f'x is {type(y)}')
print(f'x is {y}') 
```
```
x is <class 'float'>
x is -47.3
x is <class 'float'>
x is 47.3
```

``` py
x=47
y=divmod(x, 3)

print(f'x is {type(x)}')
print(f'x is {x}')
print(f'x is {type(y)}')
print(f'x is {y}') 
```
```
x is <class 'int'>
x is 47
x is <class 'tuple'>
x is (15, 2)
```

``` py 
x=47
y=x + 73j
#y=complex(x, 73)

print(f'x is {type(x)}')
print(f'x is {x}')
print(f'x is {type(y)}')
print(f'x is {y}')
```
```
x is <class 'int'>
x is 47
x is <class 'complex'>
x is (47+73j)
```
## Mathematical Functions

Mathematical functions

import [math](https://docs.python.org/3/library/math.html)


Mathematical functions for complex numbers

import [cmath](https://docs.python.org/3/library/cmath.html)

``` py 
print(min(0,1,2,3,-1,4,5,6))
print(min([0,1,2,3,-1,4,5,6]))
print(abs(-54))
print(round(0.6464,2))
print(sum([0,1,4,5,-3,9]))
```
```
-1
-1
54
0.65
16
```
## Statistics

For more advanced function use numpy

``` py 
# using Python statistics functions
import statistics

# simple statistics operations
sample_data1 = [1, 3, 5, 7]
sample_data2 = [2, 3, 5, 4, 3, 5, 3, 2, 5, 6, 4, 3]

# Use the mean function - calculates an average value
print(statistics.mean(sample_data1))

# Use the different median functions
print(statistics.median(sample_data1))
print(statistics.median_low(sample_data1))
print(statistics.median_high(sample_data1))

# The mode function indicates which data item occurs
# most frequently
print(statistics.mode(sample_data2))
```
```
4
4.0
3
5
3
```
