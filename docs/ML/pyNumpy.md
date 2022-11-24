Numpy (Numerical Python) is a python library that allows fast and easy mathematical operations to be performed on arrays. Numpy is a Python package for manipulating lists and tables of numerical data. We can use it to do a lot of statistical calculations. We call the list or table of data a numpy array.

We often will take the data from our pandas DataFrame and put it in numpy arrays. Pandas DataFrames are great because we have the column names and other text data that makes it human readable. A DataFrame, while easy for a human to read, is not the ideal format for doing calculations. The numpy arrays are generally less human readable, but are in a format that enables the necessary computation. Numpy is a Python module for doing calculations on tables of data. Pandas was actually built using Numpy as it’s foundation.

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

NumPy arrays are often called ndarrays, which stands for "N-dimensional array", because they can have multiple dimensions.

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

## Pandas Series to Numpy Array


We often start with our data in a Pandas DataFrame, but then want to convert it to a numpy array. The values attribute does this for us.

Let's convert the Fare column to a numpy array.

First we recall that we can use the single bracket notation to get a pandas Series of the Fare column as follows.

``` py
print(df['Fare'].values) #The values attribute of a Pandas Series give the data as a numpy array.
```
If we have a pandas DataFrame (instead of a Series as in the last part), we can still use the values attribute, but it returns a 2-dimensional numpy array. This is a 2-dimensional numpy array. You can tell because there’s two sets of brackets, and it expands both across the page and down. The values attribute of a Pandas DataFrame give the data as a 2d numpy array.
``` py
df[['Pclass', 'Fare', 'Age']].values 
```
```
array([[ 3.    ,  7.25  , 22.    ],
       [ 1.    , 71.2833, 38.    ],
       [ 3.    ,  7.925 , 26.    ],
       ...,
       [ 3.    , 23.45  ,  7.    ],
       [ 1.    , 30.    , 26.    ],
       [ 3.    ,  7.75  , 32.    ]])
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


## Matrix

The [NumPy](http://www.numpy.org/) library endows Python with a host of scientific computing capabilities. Chief among these is the Array object, which provides a multidimensional way to organize values of the same type. Numpy arrays allow slicing and indexing similar to lists. Most importantly, Numpy has a formidable number of mathematical operations that can be used to transform arrays and perform computations between arrays.  For those familiar with MATLab, these operations should be reminiscent of many matrix operations.

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

### Indexing and Slicing

Negative indexes count from the end of the array, so, [-3:] will result in the last 3 elements.

Numpy slicing syntax follows that of a python list: arr[start:stop:step]. When any of these are unspecified, they default to the values start=0, stop=size of dimension, step=1.

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

You can provide a condition as the index to select the elements that fulfill the given condition.

Conditions can be combined using the & (and) and | (or) operators.


``` py
x=np.arange(1,10)
print(x[x<4])
```
```
[1 2 3]
```

### Mask & Subsetting

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

## Arithmethic Functions

``` py
# Arithmetic Examples
C = A * 2 # multiplies every elemnt of A by two
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

## Assigning Values

We can use slicing for multiple elements. For example, to replace the first row by 10.

``` py
arr[0,:]=10
```
We can also combine slicing to change any subset of the array. For example, to reassign 0 to the left upper corner.

[More on slicing with numpy.](https://numpy.org/doc/stable/reference/arrays.indexing.html)
``` py
arr[:2,:2] = 0
```
## Assigning an Array to an Array

n addition, a 1darray or a 2darry can be assigned to a subset of another 2darray, as long as their shapes match.
``` py
arr[:,0]=[10,1]
```

## Combining Two Arrays

Oftentime we obtain data stored in different arrays and we need to combine them into one to keep it in one place. We can stack them horizontally (by column) to get a 2darray using 'hstack'. if we want to combine the arrays vertically (by row), we can use 'vstack'. To combine more than two arrays horizontally, simply add the additional arrays into the tuple.
``` py
arr3 = np.vstack((arr1, arr2))
```

## Concatenate

More generally, we can use the function numpy.concatenate. If we want to concatenate, link together, two arrays along rows, then pass 'axis = 1' to achieve the same result as using numpy.hstack; and pass 'axis = 0' if you want to combine arrays vertically.

You can use np.hstack to concatenate arrays ONLY if they have the same number of rows.

``` py
np.concatenate((arr1, arr2), axis=1)
```

## Broadcasting

Operations between the array and a single number. NumPy understands that the given operation should be performed with each element. This is called broadcasting.

``` py
# Broadcasting Examples
x = np.array([2, 4, 6]) # create a rank 1 array
A = np.array([[1, 3, 5], [2, 4, 6]]) # create a rank 2 array
B = np.array([[1, 2, 3], [4, 5, 6]])
H = A * x # "broadcasts" x for element-wise multiplication with the rows of A
print(H)
print('xxxxxx')
J = B + x # broadcasts for addition, again across rows
print(J)
```
```
[[ 2 12 30]
 [ 4 16 36]]
xxxxxx
[[ 3  6  9]
 [ 6  9 12]]
```

## np.min() and np.max()

min() and max() can be used to get the smallest and largest elements.

``` py
# max operation examples

X = np.array([[3, 9, 4], [10, 2, 7], [5, 11, 8]])
all_max = np.max(X) # gets the maximum value of matrix X
column_max = np.max(X, axis=0) # gets the maximum in each column -- returns a rank-1 array [10, 11, 8]
row_max = np.max(X, axis=1) # gets the maximum in each row -- returns a rank-1 array [9, 10, 11]

# In addition to max, can similarly do min. Numpy also has argmax to return indices of maximal values
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

## np.sum() & np.mean()

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

## Summing and Counting

Let’s say we want to know how many of our passengers are children. We still have the same array definition and can take our mask or boolean values from the previous part. Recall that True values are interpreted as 1 and False values are interpreted as 0. So we can just sum up the array and that’s equivalent to counting the number of true values.

``` py
print(mask.sum()) 
print((arr[:, 2] < 18).sum())
```
```
130
130
```
### np.arange() & np.reshape()

np.arange() allows you to create an array that contains a range of evenly spaced intervals (similar to a Python range).

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

### Other Functions

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
