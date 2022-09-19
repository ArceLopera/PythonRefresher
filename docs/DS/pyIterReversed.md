Returns an iterator
Python reversed() method returns an iterator that accesses the given sequence in the reverse order.

**3 ways to reverse a sequence:**

1. iter.reverse() reverses a mutable sequence in place and is not available for inmutable sequences
2. Slicing [::-1] creates a reversed copy of a sequence, it is the fastest but creates a copy of the sequence. Memory considerations to reverse millions of items. Used for both mutable and inmutable sequences.
3. reversed() returns a reversed iterator, scales well to millions of items. Used for both mutable and inmutable sequences.

``` py
# Python code to demonstrate working of
# reversed()

# For tuple
seqTuple = ('m', 'o', 'r', 'p', 's')
print(list(reversed(seqTuple)))

# For range
seqRange = range(1, 5)
print(list(reversed(seqRange)))
```

```
['s', 'p', 'r', 'o', 'm']
[4, 3, 2, 1]
```

``` py
class pyp:
	vowels = ['a', 'e', 'i', 'o', 'u']

	# Function to reverse the list
	def __reversed__(self):
		return reversed(self.vowels)

```
```
['u', 'o', 'i', 'e', 'a']

```
