## Arrays

### First Duplicate

Asked by Google - 15 min - Easy

Given an array a that contains only numbers in the range from 1 to a.length, find the first duplicate number for which the second occurrence has the minimal index. In other words, if there are more than 1 duplicated numbers, return the number for which the second occurrence has a smaller index than the second occurrence of the other number does. If there are no such elements, return -1.

**Example**

For a = [2, 1, 3, 5, 3, 2], the output should be solution(a) = 3.

There are 2 duplicates: numbers 2 and 3. The second occurrence of 3 has a smaller index than the second occurrence of 2 does, so the answer is 3.

For a = [2, 2], the output should be solution(a) = 2;

For a = [2, 4, 3, 5, 1], the output should be solution(a) = -1.

**Solutions**

Solution 1
``` py
def solution(a):
    seen = set()
    for i in a:
        if i in seen:
            return i
        seen.add(i)
    return -1
```

Solution 2
``` py
def solution(a):
    for i in a:
        a[abs(i)-1] *= -1
        if a[abs(i)-1] > 0:
            return abs(i)
    return -1
```

### First Not Repeating Character
Asked by Amazon - 15 min - Easy

Given a string s consisting of small English letters, find and return the first instance of a non-repeating character in it. If there is no such character, return '_'.

**Example**

For s = "abacabad", the output should be
solution(s) = 'c'.

There are 2 non-repeating characters in the string: 'c' and 'd'. Return c since it appears in the string first.

For s = "abacabaabacaba", the output should be
solution(s) = '_'.

There are no characters in this string that do not repeat.

``` py
from collections import Counter
def solution(s):
    st=Counter(s)
    print(st.keys())
    for i in st.keys():
        print(i)
        if st[i] == 1:
            return i
            
    return'_'
```
``` py
def solution(s):
    chk = []
    for i in range(len(s)): 
        if s[i] not in s[i+1:] and s[i] not in chk:
            return s[i]
        chk.append(s[i])
    return '_'
```

### Rotate Image

Asked by Amazon, Microsoft, and Apple - 15 min - Easy

Note: Try to solve this task in-place (with O(1) additional memory), since this is what you'll be asked to do during an interview.

You are given an n x n 2D matrix that represents an image. Rotate the image by 90 degrees (clockwise).

**Example**

For a = [[1, 2, 3],
     [4, 5, 6],
     [7, 8, 9]]
the output should be solution(a) =
    [[7, 4, 1],
     [8, 5, 2],
     [9, 6, 3]]

**Solutions**

``` py
def solution(a):
    a = list(zip(*a))    
    a = [list(l[::-1]) for l in a]
    
    return a
```
``` py
def solution(a):
    return list(zip(*reversed(a)))
```

### Sudoku 2

Asked by Apple and Uber - 30 min - Easy

Sudoku is a number-placement puzzle. The objective is to fill a 9 × 9 grid with numbers in such a way that each column, each row, and each of the nine 3 × 3 sub-grids that compose the grid all contain all of the numbers from 1 to 9 one time.

Implement an algorithm that will check whether the given grid of numbers represents a valid Sudoku puzzle according to the layout rules described above. Note that the puzzle represented by grid does not have to be solvable.

**Example**

For
```
grid = [['.', '.', '.', '1', '4', '.', '.', '2', '.'],
        ['.', '.', '6', '.', '.', '.', '.', '.', '.'],
        ['.', '.', '.', '.', '.', '.', '.', '.', '.'],
        ['.', '.', '1', '.', '.', '.', '.', '.', '.'],
        ['.', '6', '7', '.', '.', '.', '.', '.', '9'],
        ['.', '.', '.', '.', '.', '.', '8', '1', '.'],
        ['.', '3', '.', '.', '.', '.', '.', '.', '6'],
        ['.', '.', '.', '.', '.', '7', '.', '.', '.'],
        ['.', '.', '.', '5', '.', '.', '.', '7', '.']]
```
the output should be
solution(grid) = true;

For
```
grid = [['.', '.', '.', '.', '2', '.', '.', '9', '.'],
        ['.', '.', '.', '.', '6', '.', '.', '.', '.'],
        ['7', '1', '.', '.', '7', '5', '.', '.', '.'],
        ['.', '7', '.', '.', '.', '.', '.', '.', '.'],
        ['.', '.', '.', '.', '8', '3', '.', '.', '.'],
        ['.', '.', '8', '.', '.', '7', '.', '6', '.'],
        ['.', '.', '.', '.', '.', '2', '.', '.', '.'],
        ['.', '1', '.', '2', '.', '.', '.', '.', '.'],
        ['.', '2', '.', '.', '3', '.', '.', '.', '.']]

```
the output should be
solution(grid) = false.

The given grid is not correct because there are two 1s in the second column. Each column, each row, and each 3 × 3 subgrid can only contain the numbers 1 through 9 one time.

**Solution**

``` py

def line_is_valid(row):
    
    tmp_dict = {}    
    valid = True
    
    if len(row) > 0:
        #print(row)
        for r in row:
            if r in tmp_dict:
                tmp_dict[r] += 1
            else:
                tmp_dict[r] = 1
        
        if tmp_dict[max(tmp_dict, key=tmp_dict.get)] > 1:
            valid = False
    
    return valid
                

def grid_is_valid(grid):
    
    valid = True
    
    for i in range(len(grid)):       
        row = [int(x) for x in grid[i] if x != '.']
        #print(row)
        valid = line_is_valid(row)
        if not valid:
            break
                
    return valid

def solution(grid):
    
    result = False
    
    # check rows:
    rows_valid = grid_is_valid(grid)
        
    # check columns:
    col_valid = grid_is_valid(list(zip(*grid)))
          
    # check 3x3 grids:
    grid3x3_valid = True
    for i in range(0,len(grid), 3):
        
        if not grid3x3_valid:
                break
                
        sub_mat = grid[i:i+3]
        
        for j in range(0,len(grid[0]),3):
            
            tmp_list = [x[j:j+3] for x in sub_mat]
            #print(tmp_list)
            tmp_list = [tmp_list[k][l] for k in range(len(tmp_list)) for l in range(len(tmp_list[k]))]
            
            row = [int(x) for x in tmp_list if x != '.']
            grid3x3_valid = line_is_valid(row)
            #print(grid3x3_valid)
            
            if not grid3x3_valid:
                break
        
            
    if rows_valid and col_valid and grid3x3_valid:
        result = True
        
    return result

```

### Is Crypt Solution

Asked by Palantir Solutions - 15 min - Easy

A cryptarithm is a mathematical puzzle for which the goal is to find the correspondence between letters and digits, such that the given arithmetic equation consisting of letters holds true when the letters are converted to digits.

You have an array of strings crypt, the cryptarithm, and an an array containing the mapping of letters and digits, solution. The array crypt will contain three non-empty strings that follow the structure: [word1, word2, word3], which should be interpreted as the word1 + word2 = word3 cryptarithm.

If crypt, when it is decoded by replacing all of the letters in the cryptarithm with digits using the mapping in solution, becomes a valid arithmetic equation containing no numbers with leading zeroes, the answer is true. If it does not become a valid arithmetic solution, the answer is false.

Note that number 0 doesn't contain leading zeroes (while for example 00 or 0123 do).

**Example**

For crypt = ["SEND", "MORE", "MONEY"] and
```
solution = [['O', '0'],
            ['M', '1'],
            ['Y', '2'],
            ['E', '5'],
            ['N', '6'],
            ['D', '7'],
            ['R', '8'],
            ['S', '9']]
```
the output should be
solution(crypt, solution) = true.

When you decrypt "SEND", "MORE", and "MONEY" using the mapping given in crypt, you get 9567 + 1085 = 10652 which is correct and a valid arithmetic equation.

For crypt = ["TEN", "TWO", "ONE"] and
```
solution = [['O', '1'],
            ['T', '0'],
            ['W', '9'],
            ['E', '5'],
            ['N', '4']]
```
the output should be
solution(crypt, solution) = false.

Even though 054 + 091 = 145, 054 and 091 both contain leading zeroes, meaning that this is not a valid solution.

**Solution**

``` py
def solution(crypt, solution):
    # a + b = c
    a = crypt[0]
    b = crypt[1]
    c = crypt[2]
    ch_dict = {}

    for s in solution:
        ch_dict[s[0]] = int(s[1])

    hasLeadingZeros = False
    if ch_dict[a[0]] == 0 or ch_dict[b[0]] == 0 or ch_dict[c[0]] == 0:
        hasLeadingZeros = True

    n1 = ''.join([str(ch_dict[i]) for i in a])
    n2 = ''.join([str(ch_dict[i]) for i in b])
    n3 = ''.join([str(ch_dict[i]) for i in c])

    if int(n1) + int(n2) == int(n3):
        if hasLeadingZeros and int(n3) == 0 and len(n3) == len(str(int(n3))):
            return True
        elif hasLeadingZeros:
            return False
        else:
            return True
    else:
        return False
```

## LinkedLists

### Remove K from List

15 min - Easy

Note: Try to solve this task in O(n) time using O(1) additional space, where n is the number of elements in the list, since this is what you'll be asked to do during an interview.

Given a singly linked list of integers l and an integer k, remove all elements from list l that have a value equal to k.

**Example**

For 
```
l = [3, 1, 2, 3, 4, 5] 
```
and k = 3, the output should be
```
solution(l, k) = [1, 2, 4, 5];
```
For 
```
l = [1, 2, 3, 4, 5, 6, 7] 
```
and k = 10, the output should be
```
solution(l, k) = [1, 2, 3, 4, 5, 6, 7].
```
**Solution**

``` py
# Singly-linked lists are already defined with this interface:
# class ListNode(object):
#   def __init__(self, x):
#     self.value = x
#     self.next = None
#
def solution(l, k):
    if l == None:
        return l
    while l !=  None and l.value == k:
        l = l.next
        
    n = l
     
    while n != None and n.next != None:
        if n.next.value == k:
            n.next = n.next.next
        else:
            n = n.next 
        
    return l

```
### Is List Palindrome

Asked by Amazon and Meta - 30 min - Easy

Note: Try to solve this task in O(n) time using O(1) additional space, where n is the number of elements in l, since this is what you'll be asked to do during an interview.

Given a singly linked list of integers, determine whether or not it's a palindrome.

Note: in examples below and tests preview linked lists are presented as arrays just for simplicity of visualization: in real data you will be given a head node l of the linked list

**Example**

For l = [0, 1, 0], the output should be
solution(l) = true;

For l = [1, 2, 2, 3], the output should be
solution(l) = false.

**Solutions**

``` py
# Definition for singly-linked list:
# class ListNode(object):
#   def __init__(self, x):
#     self.value = x
#     self.next = None
#
def solution(l):
    a = []
    while l != None:
        a.append(l.value)
        l = l.next
    return a == a[::-1]
```

``` py
# Definition for singly-linked list:
# class ListNode(object):
#   def __init__(self, x):
#     self.value = x
#     self.next = None
#
def solution(l):
  if not l or not l.next:
    return True
  s = 1
  n = l
  while n.next:
    n = n.next
    s += 1
  
  middle = s // 2
  
  n = l
  for i in range(middle):
    n = n.next
  
  if s % 2:
    n = n.next
  
  r = n # reverse n
  m = r.next
  for _ in range(middle-1): # flip n
    m.next,r,m = r,m,m.next
  
  for _ in range(middle):
    if r.value != l.value:
      return False
    r = r.next
    l = l.next
  
  return True
```

### Add Two Huge Numbers

30 min - Easy

You're given 2 huge integers represented by linked lists. Each linked list element is a number from 0 to 9999 that represents a number with exactly 4 digits. The represented number might have leading zeros. Your task is to add up these huge integers and return the result in the same format.

**Example**

For a = [9876, 5432, 1999] and b = [1, 8001], the output should be
solution(a, b) = [9876, 5434, 0].

Explanation: 987654321999 + 18001 = 987654340000.

For a = [123, 4, 5] and b = [100, 100, 100], the output should be
solution(a, b) = [223, 104, 105].

Explanation: 12300040005 + 10001000100 = 22301040105.

``` py
# Definition for singly-linked list:
# class ListNode(object):
#   def __init__(self, x):
#     self.value = x
#     self.next = None
#
def solution(a, b):
    a = reverse(a)
    b = reverse(b)
    
    carry = 0
    result = None
    
    while a is not None or b is not None or carry > 0:
        raw = ((a.value if a is not None else 0) + 
               (b.value if b is not None else 0) + 
               carry)
                
        node = ListNode(raw % 10000)
        node.next = result
        
        result = node
        carry = raw // 10000
        
        if a is not None:
            a = a.next
        if b is not None:
            b = b.next
            
    return result
    
def reverse(list):
    current = list
    previous = None
    
    while current is not None:
        previous, current.next, current = current, previous, current.next
        
    return previous
```
### Merge Two LinkedLists

30 min - Medium

Note: Your solution should have O(l1.length + l2.length) time complexity, since this is what you will be asked to accomplish in an interview.

Given two singly linked lists sorted in non-decreasing order, your task is to merge them. In other words, return a singly linked list, also sorted in non-decreasing order, that contains the elements from both original lists.

**Example**

For l1 = [1, 2, 3] and l2 = [4, 5, 6], the output should be
solution(l1, l2) = [1, 2, 3, 4, 5, 6];
For l1 = [1, 1, 2, 4] and l2 = [0, 3, 5], the output should be
solution(l1, l2) = [0, 1, 1, 2, 3, 4, 5].

**Solution**

``` py
# Singly-linked lists are already defined with this interface:
# class ListNode(object):
#   def __init__(self, x):
#     self.value = x
#     self.next = None
#
# Create & Handle List operations
class LinkedList:
    def __init__(self):
        self.head = None
  
    # Method to display the list
    def printList(self):
        temp = self.head
        while temp:
            print(temp.value, end=" ")
            temp = temp.next
  
    # Method to add element to list
    def addToList(self, newData):
        newNode = ListNode(newData)
        if self.head is None:
            self.head = newNode
            return
  
        last = self.head
        while last.next:
            last = last.next
  
        last.next = newNode
  
  
# Function to merge the lists
# Takes two lists which are sorted
# joins them to get a single sorted list
def solution(headA, headB):
  
    # A dummy node to store the result
    dummyNode = ListNode(0)
  
    # Tail stores the last node
    tail = dummyNode
    while True:
  
        # If any of the list gets completely empty
        # directly join all the elements of the other list
        if headA is None:
            tail.next = headB
            break
        if headB is None:
            tail.next = headA
            break
  
        # Compare the data of the lists and whichever is smaller is
        # appended to the last of the merged list and the head is changed
        if headA.value <= headB.value:
            tail.next = headA
            headA = headA.next
        else:
            tail.next = headB
            headB = headB.next
  
        # Advance the tail
        tail = tail.next
  
    # Returns the head of the merged list
    return dummyNode.next
```

### Reverse Nodes in K Groups

45 min - Hard

Note: Your solution should have O(n) time complexity, where n is the number of elements in l, and O(1) additional space complexity, since this is what you would be asked to accomplish in an interview.

Given a linked list l, reverse its nodes k at a time and return the modified list. k is a positive integer that is less than or equal to the length of l. If the number of nodes in the linked list is not a multiple of k, then the nodes that are left out at the end should remain as-is.

You may not alter the values in the nodes - only the nodes themselves can be changed.

**Example**

For l = [1, 2, 3, 4, 5] and k = 2, the output should be
solution(l, k) = [2, 1, 4, 3, 5];
For l = [1, 2, 3, 4, 5] and k = 1, the output should be
solution(l, k) = [1, 2, 3, 4, 5];
For l = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11] and k = 3, the output should be
solution(l, k) = [3, 2, 1, 6, 5, 4, 9, 8, 7, 10, 11].

**Solution**

``` py
# Singly-linked lists are already defined with this interface:
# class ListNode(object):
#   def __init__(self, x):
#     self.value = x
#     self.next = None
#
def solution(l, k):
    if not l:
        return l
    c = l
    n = k
    while c and n:
        c = c.next
        n -= 1
    if n:
        return l
    curr = l
    prev = None
    next = None
    n = k
    while curr and n:
        next = curr.next
        curr.next = prev
        prev = curr
        curr = next
        n -= 1
    if next:
        l.next = solution(next, k)
    return prev
```

### Rearrange Last N

40 min - Hard

Note: Try to solve this task in O(list size) time using O(1) additional space, since this is what you'll be asked during an interview.

Given a singly linked list of integers l and a non-negative integer n, move the last n list nodes to the beginning of the linked list.

**Example**

For l = [1, 2, 3, 4, 5] and n = 3, the output should be
solution(l, n) = [3, 4, 5, 1, 2];
For l = [1, 2, 3, 4, 5, 6, 7] and n = 1, the output should be
solution(l, n) = [7, 1, 2, 3, 4, 5, 6].

**Solution**

``` py
# Singly-linked lists are already defined with this interface:
# class ListNode(object):
#   def __init__(self, x):
#     self.value = x
#     self.next = None
#
def solution(l, n):
    if n == 0:
        return l
    front, back = l, l
    for _ in range(n):
        front = front.next
    if not front:
        return l
    while front.next:
        front = front.next
        back = back.next
    out = back.next
    back.next = None
    front.next = l
    return out
```
