An array is a collection of items stored at contiguous memory locations. The idea is to store multiple items of the same type together. This makes it easier to calculate the position of each element by simply adding an offset to a base value, i.e., the memory location of the first element of the array

``` py
# Python program to demonstrate
# Creation of Array

# importing "array" for array creations
import array as arr

# creating an array with integer type
a = arr.array('i', [1, 2, 3])

# printing original array
print ("The new created array is : ", end =" ")
for i in range (0, 3):
	print (a[i], end =" ")
print()

# creating an array with float type
b = arr.array('d', [2.5, 3.2, 3.3])

# printing original array
print ("The new created array is : ", end =" ")
for i in range (0, 3):
	print (b[i], end =" ")
	

```

```
The new created array is :  1 2 3 
The new created array is :  2.5 3.2 3.3 
```

Here are the differences between List and Array in Python :

| List      | Array|
| ----------- | ----------- |
| Can consist of elements belonging to different data types      | Only consists of elements belonging to the same data type
|No need to explicitly import a module for declaration   | Need to explicitly import a module for declaration        |
| Cannot directly handle arithmetic operations|	Can directly handle arithmetic operations|
|Can be nested to contain different type of elements|	Must contain either all nested elements of same size|
|Preferred for shorter sequence of data items	|Preferred for longer sequence of data items|
|Greater flexibility allows easy modification (addition, deletion) of data|	Less flexibility since addition, deletion has to be done element wise|
|The entire list can be printed without any explicit looping|	A loop has to be formed to print or access the components of array|
|Consume larger memory for easy addition of elements	|Comparatively more compact in memory size|