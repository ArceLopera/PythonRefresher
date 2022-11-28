There are two types of sorting algorithms:

* Comparison sorting algorithms 
* Non-comparison sorting algorithms

## Complexity for Comparison Sorting

| Algorithm      |Best	|Average|	Worst| Memory | Stable |Method|
| ----------- | ----------- |----------- | ----------- | ----------- | ----------- | ----------- |
|Selection Sort|	O(n^2)	|O(n^2)	|O(n^2)|	1 |No| Selection|
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

