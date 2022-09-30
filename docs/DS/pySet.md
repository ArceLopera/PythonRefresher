Sets are data structures, similar to lists or dictionaries. They are created using curly braces, or the set function. They share some functionality with lists, such as the use of in to check whether they contain a particular item. To create an empty set, you must use set(), as {} creates an empty dictionary.

One small syntax nuisance: {1, 2, 3} is a set, but {} is an empty dictionary.

``` py
empty_set= set()
num_set={1,2,3,4,5}
word_set=set(["spam","eggs","ham"])
print(3 in num_set)
print("spam" not in word_set)
```
```
True
False
```
Sets differ from lists in several ways, but share several list operations such as len. They are unordered, which means that they can't be indexed. They cannot contain duplicate elements. Due to the way they're stored, it's faster to check whether an item is part of a set, rather than part of a list. Instead of using append to add to a set, use add. The method remove removes a specific element from a set; pop removes an arbitrary element. Basic uses of sets include membership testing and the elimination of duplicate entries.

``` py
nums={1,1,2,3,1,2,1,1}
print(nums)
nums.add(-7)
nums.remove(3)
print(nums)
```
```
{1, 2, 3}
{1, 2, -7}
```
## Set Operations
Sets can be combined using mathematical operations.

The union operator | combines two sets to form a new one containing items in either. OR
The intersection operator & gets items only in both. AND
The difference operator - gets items in the first set but not in the second.
The symmetric difference operator ^ gets items in either set, but not both. XOR
The comparison operators check for subset and superset relationships. >= and <=



``` py
f={3,2,9,4,5,6}
s={7,8,9,1,4,6,6,8}
print(f|s) #Union
print(f&s) #Intersection
print(f-s) # Difference
print(f^s) #Sym Difference
print(f>=s)#f superset of s
```
```
{1, 2, 3, 4, 5, 6, 7, 8, 9}
{9, 4, 6}
{2, 3, 5}
{1, 2, 3, 5, 7, 8}
False

```

Sets provide methods as well as operators.

The argument you pass to a method can be any iterable, not just a set. And accept more than one argument

``` py
f.issuperset([1,2,3])
```
```
False
``` 
``` py
f.union([1,2,3], (3,4,5), {5,6,7}, {7:'a', 8:'b'})
```
```
{1, 2, 3, 4, 5, 6, 7, 8, 9}
```

## Union
``` py
# Python3 program for union() function

set1 = {2, 4, 5, 6}
set2 = {4, 6, 7, 8}
set3 = {7, 8, 9, 10}

# union of two sets
print("set1 U set2 : ", set1.union(set2))

# union of three sets
print("set1 U set2 U set3 :", set1.union(set2, set3))
```
```
set1 U set2 :  {2, 4, 5, 6, 7, 8}
set1 U set2 U set3 : {2, 4, 5, 6, 7, 8, 9, 10}

```
## Intersection
``` py
# Python3 program for intersection() function
set1 = {2, 4, 5, 6}
set2 = {4, 6, 7, 8}
set3 = {4, 6, 8}

# union of two sets
print("set1 intersection set2 : ",
	set1.intersection(set2))

# union of three sets
print("set1 intersection set2 intersection set3 :",
	set1.intersection(set2, set3))
```
```
set1 intersection set2 :  {4, 6}
set1 intersection set2 intersection set3 : {4, 6}
```

``` py
# Python3 program for intersection() function
set1 = {2, 4, 5, 6}
set2 = {4, 6, 7, 8}
set3 = {1, 0, 12}

print(set1 & set2)
print(set1 & set3)

print(set1 & set2 & set3)
```
```
{4, 6}
set()
set()
```
## Difference
``` py
# Python code to get the difference between two sets
# using difference() between set A and set B

# Driver Code
A = {10, 20, 30, 40, 80}
B = {100, 30, 80, 40, 60}
print (A.difference(B))
print (B.difference(A))
```
```
{10, 20}
{100, 60}

```