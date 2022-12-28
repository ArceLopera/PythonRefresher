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