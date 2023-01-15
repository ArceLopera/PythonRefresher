# Other Topics

## Dynamic Programming: Basic

### Climbing Stairs

Asked by Apple and Adobe - 15 min - Easy

You are climbing a staircase that has n steps. You can take the steps either 1 or 2 at a time. Calculate how many distinct ways you can climb to the top of the staircase.

**Example**

For n = 1, the output should be
solution(n) = 1;

For n = 2, the output should be
solution(n) = 2.

You can either climb 2 steps at once or climb 1 step two times.

<details>
  <summary>Click me to view proposed solution</summary>

**Solution**

``` py
def solution(n):
    a, b = 1, 0
    for _ in range(n):
        a, b = a + b, a
    return a
```
</details>

### House Robber

Asked by Linkedin - 20 min - Medium

You are planning to rob houses on a specific street, and you know that every house on the street has a certain amount of money hidden. The only thing stopping you from robbing all of them in one night is that adjacent houses on the street have a connected security system. The system will automatically trigger an alarm if two adjacent houses are broken into on the same night.

Given a list of non-negative integers nums representing the amount of money hidden in each house, determine the maximum amount of money you can rob in one night without triggering an alarm.

**Example**

For nums = [1, 1, 1], the output should be
solution(nums) = 2.

The optimal way to get the most money in one night is to rob the first and the third houses for a total of 2.

<details>
  <summary>Click me to view proposed solution</summary>

**Solutions**

``` py
def solution(nums):
    prev_max = 0
    prev_prev_max = 0
    for n in nums:
        prev_prev_max, prev_max = prev_max, max(prev_prev_max + n, prev_max)
    return prev_max
```

``` py
from functools import lru_cache

def solution(nums):
    return house(tuple(nums))

@lru_cache(maxsize=1000)
def house(nums):
    if len(nums) == 0:
        return 0
    return max(house(nums[1:]), house(nums[2:]) + nums[0])

```
</details>

### Compose Ranges

Asked by Google - 15 min - Easy

Given a sorted integer array that does not contain any duplicates, return a summary of the number ranges it contains.

**Example**

For nums = [-1, 0, 1, 2, 6, 7, 9], the output should be
solution(nums) = ["-1->2", "6->7", "9"].

<details>
  <summary>Click me to view proposed solution</summary>

**Solution**

``` py
def solution(nums):

    ranges = []
    while nums:
        start = end = nums.pop(0)
        while nums and nums[0] - end == 1:
            end = nums.pop(0)
        ranges.append(str(start) + ('', '->' + str(end))[start != end])
    return ranges
```
</details>

### Map Decoding

Asked by Microsoft, Uber and Meta - 30 min - Hard

A top secret message containing uppercase letters from 'A' to 'Z' has been encoded as numbers using the following mapping:
```
'A' -> 1
'B' -> 2
...
'Z' -> 26
```
You are an FBI agent and you need to determine the total number of ways that the message can be decoded.

Since the answer could be very large, take it modulo 109 + 7.

**Example**

For message = "123", the output should be
solution(message) = 3.

"123" can be decoded as "ABC" (1 2 3), "LC" (12 3) or "AW" (1 23), so the total number of ways is 3.

<details>
  <summary>Click me to view proposed solution</summary>

**Solution**

``` py
def solution(msg):
    a, b = 1, 0
    M = 10 ** 9 + 7
    for i in range(len(msg)-1, -1, -1):
        if msg[i] == "0":
            a, b = 0, a
        else:
            a, b = (a + (i+2 <= len(msg) and msg[i:i+2] <= "26") * b) % M, a
    return a

```
</details>

### Filling Blocks

Asked by Uber - 30 min - Hard

You have a block with the dimensions 4 × n. Find the number of different ways you can fill this block with smaller blocks that have the dimensions 1 × 2. You are allowed to rotate the smaller blocks.

**Example**

For n = 1, the output should be
solution(n) = 1.

There is only one possible way to arrange the smaller 1 × 2 blocks inside the 4 × 1 block.

For n = 4, the output should be
solution(n) = 36.

Here are the 36 possible configuration of smaller blocks inside the 4 × 4 block:

![Block](./Images/block.png)

<details>
  <summary>Click me to view proposed solution</summary>

**Solution**

``` py
def solution(n):
    a = [1,1,5,11]
    for i in range(4,n+1):
        a.append(a[i-1]+5*a[i-2]+a[i-3]-a[i-4])
    return a[n]
```
</details>

## Common Techniques : Basic

### Contains Duplicates

Asked by Palantir - 15 min - Easy

Given an array of integers, write a function that determines whether the array contains any duplicates. Your function should return true if any element appears at least twice in the array, and it should return false if every element is distinct.

**Example**

For a = [1, 2, 3, 1], the output should be
solution(a) = true.

There are two 1s in the given array.

For a = [3, 1], the output should be
solution(a) = false.

The given array contains no duplicates.

<details>
  <summary>Click me to view proposed solution</summary>

**Solution**

``` py
def solution(a):
    return len(set(a)) != len(a)
```
</details>

### Sum Of Two

Asked by Google - 20 min - Easy

You have two integer arrays, a and b, and an integer target value v. Determine whether there is a pair of numbers, where one number is taken from a and the other from b, that can be added together to get a sum of v. Return true if such a pair exists, otherwise return false.

**Example**

For a = [1, 2, 3], b = [10, 20, 30, 40], and v = 42, the output should be
solution(a, b, v) = true.

<details>
  <summary>Click me to view proposed solution</summary>

**Solution**

``` py
def solution(a, b, v):
    #No need to iterate a huge list, if the other list is empty
    if not a or not b:
        return False
    
    #kill duplicates
    b = set(b)
    
    #iterate through list a to look if the wanted difference is in b
    for x in a:
        if (v-x) in b:
            return True
    return False
```
</details>

### Sum In Range

Asked by Palantir - 30 min - Medium

You have an array of integers nums and an array queries, where queries[i] is a pair of indices (0-based). Find the sum of the elements in nums from the indices at queries[i][0] to queries[i][1] (inclusive) for each query, then add all of the sums for all the queries together. Return that number modulo 109 + 7.

**Example**

For nums = [3, 0, -2, 6, -3, 2] and queries = [[0, 2], [2, 5], [0, 5]], the output should be
solution(nums, queries) = 10.

The array of results for queries is [1, 3, 6], so the answer is 1 + 3 + 6 = 10

<details>
  <summary>Click me to view proposed solution</summary>

**Solution**

``` py
from itertools import accumulate
def solution(n, q):
    a ,res = tuple(accumulate([0]+n)),0
    for i,j in q:res += a[j+1]-a[i] 
    return res % 1000000007
```
</details>

### Array Max Consecutive Sum 2

Asked by Amazon, LinkedIn, Microsoft, and Samsung - 30 min - Easy

Given an array of integers, find the maximum possible sum you can get from one of its contiguous subarrays. The subarray from which this sum comes must contain at least 1 element.

**Example**

For inputArray = [-2, 2, 5, -11, 6], the output should be
solution(inputArray) = 7.

The contiguous subarray that gives the maximum possible sum is [2, 5], with a sum of 7.

<details>
  <summary>Click me to view proposed solution</summary>

**Solution**

``` py
def solution(inputArray):
    maxsum = inputArray[0]
    l = len(inputArray)
    cumsum = inputArray[0]
    for i in range(1, l):
        cumsum += inputArray[i]
        if inputArray[i] > cumsum:
            cumsum = inputArray[i]
        maxsum = max(maxsum, cumsum)
    return maxsum
```
</details>

### Find Longest Subarray By Sum

Asked by Palantir and Meta - 30 min - Medium

You have an unsorted array arr of non-negative integers and a number s. Find a longest contiguous subarray in arr that has a sum equal to s. Return two integers that represent its inclusive bounds. If there are several possible answers, return the one with the smallest left bound. If there are no answers, return [-1].

Your answer should be 1-based, meaning that the first position of the array is 1 instead of 0.

**Example**

For s = 12 and arr = [1, 2, 3, 7, 5], the output should be
solution(s, arr) = [2, 4].

The sum of elements from the 2nd position to the 4th position (1-based) is equal to 12: 2 + 3 + 7.

For s = 15 and arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10], the output should be
solution(s, arr) = [1, 5].

The sum of elements from the 1st position to the 5th position (1-based) is equal to 15: 1 + 2 + 3 + 4 + 5.

For s = 15 and arr = [1, 2, 3, 4, 5, 0, 0, 0, 6, 7, 8, 9, 10], the output should be
solution(s, arr) = [1, 8].

The sum of elements from the 1st position to the 8th position (1-based) is equal to 15: 1 + 2 + 3 + 4 + 5 + 0 + 0 + 0.

<details>
  <summary>Click me to view proposed solution</summary>

**Solution**

``` py
def solution(s, a):
    total = j = 0
    res = (0,-1)
    for i,v in enumerate(a):
        total += v
        while j<=i and total>s:
            total -= a[j]
            j += 1
        if (total == s) and (res[1]-res[0]<i-j):
            res=(j+1,i+1)
    return res if res[0] else [-1]
```
</details>

### Product Except Self

Asked by Amazon, Linkedin, Meta, Microsoft, and Apple - 30 min - Hard

You have an array nums. We determine two functions to perform on nums. In both cases, n is the length of nums:

fi(nums) = nums[0] · nums[1] · ... · nums[i - 1] · nums[i + 1] · ... · nums[n - 1]. 

(In other words, fi(nums) is the product of all array elements except the ithf.)

g(nums) = f0(nums) + f1(nums) + ... + fn-1(nums).

Using these two functions, calculate all values of f modulo the given m. Take these new values and add them together to get g. You should return the value of g modulo the given m.

**Example**

For nums = [1, 2, 3, 4] and m = 12, the output should be
solution(nums, m) = 2.

The array of the values of f is: [24, 12, 8, 6]. If we take all the elements modulo m, we get:
[0, 0, 8, 6]. The sum of those values is 8 + 6 = 14, making the answer 14 % 12 = 2.

<details>
  <summary>Click me to view proposed solution</summary>

**Solution**

``` py
def solution(nums, m):
  s, p = 0, 1
  for num in nums:
    s, p = (p + s*num) % m, p*num % m
  return s

```
</details>

### Min Substring With All Chars

Asked by Meta - 30 min - Easy

You have two strings, s and t. The string t contains only unique elements. Find and return the minimum consecutive substring of s that contains all of the elements from t.

It's guaranteed that the answer exists. If there are several answers, return the one which starts from the smallest index.

**Example**

For s = "adobecodebanc" and t = "abc", the output should be
solution(s, t) = "banc".

<details>
  <summary>Click me to view proposed solution</summary>

**Solution**

``` py
def solution(s, t):
    result = []
    for i in range(len(s)):
        if s[i] in t:
            coll = set()
            for j in range(i, len(s)):
                if s[j] in t:
                    coll.add(s[j])
                    if len(coll) == len(t):
                        result.append(s[i:j+1])
    if result:
        return min(result, key=len)
    
    return ""
```
</details>