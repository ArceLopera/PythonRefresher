The function enumerate can be used to iterate through the values and indices of a list simultaneously.

Enumerate() method adds a counter to an iterable and returns it in a form of enumerating object. This enumerated object can then be used directly for loops or converted into a list of tuples using the list() method.

``` py
nums=[55,44,33,22,11,]
#Without enumerate use index variable
index = 0
for value in nums:
  print(index, value)
  index += 1
```
```
0 55
1 44
2 33
3 22
4 11
```

``` py
nums=[55,44,33,22,11,]
#Using range and len
for index in range(len(nums)):
  value = nums[index]
  print(index, value)
```
```
0 55
1 44
2 33
3 22
4 11
```

``` py
#using enumarate
nums=[55,44,33,22,11,]
for v in enumerate(nums):
  print(v)
```
```
(0, 55)
(1, 44)
(2, 33)
(3, 22)
(4, 11)
```

``` py
nums=[55,44,33,22,11,]
for i, v in enumerate(nums):
  print(f"value {v} is at {i} position")

```

```
value 55 is at 0 position
value 44 is at 1 position
value 33 is at 2 position
value 22 is at 3 position
value 11 is at 4 position
``` 

``` py
nums=[55,44,33,22,11,]
for i, v in enumerate(nums, start=10):
  print(f"value {v} is at {i} position")
```
```
value 55 is at 10 position
value 44 is at 11 position
value 33 is at 12 position
value 22 is at 13 position
value 11 is at 14 position
```