dataclass module is introduced in Python 3.7 as a utility tool to make structured classes specially for storing data. These classes hold certain properties and functions to deal specifically with the data and its representation.

Although the module was introduced in Python3.7, one can also use it in Python3.6 by installing dataclasses library. 
 

`pip install dataclasses`

The DataClasses are implemented by using decorators with classes. Attributes are declared using Type Hints in Python which is essentially, specifying data type for variables in python.

``` py
# A basic Data Class

# Importing dataclass module
from dataclasses import dataclass

@dataclass
class Mycle():
	"""A class for holding an article content"""

	# Attributes Declaration
	# using Type Hints

	title: str
	author: str
	language: str
	upvotes: int

# A DataClass object
article = Mycle("DataClasses",
					"vynnyl",
					"Python", 0)
print(article)

```
```
Mycle(title='DataClasses', author='vynnyl', language='Python', upvotes=0)
```

The two noticeable points in above code: 
 

* Without a \__init__() constructor, the class accepted values and assigned it to appropriate variables.
The output of printing object is a neat representation of the data present in it, without any explicit function coded to do this. That means it has a modified \__repr__() function.

* \__post_init__(): This function when made, is called by in-built \__init__() after initialization of all the attributes of DataClass. Basically, object creation of DataClass starts with \__init__() (constructor-calling) and ends with \__post__init__() (post-init processing).

``` py
from dataclasses import dataclass, field

name = {'viwal': 'Vi Awal'}


@dataclass
class GArticle:

	title : str
	language: str
	author: str
	author_name: str = field(init = False)
	upvotes: int = 0 #default value

	def __post_init__(self):
		self.author_name = name[self.author]


dClassObj = GArticle("DataClass", "Python3", "viwal")
print(dClassObj)
```
```
GArticle(title='DataClass', language='Python3', author='viwal', author_name='Vi Awal', upvotes=0)
```

## Immutable data classes

``` py
# Creating immutable data classes

from dataclasses import dataclass

@dataclass(frozen=True)  # "The "frozen" parameter makes the class immutable
class ImmutableClass:
    value1: str = "Value 1"
    value2: int = 0

    def somefunc(self, newval):
        self.value2 = newval


obj = ImmutableClass()
print(obj.value1)

# attempting to change the value of an immutable class throws an exception
#obj.value1 = "Another value"
#print(obj.value1)

# Frozen classes can't modify themselves either
#obj.somefunc(20)

```
```
Value 1
```