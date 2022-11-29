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
|Quick Sort	|O(n log(n))|	O(n log(n))|	O(n^2)|	 log(n)|No|Partitioning|
|Merge Sort	|O(n log(n))|	O(n log(n))|	O(n log(n))|n|Yes|Merging|

[NumPy](https://numpy.org/doc/stable/reference/generated/numpy.sort.html) provides implementations of three sorting algorithms, quicksort, mergesort, and heapsort.

## Complexity for Non-Comparison Sorting
The following table describes integer sorting algorithms and other sorting algorithms that are not comparison sorts. As such, they are not limited to Ω(n log n).

| Algorithm      |Best	|Average|	Worst| Memory | Stable |
| ----------- | ----------- |----------- | ----------- | ----------- | ----------- | 
|Bucket Sort	|O(n+k)|	O(n+k)|	O(n^2)|	O(n*k) |Yes |
|Radix Sort	|O(nk)|	O(nk)|	O(nk)|O(n+2^d)|Yes|	 
|Counting Sort	|O(n+k)|	O(n+k)|	O(n+k)|O(n+r)|Yes|

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