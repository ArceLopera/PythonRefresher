A list comprises a sequence of objects, usually represented using square brackets with commas between the items in the sequence as is done below:

``` py
my_list = ['a', 'b', 'c', 'd']
print(my_list)
```

``` 
['a', 'b', 'c', 'd']
```

Above, my_list contains a sequence of character objects. Lists, however, accomodate items of varying types of objects:

``` py
varied_list = ['a', 1, 'b', 3.14159] # a list with elements of char, integer, and float types
nested_list = ['hello', 'governor', [1.618, 42]] # a list within a list!
```

Lists allow for what is called indexing, in which a specified element of the list may be obtained. For instance, say you wanted to grab the second element of varied_list above. Then you could index the list as so:

``` py
second_element = varied_list[1] # Grab second element of varied_list
print(second_element)
``` 

Now is a good time to mention that Python is what's called a zero-indexed programming language. This simply means that the "first" element in a list or other collection of data items is indexed using "0" (zero) rather than "1". This is why, above, we grab the second element of varied_list using the integer index "1" instead of "2" as some might expect from a one-indexed language (like MATLab).

Another feature of python indexing that comes in handy is the use of negative indexing. As we discussed above, the "first" element of a python list is denoted by index "0"; thus, it is almost natural to consider the last element of the list as being indexed by "-1". Observe the following examples of negative indexing:

``` py
last_element = my_list[-1] # the last element of my_list
last_element_2 = my_list[len(my_list)-1] # also the last element of my_list, obtained differently
second_to_last_element = my_list[-2]
```
Similar to indexing is list slicing, in which a contiguous section of list may be accessed. The colon (:) is used to perform slicing, with integers denoting the positions at which to begin and end the slice. Below, we show that the beginning or ending integer for a slice may be omited when one is slicing from the beginning or to the end of the list. Also note below that the index for slice beginning is included in the slice, but the index for the slice end is not included.

``` py
NFL_list = ["Chargers", "Broncos", "Raiders", "Chiefs", "Panthers", "Falcons", "Cowboys", "Eagles"]
AFC_west_list = NFL_list[:4] # Slice to grab list indices 0, 1, 2, 3 -- "Chargers", "Broncos", "Raiders", "Chiefs"
NFC_south_list = NFL_list[4:6] # Slice list indices 4, 5 -- "Panthers", "Falcons"
NFC_east_list = NFL_list[6:] # Slice list indices 6, 7 -- "Cowboys", "Eagles"
```

List slices can also have a third number, representing the step, to include only alternate values in the slice.

``` py
NFL_list = ["Chargers", "Broncos", "Raiders", "Chiefs", "Panthers", "Falcons", "Cowboys", "Eagles"]
list1 = NFL_list[3::2]
print(list1)
```

```
['Chiefs', 'Falcons', 'Eagles']
```

Negative values can be used in list slicing (and normal list indexing). When negative values are used for the first and second values in a slice (or a normal index), they count from the end of the list. If a negative value is used for the step, the slice is done backwards. Using [::-1] as a slice is a common and idiomatic way to reverse a list.

``` py
squares=[0,1,4,9,16,25,36,49,64,81]
print(squares[1:-3])
print(squares[::-1])
print(squares[:4:-1])
```

```
[1, 4, 9, 16, 25, 36]
[81, 64, 49, 36, 25, 16, 9, 4, 1, 0]
[81, 64, 49, 36, 25]
```

Sometimes you need to create an empty list and populate it later during the program. For example, if you are creating a queue management program, the queue is going to be empty in the beginning and get populated with people data later. An empty list is created with an empty pair of square brackets. Nested lists can be used to represent 2D grids, such as matrices. Indexing strings behaves as though you are indexing a list containing each character in the string.

``` py
empty_list=[]
print(empty_list)
m=[
   [1,2,3],
   [4,5,6]
   ]
print(m)
s="Hello world"
print(s[6])
```

```
[]
[[1, 2, 3], [4, 5, 6]]
w
```

### List Operations 

The item at a certain index in a list can be reassigned. Lists can be added and multiplied in the same way as strings. To check if an item is in a list, the in operator can be used. It returns True if the item occurs one or more times in the list, and False if it doesn't. The in operator is also used to determine whether or not a string is a substring of another string.

``` py
M=[1,1,1]
M[1]="hello"
print(M)
print(M*3)
print(M+[1,2])
print(1 in M)
print("Spam" in M)
print(not "hello" in M)
```

```
[1, 'hello', 1]
[1, 'hello', 1, 1, 'hello', 1, 1, 'hello', 1]
[1, 'hello', 1, 1, 2]
True
False
False
```

### List Functions

+ len(list): to get the number of items in a list.
+ max(list): Returns the list item with the maximum value
+ min(list): Returns the list item with minimum value
+ list.append(item): adds an item to the end of an existing list.
+ list.insert(index, item): is similar to append, except that it allows you to insert a new item at any position in the list, as opposed to just at the end.
+ list.index(item): finds the first occurrence of a list item and returns its index. If the item isn't in the list, it raises a ValueError.
+ list.count(item): Returns a count of how many times an item occurs in a list
+ list.remove(item): Removes an object from a list
+ list.pop(index) removes the item at the given index.
+ list.reverse(): Reverses items in a list.
+ list.sort() sorts the list. By default, the list is sorted ascending. You can specify reverse=True as the parameter, to sort descending.

``` py
nums=[1,2,3]
nums.append(4)
print(nums)
nums.insert(2,"hello")
print(nums)
print(len(nums))
print(nums.index(3))
nums+=[1,2,1]
print(nums.count(1))
nums.remove("hello")
print(nums.reverse())
print(max(nums))
print(min(nums))
```

```
[1, 2, 3, 4]
[1, 2, 'hello', 3, 4]
5
3
3
None
4
1
```
``` py
# use iterator functions like enumerate, zip, iter, next
    # define a list of days in English and French
days = ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"]
daysFr = ["Dim", "Lun", "Mar", "Mer", "Jeu", "Ven", "Sam"]

    # use iter to create an iterator over a collection
i = iter(days)
print(next(i))  # Sun
print(next(i))  # Mon
print(next(i))  # Tue

    # iterate using a function and a sentinel
with open("game.txt", "r") as fp:
   for line in iter(fp.readline, ''):
      print(line)

    # use regular interation over the days
for m in range(len(days)):
   print(m+1, days[m])

```

```
1 Sun
2 Mon
3 Tue
4 Wed
5 Thu
6 Fri
7 Sat
```
``` py
# using enumerate reduces code and provides a counter
for i, m in enumerate(days, start=1):
        print(i, m)
```

```
1 Sun
2 Mon
3 Tue
4 Wed
5 Thu
6 Fri
7 Sat
```
``` py
# use zip to combine sequences
for m in zip(days, daysFr):
        print(m)

for i, m in enumerate(zip(days, daysFr), start=1):
        print(i, m[0], "=", m[1], "in French")
``` 

``` 
('Sun', 'Dim')
('Mon', 'Lun')
('Tue', 'Mar')
('Wed', 'Mer')
('Thu', 'Jeu')
('Fri', 'Ven')
('Sat', 'Sam')
1 Sun = Dim in French
2 Mon = Lun in French
3 Tue = Mar in French
4 Wed = Mer in French
5 Thu = Jeu in French
6 Fri = Ven in French
7 Sat = Sam in French
``` 