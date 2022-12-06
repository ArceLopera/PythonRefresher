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