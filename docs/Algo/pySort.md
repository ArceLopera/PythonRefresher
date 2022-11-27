There are two types of sorting algorithms:

* Comparison sorting algorithms 
* Non-comparison sorting algorithms

## Complexity for Comparison Sorting

| Algorithm      |Best	|Average|	Worst| Memory | Stable |Method|
| ----------- | ----------- |----------- | ----------- | ----------- | ----------- | ----------- |
|Selection Sort|	O(n^2)	|O(n^2)	|O(n^2)|	1 |No| Selection|
|Bubble Sort	|O(n)	|O(n^2)|	O(n^2)|	 1|Yes|Exchanging|
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