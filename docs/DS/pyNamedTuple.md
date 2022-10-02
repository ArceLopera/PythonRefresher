Named tuples are basically easy-to-create, lightweight object types. Named tuple instances can be referenced using object-like variable dereferencing or the standard tuple syntax. They can be used similarly to struct or other common record types, except that they are immutable. It is common to represent a point as a tuple (x, y). This leads to code like the following:
``` py
pt1 = (1.0, 5.0)
pt2 = (2.5, 1.5)

from math import sqrt
line_length = sqrt((pt1[0]-pt2[0])**2 + (pt1[1]-pt2[1])**2)
print(line_length)
```
```
3.8078865529319543
```
Using a named tuple it becomes more readable:

``` py
from collections import namedtuple
Point = namedtuple('Point', 'x y')
pt1 = Point(1.0, 5.0)
pt2 = Point(2.5, 1.5)

from math import sqrt
line_length = sqrt((pt1.x-pt2.x)**2 + (pt1.y-pt2.y)**2)
print(line_length)
```
```
3.8078865529319543
```
However, named tuples are still backwards compatible with normal tuples, so the following will still work:

``` py
Point = namedtuple('Point', 'x y')
pt1 = Point(1.0, 5.0)
pt2 = Point(2.5, 1.5)

from math import sqrt
# use index referencing
line_length = sqrt((pt1[0]-pt2[0])**2 + (pt1[1]-pt2[1])**2)
print(line_length)
 # use tuple unpacking
x1, y1 = pt1
print(x1)
print(y1)

```

```
3.8078865529319543
1.0
5.0
```
Thus, you should use named tuples instead of tuples anywhere you think object notation will make your code more pythonic and more easily readable. Use them to represent very simple value types, particularly when passing them as parameters to functions. It makes the functions more readable, without seeing the context of the tuple packing.

NamedTuples, like dictionaries, contain keys that are hashed to a particular value. But on contrary, it supports both access from key-value and iteration, the functionality that dictionaries lack.

``` py
# Python code to demonstrate namedtuple()
 
from collections import namedtuple
 
# Declaring namedtuple()
Student = namedtuple('Student', ['name', 'age', 'DOB'])
 
# Adding values
S = Student('Harry', '12', '31071980')
 
# Access by index: The attribute values of namedtuple() 
# are ordered and can be accessed using the index number unlike dictionaries 
# which are not accessible by index.
print("The Student age using index is : ", end="")
print(S[1])
 
# Access using name :  Access by keyname is also allowed as in dictionaries.
print("The Student name using keyname is : ", end="")
print(S.name)

# Access using getattr(): This is yet another way to access the value by 
# giving namedtuple and key value as its argument.
print("The Student DOB using getattr() is : ", end="")
print(getattr(S, 'DOB'))
```
```
The Student age using index is : 12
The Student name using keyname is : Harry
The Student DOB using getattr() is : 31071980
```
## Conversion Operations
+ **_make()** :
 This function is used to return a namedtuple() from the iterable passed as argument.
+ **_asdict()** :
 This function returns the OrderedDict() as constructed from the mapped values of namedtuple().
+ **using “\*\*” (double star) operator** :
 This function is used to convert a dictionary into the namedtuple(). 
``` py
# Python code to demonstrate namedtuple() and
# _make(), _asdict() and "**" operator

# importing "collections" for namedtuple()
import collections

# Declaring namedtuple()
Student = collections.namedtuple('Student',
								['name', 'age', 'DOB'])

# Adding values
S = Student('Harry', '12', '31071980')

# initializing iterable
li = ['Ron', '12', '01031980']

# initializing dict
di = {'name': "Hermione", 'age': 12, 'DOB': '19091979'}

# using _make() to return namedtuple()
print("The namedtuple instance using iterable is : ")
print(Student._make(li))

# using _asdict() to return an OrderedDict()
print("The OrderedDict instance using namedtuple is : ")
print(S._asdict())

# using ** operator to return namedtuple from dictionary
print("The namedtuple instance from dict is : ")
print(Student(**di))
```
```
The namedtuple instance using iterable is : 
Student(name='Ron', age='12', DOB='01031980')
The OrderedDict instance using namedtuple is : 
OrderedDict([('name', 'Harry'), ('age', '12'), ('DOB', '31071980')])
The namedtuple instance from dict is : 
Student(name='Hermione', age=12, DOB='19091979')
```
## Additional Operation 
+ **_fields**: This function is used to return all the keynames of the namespace declared.
+ **_replace()**: _replace() is like str.replace() but targets named fields( does not modify the original values)
``` py
# Python code to demonstrate namedtuple() and
# _fields and _replace()

# importing "collections" for namedtuple()
import collections

# Declaring namedtuple()
Student = collections.namedtuple('Student', ['name', 'age', 'DOB'])

# Adding values
S = Student('Harry', '12', '31071980')

# using _fields to display all the keynames of namedtuple()
print("All the fields of students are : ")
print(S._fields)

# ._replace returns a new namedtuple, it does not modify the original
print("returns a new namedtuple : ")
print(S._replace(name='Ron'))
# original namedtuple
print(S)
```
```
All the fields of students are : 
('name', 'age', 'DOB')
returns a new namedtuple : 
Student(name='Ron', age='12', DOB='31071980')
Student(name='Harry', age='12', DOB='31071980')
```