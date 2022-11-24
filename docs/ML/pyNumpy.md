Numpy (Numerical Python) is a python library that allows fast and easy mathematical operations to be performed on arrays. Numpy is a Python package for manipulating lists and tables of numerical data. We can use it to do a lot of statistical calculations. We call the list or table of data a numpy array.

We often will take the data from our pandas DataFrame and put it in numpy arrays. Pandas DataFrames are great because we have the column names and other text data that makes it human readable. A DataFrame, while easy for a human to read, is not the ideal format for doing calculations. The numpy arrays are generally less human readable, but are in a format that enables the necessary computation. Numpy is a Python module for doing calculations on tables of data. Pandas was actually built using Numpy as it’s foundation.

## Functions and Methods Overview

+ [Array Creation](#array-creation) arange, array, copy, empty, empty_like, eye, fromfile, fromfunction, identity, linspace, logspace, mgrid, ogrid, ones, ones_like, r_, zeros, zeros_like

+ [Conversions](https://numpy.org/doc/stable/reference/arrays.ndarray.html#array-conversion) ndarray.astype, atleast_1d, atleast_2d, atleast_3d, mat

+ [Manipulations](#array-manipulation) array_split, column_stack, concatenate, diagonal, dsplit, dstack, hsplit, hstack, ndarray.item, newaxis, ravel, repeat, reshape, resize, squeeze, swapaxes, take, transpose, vsplit, vstack

+ [Questions](https://numpy.org/doc/stable/reference/routines.logic.html)
all, any, nonzero

+ [Ordering](https://numpy.org/doc/stable/reference/routines.sort.html) argmax, argmin, argsort, max, min, ptp, searchsorted, sort, where

+ **Operations**
choose, compress, cumprod, cumsum, inner, ndarray.fill, imag, prod, put, putmask, real, sum

+ [Basic Statistics](https://numpy.org/doc/stable/reference/routines.statistics.html) cov, mean, std, var

+ [Basic Linear Algebra](https://numpy.org/doc/stable/reference/routines.linalg.html) cross, dot, outer, linalg.svd, vdot


``` py
import numpy as np 
data = [15, 16, 18, 19, 22, 24, 29, 30, 34]
print("Mean: ", np.mean(data))
print("Median: ",np.median(data))
print("50th percentile : ",np.percentile(data,50))
print("75th percentile : ",np.percentile(data,75))
print("Standard Deviation: ",np.std(data))
print("Variance: ",np.var(data))
```
```
Mean:  23.0
Median:  22.0
50th percentile :  22.0
75th percentile :  29.0
Standard Deviation:  6.342099196813483
Variance:  40.22222222222222
```

## Numpy Array

In Python, lists are used to store data. NumPy provides an array structure for performing operations with data. NumPy arrays are faster and more compact than lists. NumPy arrays are homogeneous, meaning they can contain only a single data type, while lists can contain multiple different types of data. To check the data type, use numpy.ndarray.dtype

NumPy arrays are ndarrays, which stands for "N-dimensional array", because they can have multiple dimensions. However, we can use array as an alias.

## [Array Creation](https://numpy.org/doc/stable/reference/routines.array-creation.html)

### From shape or value

+ **np.empty(shape[, dtype, order, like])** returns a new array of given shape and type, without initializing entries.

+ **np.ones(shape[, dtype, order, like])** return a new array of given shape and type, filled with ones.

+ **np.zeros(shape[, dtype, order, like])** return a new array of given shape and type, filled with zeros.

+ **np.full(shape, fill_value[, dtype, order, like])** return a new array of given shape and type, filled with fill_value.

### From existing data

+ **np.array(object[, dtype, copy, order, subok, ...])** Create an array.

A NumPy array can be created using the np.array() function, providing it a list as the argument


``` py
import numpy as np

xo = np.array([1, 2, 3, 4])
print(xo[0]) 

x = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
 
print(x[1][2])
```
```
1
6
```

``` py
import numpy as np 

x = np.array([2, 4, 6]) # create a rank 1 array
A = np.array([[1, 3, 5], [2, 4, 6]]) # create a rank 2 array
B = np.array([[1, 2, 3], [4, 5, 6]])

print("Matrix A: \n")
print(A)

print("\nMatrix B: \n")
print(B)
```
```
Matrix A: 

[[1 3 5]
 [2 4 6]]

Matrix B: 

[[1 2 3]
 [4 5 6]]
```

+ **np.fromfunction(function, shape, *[, dtype, like])** construct an array by executing a function over each coordinate.

``` py
def f(x, y):
    return 10 * x + y

b = np.fromfunction(f, (5, 4), dtype=int)
print(b)
```
```
[[ 0,  1,  2,  3],
 [10, 11, 12, 13],
 [20, 21, 22, 23],
 [30, 31, 32, 33],
 [40, 41, 42, 43]]
```

### Numerical ranges

+ **np.arange([start,] stop[, step,][, dtype, like])** return evenly spaced values within a given interval.

+ **np.linspace(start, stop[, num, endpoint, ...])** return evenly spaced numbers over a specified interval.


### Pandas to Numpy Array


We often start with our data in a Pandas DataFrame, but then want to convert it to a numpy array. The values attribute does this for us. However, it is better to use .to_numpy() function.

``` py
# instead of values attribute
df['Fare'].values # For series
df[['Pclass', 'Fare', 'Age']].values # or Dataframes
# Use .to_numpy()
print(df['Fare'].to_numpy())
print(df[['Pclass', 'Fare', 'Age']].to_numpy())
```


## Array Attributes

Can be accessed using a dot.

+ **ndim** returns the number of dimensions of the array.

+ **size** returns the total number of elements of the array.

+ **shape** returns a tuple of integers that indicate the number of elements stored along each dimension of the array. Note that once an array is created in numpy, its size cannot be changed.

Size tells us how big the array is, shape tells us the dimension. 

**Numpy Shape Attribute**

We use the numpy shape attribute to determine the size of our numpy array. The size tells us how many rows and columns are in our data. This result means we have 887 rows and 3 columns. Use the shape attribute to find the number of rows and number columns for a Numpy array. You can also use the shape attribute on a pandas DataFrame (df.shape).

``` py
x = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]]) 
print(x.ndim) # 2
print(x.size) # 9
print(x.shape) # (3, 3)
```
```
2
9
(3, 3)
```

``` py
arr = df[['Pclass', 'Fare', 'Age']].values
print(arr.shape) #(887, 3)
```
```
(887, 3)
```
## Indexing and Slicing

Negative indexes count from the end of the array, so, [-3:] will result in the last 3 elements.

Numpy slicing syntax follows that of a python list: arr[start:stop:step]. When any of these are unspecified, they default to the values start=0, stop=size of dimension, step=1.

NumPy offers more indexing facilities than regular Python sequences. In addition to indexing by integers and slices, as we saw before, arrays can be indexed by [arrays of integers](https://numpy.org/doc/stable/user/quickstart.html#indexing-with-arrays-of-indices) and [arrays of booleans](https://numpy.org/doc/stable/user/quickstart.html#indexing-with-boolean-arrays).

``` py
# Indexing/Slicing examples
print(A[0, :]) # index the first "row" and all columns
print(A[1, 2]) # index the second row, third column entry
print(A[:, 1]) # index entire second column
```
```
[1 3 5]
6
[3 4]
```

When fewer indices are provided than the number of axes, the missing indices are considered complete slices.

``` py
b[-1]   # the last row. Equivalent to b[-1, :]
```
```
array([40, 41, 42, 43])
```

NumPy also allows you to write this using dots as b[i, ...].

The dots (...), called ellipsis, represent as many colons as needed to produce a complete indexing tuple. For example, if x is an array with 5 axes, then

+ x[1, 2, ...] is equivalent to x[1, 2, :, :, :],
+ x[..., 3] to x[:, :, :, :, 3] and
+ x[4, ..., 5, :] to x[4, :, :, 5, :].

``` py
c = np.array([[[  0,  1,  2],  # a 3D array (two stacked 2D arrays)
               [ 10, 12, 13]],
              [[100, 101, 102],
               [110, 112, 113]]])

#c.shape # (2, 2, 3)

c[1, ...]  # same as c[1, :, :] or c[1]

```
```
array([[100, 101, 102],
       [110, 112, 113]])
```
``` py
c[..., 2]  # same as c[:, :, 2]
```
```
array([[  2,  13],
       [102, 113]])
```

You can provide a condition as the index to select the elements that fulfill the given condition.

Conditions can be combined using the & (and) and | (or) operators.


``` py
x=np.arange(1,10)
print(x[x<4])
```
```
[1 2 3]
```

[More on slicing with numpy.](https://numpy.org/doc/stable/user/basics.indexing.html)

## Mask & Subsetting

A mask is a boolean array (True/False values) that tells us which values from the array we’re interested in. Masking is used to extract, modify, count, or otherwise manipulate values in an array based on some criterion. We can create a mask satisfying more than one criteria. We use & to separate the conditions and each condition is encapsulated with parentheses "()"

``` py
mask = arr[:, 2] < 18 #all children passengers
print(arr[mask])
# or arr[arr[:, 2] < 18] 
```

The condition can also be assigned to a variable, which will be an array of boolean values showing whether or not the values in the array fulfill the condition: y = (x>5) & (x%2==0)

``` py
print(x[(x>5)&(x%2==0)])
y = (x>5) & (x%2==0)
print(x[y])
```
```
[6 8]
[6 8]
```

We can use operations including "<", ">", ">=", "<=", and "==" . To find out how many rows satisfy the condition, use .sum() on the resultant 1d boolean array, e.g., (arr[:, 1] == 10).sum(). True is treated as 1 and False as 0 in the sum.

## Assigning Values

We can use slicing for multiple elements. For example, to replace the first row by 10.

``` py
arr[0,:]=10
```
We can also combine slicing to change any subset of the array. For example, to reassign 0 to the left upper corner.


``` py
arr[:2,:2] = 0
```
### Assigning an Array to an Array

In addition, a 1darray or a 2darry can be assigned to a subset of another 2darray, as long as their shapes match.
``` py
arr[:,0]=[10,1]
```


## Basic Operations

Arithmetic operators on arrays apply elementwise. A new array is created and filled with the result.

``` py
# Arithmetic Examples
C = A * 2 # multiplies every element of A by two - This is called Broadcasting
D = A * B # elementwise multiplication rather than matrix multiplication
E = np.transpose(B)
F = np.matmul(A, E) # performs matrix multiplication -- could also use np.dot()
G = np.matmul(A, x) # performs matrix-vector multiplication -- again could also use np.dot() 

print("\n Matrix E (the transpose of B): \n")
print(E)

print("\n Matrix F (result of matrix multiplication A x E): \n")
print(F)

print("\n Matrix G (result of matrix-vector multiplication A*x): \n")
print(G)
```
```
Matrix E (the transpose of B): 

[[1 4]
 [2 5]
 [3 6]]

 Matrix F (result of matrix multiplication A x E): 

[[22 49]
 [28 64]]

 Matrix G (result of matrix-vector multiplication A*x): 

[44 56]
```
Unlike in many matrix languages, the product operator * operates elementwise in NumPy arrays. The matrix product can be performed using the @ operator (in python >=3.5) or the dot function or method.

``` py
A = np.array([[1, 1],
              [0, 1]])
B = np.array([[2, 0],
              [3, 4]])

A * B     # elementwise product
```
```
array([[2, 0],
       [0, 4]])
```
``` py
A @ B     # matrix product, same as A.dot(B)
```
```
array([[5, 4],
       [3, 4]])
```

Some operations, such as += and *=, act in place to modify an existing array rather than create a new one. When operating with arrays of different types, the type of the resulting array corresponds to the more general or precise one (a behavior known as upcasting).

Many unary operations, such as computing the sum of all the elements in the array, are implemented as methods of the ndarray class. By default, these operations apply to the array as though it were a list of numbers, regardless of its shape. However, by specifying the axis parameter you can apply an operation along the specified axis of an array.

### np.min() and np.max()

min() and max() can be used to get the smallest and largest elements.

``` py
# max operation examples

X = np.array([[3, 9, 4], [10, 2, 7], [5, 11, 8]])
all_max = np.max(X) # gets the maximum value of matrix X
column_max = np.max(X, axis=0) # gets the maximum in each column -- returns a rank-1 array [10, 11, 8]
row_max = np.max(X, axis=1) # gets the maximum in each row -- returns a rank-1 array [9, 10, 11]

# Numpy also has argmax to return indices of maximal values
column_argmax = np.argmax(X, axis=0) # note that the "index" here is actually the row the maximum occurs for each column

print("Matrix X: \n")
print(X)
print("\n Maximum value in X: \n")
print(all_max)
print("\n Column-wise max of X: \n")
print(column_max)
print("\n Indices of column max: \n")
print(column_argmax)
print("\n Row-wise max of X: \n")
print(row_max)

```
```
Matrix X: 

[[ 3  9  4]
 [10  2  7]
 [ 5 11  8]]

 Maximum value in X: 

11

 Column-wise max of X: 

[10 11  8]

 Indices of column max: 

[1 2 2]

 Row-wise max of X: 

[ 9 10 11]
```

### np.sum() & np.mean()

These work similarly to the max operations -- use the axis argument to denote if summing over rows or columns

``` py
# Sum operation examples

total_sum = np.sum(X)
column_sum = np.sum(X, axis=0)
row_sum = np.sum(X, axis=1)

print("Matrix X: \n")
print(X)
print("\n Sum over all elements of X: \n")
print(total_sum)
print("\n Column-wise sum of X: \n")
print(column_sum)
print("\n Row-wise sum of X: \n")
print(row_sum)
```
```
Matrix X: 

[[ 3  9  4]
 [10  2  7]
 [ 5 11  8]]

 Sum over all elements of X: 

59

 Column-wise sum of X: 

[18 22 19]

 Row-wise sum of X: 

[16 19 24]
```

## Universal Functions

NumPy provides familiar mathematical functions such as sin, cos, and exp. In NumPy, these are called “universal functions” (ufunc). Within NumPy, these functions operate elementwise on an array, producing an array as output.

### Methods

+ [**ufunc.reduce(array[, axis, dtype, out, ...])**](https://numpy.org/doc/stable/reference/generated/numpy.ufunc.reduce.html) Reduces array's dimension by one, by applying ufunc along one axis.

``` py
np.multiply.reduce([2,3,5])  #30
```

+ [**ufunc.accumulate(array[, axis, dtype, out])**](https://numpy.org/doc/stable/reference/generated/numpy.ufunc.accumulate.html) Accumulate the result of applying the operator to all elements.

``` py
np.add.accumulate([2, 3, 5])  # array([ 2,  5, 10])
```

### Operations

+ [**Math:**](https://numpy.org/doc/stable/reference/ufuncs.html#math-operations) Add, subtract, multiply, divide, matmul, power, mod, absolute, exp, log, sqrt, cbrt, gcd, lcm, etc...
+ [**Trigonometric functions:**](https://numpy.org/doc/stable/reference/ufuncs.html#trigonometric-functions) sin, cos, tan, arcsin, sinh, deg2rad, etc...
+ [**Bit-twiddling functions**](https://numpy.org/doc/stable/reference/ufuncs.html#bit-twiddling-functions) invert, left_shift, bitwise_and, etc..
+ [**Comparison functions**](https://numpy.org/doc/stable/reference/ufuncs.html#comparison-functions) greater, greater_equal, less, not_equal, equal, logical_and, maximum, etc...
+ [**Floating functions**](https://numpy.org/doc/stable/reference/ufuncs.html#floating-functions) isfinite, isinf, isnan, floor, ceil, trunc, etc...


## [Array Manipulation](https://numpy.org/doc/stable/reference/routines.array-manipulation.html)

### Changing Array Shape

+ **np.reshape()** Gives a new shape to an array without changing its data.

+ **np.ravel(a[, order])** Return a contiguous flattened array.

+ **np.flatten([order])** Return a copy of the array collapsed into one dimension.

When you use the reshape method, the array you want to produce needs to have the same number of elements as the original array. Reshape can also do the opposite: take a 2-dimensional array and make a 1-dimensional array from it. The same result can be achieved using the flatten() function.

Numpy can calculate the shape (dimension) for us if we indicate the unknown dimension as -1. For example, given a 2darray arr of shape (3,4), arr.reshape(-1) would output a 1darray of shape (12,), while arr.reshape((-1,2)) would generate a 2darray of shape (6,2).

``` py
# Matrix reshaping

X = np.arange(16) # makes a rank-1 array of integers from 0 to 15
X_square = np.reshape(X, (4, 4)) # reshape X into a 4 x 4 matrix
X_rank_3 = np.reshape(X, (2, 2, 4)) # reshape X to be 2 x 2 x 4 --a rank-3 array
                                    # consider as two rank-2 arrays with 2 rows and 4 columns
print("Rank-1 array X: \n")
print(X)
print("\n Reshaped into a square matrix: \n")
print(X_square)
print("\n Reshaped into a rank-3 array with dimensions 2 x 2 x 4: \n")
print(X_rank_3)
print("\n Reshaped into Rank 1")
print(X_square.reshape(16))
print("Using Flatten")
print(X_rank_3.flatten())
```
```
Rank-1 array X: 

[ 0  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15]

 Reshaped into a square matrix: 

[[ 0  1  2  3]
 [ 4  5  6  7]
 [ 8  9 10 11]
 [12 13 14 15]]

 Reshaped into a rank-3 array with dimensions 2 x 2 x 4: 

[[[ 0  1  2  3]
  [ 4  5  6  7]]

 [[ 8  9 10 11]
  [12 13 14 15]]]

 Reshaped into Rank 1
[ 0  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15]
Using Flatten
[ 0  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15]
```

**Automatic Reshaping**
To change the dimensions of an array, you can omit one of the sizes which will then be deduced automatically.

``` py
a = np.arange(30)
b = a.reshape((2, -1, 3))  # -1 means "whatever is needed"
b.shape  #(2, 5, 3)
b
```
```
array([[[ 0,  1,  2],
        [ 3,  4,  5],
        [ 6,  7,  8],
        [ 9, 10, 11],
        [12, 13, 14]],

       [[15, 16, 17],
        [18, 19, 20],
        [21, 22, 23],
        [24, 25, 26],
        [27, 28, 29]]])
```

Iterating over multidimensional arrays is done with respect to the first axis:
``` py
for row in b:
    print(row)
```
However, if one wants to perform an operation on each element in the array, one can use the flat attribute which is an iterator over all the elements of the array.

``` py
for element in b.flat:
    print(element)
```

### Transpose

+ **np.transpose(a[, axes])** Reverse or permute the axes of an array; returns the modified array.

### Combining  Arrays

Oftentime we obtain data stored in different arrays and we need to combine them into one to keep it in one place. We can stack them horizontally (by column) to get a 2darray using 'hstack'. if we want to combine the arrays vertically (by row), we can use 'vstack'. To combine more than two arrays horizontally, simply add the additional arrays into the tuple.
``` py
arr3 = np.vstack((arr1, arr2))
```

+ **np.vstack(tup)** Stack arrays in sequence vertically (row wise).
+ **np.hstack(tup)** Stack arrays in sequence horizontally (column wise).
+ **np.concatenate([axis, out, dtype, casting])** Join a sequence of arrays along an existing axis.

More generally, we can use the function numpy.concatenate. If we want to concatenate, link together, two arrays along rows, then pass 'axis = 1' to achieve the same result as using numpy.hstack; and pass 'axis = 0' if you want to combine arrays vertically.

You can use np.hstack to concatenate arrays ONLY if they have the same number of rows.

``` py
np.concatenate((arr1, arr2), axis=1)
```

### Adding and removing elements

+ **np.delete(arr, obj[, axis])** Return a new array with sub-arrays along an axis deleted.
+ **np.insert(arr, obj, values[, axis])** Insert values along the given axis before the given indices.
+ **np.append(arr, values[, axis])** Append values to the end of an array.

We can add, remove and sort an array using the np.append(), np.delete() and np.sort() functions.

``` py
x= np.array([2,1,3])
#add an element
x=np.append(x,4)
#delete an element
x=np.delete(x,0)
#sort array
x=np.sort(x)

x = np.arange(2, 8, 2)
print(x)
x = np.append(x, x.size)
x = np.sort(x)
print(x[1])
```
```
[2 4 6]
3
```

## Copies and Views

Simple assignments make no copy of objects or their data.

``` py
a = np.array([[ 0,  1,  2,  3],
              [ 4,  5,  6,  7],
              [ 8,  9, 10, 11]])

b = a            # no new object is created
b is a           # a and b are two names for the same ndarray object
```
```
True
```

### View or Shallow Copy
Different array objects can share the same data. The view method creates a new array object that looks at the same data.

``` py
c = a.view()
c is a #False
c.base is a       # True, c is a view of the data owned by a
c.flags.owndata   #False

c = c.reshape((2, 6))  # a's shape doesn't change
c[0, 4] = 1234         # a's data changes
```
Slicing an array returns a view of it.
``` py
s = a[:, 1:3]
s[:] = 10  
# s[:] is a view of s. 
# Note the difference between s = 10 and s[:] = 10
```

### Deep Copy
The copy method makes a complete copy of the array and its data.

``` py
d = a.copy()  # a new array object with new data is created
d is a        # False
d.base is a  # False, d doesn't share anything with a
```