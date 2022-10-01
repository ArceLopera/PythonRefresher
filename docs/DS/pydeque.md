The collection Module in Python provides different types of containers. A Container is an object that is used to store different objects and provide a way to access the contained objects and iterate over them. Some of the built-in containers are Tuple, List, Dictionary, etc.

``` py
import collections
```

Deque (Doubly Ended Queue) in Python is implemented using the module “collections“. Deque is preferred over list in the cases where we need quicker append and pop operations from both the ends of container, as deque provides an O(1) time complexity for append and pop operations as compared to list which provides O(n) time complexity.

With Python lists, we can add and remove elements from the end of the list in constant time, but adding and removing from the beginning takes linear time. That’s because Python lists are implemented using arrays that grow dynamically.

With linked lists, we can add and remove elements from the beginning of the list in constant time, but adding and removing from the end takes linear time.

With either of these implementations, it is easy to make a stack, that is, a collection where the first element we add is the last element we remove. A stack is also called a “first-in, last-out” queue, abbreviated FILO.

But it is not easy to implement a “first-in, first-out” queue, that is, a collection where the first element we add is the first element we remove.

Fortunately, there are ways to implement lists that can add and remove elements from both ends in constant time. A collection that has this property is called a double-ended queue, abbreviated “deque” and pronounced like “deck”.

One way to implement a deque is a doubly-linked list, also known as a “head-tail linked list”. Each node in a doubly-linked list has a reference to the previous node in the list as well as the next element, which I will call left and right.

## Constructor
``` py
dq = collections.deque(range(10))
dq
```
```
deque([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])
```
## append() & popleft()
``` py
for i in range(10,15):
  dq.append(i)
  v = dq.popleft()

  print ("Inserted :",i,"- popped: ",v, "-result:",dq )

```
```
Inserted : 10 - popped:  0 -result: deque([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])
Inserted : 11 - popped:  1 -result: deque([2, 3, 4, 5, 6, 7, 8, 9, 10, 11])
Inserted : 12 - popped:  2 -result: deque([3, 4, 5, 6, 7, 8, 9, 10, 11, 12])
Inserted : 13 - popped:  3 -result: deque([4, 5, 6, 7, 8, 9, 10, 11, 12, 13])
Inserted : 14 - popped:  4 -result: deque([5, 6, 7, 8, 9, 10, 11, 12, 13, 14])
```
## appendleft() & pop()
``` py
for i in reversed(range(0,5)):
  dq.appendleft(i)
  v = dq.pop()

  print ("Inserted :",i,"- popped: ",v, "-result:",dq )
```
```
Inserted : 4 - popped:  14 -result: deque([4, 5, 6, 7, 8, 9, 10, 11, 12, 13])
Inserted : 3 - popped:  13 -result: deque([3, 4, 5, 6, 7, 8, 9, 10, 11, 12])
Inserted : 2 - popped:  12 -result: deque([2, 3, 4, 5, 6, 7, 8, 9, 10, 11])
Inserted : 1 - popped:  11 -result: deque([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])
Inserted : 0 - popped:  10 -result: deque([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])

```

## index(ele, beg, end) 
- This function returns the first index of the value mentioned in arguments, starting searching from beg till end index.

## insert(i, a) 
- This function inserts the value mentioned in arguments(a) at index(i) specified in arguments.

## remove() 
- This function removes the first occurrence of value mentioned in arguments.

## count()
- This function counts the number of occurrences of value mentioned in arguments.

``` py
# Python code to demonstrate working of
# insert(), index(), remove(), count()

# importing "collections" for deque operations
import collections

# initializing deque
de = collections.deque([1, 2, 3, 3, 4, 2, 4])

# using index() to print the first occurrence of 4
print ("The number 4 first occurs at a position : ")
print (de.index(4,2,5))

# using insert() to insert the value 3 at 5th position
de.insert(4,3)

# printing modified deque
print ("The deque after inserting 3 at 5th position is : ")
print (de)

# using count() to count the occurrences of 3
print ("The count of 3 in deque is : ")
print (de.count(3))

# using remove() to remove the first occurrence of 3
de.remove(3)

# printing modified deque
print ("The deque after deleting first occurrence of 3 is : ")
print (de)

```

```
The number 4 first occurs at a position : 
4
The deque after inserting 3 at 5th position is : 
deque([1, 2, 3, 3, 3, 4, 2, 4])
The count of 3 in deque is : 
3
The deque after deleting first occurrence of 3 is : 
deque([1, 2, 3, 3, 4, 2, 4])
```
## extend(iterable) 
- This function is used to add multiple values at the right end of deque. The argument passed is an iterable.

## extendleft(iterable) 
- This function is used to add multiple values at the left end of deque. The argument passed is an iterable. Order is reversed as a result of left appends.

## reverse() 
- This function is used to reverse order of deque elements.

## rotate() 
- This function rotates the deque by the number specified in arguments. If the number specified is negative, rotation occurs to left. Else rotation is to right.

``` py
# Python code to demonstrate working of
# extend(), extendleft(), rotate(), reverse()

# importing "collections" for deque operations
import collections

# initializing deque
de = collections.deque([1, 2, 3,])

# using extend() to add numbers to right end
# adds 4,5,6 to right end
de.extend([4,5,6])

# printing modified deque
print ("The deque after extending deque at end is : ")
print (de)

# using extendleft() to add numbers to left end
# adds 7,8,9 to right end
de.extendleft([7,8,9])

# printing modified deque
print ("The deque after extending deque at beginning is : ")
print (de)

# using rotate() to rotate the deque
# rotates by 3 to left
de.rotate(-3)

# printing modified deque
print ("The deque after rotating deque is : ")
print (de)

# using reverse() to reverse the deque
de.reverse()

# printing modified deque
print ("The deque after reversing deque is : ")
print (de)
```
```
The deque after extending deque at end is : 
deque([1, 2, 3, 4, 5, 6])
The deque after extending deque at beginning is : 
deque([9, 8, 7, 1, 2, 3, 4, 5, 6])
The deque after rotating deque is : 
deque([1, 2, 3, 4, 5, 6, 9, 8, 7])
The deque after reversing deque is : 
deque([7, 8, 9, 6, 5, 4, 3, 2, 1])
```