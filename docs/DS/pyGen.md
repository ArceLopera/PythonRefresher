Generators are a type of iterable, like lists or tuples. Unlike lists, they don't allow indexing with arbitrary indices, but they can still be iterated through with for loops. They can be created using functions and the yield statement. The yield statement is used to define a generator, replacing the return of a function to provide a result to its caller without destroying local variables.

Generators are a shortcut to write functions that implement iterators.

``` py
def countdown():
  i=5
  while i>0:
    yield i
    i-=1

for i in countdown():
  print(i)
```

```
5
4
3
2
1
```

Due to the fact that they yield one item at a time, generators don't have the memory restrictions of lists. In fact, they can be infinite! generators allow you to declare a function that behaves like an iterator, i.e. it can be used in a for loop. Finite generators can be converted into lists by passing them as arguments to the list function.Using generators results in improved performance, which is the result of the lazy (on demand) generation of values, which translates to lower memory usage. Furthermore, we do not need to wait until all the elements have been generated before we start to use them.

``` py
def numbers(x):
  for i in range(x):
    if i%2==0:
      yield i
print(list(numbers(11)))
```

```
[0, 2, 4, 6, 8, 10]
```

