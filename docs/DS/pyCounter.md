A Counter is a subclass of dict. Therefore it is an unordered collection where elements and their respective count are stored as a dictionary. This is equivalent to a bag or multiset of other languages. It is used to keep the count of the elements in an iterable in the form of an unordered dictionary where the key represents the element in the iterable and value represents the count of that element in the iterable.

Counter class is a special type of object data-set provided with the collections module in Python3. Collections module provides the user with specialized container datatypes, thus, providing an alternative to Python’s general-purpose built-ins like dictionaries, lists and tuples. Counter is a sub-class that is used to count hashable objects. It implicitly creates a hash table of an iterable when invoked.

Counter object along with its functions are used collectively for processing huge amounts of data. 

## Initialization
The constructor of counter can be called in any one of the following ways :

* With sequence of items
* With dictionary containing keys and counts
* With keyword arguments mapping string names to counts

``` py
# A Python program to show different ways to create
# Counter
from collections import Counter

# With sequence of items
print(Counter(['B','B','A','B','C','A','B','B','A','C']))

# with dictionary
print(Counter({'A':3, 'B':5, 'C':2}))

# with keyword arguments
print(Counter(A=3, B=5, C=2))
```

```
Counter({'B': 5, 'A': 3, 'C': 2})
Counter({'B': 5, 'A': 3, 'C': 2})
Counter({'B': 5, 'A': 3, 'C': 2})
```
## Updation

We can also create an empty counter and can be updated via update() method
``` py
# A Python program to demonstrate update()
from collections import Counter
coun = Counter()

coun.update([1, 2, 3, 1, 2, 1, 1, 2])
print(coun)

coun.update([1, 2, 4])
print(coun)

```

```
Counter({1: 4, 2: 3, 3: 1})
Counter({1: 5, 2: 4, 3: 1, 4: 1})
```
Data can be provided in any of the three ways as mentioned in initialization and the counter’s data will be increased not replaced. Counts can be zero and negative also.

``` py
# Python program to demonstrate that counts in
# Counter can be 0 and negative
from collections import Counter

c1 = Counter(A=4, B=3, C=10)
c2 = Counter(A=10, B=3, C=4)

c1.subtract(c2)
print(c1)
```

```
Counter({'C': 6, 'B': 0, 'A': -6})
```
We can use Counter to count distinct elements of a list or other collections.
``` py
# An example program where different list items are
# counted using counter
from collections import Counter

# Create a list
z = ['blue', 'red', 'blue', 'yellow', 'blue', 'red']

# Count distinct elements and print Counter object
print(Counter(z))
```

```
Counter({'blue': 3, 'red': 2, 'yellow': 1})
```
Once initialized, counters are accessed just like dictionaries. Also, it does not raise the KeyValue error (if key is not present) instead the value’s count is shown as 0.

``` py
# Python program to demonstrate accessing of
# Counter elements
from collections import Counter

# Create a list
z = ['blue', 'red', 'blue', 'yellow', 'blue', 'red']
col_count = Counter(z)
print(col_count)

col = ['blue','red','yellow','green']

# Here green is not in col_count
# so count of green will be zero
for color in col:
	print (color, col_count[color])
```

```
Counter({'blue': 3, 'red': 2, 'yellow': 1})
blue 3
red 2
yellow 1
green 0
```
## items()

The Counter.items() method helps to see the elements of the list along with their respective frequencies in a tuple.

``` py
# importing the module
from collections import Counter

# making a list
list = [1, 1, 2, 3, 4, 5,
		6, 7, 9, 2, 3, 4, 8]

# instantiating a Counter object
ob = Counter(list)

# Counter.items()
items = ob.items()

print("The datatype is "
	+ str(type(items)))

# displaying the dict_items
print(items)

# iterating over the dict_items
for i in items:
	print(i)

```

```
The datatype is <class 'dict_items'>
dict_items([(1, 2), (2, 2), (3, 2), (4, 2), (5, 1), (6, 1), (7, 1), (9, 1), (8, 1)])
(1, 2)
(2, 2)
(3, 2)
(4, 2)
(5, 1)
(6, 1)
(7, 1)
(9, 1)
(8, 1)
```
## keys()

The Counter.keys() method helps to see the unique elements in the list.

``` py
# importing the module
from collections import Counter

# making a list
list = [1, 1, 2, 3, 4, 5,
		6, 7, 9, 2, 3, 4, 8]

# instantiating a Counter object
ob = Counter(list)

# Counter.keys()
keys = ob.keys()

print("The datatype is "
	+ str(type(keys)))

# displaying the dict_items
print(keys)

# iterating over the dict_items
for i in keys:
	print(i)
```

```
The datatype is <class 'dict_keys'>
dict_keys([1, 2, 3, 4, 5, 6, 7, 9, 8])
1
2
3
4
5
6
7
9
8
```
## values()

The Counter.values() method helps to see the frequencies of each unique element.

``` py
# importing the module
from collections import Counter

# making a list
list = [1, 1, 2, 3, 4, 5,
		6, 7, 9, 2, 3, 4, 8]

# instantiating a Counter object
ob = Counter(list)

# Counter.values()
values = ob.values()

print("The datatype is "
	+ str(type(values)))

# displaying the dict_items
print(values)

# iterating over the dict_items
for i in values:
	print(i)

```

```
The datatype is <class 'dict_values'>
dict_values([2, 2, 2, 2, 1, 1, 1, 1, 1])
2
2
2
2
1
1
1
1
1
```

## elements()

elements() is one of the functions of Counter class, when invoked on the Counter object will return an itertool of all the known elements in the Counter object. The elements() method returns an iterator that produces all of the items known to the Counter. Note : Elements with count <= 0 are not included.

``` py
# import counter class from collections module
from collections import Counter

# Creation of a Counter Class object using
# a string as an iterable data container
# Example - 1
a = Counter("treatortrips")

# Elements of counter object
for i in a.elements():
	print ( i, end = " ")
print()
	
# Example - 2
b = Counter({'trips' : 4, 'for' : 1,
			'gfg' : 2, 'Trean' : 3})

for i in b.elements():
	print ( i, end = " ")
print()

# Example - 3
c = Counter([1, 2, 21, 12, 2, 44, 5,
			13, 15, 5, 19, 21, 5])

for i in c.elements():
	print ( i, end = " ")
print()			
			
# Example - 4
d = Counter( a = 2, b = 3, c = 6, d = 1, e = 5)

for i in d.elements():
	print ( i, end = " ")
```
```
t t t r r r e a o i p s 
trips trips trips trips for gfg gfg Trean Trean Trean 
1 2 2 21 21 12 44 5 5 5 13 15 19 
a a b b b c c c c c c d e e e e e 
```
## most_common()

most_common() is used to produce a sequence of the n most frequently encountered input values and their respective counts.

``` py
# Python example to demonstrate most_elements() on
# Counter
from collections import Counter

coun = Counter(a=1, b=2, c=3, d=120, e=1, f=219)

# This prints 3 most frequent characters
for letter, count in coun.most_common(3):
	print('%s: %d' % (letter, count))
```
```
f: 219
d: 120
c: 3
```