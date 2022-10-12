Unlike Arrays, Linked Lists, Stack and Queues, which are linear data structures, trees are hierarchical data structures. 

Tree Vocabulary: 

+ **Root** The topmost node is called root of the tree. 
+ **Children** The elements that are directly under an element are called its children. 
+ **Parent** The element directly above something is called its parent.
    For example, ‘a’ is a child of ‘f’, and ‘f’ is the parent of ‘a’. 
+ **Leaf** Finally, elements with no children are called leaves.

Main applications of trees include: 
1. Manipulate hierarchical data. 
2. Make information easy to search (see tree traversal). 
3. Manipulate sorted lists of data. 
4. As a workflow for compositing digital images for visual effects. 
5. Router algorithms 
6. Form of a multi-stage decision-making

``` py
# Python program to introduce Binary Tree

# A class that represents an individual node in a
# Binary Tree
class Node:
	def __init__(self,key):
		self.left = None
		self.right = None
		self.val = key


# create root
root = Node(1)
''' following is the tree after above statement
		1
	   / \
	None None'''

root.left	 = Node(2);
root.right	 = Node(3);

''' 2 and 3 become left and right children of 1
		  1
		/   \
	   2     3
	  / \   /  \
  None None None None'''


root.left.left = Node(4);
'''4 becomes left child of 2
		1
	  /	  \
	 2	   3
	/ \	  /  \
   4 None None None
  / \
None None'''
```
