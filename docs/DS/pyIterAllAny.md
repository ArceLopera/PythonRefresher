Often used in conditional statements, all and any take a list as an argument, and return True if all or any (respectively) of their arguments evaluate to True (and False otherwise).

``` py
nums=[55,44,33,22,11,]

if all([i>5 for i in nums]):
  print("All larger than 5")

if any([i%2 == 0 for i in nums]):
  print("At least one is even")

```

```
All larger than 5
At least one is even
```