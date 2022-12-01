- Breadth-first search is used to calculate the shortest path for an unweighted graph.
- Dijkstra’s algorithm is used to calculate the shortest path for a weighted graph.
- Dijkstra’s algorithm works when all the weights are positive.
  - If you have negative weights, use the Bellman-Ford algorithm.

## Binary Search

Binary search only works when your list is in sorted order. For example, the names in a phone book are sorted in alphabetical order, so you can use binary search to look for a name.

Binary search is a lot faster than simple search.

His time complexity is O(log n) is faster than O(n) -Simple search, but it gets a lot faster once the list of items you’re searching through grows.

Algorithm speed isn’t measured in seconds. Algorithm times are measured in terms of growth of an algorithm. Algorithm times are written in Big O notation.

``` py
def binary_search(list, item):
 low = 0
 high = len(list)-1
 while low <= high:
  mid = (low + high)
  guess = list[mid]
  if guess == item:
   return mid
  if guess > item:
   high = mid - 1
  else:
   low = mid + 1
 return None

my_list = [1, 3, 5, 7, 9]
print(binary_search(my_list, 3)) # => 1
print(binary_search(my_list, -1)) # => None
```
```
1
None
```

## Hash Tables

Hashes are good for:

*   Modeling relationships from one thing to another thing
*   Filtering out duplicates
*   Caching/memorizing data instead of making your server do work

Python has hash tables; they’re called dictionaries. 
You can make a new hash table using the dict function:

``` py
book = dict()
book['apple'] = 0.67 
book['milk'] = 1.49
book['avocado'] = 1.49
print(book)
print(book['avocado'])
```
```
{'apple': 0.67, 'milk': 1.49, 'avocado': 1.49}
1.49
```

A hash table has keys and values. In the book hash, the names of
produce are the keys, and their prices are the values. A hash table maps
keys to values.

|         | Hash Table (Average) | Hash Table (Worst) |Arrays |Linked List |
|---------|:--:|:--:|:--:|:--:|
| Search  |O(1)|O(n)|O(1)|O(n)|
| Insert  |O(1)|O(n)|O(n)|O(1)|
| Delete  |O(1)|O(n)|O(n)|O(1)|

* You can make a hash table by combining a hash function
with an array.
* Collisions are bad. You need a hash function that
minimizes collisions.
* Hash tables have really fast search, insert, and delete.
* Hash tables are good for modeling relationships from one
item to another item.
* Once your load factor is greater than .07, it’s time to resize
your hash table.
* Hash tables are used for caching data (for example, with
a web server).
* Hash tables are great for catching duplicates.

``` py
# 2-Sum Interview Problem Solution

def two_sum_hash_table(arr, total):
    hash_table = {}
    for idx, val in enumerate(arr):
        complement = total - val
        if complement in hash_table:
            return idx, hash_table[complement]
        else:
            # The hash table stores the values from the array as keys, and the indices of
            # these values as the values in the table.
            print(f"Adding to hash table: key:{val}, value: {idx}")
        hash_table[val] = idx
    return None


assert two_sum_hash_table([1, 2, 3], 4) in [(0, 2), (2, 0)]
assert two_sum_hash_table([1234, 5678, 9012], 14690) in [(1, 2), (2, 1)]
assert two_sum_hash_table([2, 2, 3], 4) in [(0, 1), (1, 0)]
assert two_sum_hash_table([2, 2], 4) in [(0, 1), (1, 0)]
assert two_sum_hash_table([8, 7, 2, 5, 3, 1], 10) in [(0, 2), (2, 0), (1, 4), (4, 1)]
```
```
Adding to hash table: key:1, value: 0
Adding to hash table: key:2, value: 1
Adding to hash table: key:1234, value: 0
Adding to hash table: key:5678, value: 1
Adding to hash table: key:2, value: 0
Adding to hash table: key:2, value: 0
Adding to hash table: key:8, value: 0
Adding to hash table: key:7, value: 1
```

Ransom note example:

``` py
def ransom_note(magazine, note):
    mag_words = {}
    for word in magazine:
        if word in mag_words:
            mag_words[word] += 1
        else:
            mag_words[word] = 1
    for word in note:
        if mag_words.get(word, 0) < 1:
            return False
        else:
            mag_words[word] -= 1
    return True


# # This criminal has no regard for punctuation
magazine = "give me one grand today night".split()
note = "give one grand today".split()
assert ransom_note(magazine, note) is True

magazine = "two times three is not four".split()
note = "two times two is four".split()
assert ransom_note(magazine, note) is False
```

``` py
from collections import Counter


def ransom_note(magazine, note):
    mag_counter = Counter(magazine)
    note_counter = Counter(note)
    # intersection operator &. This returns the minimum of corresponding counts.
    return mag_counter & note_counter == note_counter


# # This criminal has no regard for punctuation
magazine = "give me one grand today night".split()
note = "give one grand today".split()
assert ransom_note(magazine, note) is True

magazine = "two times three is not four".split()
note = "two times two is four".split()
assert ransom_note(magazine, note) is False
```

## Breadth-first search

Make a queue to start. In Python, you use the double-ended queue (deque) function for this:

``` py
graph = {}
graph['you'] = ['alice', 'bob', 'claire']
graph['bob'] = ['anuj', 'peggy']
graph['alice'] = ['peggy']
graph['claire'] = ['thom', 'jonny']
graph['anuj'] = []
graph['peggy'] = []
graph['thom'] = []
graph['jonny'] = []
```
``` py
from collections import deque

def person_is_seller(name):
  return name[-1] == 'm'

def search(name):
  search_queue = deque()
  search_queue += graph[name]
  searched = []
  while search_queue:
    person = search_queue.popleft()
    if not person in searched:
      if person_is_seller(person):
        print(person + ' is a mango seller!')
        return True
      else:
        search_queue += graph[person]
        searched.append(person)
  return False

search('you')
```
```
thom is a mango seller!
True
```

+ Breadth-first search tells you if there’s a path from A to B.
+ If there’s a path, breadth-first search will find the shortest path.
+ If you have a problem like “find the shortest X,” try modeling your
problem as a graph, and use breadth-first search to solve.
+ A directed graph has arrows, and the relationship follows the
direction of the arrow (rama -> adit means “rama owes adit money”).
+ Undirected graphs don’t have arrows, and the relationship goes both
ways (ross - rachel means “ross dated rachel and rachel dated ross”).
+ Queues are FIFO (First In, First Out).
+ Stacks are LIFO (Last In, First Out).
+ You need to check people in the order they were added to the search
list, so the search list needs to be a queue. Otherwise, you won’t get
the shortest path.
+ Once you check someone, make sure you don’t check them again.
Otherwise, you might end up in an infinite loop.

## Depth-first search
BFS uses queues and DFS uses Stacks

DFS starts at the root of the tree and selects the first child. If the child has children, it selects the first child again. When it gets to a node with no children, it backtracks, moving up the tree to the parent node, where it selects the next child if there is one; otherwise it backtracks again. When it has explored the last child of the root, it’s done.

There are two common ways to implement DFS, recursively and iteratively. The recursive implementation looks like this:


``` py
html_doc = """
<html><head><title>The Dormouse's story</title></head>
<body>
<p class="title"><b>The Dormouse's story</b></p>

<p class="story">Once upon a time there were three little sisters; and their names were
<a href="http://example.com/elsie" class="sister" id="link1">Elsie</a>,
<a href="http://example.com/lacie" class="sister" id="link2">Lacie</a> and
<a href="http://example.com/tillie" class="sister" id="link3">Tillie</a>;
and they lived at the bottom of a well.</p>

<p class="story">...</p>
"""
```
``` py
from bs4 import BeautifulSoup

soup = BeautifulSoup(html_doc)
type(soup) #bs4.BeautifulSoup
```

``` py
from bs4 import Tag, NavigableString

def print_element(element):
    if isinstance(element, Tag):
        print(f'{type(element).__name__}<{element.name}>')
    if isinstance(element, NavigableString):
        print(type(element).__name__)
```
``` py
element = soup.contents[0]
print_element(element) # Tag<html>
```

``` py
def recursive_DFS(element):
    if isinstance(element, NavigableString):
        print(element, end='')
        return

    for child in element.children:
        recursive_DFS(child)
```
``` py
recursive_DFS(soup)
```
```
The Dormouse's story

The Dormouse's story
Once upon a time there were three little sisters; and their names were
Elsie,
Lacie and
Tillie;
and they lived at the bottom of a well.
...
```

Here is an iterative version of DFS that uses a list to represent a stack of elements:

``` py
def iterative_DFS(root):
    stack = [root]
    
    while(stack):
        element = stack.pop()
        if isinstance(element, NavigableString):
            print(element, end='')
        else:
            children = reversed(element.contents)
            stack.extend(children)
```

The parameter, root, is the root of the tree we want to traverse, so we start by creating the stack and pushing the root onto it.

The loop continues until the stack is empty. Each time through, it pops a PageElement off the stack. If it gets a NavigableString, it prints the contents. Then it pushes the children onto the stack. In order to process the children in the right order, we have to push them onto the stack in reverse order.

``` py
iterative_DFS(soup)
```
```
The Dormouse's story

The Dormouse's story
Once upon a time there were three little sisters; and their names were
Elsie,
Lacie and
Tillie;
and they lived at the bottom of a well.
...
```

## A* Search Algorithm

A* Search algorithm is one of the best and popular technique used in path-finding and graph traversals.

Consider a square grid having many obstacles and we are given a starting cell and a target cell. We want to reach the target cell (if possible) from the starting cell as quickly as possible. Here A* Search Algorithm comes to the rescue.

What A* Search Algorithm does is that at each step it picks the node according to a value-‘f’ which is a parameter equal to the sum of two other parameters – ‘g’ and ‘h’. At each step it picks the node/cell having the lowest ‘f’, and process that node/cell.

f = g + h

g = the movement cost to move from the starting point to a given square on the grid, following the path generated to get there. 
h = the estimated movement cost to move from that given square on the grid to the final destination. This is often referred to as the heuristic, which is nothing but a kind of smart guess. We really don’t know the actual distance until we find the path, because all sorts of things can be in the way (walls, water, etc.). There can be many ways to calculate this ‘h’.

**Algorithm**

We create two lists – Open List and Closed List (just like Dijkstra Algorithm)


```
// A* Search Algorithm
1.  Initialize the open list
2.  Initialize the closed list
    put the starting node on the open 
    list (you can leave its f at zero)

3.  while the open list is not empty
    a) find the node with the least f on 
       the open list, call it "q"

    b) pop q off the open list
  
    c) generate q's 8 successors and set their 
       parents to q
   
    d) for each successor
        i) if successor is the goal, stop search
        
        ii) else, compute both g and h for successor
          successor.g = q.g + distance between 
                              successor and q
          successor.h = distance from goal to 
          successor (This can be done using many 
          ways, we will discuss three heuristics- 
          Manhattan, Diagonal and Euclidean 
          Heuristics)
          
          successor.f = successor.g + successor.h

        iii) if a node with the same position as 
            successor is in the OPEN list which has a 
           lower f than successor, skip this successor

        iV) if a node with the same position as 
            successor  is in the CLOSED list which has
            a lower f than successor, skip this successor
            otherwise, add  the node to the open list
     end (for loop)
  
    e) push q on the closed list
    end (while loop)
```

``` py
from collections import deque
 
class Graph:
    def __init__(self, adjac_lis):
        self.adjac_lis = adjac_lis
 
    def get_neighbors(self, v):
        return self.adjac_lis[v]
 
    # This is heuristic function which is having equal values for all nodes
    def h(self, n):
        H = {
            'A': 1,
            'B': 1,
            'C': 1,
            'D': 1
        }
 
        return H[n]
 
    def a_star_algorithm(self, start, stop):
        # In this open_lst is a lisy of nodes which have been visited, but who's 
        # neighbours haven't all been always inspected, It starts off with the start 
  #node
        # And closed_lst is a list of nodes which have been visited
        # and who's neighbors have been always inspected
        open_lst = set([start])
        closed_lst = set([])
 
        # poo has present distances from start to all other nodes
        # the default value is +infinity
        poo = {}
        poo[start] = 0
 
        # par contains an adjac mapping of all nodes
        par = {}
        par[start] = start
 
        while len(open_lst) > 0:
            n = None
 
            # it will find a node with the lowest value of f() -
            for v in open_lst:
                if n == None or poo[v] + self.h(v) < poo[n] + self.h(n):
                    n = v;
 
            if n == None:
                print('Path does not exist!')
                return None
 
            # if the current node is the stop
            # then we start again from start
            if n == stop:
                reconst_path = []
 
                while par[n] != n:
                    reconst_path.append(n)
                    n = par[n]
 
                reconst_path.append(start)
 
                reconst_path.reverse()
 
                print('Path found: {}'.format(reconst_path))
                return reconst_path
 
            # for all the neighbors of the current node do
            for (m, weight) in self.get_neighbors(n):
              # if the current node is not presentin both open_lst and closed_lst
                # add it to open_lst and note n as it's par
                if m not in open_lst and m not in closed_lst:
                    open_lst.add(m)
                    par[m] = n
                    poo[m] = poo[n] + weight
 
                # otherwise, check if it's quicker to first visit n, then m
                # and if it is, update par data and poo data
                # and if the node was in the closed_lst, move it to open_lst
                else:
                    if poo[m] > poo[n] + weight:
                        poo[m] = poo[n] + weight
                        par[m] = n
 
                        if m in closed_lst:
                            closed_lst.remove(m)
                            open_lst.add(m)
 
            # remove n from the open_lst, and add it to closed_lst
            # because all of his neighbors were inspected
            open_lst.remove(n)
            closed_lst.add(n)
 
        print('Path does not exist!')
        return None
```

``` py
adjac_lis = {
    'A': [('B', 1), ('C', 3), ('D', 7)],
    'B': [('D', 5)],
    'C': [('D', 12)]
}
graph1 = Graph(adjac_lis)
graph1.a_star_algorithm('A', 'D')
```
```
Path found: ['A', 'B', 'D']
['A', 'B', 'D']
```
A-star can be implemented using a priority QUEUE.

``` py
# Credit for this: Nicholas Swift
# as found at https://medium.com/@nicholas.w.swift/easy-a-star-pathfinding-7e6689c7f7b2
from warnings import warn
import heapq

class Node:
    """
    A node class for A* Pathfinding
    """

    def __init__(self, parent=None, position=None):
        self.parent = parent
        self.position = position

        self.g = 0
        self.h = 0
        self.f = 0

    def __eq__(self, other):
        return self.position == other.position
    
    def __repr__(self):
      return f"{self.position} - g: {self.g} h: {self.h} f: {self.f}"

    # defining less than for purposes of heap queue
    def __lt__(self, other):
      return self.f < other.f
    
    # defining greater than for purposes of heap queue
    def __gt__(self, other):
      return self.f > other.f

def return_path(current_node):
    path = []
    current = current_node
    while current is not None:
        path.append(current.position)
        current = current.parent
    return path[::-1]  # Return reversed path


def astar(maze, start, end, allow_diagonal_movement = False):
    """
    Returns a list of tuples as a path from the given start to the given end in the given maze
    :param maze:
    :param start:
    :param end:
    :return:
    """

    # Create start and end node
    start_node = Node(None, start)
    start_node.g = start_node.h = start_node.f = 0
    end_node = Node(None, end)
    end_node.g = end_node.h = end_node.f = 0

    # Initialize both open and closed list
    open_list = []
    closed_list = []

    # Heapify the open_list and Add the start node
    heapq.heapify(open_list) 
    heapq.heappush(open_list, start_node)

    # Adding a stop condition
    outer_iterations = 0
    max_iterations = (len(maze[0]) * len(maze) // 2)

    # what squares do we search
    adjacent_squares = ((0, -1), (0, 1), (-1, 0), (1, 0),)
    if allow_diagonal_movement:
        adjacent_squares = ((0, -1), (0, 1), (-1, 0), (1, 0), (-1, -1), (-1, 1), (1, -1), (1, 1),)

    # Loop until you find the end
    while len(open_list) > 0:
        outer_iterations += 1

        if outer_iterations > max_iterations:
          # if we hit this point return the path such as it is
          # it will not contain the destination
          warn("giving up on pathfinding too many iterations")
          return return_path(current_node)       
        
        # Get the current node
        current_node = heapq.heappop(open_list)
        closed_list.append(current_node)

        # Found the goal
        if current_node == end_node:
            return return_path(current_node)

        # Generate children
        children = []
        
        for new_position in adjacent_squares: # Adjacent squares

            # Get node position
            node_position = (current_node.position[0] + new_position[0], current_node.position[1] + new_position[1])

            # Make sure within range
            if node_position[0] > (len(maze) - 1) or node_position[0] < 0 or node_position[1] > (len(maze[len(maze)-1]) -1) or node_position[1] < 0:
                continue

            # Make sure walkable terrain
            if maze[node_position[0]][node_position[1]] != 0:
                continue

            # Create new node
            new_node = Node(current_node, node_position)

            # Append
            children.append(new_node)

        # Loop through children
        for child in children:
            # Child is on the closed list
            if len([closed_child for closed_child in closed_list if closed_child == child]) > 0:
                continue

            # Create the f, g, and h values
            child.g = current_node.g + 1
            child.h = ((child.position[0] - end_node.position[0]) ** 2) + ((child.position[1] - end_node.position[1]) ** 2)
            child.f = child.g + child.h

            # Child is already in the open list
            if len([open_node for open_node in open_list if child.position == open_node.position and child.g > open_node.g]) > 0:
                continue

            # Add the child to the open list
            heapq.heappush(open_list, child)

    warn("Couldn't get a path to destination")
    return None

def example(print_maze = True):

    maze = [[0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,] * 2,
            [0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,] * 2,
            [0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,] * 2,
            [0,0,0,0,0,0,0,0,0,0,1,1,1,1,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,] * 2,
            [0,0,0,1,1,0,0,1,1,1,1,0,0,0,1,0,0,0,0,0,0,0,0,0,0,0,1,0,0,0,] * 2,
            [0,0,0,1,0,0,0,1,0,0,0,0,0,0,1,0,0,0,0,0,0,0,0,0,0,0,1,0,1,0,] * 2,
            [0,0,0,1,0,1,1,1,1,0,1,1,0,0,1,1,1,0,0,0,1,1,1,1,1,1,1,0,0,0,] * 2,
            [0,0,0,1,0,1,0,0,0,0,0,1,0,0,0,0,1,1,0,1,0,0,0,0,0,0,1,1,1,0,] * 2,
            [0,0,0,1,0,1,1,0,1,1,0,1,1,1,0,0,0,0,0,1,0,0,1,1,1,1,1,0,0,0,] * 2,
            [0,0,0,1,0,1,0,0,0,0,0,0,0,1,1,1,1,1,1,1,0,0,0,0,1,0,1,0,1,1,] * 2,
            [0,0,0,1,0,1,0,1,1,0,1,1,1,1,0,0,1,1,1,1,1,1,1,0,1,0,1,0,0,0,] * 2,
            [0,0,0,1,0,1,0,0,0,0,1,0,0,0,0,0,0,0,0,0,1,0,0,0,1,0,1,1,1,0,] * 2,
            [0,0,0,1,0,1,1,1,1,0,1,0,0,1,1,1,0,1,1,1,1,0,1,1,1,0,1,0,0,0,] * 2,
            [0,0,0,1,0,0,0,0,1,0,0,0,0,0,0,1,0,0,0,0,0,0,0,0,0,0,1,0,1,1,] * 2,
            [0,0,0,1,0,0,0,0,0,0,0,0,1,0,0,0,0,0,1,0,0,0,0,0,0,0,1,0,0,0,] * 2,
            [1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,0,] * 2,]
    
    start = (0, 0)
    end = (len(maze)-1, len(maze[0])-1)

    path = astar(maze, start, end)

    if print_maze:
      for step in path:
        maze[step[0]][step[1]] = 2
      
      for row in maze:
        line = []
        for col in row:
          if col == 1:
            line.append("\u2588")
          elif col == 0:
            line.append(" ")
          elif col == 2:
            line.append(".")
        print("".join(line))

    print(path)
```

![astar](./Images/Astar.gif)