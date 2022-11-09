These are almost comprehension, but we don´t want to collect the results in a list, dict or set. Rather, we want to consume them inmediately, one by one. No data structure is created so we save memory and time.

Sum the squares of the first 10 even numbers
``` py
sum(i**2 for i in range(20) if i%2 == 0)
```

```
1140
```

``` py
even = i**2 for i in range(20) if i%2 == 0
```

```
even = i**2 for i in range(20) if i%2 == 0
                  ^
SyntaxError: invalid syntax
```
It needs parentheses!!

``` py
even = (i**2 for i in range(20) if i%2 == 0)
```
What is even? It is a generator object. So it implements the iterator protocol. Therefore, we can used it in loops or feed it to functions like sum that accept iterators.

``` py
even
```

```
<generator object <genexpr> at 0x7f8ff8005cd0>
```

``` py
even.__next__()
```

```
0
```

``` py
even.__next__()
```

```
4
```

``` py
even.__next__()
```

```
16
```
When one line is not sufficient but you still want the convinience of iterators. You can write a function called generator which has the special keyword yield

``` py
def fibonacci() :
  print("Let's get set!")
  f1, f2 =0,1
  while True:
    yield f2

    f1,f2 = f2, f1 + f2

f = fibonacci()

f
```

```
<generator object fibonacci at 0x7f2ec8ba3550>
```

``` py
f.__next__()
f.__next__()
f.__next__()
#the same as
next(f)
next(f)
```

``` py
for x in fibonacci():
  if x>1000:
    break
  print(x)
```

``` 
Let's get set!
1
1
2
3
5
8
13
21
34
55
89
144
233
377
610
987
```

``` py
def fibonacci(fmax) :
  print("Let's get set!")
  f1, f2 =0,1
  while True:
    yield f2

    f1,f2 = f2, f1 + f2

    if f2 > fmax:
      return

[x for x in fibonacci(1000)]
```

```
Let's get set!
[1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377, 610, 987]
```

## Advance concepts for generators

* [Context Managers](../Func/pyCtxtMgr.md)
* [Coroutines](https://www.geeksforgeeks.org/coroutine-in-python/)
