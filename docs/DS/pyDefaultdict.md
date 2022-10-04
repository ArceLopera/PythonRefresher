Dictionary in Python is an unordered collection of data values that are used to store data values like a map. Unlike other Data Types that hold only single value as an element, the Dictionary holds key-value pair. In Dictionary, the key must be unique and immutable. This means that a Python Tuple can be a key whereas a Python List can not. A Dictionary can be created by placing a sequence of elements within curly {} braces, separated by ‘comma’.

``` py
# Python program to demonstrate
# dictionary
Dict = {1: 'Treats', 2: 'For', 3: 'Pricks'}
print("Dictionary:")
print(Dict)
print(Dict[1])

# Uncommenting this print(Dict[4])
# will raise a KeyError as the
# 4 is not present in the dictionary
```
```
Dictionary:
{1: 'Treats', 2: 'For', 3: 'Pricks'}
Treats
```
Sometimes, when the KeyError is raised, it might become a problem. To overcome this Python introduces another dictionary like container known as Defaultdict which is present inside the collections module.

Defaultdict is a container like dictionaries present in the module collections. Defaultdict is a sub-class of the dictionary class that returns a dictionary-like object. The functionality of both dictionaries and defaultdict are almost same except for the fact that defaultdict never raises a KeyError. It provides a default value for the key that does not exists.

``` py
# Python program to demonstrate defaultdict
from collections import defaultdict
# Function to return a default
# values for keys that are not present
def def_value():
	return "Not Present"
	
# Defining the dict
d = defaultdict(def_value)
d["a"] = 1
d["b"] = 2

print(d["a"])
print(d["b"])
print(d["c"])
```
```
1
2
Not Present
```
## Inner Working of defaultdict

Defaultdict adds one writable instance variable and one method in addition to the standard dictionary operations. The instance variable is the default_factory parameter and the method provided is missing.

Default_factory: It is a function returning the default value for the dictionary defined. If this argument is absent then the dictionary raises a KeyError.

``` py
# Python program to demonstrate # default_factory argument of # defaultdict
from collections import defaultdict
	
# Defining the dict and passing # lambda as default_factory argument
d = defaultdict(lambda: "Not Present")
d["a"] = 1
d["b"] = 2

print(d["a"])
print(d["b"])
print(d["c"])
```
```
1
2
Not Present
```

``` py
from collections import defaultdict
# Correct instantiation
def_dict = defaultdict(list)  # Pass list to .default_factory
def_dict['one'] = 1  # Add a key-value pair
def_dict['missing']  # Access a missing key returns an empty list
```
```
[]
```

``` py
def_dict['another_missing'].append(4)  # Modify a missing key
def_dict
```
```
defaultdict(list, {'another_missing': [4], 'missing': [], 'one': 1})
```

``` py
dep = [('Sales', 'John Doe'),
       ('Sales', 'Martin Smith'),
       ('Accounting', 'Jane Doe'),
       ('Marketing', 'Elizabeth Smith'),
       ('Marketing', 'Adam Doe')]

from collections import defaultdict

dep_dd = defaultdict(list) #For uniqueness instead of list use set
for department, employee in dep:
    dep_dd[department].append(employee)

print(dep_dd)
```
```
defaultdict(<class 'list'>, {'Sales': ['John Doe', 'Martin Smith'], 'Accounting': ['Jane Doe'], 'Marketing': ['Elizabeth Smith', 'Adam Doe']})
```
In this example, you group the employees by their department using a defaultdict with .default_factory set to list. To do this with a regular dictionary, you can use dict.setdefault() as follows:

``` py
dep_d = dict()
for department, employee in dep:
    dep_d.setdefault(department, []).append(employee)

print(dep_d)
```
```
{'Sales': ['John Doe', 'Martin Smith'], 'Accounting': ['Jane Doe'], 'Marketing': ['Elizabeth Smith', 'Adam Doe']}
```

This code is straightforward, and you’ll find similar code quite often in your work as a Python coder. However, the defaultdict version is arguably more readable, and for large datasets, it can also be a lot faster and more efficient. So, if speed is a concern for you, then you should consider using a defaultdict instead of a standard dict.

## Auto-vivification

Defauldict are used to easily make nested dicts. It is called Auto-vivification.

``` py
from collections import defaultdict
import json
def turtles():
  return defaultdict(turtles)

data = turtles()
data["Hello"]="Hey!"
data["Foo"]["bar"]["baz"]="hmmm"

print(json.dumps(data, indent=1))
```
```
{
 "Hello": "Hey!",
 "Foo": {
  "bar": {
   "baz": "hmmm"
  }
 }
}
```
