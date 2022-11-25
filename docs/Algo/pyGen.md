Useful Algorithms

+ [Divide and Conquer](#divide-and-conquer)
+ [Transform and Conquer](#transform-and-conquer)
+ Dynamic Programming
+ Sorting Algorithms
+ Searching Algorithms
+ Array Algorithms
+ Graph Algorithms
+ Other Algorithms
+ Greedy Algorithms
+ Strategies
+ Patterns

## Divide and Conquer

A typical Divide and Conquer algorithm solves a problem using following three steps:

1. Divide: This involves dividing the problem into smaller sub-problems.
2. Conquer: Solve sub-problems by calling recursively until solved.
3. Combine: Combine the sub-problems to get the final solution of the whole problem.

Divide and Conquer deals with non-overlapping subproblems. When subproblems overlap use Dynamic Programming.

Examples:

1. **Quicksort** is a sorting algorithm. The algorithm picks a pivot element and rearranges the array elements so that all elements smaller than the picked pivot element move to the left side of the pivot, and all greater elements move to the right side. Finally, the algorithm recursively sorts the subarrays on the left and right of the pivot element.
2. **Merge Sort** is also a sorting algorithm. The algorithm divides the array into two halves, recursively sorts them, and finally merges the two sorted halves.
3. **Closest Pair of Points** The problem is to find the closest pair of points in a set of points in the x-y plane. The problem can be solved in O(n^2) time by calculating the distances of every pair of points and comparing the distances to find the minimum. The Divide and Conquer algorithm solves the problem in O(N log N) time.
4. **Strassen’s Algorithm** is an efficient algorithm to multiply two matrices. A simple method to multiply two matrices needs 3 nested loops and is O(n^3). Strassen’s algorithm multiplies two matrices in O(n^2.8974) time.
Cooley–Tukey Fast Fourier Transform (FFT) algorithm is the most common algorithm for FFT. It is a divide and conquer algorithm which works in O(N log N) time.
5. **Karatsuba algorithm for fast multiplication** does the multiplication of two n-digit numbers in at most 3n^{log_{2}^{3}}\approx 3n^{1.585} single-digit multiplications in general (and exactly n^{\log_23}        when n is a power of 2). It is, therefore, faster than the classical algorithm, which requires n2 single-digit products. If n = 210 = 1024, in particular, the exact counts are 310 = 59, 049 and (210)2 = 1, 048, 576, respectively.

## [Transform and Conquer](http://www.csl.mtu.edu/cs4321/www/Lectures/Lecture%2012%20-%20Transform%20and%20Conquer-Presort%20and%20Heap.htm)

Transform and Conquer is a technique whose main idea is to transfer the problem into some easier or similar versions using some procedure and then solve that easier or simpler versions and combine those versions to get the solution of the actual one. The design consists of two parts: 

The first stage involves the transformation/breakdown of the complex problem into other problems that is simpler than the original one.
The second stage involves solving the simpler problems and after the problem is solved the solutions are combined and converted back to get the solution of the original problem.

There are three ways to do that:

1. **Instance simplification:** a technique of simplifying the problem to more convenient or simpler instances. e.g. [Presorting](#presorting-instance-simplification)
2. **Representation change:** the data structure is transformed to represent the problem more efficiently.
3. **Problem reduction:** the problem can be transformed to an easier problem to solve

### Presorting: Instance simplification
"Presorting" is a common example of "instance simplification." Presorting is sorting ahead of time, to make repetitive solutions faster. For example if you wish to find many kth statistics in an array then it might make sense to sort the array ahead of time for so that the cost for determining each statistics is constant time.

Presorting is a form of preconditioning. Preconditioning is manipulating the data to make the algorithm faster.

Another example is the problem to determine the uniqueness of array elements. The brute force algorithm would compare each array element with the rest of the array. The cost would be Θ(n2). If we presort the array then the algorithm only needs to compare adjacent elements for uniqueness. The cost for determining uniqueness (without the sorting cost) is Θ(n).

The total cost is

T(n) = Tsort(n) + Tscan(n) ε Θ(n log n) + Θ(n) = Θ(n log n)

Another example is computing the mode of an array. The mode is the most frequent array element. The brute force cost would be quadratic. If the array is sorted then we only need to count runs of value. 

``` java

Algorithm PresortMode(A[0...n-1])

// assumes that A is sorted
i ← 0
modefrequency ← 0
while i < n do
runlength ← 1
runvalue ← A[i]

while i+runlength < n and A[i+runlength] = runvalue do
runlength++

if runlength > modefequency then
modefrequency ← runlength
modevalue ← runvalue
return modevalue
```

The algorithm runs in linear time, so the cost is sorting is presorting the array.

Geometrical problems frequently sort the collection of points before solving the problem. Also diagraphs algorithms frequently do a topological sort before running.

``` py
def mode_presort(arr):
    arr.sort()  # Array must be sorted before we apply the algorithm.
    i = 0
    mode_frequency = 0
    while i < len(arr):
        run_length = 1
        run_value = arr[i]
        while i + run_length < len(arr) and arr[i + run_length] == run_value:
            run_length += 1
        if run_length > mode_frequency:
            mode_frequency = run_length
            mode_value = [run_value]  # Make it a list
        elif run_length == mode_frequency:  # Also deal with this case
            # Add alternative to existing list of modes
            mode_value.append(run_value)
        i += run_length
    return mode_value


arr = [1, 1, 1, 2, 2]
print(mode_presort(arr))
arr = [1, 1, 2, 2]
print(mode_presort(arr))
arr = [3, 7, 5, 13, 20, 23, 39, 23, 40, 23, 14, 12, 56, 23, 29]
print(mode_presort(arr))
```
```
[1]
[1, 2]
[23]
```

``` py
## Number placement puzzle

import random

PUZZLE_SIZE = 10

# Create random puzzle
# random.sample ensures no duplicates
puzzle_nums = random.sample(range(100), PUZZLE_SIZE)
puzzle_symbols = []

# Randomly assign inequalities
for i in range(PUZZLE_SIZE - 1):
    puzzle_symbols.append(">" if random.random() < .5 else "<")

# print(puzzle_nums)
# print(puzzle_symbols)

# Sort puzzle numbers first
# Use largest remaining if greater than, smallest remaining if less than
sorted_puzzle_nums = sorted(puzzle_nums, reverse=True)

# Vars for the "two pointer" method
high = 0
low = PUZZLE_SIZE - 1

# store solution values
solution_values = []

# Integrate through the puzzle symbols and apply solution algorithm
for symbol in puzzle_symbols:
    if symbol == ">":
        solution_values.append(sorted_puzzle_nums[high])
        high += 1
    elif symbol == "<":
        solution_values.append(sorted_puzzle_nums[low])
        low -= 1
solution_values.append(sorted_puzzle_nums[high])

# Convert solution_values to list of strings
solution_values = list(map(str, solution_values))

# Create a list to store the final solution representation
final_solution_representation = [None] * (len(solution_values) + len(puzzle_symbols))

# Create solution representation using nifty slicing with step parameter
final_solution_representation[::2] = solution_values
final_solution_representation[1::2] = puzzle_symbols

# Display final solution
# The join() method takes all items in an iterable and joins them into one string
print(" ".join(final_solution_representation))

# Evaluate whether solution is correct. Some say eval is evil!
print(eval(" ".join(final_solution_representation)))
```
```
18 < 21 < 99 > 94 > 44 < 93 > 53 < 92 > 90 > 74
True
```

### Heaps:  Representation change

A heap is a priority queue that is a complete tree. The textbook has the largest key at the root, so parent keys are larger than their children. The data structure finds the largest priority item in constant time. Removing the highest priority item and adding new item are lg(n) time, using bubble down and bubble up algorithm.


Properties of Heaps

1. The height of a heap is floor(lg n).
2. The root contains the highest priority item.
3. A node and all the descendants is a heap
4. A heap can be implemented using an array and all operations are in-place.
5. if index of the root = 1 then index of left child = 2i and right child = 2i+1
6. Level i of the heap has 2i elements
7. heap order, the parent value is larger than the children

The naive construction of the heap is by adding the items one at a time. The cost is Θ(n lg n).


There is a faster construction in linear time, **bottom-up heap construction**.

Bottom-up heap construction starts at the last trivial sub heap, floor(n/2), and checks for heap ordering and correctly. Iteratively the algorithm moves up the heap checking the heap ordering and correcting.

``` java
Algorithm HeapBottomUp(H[1...n])

for i ← floor(n/2) down to 1 do

k ← i // parent index

v ← H[k] // proposed parent value

heap ← false

while not heap and 2*k ≤ n do

j ← 2*k  // left child index

if j < n  then // there are children

if H[j] < H[j+1] then j++ // find the larger child value

if v ≥ H[j] then heap ← true  // check heap ordering

else // correct the heap ordering

H[k] ← H[j] // bubble down

k ← j // move down the heap

H[k] ← v // insert the value
```

The worst case cost is O(n), less than 2n comparisons.