A linked list is a sequence of nodes where each node stores its own data and a link to the next node. One node links to another forming what can be thought of as a linked chain. The first node is called the head, and it's used as the starting point for any iteration through the list. The last node must have its link pointing to None to determine the end of the list.

Unlike stacks and queues, you can insert and remove nodes in any position of the linked list (similar to a standard list).

Applications

Linked lists are useful when your data is linked. For example when you need undo/redo functionality, the nodes can represent the state with links to the previous and next states. Another example would be a playlist of music, where each clip is linked with the next one.

Linked lists can also be used to create other data structures, such as stack, queues and graphs.

``` py
class Node:
  def __init__(self, data, next):
    self.data = data
    self.next = next

class LinkedList:
  def __init__(self):
    self.head = None
  def add_at_front(self,data):
    self.head = Node(data, self.head)
  def add_at_end(self,data):
    if not self.head:
      self.head = Node(data, None)
      return
    curr = self.head
    while curr.next:
      curr = curr.next
    curr.next = Node(data, None)
  def get_last_node(self):
    n = self.head
    while (n.next != None):
      n = n.next
    return n.data
  def print_list(self):
    n = self.head
    while n != None:
      print(n.data,end=" => ")
      n = n.next
    print()
```
There are two types of linked list: 

+ Single-Linked List: In this, the nodes point to the node immediately after it
+ Doubly Linked List: In this, the nodes not only reference the node next to it but also the node before it.

To start with Python, it does not have a linked list library built into it like the classical programming languages. Python does have an inbuilt type list that works as a dynamic array but its operation shouldn’t be confused with a typical function of a linked list. This doesn’t mean one cannot implement a linked list in Python, they can but it will not be straight up.

## Using deque() package

When to use deque() as a linked list?

+ Inserting and deleting elements at front and back respectively is the only need. Inserting and removing elements from the middle becomes time-consuming.
+ In-place reversal since Python now allows elements to be reversed in the place itself.
+ Storage is preferred over performance and not all elements get a separate node of their own

``` py
# importing module
import collections

# initialising a deque() of arbitrary length
linked_lst = collections.deque()

# filling deque() with elements
linked_lst.append('first')
linked_lst.append('second')
linked_lst.append('third')

print("elements in the linked_list:")
print(linked_lst)

# adding element at an arbitrary position
linked_lst.insert(1, 'fourth')

print("elements in the linked_list:")
print(linked_lst)

# deleting the last element
linked_lst.pop()

print("elements in the linked_list:")
print(linked_lst)

# removing a specific element
linked_lst.remove('fourth')

print("elements in the linked_list:")
print(linked_lst)

```
```
elements in the linked_list:
deque(['first', 'second', 'third'])
elements in the linked_list:
deque(['first', 'fourth', 'second', 'third'])
elements in the linked_list:
deque(['first', 'fourth', 'second'])
elements in the linked_list:
deque(['first', 'second'])
```
## Using llist package

The llist is an extension module for CPython providing basic linked list data structures.

``` py
pip install llist
```


``` py
# importing packages
import llist
from llist import sllist,sllistnode

# creating a singly linked list
lst = sllist(['first','second','third'])
print(lst)
print(lst.first)
print(lst.last)
print(lst.size)
print()

# adding and inserting values
lst.append('fourth')
node = lst.nodeat(2)

lst.insertafter('fifth',node)

print(lst)
print(lst.first)
print(lst.last)
print(lst.size)
print()

# poping a value
#i.e. removing the last entry
# of the list
lst.pop()
print(lst)
print(lst.first)
print(lst.last)
print(lst.size)
print()

# removing a specific element
node = lst.nodeat(1)
lst.remove(node)
print(lst)
print(lst.first)
print(lst.last)
print(lst.size)
print()

```
```
sllist([first, second, third])
sllistnode(first)
sllistnode(third)
3

sllist([first, second, third, fifth, fourth])
sllistnode(first)
sllistnode(fourth)
5

sllist([first, second, third, fifth])
sllistnode(first)
sllistnode(fifth)
4

sllist([first, third, fifth])
sllistnode(first)
sllistnode(fifth)
3
```
## Using StructLinks package

StructLinks is used to easily Access and visualize different Data structures including Linked lists, Doubly Linked lists, Binary trees, Graphs, Stacks, and Queues.

The structlinks.LinkedList and structlinks.DoublyLikedList modules could be used to make linked lists. All the operations that could be performed with a list could also be performed with structlinks.LinkedList class.


``` py
# 1. Download the repo and set it as the current directory
git clone https://github.com/eeshannarula29/structlinks

# 2. Add the project directory to the path
import os, sys
sys.path.append(os.getcwd())

cd LinkedList/

import LinkedList as ll

# create an empty linked list
lst = ll.LinkedList()
# create a linked list with initial values
lst = ll.LinkedList([1, 10.0, 'string'])

print(lst)

print()

print('Elements of list:')

# elements of the list
element0 = lst[0]
element1 = lst[1]
element2 = lst[2]

print(f'first element : {element0}')
print(f'second element : {element1 }')
print(f'third element : {element2}')

print()

print('Length of list:')

# Length of the list
length = len(lst)

print(f'size of the list : {length}')

print()

print('Set item:')

# Set item
lst[0] = 10

print(f'list after setting lst[0] to 10 : {lst}')

print()

print('Append And Insert:')

# Append And Insert
lst.append('another string')
lst.insert(1, 0.0)

print(f'list after appedning and inserting: {lst}')

print()

print('Pop and Remove')

# Pop and Remove
element = lst.pop(0)
lst.remove(10.0)

print(f'list after poping and removing : {lst}')
print(f'pop function also returns the element : {element}')

```
```
[1 -> 10 -> -3 -> 5]

Elements of list:
first element : 1
second element : 10
third element : -3

Length of list:
size of the list : 4

Set item:
list after setting lst[0] to 10 : [10 -> 10 -> -3 -> 5]

Append And Insert:
list after appedning and inserting: [10 -> 0.0 -> 10 -> -3 -> 5 -> another string]

Pop and Remove
list after poping and removing : [0.0 -> -3 -> 5 -> another string]
pop function also returns the element : 10
```