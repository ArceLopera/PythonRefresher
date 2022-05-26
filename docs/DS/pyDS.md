##Python Collections

###**Iterable** 
Anything that you can loop over using a for loop
e.g: list, tuples, strings, set and dictionaries

###**Sequence** 
a subset of Iterables that have: 
1. A length
2. An Index
3. Can be sliced

e.g: Strings, list, tuples

Not dictionaries, sets, files and generators

###**Data Structures**

Python supports the following data structures: lists, dictionaries, tuples, sets. For arrays, see numpy array.

When to use a dictionary:
- When you need a logical association between a key:value pair.
- When you need fast lookup for your data, based on a custom key.
- When your data is being constantly modified. Remember, dictionaries are mutable.

When to use the other types:
- Use lists if you have a collection of data that does not need random access. Try to choose lists when you need a simple, iterable collection that is modified frequently.
- Use a set if you need uniqueness for the elements.
- Use tuples when your data cannot change.

Many times, a tuple is used in combination with a dictionary, for example, a tuple might represent a key, because it's immutable.

| Tuples | Lists | Dict | Sets |
| --- | --- | --- | --- |
| ( ) | [ ] | {k:v} | { } |
|Immutable|Mutable|Mutable|Mutable|
|Ordered|Ordered|Ordered(>3.7)|Unordered|
|Iterable|Iterable|Iterable|Iterable|
|Constant time|Linear time|Constant time|Constant time|
|mytuple[0]|mylist[0]|mydict['somekey']|myset[0]|
|Allow repetition|Allow repetition|Allow repetition|Unique data|
|len(mytuple)|len(mylist)|len(mydict)|len(myset)|
|.count()|.append() and .insert()|.keys(), .values() and .items()|.add() and .update()|
|.index()|.pop() and .remove()|.pop() or del mydict['somekey']|.remove()|
||.reverse() and sort()|||.intersection() and .difference()|
