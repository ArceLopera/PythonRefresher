
del is used in Python to unset a variable or name. You can use it on variable names, but a more common use is to remove indexes from a list or dictionary.

``` py
my_list1 = [1, 2, 3, 4, 5, 6, 7, 8, 9]
print(my_list1)

# delete second element of my_list1
del my_list1[1]
print(my_list1)
# slice my_list1 from index 3 to 5
del my_list1[3:5]
print(my_list1)
```
```
[1, 2, 3, 4, 5, 6, 7, 8, 9]
[1, 3, 4, 5, 6, 7, 8, 9]
[1, 3, 4, 7, 8, 9]
```

``` py
my_dict1 = {"small": "big", "black": "white", "up": "down"}
print(my_dict1)

# delete key-value pair with key "black" from my_dict1
del my_dict1["black"]
print(my_dict1)
```

```
{'small': 'big', 'black': 'white', 'up': 'down'}
{'small': 'big', 'up': 'down'}
```