There are two types of sorting algorithms:

* Comparison sorting algorithms 
* Non-comparison sorting algorithms

## Complexity for Comparison Sorting

| Algorithm      |Best	|Average|	Worst| Memory | Stable |Method|
| ----------- | ----------- |----------- | ----------- | ----------- | ----------- | ----------- |
|[Selection Sort](#selection-sort)|	O(n^2)	|O(n^2)	|O(n^2)|	1 |No| Selection|
|[Bubble Sort](#bubble-sort)	|O(n)	|O(n^2)|	O(n^2)|	 1|Yes|Exchanging|
|Insertion Sort|	O(n)|	O(n^2)|	O(n^2)|1|Yes|Insertion|	 
|Heap Sort	|O(n log(n))|	O(n log(n))	|O(n log(n))|		1 |No| Selection| 
|[Quick Sort](#quicksort-divide-and-conquer)	|O(n log(n))|	O(n log(n))|	O(n^2)|	 log(n)|No|Partitioning|
|[Merge Sort](#merge-sort)	|O(n log(n))|	O(n log(n))|	O(n log(n))|n|Yes|Merging|

[NumPy](https://numpy.org/doc/stable/reference/generated/numpy.sort.html) provides implementations of three sorting algorithms, quicksort, mergesort, and heapsort.

## Complexity for Non-Comparison Sorting
The following table describes integer sorting algorithms and other sorting algorithms that are not comparison sorts. As such, they are not limited to Ω(n log n).

| Algorithm      |Best	|Average|	Worst| Memory | Stable |
| ----------- | ----------- |----------- | ----------- | ----------- | ----------- | 
|Bucket Sort	|O(n+k)|	O(n+k)|	O(n^2)|	O(n*k) |Yes |
|[Radix Sort](#radix-sort)	|O(nk)|	O(nk)|	O(nk)|O(n+2^d)|Yes|	 
|[Counting Sort](#counting-sort)	|O(n+k)|	O(n+k)|	O(n+k)|O(n+r)|Yes|

## Bubble Sort

Bubble Sort is the simplest sorting algorithm that works by repeatedly swapping the adjacent elements if they are in wrong order. Two values are compared to each other incrementally, the largest value is shifted until it is at the top.

+ **Complexity:** O(n^2)
+ **Worst and Average Case Time Complexity:** O(n*n). Worst case occurs when array is reverse sorted.
+ **Best Case Time Complexity:** O(n). Best case occurs when array is already sorted.
+ **Auxiliary Space:** O(1)
+ **Boundary Cases:** Bubble sort takes minimum time (Order of n) when elements are already sorted.
+ **Sorting In Place:** Yes
+ **Stable:** Yes

``` py
# Python program for implementation of Bubble Sort

def bubbleSort(arr):
	n = len(arr)

	# Traverse through all array elements
	for i in range(n):

		# Last i elements are already in place
		for j in range(0, n-i-1):

			# traverse the array from 0 to n-i-1
			# Swap if the element found is greater
			# than the next element
			if arr[j] > arr[j+1] :
				arr[j], arr[j+1] = arr[j+1], arr[j]

# Driver code to test above
arr = [64, 34, 25, 12, 22, 11, 90]

bubbleSort(arr)

print ("Sorted array is:")
for i in range(len(arr)):
	print ("%d" %arr[i]),
```
```
Sorted array is:
11
12
22
25
34
64
90
```

## Selection Sort

When you want to store multiple elements, use an array or a list.

• With an array, all your elements are stored right next to each other.

• With a list, elements are strewn all over, and one element stores the address of the next one.

• Arrays allow fast reads.

• Linked lists allow fast inserts and deletes.

• All elements in the array should be the same type (all ints,
all doubles, and so on).

The selection sort algorithm sorts an array by repeatedly finding the minimum element (considering ascending order) from unsorted part and putting it at the beginning. The algorithm maintains two subarrays in a given array.
1) The subarray which is already sorted. 
2) Remaining subarray which is unsorted.
In every iteration of selection sort, the minimum element (considering ascending order) from the unsorted subarray is picked and moved to the sorted subarray. 

+ **Time Complexity:** O(n2) as there are two nested loops.
+ **Auxiliary Space:** O(1) 
The good thing about selection sort is it never makes more than O(n) swaps and can be useful when memory write is a costly operation. 
+ **Stability :** The default implementation is not stable. However it can be made stable. Please see [stable selection sort](https://www.geeksforgeeks.org/stable-selection-sort/) for details.
+ **In Place :** Yes, it does not require extra space.

A sorting algorithm is said to be stable if two objects with equal or same keys appear in the same order in sorted output as they appear in the input array to be sorted.

``` py
def findSmallest(arr):
  smallest = arr[0] #Stores the smallest value
  smallest_index = 0 #Stores the index of the smallest value
  for i in range(1, len(arr)):
    if arr[i] < smallest:
      smallest = arr[i]
      smallest_index = i
  return smallest_index

def selectionSort(arr): #Sorts an array
  newArr = []
  for i in range(len(arr)):
    smallest = findSmallest(arr)
    newArr.append(arr.pop(smallest))
  return newArr

print(selectionSort([5, 3, 6, 2, 10]))
```
```
[2, 3, 5, 6, 10]
```

``` py
# Python program for implementation of Selection
# Sort
import sys
A = [64, 25, 12, 22, 11]

# Traverse through all array elements
for i in range(len(A)):
	
	# Find the minimum element in remaining
	# unsorted array
	min_idx = i
	for j in range(i+1, len(A)):
		if A[min_idx] > A[j]:
			min_idx = j
			
	# Swap the found minimum element with
	# the first element	
	A[i], A[min_idx] = A[min_idx], A[i]

# Driver code to test above
print ("Sorted array")
for i in range(len(A)):
	print("%d" %A[i]),
```
```
Sorted array
11
12
22
25
64
```

## QuickSort (Divide and Conquer)

Quicksort is a sorting algorithm. It’s much faster than selection sort and is frequently used in real life. For example, the C standard library has a function called qsort, which is its implementation of quicksort.

A quick sort sets a pit point to partition a data set. High and low index values are then used to rearrange data values that are on the "wrong" side of the pivot point.

Like Merge Sort, QuickSort is a Divide and Conquer algorithm. It picks an element as pivot and partitions the given array around the picked pivot. There are many different versions of quickSort that pick pivot in different ways.

1. Always pick first element as pivot.
2. Always pick last element as pivot (implemented below)
3. Pick a random element as pivot.
4. Pick median as pivot.

The key process in quickSort is partition(). Target of partitions is, given an array and an element x of array as pivot, put x at its correct position in sorted array and put all smaller elements (smaller than x) before x, and put all greater elements (greater than x) after x. All this should be done in linear time.

![quick](./Images/quicksort.png)

``` py
# Python3 implementation of QuickSort

# This Function handles sorting part of quick sort
# start and end points to first and last element of
# an array respectively
def partition(start, end, array):
	
	# Initializing pivot's index to start
	pivot_index = start
	pivot = array[pivot_index]
	
	# This loop runs till start pointer crosses
	# end pointer, and when it does we swap the
	# pivot with element on end pointer
	while start < end:
		
		# Increment the start pointer till it finds an
		# element greater than pivot
		while start < len(array) and array[start] <= pivot:
			start += 1
			
		# Decrement the end pointer till it finds an
		# element less than pivot
		while array[end] > pivot:
			end -= 1
		
		# If start and end have not crossed each other,
		# swap the numbers on start and end
		if(start < end):
			array[start], array[end] = array[end], array[start]
	
	# Swap pivot element with element on end pointer.
	# This puts pivot on its correct sorted place.
	array[end], array[pivot_index] = array[pivot_index], array[end]
	
	# Returning end pointer to divide the array into 2
	return end
	
# The main function that implements QuickSort
def quick_sort(start, end, array):
	
	if (start < end):
		
		# p is partitioning index, array[p]
		# is at right place
		p = partition(start, end, array)
		
		# Sort elements before partition
		# and after partition
		quick_sort(start, p - 1, array)
		quick_sort(p + 1, end, array)
		
# Driver code
array = [ 10, 7, 8, 9, 1, 5 ]
quick_sort(0, len(array) - 1, array)

print(f'Sorted array: {array}')
```
```
Sorted array: [1, 5, 7, 8, 9, 10]
```

``` py
def quicksort(array):
  if len(array) < 2:
    return array #Base case: arrays with 0 or 1 element are already “sorted.”
  else:
    pivot = array[0] #Recursive case
    less = [i for i in array[1:] if i <= pivot] #Sub-array of all the elements less than the pivot
    greater = [i for i in array[1:] if i > pivot] #Sub-array of all the elements greater than the pivot
    return quicksort(less) + [pivot] + quicksort(greater)

print(quicksort([10, 5, 2, 3]))
```
```
[2, 3, 5, 10]
```
``` py
def quicksort(arr):
    if len(arr) <= 1:
        return arr
    pivot = arr[len(arr) // 2]
    left = [x for x in arr if x < pivot]
    middle = [x for x in arr if x == pivot]
    right = [x for x in arr if x > pivot]
    return quicksort(left) + middle + quicksort(right)


def quicksort_verbose(arr):
    print(f"Calling quicksort on {arr}")
    if len(arr) <= 1:
        print(f"returning {arr}")
        return arr
    pivot = arr[len(arr) // 2]
    left = [x for x in arr if x < pivot]
    print(f"left: {left}; ", end="")
    middle = [x for x in arr if x == pivot]
    print(f"middle: {middle}; ", end="")
    right = [x for x in arr if x > pivot]
    print(f"right: {right}")
    to_return = quicksort_verbose(left) + middle + quicksort_verbose(right)
    print(f"returning: {to_return}")
    return to_return


data = [3, 1, 4, 2]
# print(quicksort(data))
# print(quicksort_verbose(data))

# What about data with duplicates?
data = [1, 6, 5, 5, 2, 6, 1]
print(quicksort(data))
```
## Merge Sort

A merge sort uses recursion. It breaks down the data into smaller manageable sets. As it sorts the smaller sets, it gradually rebuilds and works its way up to the original full data set. Like QuickSort, Merge Sort is a Divide and Conquer algorithm. It divides the input array into two halves, calls itself for the two halves, and then merges the two sorted halves. The merge() function is used for merging two halves. The merge(arr, l, m, r) is a key process that assumes that arr[l..m] and arr[m+1..r] are sorted and merges the two sorted sub-arrays into one.

![merge](./Images/mergesort.png)

+ **Time Complexity:** Sorting arrays on different machines. Merge Sort is a recursive algorithm and time complexity can be expressed as following recurrence relation. 
T(n) = 2T(n/2) + θ(n)

The above recurrence can be solved either using the Recurrence Tree method or the Master method. It falls in case II of Master Method and the solution of the recurrence is θ(nLogn). Time complexity of Merge Sort is  θ(nLogn) in all 3 cases (worst, average and best) as merge sort always divides the array into two halves and takes linear time to merge two halves.

+ **Auxiliary Space:** O(n)
+ **Algorithmic Paradigm:** Divide and Conquer
+ **Sorting In Place:** No in a typical implementation
+ **Stable:** Yes

### Applications of Merge Sort 

+ Merge Sort is useful for sorting linked lists in O(nLogn) time.
+ Inversion Count Problem
+ Used in External Sorting

### Drawbacks of Merge Sort

+ Slower comparative to the other sort algorithms for smaller tasks.
+ Merge sort algorithm requires an additional memory space of 0(n) for the temporary array.
+ It goes through the whole process even if the array is sorted.

``` py
# Python program for implementation of MergeSort
def mergeSort(arr):
	if len(arr) > 1:

		# Finding the mid of the array
		mid = len(arr)//2

		# Dividing the array elements
		L = arr[:mid]

		# into 2 halves
		R = arr[mid:]

		# Sorting the first half
		mergeSort(L)

		# Sorting the second half
		mergeSort(R)

		i = j = k = 0

		# Copy data to temp arrays L[] and R[]
		while i < len(L) and j < len(R):
			if L[i] < R[j]:
				arr[k] = L[i]
				i += 1
			else:
				arr[k] = R[j]
				j += 1
			k += 1

		# Checking if any element was left
		while i < len(L):
			arr[k] = L[i]
			i += 1
			k += 1

		while j < len(R):
			arr[k] = R[j]
			j += 1
			k += 1

# Code to print the list


def printList(arr):
	for i in range(len(arr)):
		print(arr[i], end=" ")
	print()


# Driver Code
if __name__ == '__main__':
	arr = [12, 11, 13, 5, 6, 7]
	print("Given array is", end="\n")
	printList(arr)
	mergeSort(arr)
	print("Sorted array is: ", end="\n")
	printList(arr)
```
```
Given array is
12 11 13 5 6 7 
Sorted array is: 
5 6 7 11 12 13 
```

## Counting Sort

Counting sort is a sorting technique based on keys between a specific range. It works by counting the number of objects having distinct key values (kind of hashing). Then doing some arithmetic to calculate the position of each object in the output sequence.

**Time Complexity:** O(n+k) where n is the number of elements in input array and k is the range of input. 

**Auxiliary Space:** O(n+k)

For simplicity, consider the data in the range 0 to 9. Input data: 1, 4, 1, 2, 7, 5, 2

1) Take a count array to store the count of each unique object.

Index: 0 1 2 3 4 5 6 7 8 9

Count: 0 2 2 0 1 1 0 1 0 0

2) Modify the count array such that each element at each index stores the sum of previous counts.

Index: 0 1 2 3 4 5 6 7 8 9

Count: 0 2 4 4 5 6 6 7 7 7

The modified count array indicates the position of each object in the output sequence.

3) Rotate the array clockwise for one time.

Index: 0 1 2 3 4 5 6 7 8 9

Count: 0 0 2 4 4 5 6 6 7 7

4) Output each object from the input sequence followed by increasing its count by 1.

Process the input data: 1, 4, 1, 2, 7, 5, 2. Position of 1 is 0.

Put data 1 at index 0 in output. Increase count by 1 to place next data 1 at an index 1 greater than this index.

**Points to be noted**: 

1. Counting sort is efficient if the range of input data is not significantly greater than the number of objects to be sorted. Consider the situation where the input sequence is between range 1 to 10K and the data is 10, 5, 10K, 5K. 
2. It is not a comparison based sorting. It running time complexity is O(n) with space proportional to the range of data. 
3. It is often used as a sub-routine to another sorting algorithm like radix sort. 
4. Counting sort uses a partial hashing to count the occurrence of the data object in O(1). 
5. Counting sort can be extended to work for negative inputs also.

``` py
# Python program for counting sort

# The main function that sort the given string arr[] in
# alphabetical order
def countSort(arr):

	# The output character array that will have sorted arr
	output = [0 for i in range(len(arr))]

	# Create a count array to store count of individual
	# characters and initialize count array as 0
	count = [0 for i in range(256)]

	# For storing the resulting answer since the
	# string is immutable
	ans = ["" for _ in arr]

	# Store count of each character
	for i in arr:
		count[ord(i)] += 1

	# Change count[i] so that count[i] now contains actual
	# position of this character in output array
	for i in range(256):
		count[i] += count[i-1]

	# Build the output character array
	for i in range(len(arr)):
		output[count[ord(arr[i])]-1] = arr[i]
		count[ord(arr[i])] -= 1

	# Copy the output array to arr, so that arr now
	# contains sorted characters
	for i in range(len(arr)):
		ans[i] = output[i]
	return ans

# Driver program to test above function
arr = "meatforall"
ans = countSort(arr)
print("Sorted character array is % s" %("".join(ans)))
```
```
Sorted character array is aaefllmort
```

## Radix Sort
The lower bound for Comparison based sorting algorithm (Merge Sort, Heap Sort, Quick-Sort .. etc) is Ω(nLogn), i.e., they cannot do better than nLogn.

Counting sort is a linear time sorting algorithm that sort in O(n+k) time when elements are in the range from 1 to k.

What if the elements are in the range from 1 to n2? We can’t use counting sort because counting sort will take O(n2) which is worse than comparison-based sorting algorithms. Can we sort such an array in linear time?

Radix Sort is the answer. The idea of Radix Sort is to do digit by digit sort starting from least significant digit to most significant digit. Radix sort uses counting sort as a subroutine to sort.

Original, unsorted list:

170, 45, 75, 90, 802, 24, 2, 66

Sorting by least significant digit (1s place) gives:

[*Notice that we keep 802 before 2, because 802 occurred before 2 in the original list, and similarly for pairs 170 & 90 and 45 & 75.]

170, 90, 802, 2, 24, 45, 75, 66

Sorting by next digit (10s place) gives:

[*Notice that 802 again comes before 2 as 802 comes before 2 in the previous list.]

802, 2, 24, 45, 66, 170, 75, 90

Sorting by the most significant digit (100s place) gives:

2, 24, 45, 66, 75, 90, 170, 802

``` py
# Python program for implementation of Radix Sort
# A function to do counting sort of arr[] according to
# the digit represented by exp.

def countingSort(arr, exp1):

	n = len(arr)

	# The output array elements that will have sorted arr
	output = [0] * (n)

	# initialize count array as 0
	count = [0] * (10)

	# Store count of occurrences in count[]
	for i in range(0, n):
		index = arr[i] // exp1
		count[index % 10] += 1

	# Change count[i] so that count[i] now contains actual
	# position of this digit in output array
	for i in range(1, 10):
		count[i] += count[i - 1]

	# Build the output array
	i = n - 1
	while i >= 0:
		index = arr[i] // exp1
		output[count[index % 10] - 1] = arr[i]
		count[index % 10] -= 1
		i -= 1

	# Copying the output array to arr[],
	# so that arr now contains sorted numbers
	i = 0
	for i in range(0, len(arr)):
		arr[i] = output[i]

# Method to do Radix Sort
def radixSort(arr):

	# Find the maximum number to know number of digits
	max1 = max(arr)

	# Do counting sort for every digit. Note that instead
	# of passing digit number, exp is passed. exp is 10^i
	# where i is current digit number
	exp = 1
	while max1 / exp > 1:
		countingSort(arr, exp)
		exp *= 10


# Driver code
arr = [170, 45, 75, 90, 802, 24, 2, 66]

# Function Call
radixSort(arr)

for i in range(len(arr)):
	print(arr[i],end=" ")
```
```
2 24 45 66 75 90 170 802 
```