Functions can also be used as arguments of other functions.

``` py
def add(x,y):
  return x+y

def twice(func, x, y):
  return func(func(x,y),func(x,y))

a=2
b=3
print(twice(add,a,b))
```
```
10
```

Functions that operate on other functions are called "higher-order functions." there are higher-order functions built into Python that you might find useful to call.

Here's an interesting example using the max function.

By default, max returns the largest of its arguments. But if we pass in a function using the optional key argument, it returns the argument x that maximizes key(x) (aka the 'argmax').

``` py
def mod_5(x):
    """Return the remainder of x after dividing by 5"""
    return x % 5

print(
    'Which number is biggest?',
    max(100, 51, 14),
    'Which number is the biggest modulo 5?',
    max(100, 51, 14, key=mod_5),
    sep='\n',
)
```
```
Which number is biggest?
100
Which number is the biggest modulo 5?
14
```
