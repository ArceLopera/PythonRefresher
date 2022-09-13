Python sorted() function returns a sorted list from the iterable object.

Sorted() sorts any sequence (list, tuple) and always returns a list with the elements in a sorted manner, without modifying the original sequence.

``` py
x = [2, 8, 1, 4, 6, 3, 7]

print("Sorted List returned :"),
print(sorted(x))

print("\nReverse sort :"),
print(sorted(x, reverse=True))

print("\nOriginal list not modified :"),
print(x)
```
```
Sorted List returned :
[1, 2, 3, 4, 6, 7, 8]

Reverse sort :
[8, 7, 6, 4, 3, 2, 1]

Original list not modified :
[2, 8, 1, 4, 6, 3, 7]
```
``` py
# List
x = ['q', 'w', 'r', 'e', 't', 'y']
print(f'List : {sorted(x)}')

# Tuple
x = ('q', 'w', 'e', 'r', 't', 'y')
print(f'Tuple : {sorted(x)}')

# String-sorted based on ASCII translations
x = "python"
print(f'String : {sorted(x)}')

# Dictionary
x = {'q': 1, 'w': 2, 'e': 3, 'r': 4, 't': 5, 'y': 6}
print(f'Dict : {sorted(x)}')

# Set
x = {'q', 'w', 'e', 'r', 't', 'y'}
print(f'Set : {sorted(x)}')

# Frozen Set
x = frozenset(('q', 'w', 'e', 'r', 't', 'y'))
print(f'Frozen Set : {sorted(x)}')
```
```
List : ['e', 'q', 'r', 't', 'w', 'y']
Tuple : ['e', 'q', 'r', 't', 'w', 'y']
String : ['h', 'n', 'o', 'p', 't', 'y']
Dict : ['e', 'q', 'r', 't', 'w', 'y']
Set : ['e', 'q', 'r', 't', 'w', 'y']
Frozen Set : ['e', 'q', 'r', 't', 'w', 'y']
```
``` py
L = ["cccc", "b", "dd", "aaa"]

print("Normal sort :", sorted(L))

print("Sort with len :", sorted(L, key=len))
```
```
Normal sort : ['aaa', 'b', 'cccc', 'dd']
Sort with len : ['b', 'dd', 'aaa', 'cccc']
```
``` py
# Sort a list of integers based on
# their remainder on dividing from 7
def func(x):
    return x % 7
 
L = [15, 3, 11, 7]
 
print("Normal sort :", sorted(L))
print("Sorted with key:", sorted(L, key=func))
```
```
Normal sort : [3, 7, 11, 15]
Sorted with key: [7, 15, 3, 11]
```
