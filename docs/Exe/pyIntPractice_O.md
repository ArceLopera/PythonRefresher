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

**Solution**

``` py
def solution(n):
    a, b = 1, 0
    for _ in range(n):
        a, b = a + b, a
    return a
```
### House Robber

Asked by Linkedin - 20 min - Medium

You are planning to rob houses on a specific street, and you know that every house on the street has a certain amount of money hidden. The only thing stopping you from robbing all of them in one night is that adjacent houses on the street have a connected security system. The system will automatically trigger an alarm if two adjacent houses are broken into on the same night.

Given a list of non-negative integers nums representing the amount of money hidden in each house, determine the maximum amount of money you can rob in one night without triggering an alarm.

**Example**

For nums = [1, 1, 1], the output should be
solution(nums) = 2.

The optimal way to get the most money in one night is to rob the first and the third houses for a total of 2.

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
### Compose Ranges

Asked by Google - 15 min - Easy

Given a sorted integer array that does not contain any duplicates, return a summary of the number ranges it contains.

**Example**

For nums = [-1, 0, 1, 2, 6, 7, 9], the output should be
solution(nums) = ["-1->2", "6->7", "9"].

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