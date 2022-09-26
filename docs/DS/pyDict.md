Since you've seen parenthesis (for tuples) and square brackets (for lists), you may be wondering what curly braces are used for in Python. The answer: Python dictionaries.  The defining feature of a Python dictionary is that it has **keys** and **values** that are associated with each other.  When defining a dictionary, this association may be accomplished using the colon (:) as is done below. Dictionaries are data structures used to map arbitrary keys to values.
Lists can be thought of as dictionaries with integer keys within a certain range. Dictionaries can be indexed in the same way as lists, using square brackets containing keys. 
## Dict Creation
An empty dictionary is defined as {}.

Dictionary can also be created by the built-in function dict().

``` py
# Creating an empty Dictionary
Dict = {}
print("Empty Dictionary: ")
print(Dict)

# Creating a Dictionary
# with dict() method
Dict = dict({1: 'Trips', 2: 'For', 3:'chips'})
print("\nDictionary with the use of dict(): ")
print(Dict)

# Creating a Dictionary
# with each item as a Pair
Dict = dict([(1, 'Trips'), (2, 'For')])
print("\nDictionary with each item as a pair: ")
print(Dict)
```
```
Empty Dictionary: 
{}

Dictionary with the use of dict(): 
{1: 'Trips', 2: 'For', 3: 'chips'}

Dictionary with each item as a pair: 
{1: 'Trips', 2: 'For'}
```
``` py
Dict={}
#Set default value
Dict.setdefault(1, 'Trips')
Dict.setdefault(3, 'chips')
print(Dict)
```
```
{1: 'Trips', 3: 'chips'}
```
``` py
empty_dic={}
book_dictionary = {"Title": "Frankenstein", "Author": "Mary Shelley", "Year": 1818}
print(book_dictionary["Author"])
```

```
Mary Shelley
```

Above, the keys of the book_dictionary are "Title", "Author", and "Year", and each of these keys has a corresponding value associated with it. Notice that the key-value pairs are separated by a comma. Using keys allows us to access a piece of the dictionary by its name, rather than needing to know the index of the piece that we want, as is the case with lists and tuples. For instance, above we could get the author of Frankenstein using the "Author" key, rather than using an index. In fact, unlike in a list or tuple, the order of elements in a dictionary doesn't matter, and dictionaries cannot be indexed using integers, which we see below when we try to access the second element of the dictionary using an integer:
``` py
print(book_dictionary[1])
```
```
---------------------------------------------------------------------------
KeyError                                  Traceback (most recent call last)
<ipython-input-11-43bbaea82a52> in <module>()
----> 1 print(book_dictionary[1])

KeyError: 1
```

Just like lists, dictionary keys can be assigned to different values. However, unlike lists, a new dictionary key can also be assigned a value, not just ones that already exist.
``` py
squares={1:1,2:4,3:"Error",4:16,}
squares[8]=64
squares[3]=9
print(squares)
```

```
{1: 1, 2: 4, 3: 9, 4: 16, 8: 64}
```
## in operator

To determine whether a key is in a dictionary, you can use in and not in, just as you can for a list.

``` py
nums={1:"one",2:"two",3:"three",}
print(1 in nums)
print("three" in nums)
print(4 not in nums)
``` 

```
True
False
True
```
## Dictionary Functions

### get()
A useful dictionary method is get. It does the same thing as indexing, but if the key is not found in the dictionary it returns another specified value instead ('None', by default).
``` py
pairs={
    1: "apple",
    "orange":[2,3,4],
    True: False,
    None: "True"
}
print(pairs.get("orange"))
print(pairs.get(7))
print(pairs.get(12345,"not in dictionary")) ##Default message when not found

fib={1:1,2:1,3:2,4:3,}
print(fib.get(4,0)+fib.get(7,5))
```
```
[2, 3, 4]
None
not in dictionary
8
```
### values()
To iterate over the values of a dictionary, you can use the .values() function: 
``` py 
for value in data.values():
    pass
```

### Other funtions:

+ **copy()**	They copy() method returns a shallow copy of the dictionary.
+ **clear()**	The clear() method removes all items from the dictionary.
+ **pop()**	Removes and returns an element from a dictionary having the given key.
+ **popitem()**	Removes the arbitrary key-value pair from the dictionary and returns it as tuple.
+ **get()**	It is a conventional method to access a value for a key.
+ **dictionary_name.values()**	returns a list of all the values available in a given dictionary.
+ **str()**	Produces a printable string representation of a dictionary.
+ **update()**	Adds dictionary dict2’s key-values pairs to dict
+ **setdefault()**	Set dict[key]=default if key is not already in dict
+ **keys()**	Returns list of dictionary dict’s keys
+ **items()**	Returns a list of dict’s (key, value) tuple pairs
+ **has_key()**	Returns true if key in dictionary dict, false otherwise
+ **fromkeys()**	Create a new dictionary with keys from seq and values set to value.
+ **type()**	Returns the type of the passed variable.
+ **cmp()**	Compares elements of both dict.
