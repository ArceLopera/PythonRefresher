# Sorting & Searching

## DFS & BFS

### Traverse Tree

30 min - Easy

Note: Try to solve this task without using recursion, since this is what you'll be asked to do during an interview.

Given a binary tree of integers t, return its node values in the following format:

The first element should be the value of the tree root;
The next elements should be the values of the nodes at height 1 (i.e. the root children), ordered from the leftmost to the rightmost one;
The elements after that should be the values of the nodes at height 2 (i.e. the children of the nodes at height 1) ordered in the same way;
Etc.

**Example**

For
```
t = {
    "value": 1,
    "left": {
        "value": 2,
        "left": null,
        "right": {
            "value": 3,
            "left": null,
            "right": null
        }
    },
    "right": {
        "value": 4,
        "left": {
            "value": 5,
            "left": null,
            "right": null
        },
        "right": null
    }
}
```
the output should be
solution(t) = [1, 2, 4, 3, 5].

This t looks like this:
```
     1
   /   \
  2     4
   \   /
    3 5
```

**Solution**

``` py
#
# Binary trees are already defined with this interface:
# class Tree(object):
#   def __init__(self, x):
#     self.value = x
#     self.left = None
#     self.right = None
def solution(t):
    if t is None:
        return []
    res=[]
    q=[t]
    while q:
        v=q.pop(0)
        res+=[v.value]
        if v.left:
            q += [v.left]
        if v.right:
            q+=[v.right]
    return res

```
### Largest Values In Tree Rows

30 min - Easy

You have a binary tree t. Your task is to find the largest value in each row of this tree. In a tree, a row is a set of nodes that have equal depth. For example, a row with depth 0 is a tree root, a row with depth 1 is composed of the root's children, etc.

Return an array in which the first element is the largest value in the row with depth 0, the second element is the largest value in the row with depth 1, the third element is the largest element in the row with depth 2, etc.

**Example**

For
```
t = {
    "value": -1,
    "left": {
        "value": 5,
        "left": null,
        "right": null
    },
    "right": {
        "value": 7,
        "left": null,
        "right": {
            "value": 1,
            "left": null,
            "right": null
        }
    }
}
```
the output should be solution(t) = [-1, 7, 1].

The tree in the example looks like this:
```
    -1
   / \
  5   7
       \
        1
```
In the row with depth 0, there is only one vertex - the root with value -1;
In the row with depth 1, there are two vertices with values 5 and 7, so the largest value here is 7;
In the row with depth 2, there is only one vertex with value 1.

**Solution**
``` py
# Definition for binary tree:
# class Tree(object):
#   def __init__(self, x):
#     self.value = x
#     self.left = None
#     self.right = None
import math
def solution(t):
    if t is None:
        return []
    stack = [t]
    result = []
    while len(stack) > 0:
        result.append(max(tree.value for tree in stack))
        next_row = [tree.left for tree in stack if tree.left] + [tree.right for tree in stack if tree.right]
        stack = next_row
    return result
```

### Digit Tree Sum

30 min - Medium

We're going to store numbers in a tree. Each node in this tree will store a single digit (from 0 to 9), and each path from root to leaf encodes a non-negative integer.

Given a binary tree t, find the sum of all the numbers encoded in it.

**Example**

For
```
t = {
    "value": 1,
    "left": {
        "value": 0,
        "left": {
            "value": 3,
            "left": null,
            "right": null
        },
        "right": {
            "value": 1,
            "left": null,
            "right": null
        }
    },
    "right": {
        "value": 4,
        "left": null,
        "right": null
    }
}
```
the output should be
solution(t) = 218.
There are 3 numbers encoded in this tree:

Path 1->0->3 encodes 103
Path 1->0->1 encodes 101
Path 1->4 encodes 14
and their sum is 103 + 101 + 14 = 218.
```
t = {
    "value": 0,
    "left": {
        "value": 9,
        "left": null,
        "right": null
    },
    "right": {
        "value": 9,
        "left": {
            "value": 1,
            "left": null,
            "right": null
        },
        "right": {
            "value": 3,
            "left": null,
            "right": null
        }
    }
}
```
the output should be
solution(t) = 193.
Because 09 + 091 + 093 = 193

**Solution**

``` py
# Definition for binary tree:
# class Tree(object):
#   def __init__(self, x):
#     self.value = x
#     self.left = None
#     self.right = None
def solution(t):
    if not t:
        return 0
    
    stack = [(t, 0)]
    sum = 0
    while stack:
        
        cur, v = stack.pop()
        if cur.left or cur.right:
            if cur.left:
                stack.append((cur.left, cur.value + v * 10))
            if cur.right:
                stack.append((cur.right, cur.value + v * 10))
        else:
            sum += cur.value + v * 10
    
    return sum
```

### Longest Path

Asked by Google - 45 min - Hard

Suppose we represent our file system as a string. For example, the string "user\n\tpictures\n\tdocuments\n\t\tnotes.txt" represents:
```
user
    pictures
    documents
        notes.txt    
```
The directory user contains an empty sub-directory pictures and a sub-directory documents containing a file notes.txt.

The string "user\n\tpictures\n\t\tphoto.png\n\t\tcamera\n\tdocuments\n\t\tlectures\n\t\t\tnotes.txt" represents:
```
user
    pictures
        photo.png
        camera
    documents
        lectures
            notes.txt
```
The directory user contains two sub-directories pictures and documents. pictures contains a file photo.png and an empty second-level sub-directory camera. documents contains a second-level sub-directory lectures containing a file notes.txt.

We want to find the longest (as determined by the number of characters) absolute path to a file within our system. For example, in the second example above, the longest absolute path is "user/documents/lectures/notes.txt", and its length is 33 (not including the double quotes).

Given a string representing the file system in this format, return the length of the longest absolute path to a file in the abstracted file system. If there is not a file in the file system, return 0.

Notes:

Due to system limitations, test cases use form feeds ('\f', ASCII code 12) instead of newline characters.
File names do not contain spaces at the beginning.

**Example**

For fileSystem = "user\f\tpictures\f\tdocuments\f\t\tnotes.txt", the output should be
solution(fileSystem) = 24.

The longest path is "user/documents/notes.txt", and it consists of 24 characters.

**Solution**
``` py
def solution(fileSystem):
    maxlen = 0
    pathlen = {0:0}
    for line in fileSystem.splitlines():
        name = line.lstrip('\t')
        depth = len(line)-len(name)
        if '.' in name:
            maxlen = max(maxlen, pathlen[depth]+len(name))
        else:
            pathlen[depth+1] = pathlen[depth] + len(name)+1
    return maxlen
```