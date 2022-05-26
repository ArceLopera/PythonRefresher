## (Star) \* Operator

The single star * unpacks the sequence/collection into positional arguments, so you can do this:

``` py
def sum(a, b):
    return a + b

values = (1, 2)

s = sum(*values)
print(s)
s = sum(1, 2) #The same
print(s)
```
```
3
3
```
The double star ** does the same, only using a dictionary and thus named arguments:
``` py
values = { 'a': 1, 'b': 2 }
s = sum(**values)
print(s)
```
```
3
```
Combining the two:
``` py
def sum(a, b, c, d):
    return a + b + c + d

values1 = (1, 2)
values2 = { 'c': 10, 'd': 15 }
s = sum(*values1, **values2)
print(s)
# the same as
s = sum(1, 2, c=10, d=15)
print(s)
```

```
28
28
```
Additionally you can define functions to take *x and **y arguments, this allows a function to accept any number of positional and/or named arguments that aren't specifically named in the declaration.

``` py
def sum(*values):
    s = 0
    for v in values:
        s = s + v
    return s

s = sum(1, 2, 3, 4, 5)
print(s)
```

```
15
```
or with **
``` py
def get_a(**values):
    return values['a']

s = get_a(a=1, b=2)      # returns 1
print(s)
```

```
1
```
this can allow you to specify a large number of optional parameters without having to declare them.

And again, you can combine:

``` py
def sum(*values, **options):
    s = 0
    for i in values:
        s = s + i
    if "neg" in options:
        if options["neg"]:
            s = -s
    return s

s = sum(1, 2, 3, 4, 5)            # returns 15
s = sum(1, 2, 3, 4, 5, neg=True)  # returns -15
s = sum(1, 2, 3, 4, 5, neg=False) # returns 15
```
