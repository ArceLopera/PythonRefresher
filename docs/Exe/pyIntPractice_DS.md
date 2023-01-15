# Data Structures
## Arrays

### First Duplicate

Asked by Google - 15 min - Easy

Given an array a that contains only numbers in the range from 1 to a.length, find the first duplicate number for which the second occurrence has the minimal index. In other words, if there are more than 1 duplicated numbers, return the number for which the second occurrence has a smaller index than the second occurrence of the other number does. If there are no such elements, return -1.

**Example**

For a = [2, 1, 3, 5, 3, 2], the output should be solution(a) = 3.

There are 2 duplicates: numbers 2 and 3. The second occurrence of 3 has a smaller index than the second occurrence of 2 does, so the answer is 3.

For a = [2, 2], the output should be solution(a) = 2;

For a = [2, 4, 3, 5, 1], the output should be solution(a) = -1.

<details>
  <summary>Click me to view proposed solution</summary>
  
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
</details>

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

<details>
  <summary>Click me to view proposed solution</summary>

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
</details>

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

<details>
  <summary>Click me to view proposed solution</summary>

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
</details>

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

<details>
  <summary>Click me to view proposed solution</summary>

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
</details>

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

<details>
  <summary>Click me to view proposed solution</summary>

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
</details>

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
<details>
  <summary>Click me to view proposed solution</summary>

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
</details>

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

<details>
  <summary>Click me to view proposed solution</summary>

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
</details>

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
<details>
  <summary>Click me to view proposed solution</summary>

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
</details>

### Merge Two LinkedLists

30 min - Medium

Note: Your solution should have O(l1.length + l2.length) time complexity, since this is what you will be asked to accomplish in an interview.

Given two singly linked lists sorted in non-decreasing order, your task is to merge them. In other words, return a singly linked list, also sorted in non-decreasing order, that contains the elements from both original lists.

**Example**

For l1 = [1, 2, 3] and l2 = [4, 5, 6], the output should be
solution(l1, l2) = [1, 2, 3, 4, 5, 6];
For l1 = [1, 1, 2, 4] and l2 = [0, 3, 5], the output should be
solution(l1, l2) = [0, 1, 1, 2, 3, 4, 5].

<details>
  <summary>Click me to view proposed solution</summary>

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
</details>

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

<details>
  <summary>Click me to view proposed solution</summary>

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
</details>

### Rearrange Last N

40 min - Hard

Note: Try to solve this task in O(list size) time using O(1) additional space, since this is what you'll be asked during an interview.

Given a singly linked list of integers l and a non-negative integer n, move the last n list nodes to the beginning of the linked list.

**Example**

For l = [1, 2, 3, 4, 5] and n = 3, the output should be
solution(l, n) = [3, 4, 5, 1, 2];
For l = [1, 2, 3, 4, 5, 6, 7] and n = 1, the output should be
solution(l, n) = [7, 1, 2, 3, 4, 5, 6].

<details>
  <summary>Click me to view proposed solution</summary>

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
</details>

## Hashtables

### Grouping Dishes

Asked by Linkedin - 20 min - Easy

You are given a list dishes, where each element consists of a list of strings beginning with the name of the dish, followed by all the ingredients used in preparing it. You want to group the dishes by ingredients, so that for each ingredient you'll be able to find all the dishes that contain it (if there are at least 2 such dishes).

Return an array where each element is a list beginning with the ingredient name, followed by the names of all the dishes that contain this ingredient. The dishes inside each list should be sorted alphabetically, and the result array should be sorted alphabetically by the names of the ingredients.

**Example**

For
``` py 
  dishes = [["Salad", "Tomato", "Cucumber", "Salad", "Sauce"],
            ["Pizza", "Tomato", "Sausage", "Sauce", "Dough"],
            ["Quesadilla", "Chicken", "Cheese", "Sauce"],
            ["Sandwich", "Salad", "Bread", "Tomato", "Cheese"]]
```
the output should be
``` py 
  solution(dishes) = [["Cheese", "Quesadilla", "Sandwich"],
                      ["Salad", "Salad", "Sandwich"],
                      ["Sauce", "Pizza", "Quesadilla", "Salad"],
                      ["Tomato", "Pizza", "Salad", "Sandwich"]]

```
For

``` py
  dishes = [["Pasta", "Tomato Sauce", "Onions", "Garlic"],
            ["Chicken Curry", "Chicken", "Curry Sauce"],
            ["Fried Rice", "Rice", "Onions", "Nuts"],
            ["Salad", "Spinach", "Nuts"],
            ["Sandwich", "Cheese", "Bread"],
            ["Quesadilla", "Chicken", "Cheese"]]
``` 
the output should be
``` py 
  solution(dishes) = [["Cheese", "Quesadilla", "Sandwich"],
                      ["Chicken", "Chicken Curry", "Quesadilla"],
                      ["Nuts", "Fried Rice", "Salad"],
                      ["Onions", "Fried Rice", "Pasta"]]
```
<details>
  <summary>Click me to view proposed solution</summary>

**Solution**

``` py 
def solution(dishes):
    groups = {}
    for d, *v in dishes:
        for x in v:
            groups.setdefault(x, []).append(d)
    ans = []
    for x in sorted(groups):
        if len(groups[x]) >= 2:
            ans.append([x] + sorted(groups[x]))
    return ans
```
</details>

### Are Following Patterns

Asked by Google - 30 min - Easy

Given an array strings, determine whether it follows the sequence given in the patterns array. In other words, there should be no i and j for which strings[i] = strings[j] and patterns[i] ≠ patterns[j] or for which strings[i] ≠ strings[j] and patterns[i] = patterns[j].

**Example**

For strings = ["cat", "dog", "dog"] and patterns = ["a", "b", "b"], the output should be
solution(strings, patterns) = true;
For strings = ["cat", "dog", "doggy"] and patterns = ["a", "b", "b"], the output should be
solution(strings, patterns) = false.

<details>
  <summary>Click me to view proposed solution</summary>

**Solution**

``` py
def solution(strings, patterns):
    return len(set(strings)) == len(set(patterns)) == len(set(zip(strings, patterns)))

```
</details>

### Contains Close Nuns

Asked by Palantir - 30 min - Medium

Given an array of integers nums and an integer k, determine whether there are two distinct indices i and j in the array where nums[i] = nums[j] and the absolute difference between i and j is less than or equal to k.

Example

For nums = [0, 1, 2, 3, 5, 2] and k = 3, the output should be
solution(nums, k) = true.

There are two 2s in nums, and the absolute difference between their positions is exactly 3.

For nums = [0, 1, 2, 3, 5, 2] and k = 2, the output should be
solution(nums, k) = false.

The absolute difference between the positions of the two 2s is 3, which is more than k.

<details>
  <summary>Click me to view proposed solution</summary>

**Solution**

``` py
def solution(nums, k):
    dct={}#key:number, value:index contains the last occurance index of a number
    if not nums or k==0:
        return False

    for index,num in enumerate(nums):
        try:
            if index-dct[num] <= k:
                return True
        except:
            pass
        dct[num]=index

    return False
```
</details>

### Possible Sums

Asked by Google - 45 min - Hard

You have a collection of coins, and you know the values of the coins and the quantity of each type of coin in it. You want to know how many distinct sums you can make from non-empty groupings of these coins.

**Example**

For coins = [10, 50, 100] and quantity = [1, 2, 1], the output should be
solution(coins, quantity) = 9.

Here are all the possible sums:

```
50 = 50;
10 + 50 = 60;
50 + 100 = 150;
10 + 50 + 100 = 160;
50 + 50 = 100;
10 + 50 + 50 = 110;
50 + 50 + 100 = 200;
10 + 50 + 50 + 100 = 210;
10 = 10;
100 = 100;
10 + 100 = 110.
```
As you can see, there are 9 distinct sums that can be created from non-empty groupings of your coins.

<details>
  <summary>Click me to view proposed solution</summary>

**Solution**

``` py
def solution(coins, quantity):
    possible_sums = {0}
    for c, q in zip(coins, quantity):
        possible_sums = {x + c * i for x in possible_sums for i in range(q + 1)}
    
    return len(possible_sums) - 1
```
</details>

### Swap Lex Order

Asked by Meta - 45 min - Hard

Given a string str and array of pairs that indicates which indices in the string can be swapped, return the lexicographically largest string that results from doing the allowed swaps. You can swap indices any number of times.

**Example**

For str = "abdc" and pairs = [[1, 4], [3, 4]], the output should be
solution(str, pairs) = "dbca".

By swapping the given indices, you get the strings: "cbda", "cbad", "dbac", "dbca". The lexicographically largest string in this list is "dbca".

<details>
  <summary>Click me to view proposed solution</summary>

**Solution**

``` py
def solution(strn, pairs):
    # if not strn or not pairs : return strn
    # check for connected node groupings which can be sorted individually
    grp = {} # set of all possible locations an index could end up
    for a,b in pairs : 
        g = grp.get(a,{a}) | grp.get(b,{b}) 
        for n in g : # reset all nodes in group
            grp[n] = g
    for n in grp : 
        grp[n] = tuple(sorted(grp[n]))
    reord = {}
    for c in set(grp.values())  : 
        word = sorted((strn[i-1] for i in c), reverse = True)
        for i,l in zip(c,word) : 
            reord[i-1] = l # string is 0 indexed
    return ''.join(reord.get(i,x) for i,x in enumerate(strn))
```
</details>

## Trees: Basic

### Has Path With Given Sum

20 min - Easy

Given a binary tree t and an integer s, determine whether there is a root to leaf path in t such that the sum of vertex values equals s.

**Example**

For

```
t = {
    "value": 4,
    "left": {
        "value": 1,
        "left": {
            "value": -2,
            "left": null,
            "right": {
                "value": 3,
                "left": null,
                "right": null
            }
        },
        "right": null
    },
    "right": {
        "value": 3,
        "left": {
            "value": 1,
            "left": null,
            "right": null
        },
        "right": {
            "value": 2,
            "left": {
                "value": -2,
                "left": null,
                "right": null
            },
            "right": {
                "value": -3,
                "left": null,
                "right": null
            }
        }
    }
}
```
and
s = 7,
the output should be solution(t, s) = true.

This is what this tree looks like:
```
      4
     / \
    1   3
   /   / \
  -2  1   2
    \    / \
     3  -2 -3
```
Path 4 -> 3 -> 2 -> -2 gives us 7, the required sum.

For
```
t = {
    "value": 4,
    "left": {
        "value": 1,
        "left": {
            "value": -2,
            "left": null,
            "right": {
                "value": 3,
                "left": null,
                "right": null
            }
        },
        "right": null
    },
    "right": {
        "value": 3,
        "left": {
            "value": 1,
            "left": null,
            "right": null
        },
        "right": {
            "value": 2,
            "left": {
                "value": -4,
                "left": null,
                "right": null
            },
            "right": {
                "value": -3,
                "left": null,
                "right": null
            }
        }
    }
}
```
and
s = 7,
the output should be solution(t, s) = false.

This is what this tree looks like:
```
      4
     / \
    1   3
   /   / \
  -2  1   2
    \    / \
     3  -4 -3
```
There is no path from root to leaf with the given sum 7.

<details>
  <summary>Click me to view proposed solution</summary>

**Solution**
``` py
#
# Definition for binary tree:
# class Tree(object):
#   def __init__(self, x):
#     self.value = x
#     self.left = None
#     self.right = None
def solution(t, s):
    if t is None:
        return s == 0    

    return solution(t.left, s - t.value) or solution(t.right, s - t.value)
```
</details>

### Is Tree Symmetric

Asked by Linkedin and Microsoft - 30 min - Easy

Given a binary tree t, determine whether it is symmetric around its center, i.e. each side mirrors the other.

**Example**

For
```
t = {
    "value": 1,
    "left": {
        "value": 2,
        "left": {
            "value": 3,
            "left": null,
            "right": null
        },
        "right": {
            "value": 4,
            "left": null,
            "right": null
        }
    },
    "right": {
        "value": 2,
        "left": {
            "value": 4,
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
the output should be solution(t) = true.

Here's what the tree in this example looks like:
```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```
As you can see, it is symmetric.

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
        "value": 2,
        "left": null,
        "right": {
            "value": 3,
            "left": null,
            "right": null
        }
    }
}
```
the output should be solution(t) = false.

Here's what the tree in this example looks like:
```
    1
   / \
  2   2
   \   \
   3    3
```
As you can see, it is not symmetric.

<details>
  <summary>Click me to view proposed solution</summary>

**Solutions**

``` py
#
# Definition for binary tree:
# class Tree(object):
#   def __init__(self, x):
#     self.value = x
#     self.left = None
#     self.right = None
def solution(t):
    def mirrorEquals(left,right):
        if left is None or right is None:
            return left == None and right == None
        return left.value == right.value and \
               mirrorEquals(left.left, right.right) and \
               mirrorEquals(left.right, right.left)
    return mirrorEquals(t,t)
```

``` py
def solution(t):
    
    def iTS(le, ri):
        if le is None and ri is None:
            return True
        elif le is None or ri is None:
            return False
        else:
            if le.value == ri.value:
                return iTS(le.left, ri.right) and iTS(le.right, ri.left)
            else:
                return False
    if t is None:
        return True
    else:
        return iTS(t.left, t.right)
```
</details>

### Find Profession

20 min - Easy

Consider a special family of Engineers and Doctors. This family has the following rules:

Everybody has two children.
The first child of an Engineer is an Engineer and the second child is a Doctor.
The first child of a Doctor is a Doctor and the second child is an Engineer.
All generations of Doctors and Engineers start with an Engineer.
We can represent the situation using this diagram:
```
                E
           /         \
          E           D
        /   \        /  \
       E     D      D    E
      / \   / \    / \   / \
     E   D D   E  D   E E   D
```

Given the level and position of a person in the ancestor tree above, find the profession of the person.
Note: in this tree first child is considered as left child, second - as right.

**Example**

For level = 3 and pos = 3, the output should be
solution(level, pos) = "Doctor".

<details>
  <summary>Click me to view proposed solution</summary>

**Solution**
``` py
def solution(level, pos):
    """
    Level 1: E
    Level 2: ED
    Level 3: EDDE
    Level 4: EDDEDEED
    Level 5: EDDEDEEDDEEDEDDE 
    
    Level input is not necessary because first elements are the same
    The result is based on the count of 1's in binary representation of position-1
    If position is even, then Engineer; Else Doctor
    """
    bits  = bin(pos-1).count('1')
    if bits%2 == 0: 
        return "Engineer"
    else:
        return "Doctor"
```
</details>

### Kth Smallest in BST

30 min - Medium

Note: Your solution should have only one BST traversal and O(1) extra space complexity, since this is what you will be asked to accomplish in an interview.

A tree is considered a binary search tree (BST) if for each of its nodes the following is true:

The left subtree of a node contains only nodes with keys less than the node's key.
The right subtree of a node contains only nodes with keys greater than the node's key.
Both the left and the right subtrees must also be binary search trees.
Given a binary search tree t, find the kth smallest element in it.

Note that kth smallest element means kth element in increasing order. See examples for better understanding.

**Example**

For
```
t = {
    "value": 3,
    "left": {
        "value": 1,
        "left": null,
        "right": null
    },
    "right": {
        "value": 5,
        "left": {
            "value": 4,
            "left": null,
            "right": null
        },
        "right": {
            "value": 6,
            "left": null,
            "right": null
        }
    }
}
```
and k = 4, the output should be
solution(t, k) = 5.

Here is what t looks like:
```
   3
 /   \
1     5
     / \
    4   6
```
The values of t are [1, 3, 4, 5, 6], and the 4th smallest is 5.

For
```
t = {
    "value": 1,
    "left": {
        "value": -1,
        "left": {
            "value": -2,
            "left": null,
            "right": null
        },
        "right": {
            "value": 0,
            "left": null,
            "right": null
        }
    },
    "right": null
}
```
and k = 1, the output should be
solution(t, k) = -2.

Here is what t looks like:
```
     1
    /
  -1
  / \
-2   0
```
The values of t are [-2, -1, 0, 1], and the 1st smallest is -2.

<details>
  <summary>Click me to view proposed solution</summary>

**Solution**
``` py
#
# Definition for binary tree:
# class Tree(object):
#   def __init__(self, x):
#     self.value = x
#     self.left = None
#     self.right = None
def solution(root, K):
    def dfs(node):
        if node:
            yield from dfs(node.left)
            yield node.value
            yield from dfs(node.right)
    
    f = dfs(root)
    for _ in range(K):
        ans = next(f)
    return ans
```

``` py
#
# Definition for binary tree:
# class Tree(object):
#   def __init__(self, x):
#     self.value = x
#     self.left = None
#     self.right = None
def solution(t, k):
    # Morris in-order traversal (O(1) memory usage)
    # https://www.youtube.com/watch?v=wGXB9OWhPTg explains this pretty well
    
    current = t
    
    while current:
        if not current.left:
            k -= 1
            if k == 0:
                return current.value
            
            current = current.right
        else:
            predecessor = find_predecessor(current)
            if not predecessor.right:
                predecessor.right = current
                current = current.left
            else:
                predecessor.right = None
                k -= 1
                if k == 0:
                    return current.value
                current = current.right
                
                
    return None
         
def find_predecessor(t):
    # Go left once, then right as much times as possible
    predecessor = t.left
    
    while predecessor.right and predecessor.right != t:
        predecessor = predecessor.right
        
    return predecessor
```
</details>

### Is Subtree

30 min - Medium

Given two binary trees t1 and t2, determine whether the second tree is a subtree of the first tree. A subtree for vertex v in a binary tree t is a tree consisting of v and all its descendants in t. Determine whether or not there is a vertex v (possibly none) in tree t1 such that a subtree for vertex v (possibly empty) in t1 equals t2.

**Example**

For
```
t1 = {
    "value": 5,
    "left": {
        "value": 10,
        "left": {
            "value": 4,
            "left": {
                "value": 1,
                "left": null,
                "right": null
            },
            "right": {
                "value": 2,
                "left": null,
                "right": null
            }
        },
        "right": {
            "value": 6,
            "left": null,
            "right": {
                "value": -1,
                "left": null,
                "right": null
            }
        }
    },
    "right": {
        "value": 7,
        "left": null,
        "right": null
    }
}
```
and
```
t2 = {
    "value": 10,
    "left": {
        "value": 4,
        "left": {
            "value": 1,
            "left": null,
            "right": null
        },
        "right": {
            "value": 2,
            "left": null,
            "right": null
        }
    },
    "right": {
        "value": 6,
        "left": null,
        "right": {
            "value": -1,
            "left": null,
            "right": null
        }
    }
}
```
the output should be solution(t1, t2) = true.

This is what these trees look like:
```
      t1:             t2:
       5              10
      / \            /  \
    10   7          4    6
   /  \            / \    \
  4    6          1   2   -1
 / \    \
1   2   -1
```
As you can see, t2 is a subtree of t1 (the vertex in t1 with value 10).

For
```
t1 = {
    "value": 5,
    "left": {
        "value": 10,
        "left": {
            "value": 4,
            "left": {
                "value": 1,
                "left": null,
                "right": null
            },
            "right": {
                "value": 2,
                "left": null,
                "right": null
            }
        },
        "right": {
            "value": 6,
            "left": {
                "value": -1,
                "left": null,
                "right": null
            },
            "right": null
        }
    },
    "right": {
        "value": 7,
        "left": null,
        "right": null
    }
}
```
and
```
t2 = {
    "value": 10,
    "left": {
        "value": 4,
        "left": {
            "value": 1,
            "left": null,
            "right": null
        },
        "right": {
            "value": 2,
            "left": null,
            "right": null
        }
    },
    "right": {
        "value": 6,
        "left": null,
        "right": {
            "value": -1,
            "left": null,
            "right": null
        }
    }
}
```
the output should be solution(t1, t2) = false.

This is what these trees look like:
```
        t1:            t2:
         5             10
       /   \          /  \
     10     7        4    6
   /    \           / \    \
  4     6          1   2   -1
 / \   / 
1   2 -1
```
As you can see, there is no vertex v such that the subtree of t1 for vertex v equals t2.

For
```
t1 = {
    "value": 1,
    "left": {
        "value": 2,
        "left": null,
        "right": null
    },
    "right": {
        "value": 2,
        "left": null,
        "right": null
    }
}
```
and
```
t2 = {
    "value": 2,
    "left": {
        "value": 1,
        "left": null,
        "right": null
    },
    "right": null
}
```
the output should be solution(t1, t2) = false.

<details>
  <summary>Click me to view proposed solution</summary>

**Solution**
``` py
#
# Definition for binary tree:
# class Tree(object):
#   def __init__(self, x):
#     self.value = x
#     self.left = None
#     self.right = None
from functools import reduce

def solution(t1, t2):
    if not t2:
        return True
    if not t1:
        return False
    
    return equals(t1, t2) or solution(t1.left, t2) or solution(t1.right, t2)

def equals(t1, t2):
    if not t1 and not t2:
        return True
    if not t1 or not t2:
        return False
    if t1.value == t2.value:
        return equals(t1.left, t2.left) and equals(t1.right, t2.right)
    return False
```
</details>

### Restore Binary Tree

40 min - Hard

Note: Your solution should have O(inorder.length) time complexity, since this is what you will be asked to accomplish in an interview.

Let's define inorder and preorder traversals of a binary tree as follows:

Inorder traversal first visits the left subtree, then the root, then its right subtree;
Preorder traversal first visits the root, then its left subtree, then its right subtree.
For example, if tree looks like this:
```
    1
   / \
  2   3
 /   / \
4   5   6
```
then the traversals will be as follows:

Inorder traversal: [4, 2, 1, 5, 3, 6]

Preorder traversal: [1, 2, 4, 3, 5, 6]

Given the inorder and preorder traversals of a binary tree t, but not t itself, restore t and return it.

**Example**

For inorder = [4, 2, 1, 5, 3, 6] and preorder = [1, 2, 4, 3, 5, 6], the output should be

```
solution(inorder, preorder) = {
    "value": 1,
    "left": {
        "value": 2,
        "left": {
            "value": 4,
            "left": null,
            "right": null
        },
        "right": null
    },
    "right": {
        "value": 3,
        "left": {
            "value": 5,
            "left": null,
            "right": null
        },
        "right": {
            "value": 6,
            "left": null,
            "right": null
        }
    }
}
```
For inorder = [2, 5] and preorder = [5, 2], the output should be
```
solution(inorder, preorder) = {
    "value": 5,
    "left": {
        "value": 2,
        "left": null,
        "right": null
    },
    "right": null
}
```
<details>
  <summary>Click me to view proposed solution</summary>

**Solution**

``` py
#
# Definition for binary tree:
# class Tree(object):
#   def __init__(self, x):
#     self.value = x
#     self.left = None
#     self.right = None
def solution(inorder, preorder):
  if not preorder:
    return None
  root = Tree(preorder[0])
  i = inorder.index(preorder[0])
  root.left = solution(inorder[:i], preorder[1:i+1])
  root.right = solution(inorder[i+1:],preorder[i+1:])
  return root
```
</details>

### Find Substrings

Asked by Uber - 40 min - Hard

You have two arrays of strings, words and parts. Return an array that contains the strings from words, modified so that any occurrences of the substrings from parts are surrounded by square brackets [], following these guidelines:

If several parts substrings occur in one string in words, choose the longest one. If there is still more than one such part, then choose the one that appears first in the string.

**Example**

For words = ["Apple", "Melon", "Orange", "Watermelon"] and parts = ["a", "mel", "lon", "el", "An"], the output should be
solution(words, parts) = ["Apple", "Me[lon]", "Or[a]nge", "Water[mel]on"].

While "Watermelon" contains three substrings from the parts array, "a", "mel", and "lon", "mel" is the longest substring that appears first in the string.

<details>
  <summary>Click me to view proposed solution</summary>

**Solution**

``` py
class Trie(object):
    def __init__(self):
        self.nxt = {}
        self.end = False

    def add(self, word):
        if not word:
            self.end = True
        else:
            self.nxt.setdefault(word[0], Trie()).add(word[1:])


def solution(words, parts):
    trie = Trie()
    for x in parts:
        trie.add(x)
    for i, w in enumerate(words):
        pos = len(w)
        L = -1
        for j in range(len(w)):
            t = trie
            k = j
            while k < len(w) and w[k] in t.nxt:
                t = t.nxt[w[k]]
                k += 1
                if t.end and k - j > L:
                    L = k - j
                    pos = j
        if L > 0:
            words[i] = "%s[%s]%s" % (w[:pos], w[pos:pos+L], w[pos+L:])
    return words
```
</details>

### Delete From BST

30 min - Medium

A tree is considered a binary search tree (BST) if for each of its nodes the following is true:

The left subtree of a node contains only nodes with keys less than the node's key.
The right subtree of a node contains only nodes with keys greater than the node's key.
Both the left and the right subtrees must also be binary search trees.
Removing a value x from a BST t is done in the following way:

If there is no x in t, nothing happens;
Otherwise, let t' be a subtree of t such that t'.value = x.
If t' has a left subtree, remove the rightmost node from it and put it at the root of t';
Otherwise, remove the root of t' and its right subtree becomes the new t's root.
For example, removing 4 from the following tree has no effect because there is no such value in the tree:
```
    5
   / \
  2   6
 / \   \
1   3   8
       /
      7
```
Removing 5 causes 3 (the rightmost node in left subtree) to move to the root:
```
    3
   / \
  2   6
 /     \
1       8
       /
      7
```
And removing 6 after that creates the following tree:
```
    3
   / \
  2   8
 /   /
1   7
```
You're given a binary search tree t and an array of numbers queries. Your task is to remove queries[0], queries[1], etc., from t, step by step, following the algorithm above. Return the resulting BST.

**Example**

For
```
t = {
    "value": 5,
    "left": {
        "value": 2,
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
    },
    "right": {
        "value": 6,
        "left": null,
        "right": {
            "value": 8,
            "left": {
                "value": 7,
                "left": null,
                "right": null
            },
            "right": null
        }
    }
}
```
and queries = [4, 5, 6], the output should be
```
solution(t, queries) = {
    "value": 3,
    "left": {
        "value": 2,
        "left": {
            "value": 1,
            "left": null,
            "right": null
        },
        "right": null
    },
    "right": {
        "value": 8,
        "left": {
            "value": 7,
            "left": null,
            "right": null
        },
        "right": null
    }
}
```
<details>
  <summary>Click me to view proposed solution</summary>

**Solution**

``` py
#
# Definition for binary tree:
# class Tree(object):
#   def __init__(self, x):
#     self.value = x
#     self.left = None
#     self.right = None
def solution(t, queries):
    
    def max_of_tree(t):
        if t is None: return(None)
        while t.right is not None:
            t = t.right
        return(t.value)

    def remove_right(t):
        if t.right is None:
            return(t.left)
        else:
            t.right = remove_right(t.right)
        return(t)

    def f1(t, q):
        if t is None: return(None)
        if q == t.value:
            if t.left:
                t.value = max_of_tree(t.left)
                t.left = remove_right(t.left)
            else:
                t = t.right
        elif q < t.value:
            t.left = f1(t.left, q)
        elif q > t.value:
            t.right = f1(t.right, q)
        return(t)

    for q in queries:
        t = f1(t, q)

    return(t)
```
</details>