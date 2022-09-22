A tuple is a Python collection that is extremely similar to a list, with some subtle differences.  For starters, tuples are indicated using parentheses instead of square brackets. Like lists and dictionaries, tuples can be nested within each other.

``` py
x = 1
y = 2
coordinates = (x, y)
```
The variable coordinates above is a tuple containing the variables x and y. This example was chosen to also demonstrate a difference between the typical usage of tuples versus lists. Whereas lists are frequently used to contain objects whose values are similar in some sense, tuples are frequently used to contain attributes of a coherent unit. For instance, as above, it makes sense to treat the coordinates of a point as a single unit. As another example, consider the following tuple and list concerning dates:

``` py
year1 = 2011
month1 = "May"
day1 = 18
date1 = (month1, day1, year1)
year2 = 2017
month2 = "June"
day2 = 13
date2 = (month2, day2, year2)
years_list = [year1, year2]
```

Notice above that we have collected the attributes of a single date into one tuple: those pieces of information all describe a single "unit".

By contrast, in the years list we have collected the different years.

In the code-snippet: the values in the list have a commonality (they are both years), but they do not describe the same unit.

The distinction drawn between tuples and lists is one that many Python programmers recognize in practice, but not one that is strictly enforced (i.e., you won't get any errors if you break this convention!). Another subtle way in which tuples and lists differ involves what is called mutability of Python variables. Mutability refers to the fact that a mutable object can be changed after it is created, and an immutable object can’t. Tuples are not mutable, lists are mutable. Tuples are very similar to lists, except that they are immutable (they cannot be changed). Trying to reassign a value in a tuple causes a TypeError. Objects of built-in types like (int, float, bool, str, tuple, frozenset, unicode) are immutable. Objects of built-in types like (list, set, dict, byte array) are mutable. Custom classes are generally mutable. To simulate immutability in a class, one should override attribute setting and deletion to raise exceptions. To read further.

``` py
words = ("spam", "eggs", "sausages",)
print(words[0])
words[1]="cheese"
```

```
spam
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-85-a8af92c7d33f> in <module>()
      1 words = ("spam", "eggs", "sausages",)
      2 print(words[0])
----> 3 words[1]="cheese"

TypeError: 'tuple' object does not support item assignment
```
Tuples can be created without the parentheses, by just separating the values with commas. An empty tuple is created using an empty parenthesis pair. Tuples are faster than lists, but they cannot be changed. Slicing can also be done on tuples.

``` py
my_tp=()
tp= "one","two","three"
print(tp[0])
print(len(my_tp))
print(tp[1:])

```

```
one
0
('two', 'three')
```

## Tuple unpacking

Tuple unpacking allows you to assign each item in an iterable (often a tuple) to a variable. This can be also used to swap variables by doing a, b = b, a , since b, a on the right hand side forms the tuple (b, a) which is then unpacked.

A variable that is prefaced with an asterisk (*) takes all values from the iterable that are left over from the other variables.

``` py
numbers = (1,2,3)
a,b,c = numbers #unpacking
print(a)
print(b)
print(c)
```
```
1
2
3
```

``` py
a,b,*c,d=(1,2,3,4,5,6,7,8,9)
print(a)
print(b)
print(c)
print(d)
```
```
1
2
[3, 4, 5, 6, 7, 8]
9
```