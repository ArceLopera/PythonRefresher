A ChainMap encapsulates many dictionaries into a single unit and returns a list of dictionaries.

``` py
# Python program to demonstrate ChainMap
from collections import ChainMap

d1 = {'a': 1, 'b': 2}
d2 = {'c': 3, 'd': 4}
d3 = {'e': 5, 'f': 6}

# Defining the chainmap
c = ChainMap(d1, d2, d3)
print(c)
```
```
ChainMap({'a': 1, 'b': 2}, {'c': 3, 'd': 4}, {'e': 5, 'f': 6})
```
Accessing Keys and Values from ChainMap Values from ChainMap can be accessed using the key name. They can also be accessed by using the keys() and values() method.

``` py
from collections import ChainMap
	
d1 = {'a': 1, 'b': 2}
d2 = {'c': 3, 'd': 4}
d3 = {'e': 5, 'f': 6}

# Defining the chainmap
c = ChainMap(d1, d2, d3)
	
# Accessing Values using key name
print(c['a'])

# Accessing values using values()
# method
print(c.values())

# Accessing keys using keys()
# method
print(c.keys())
```
```
1
ValuesView(ChainMap({'a': 1, 'b': 2}, {'c': 3, 'd': 4}, {'e': 5, 'f': 6}))
KeysView(ChainMap({'a': 1, 'b': 2}, {'c': 3, 'd': 4}, {'e': 5, 'f': 6}))
```
## Adding new dictionary

A new dictionary can be added by using the new_child() method. The newly added dictionary is added at the beginning of the ChainMap.

``` py
import collections

# initializing dictionaries
dic1 = { 'a' : 1, 'b' : 2 }
dic2 = { 'b' : 3, 'c' : 4 }
dic3 = { 'f' : 5 }

# initializing ChainMap
chain = collections.ChainMap(dic1, dic2)

# printing chainMap
print ("All the ChainMap contents are : ")
print (chain)

# using new_child() to add new dictionary
chain1 = chain.new_child(dic3)

# printing chainMap
print ("Displaying new ChainMap : ")
print (chain1)

```
```
All the ChainMap contents are : 
ChainMap({'a': 1, 'b': 2}, {'b': 3, 'c': 4})
Displaying new ChainMap : 
ChainMap({'f': 5}, {'a': 1, 'b': 2}, {'b': 3, 'c': 4})
```