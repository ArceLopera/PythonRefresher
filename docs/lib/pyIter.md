
The module itertools is a standard library that contains several functions that are useful in functional programming. Advanced iteration functions capabilities for:

+ [Infinite iterators](#infinite-iterators)
+ [Iterators terminating on the shortest input sequence](#iterators-terminating-on-the-shortest-input-sequence)
+ [Combinatoric iterators](#combinatoric-iterators)

## **Infinite iterators**

| Iterator      | Arguments | Syntax      | Example |
| ----------- | ----------- | ----------- | ----------- |
|  [count()](https://docs.python.org/3/library/itertools.html#itertools.count)      | start, [step]       | start, start+step, start+2*step, …      | count(10) --> 10 11 12 13 14 ...       |
| [cycle()](https://docs.python.org/3/library/itertools.html#itertools.cycle)   | p        | p0, p1, … plast, p0, p1, …   | cycle('ABCD') --> A B C D A B C D ...        |
| [repeat()](https://docs.python.org/3/library/itertools.html#itertools.repeat) | elem [,n] | elem, elem, elem, … endlessly or up to n times | repeat(10, 3) --> 10 10 10

* The function [count()](https://docs.python.org/3/library/itertools.html#itertools.count) counts up infinitely from a value.

``` py
from itertools import count
for i in count(3):
  print(i)
  if i>=11:
    break
```
```
3
4
5
6
7
8
9
10
11
```

``` py
import itertools
# use count to create a simple counter
count1 = itertools.count(100, 10)
print(next(count1))
print(next(count1))
print(next(count1))
```
```
100
110
120
```

* The function [cycle()](https://docs.python.org/3/library/itertools.html#itertools.cycle) infinitely iterates through an iterable (for instance a list or string).

``` py
import itertools
# cycle iterator can be used to cycle over a collection
seq1 = ["Joe", "John", "Mike"]
cycle1 = itertools.cycle(seq1)
print(next(cycle1))
print(next(cycle1))
print(next(cycle1))
print(next(cycle1))
```
```
Joe
John
Mike
Joe
```

* The function [repeat()](https://docs.python.org/3/library/itertools.html#itertools.repeat) repeats an object, either infinitely or a specific number of times.

A common use for repeat is to supply a stream of constant values to map or zip

``` py
list(map(pow, range(10), itertools.repeat(2)))
```
```
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```

## Iterators terminating on the shortest input sequence

[All list](https://docs.python.org/3/library/itertools.html)

| Iterator      | Arguments | Syntax      | Example |
| ----------- | ----------- | ----------- | ----------- |
|  [accumulate()](https://docs.python.org/3/library/itertools.html#itertools.accumulate)      | p [,func]      | p0, p0+p1, p0+p1+p2, …     | accumulate([1,2,3,4,5]) --> 1 3 6 10 15      |
|[dropwhile()](https://docs.python.org/3/library/itertools.html#itertools.dropwhile) | pred, seq | seq[n], seq[n+1], starting when pred fails | dropwhile(lambda x: x<5, [1,4,6,4,1]) --> 6 4 1 |
| [takewhile()](https://docs.python.org/3/library/itertools.html#itertools.takewhile)|pred, seq|seq[0], seq[1], until pred fails|takewhile(lambda x: x<5, [1,4,6,4,1]) --> 1 4|
|[chain()](https://docs.python.org/3/library/itertools.html#itertools.chain)|p, q, …|p0, p1, … plast, q0, q1, …|chain('ABC', 'DEF') --> A B C D E F|
|[chain.from_iterable()](https://docs.python.org/3/library/itertools.html#itertools.chain.from_iterable)|iterable|p0, p1, … plast, q0, q1, …|chain.from_iterable(['ABC', 'DEF']) --> A B C D E F|
| [groupby()](https://docs.python.org/3/library/itertools.html#itertools.groupby)|iterable[, key] |sub-iterators grouped by value of key(v) | |
|[zip_longest()](https://docs.python.org/3/library/itertools.html#itertools.zip_longest)|p, q, …|(p[0], q[0]), (p[1], q[1]), …|zip_longest('ABCD', 'xy', fillvalue='-') --> Ax By C- D-|
|[compress()](https://docs.python.org/3/library/itertools.html#itertools.compress)|data, selectors|(d[0] if s[0]), (d[1] if s[1]), …|compress('ABCDEF', [1,0,1,0,1,1]) --> A C E F|
|[filterfalse()](https://docs.python.org/3/library/itertools.html#itertools.filterfalse)|pred, seq|elements of seq where pred(elem) is false|filterfalse(lambda x: x%2, range(10)) --> 0 2 4 6 8|
|[islice()](https://docs.python.org/3/library/itertools.html#itertools.islice)|seq, [start,] stop [, step]|elements from seq[start:stop:step]|islice('ABCDEFG', 2, None) --> C D E F G|
|[pairwise()](https://docs.python.org/3/library/itertools.html#itertools.pairwise)|iterable|(p[0], p[1]), (p[1], p[2])|pairwise('ABCDEFG') --> AB BC CD DE EF FG|
|[starmap()](https://docs.python.org/3/library/itertools.html#itertools.starmap)|func, seq|func(*seq[0]), func(*seq[1]), …|starmap(pow, [(2,5), (3,2), (10,3)]) --> 32 9 1000|
|[tee()](https://docs.python.org/3/library/itertools.html#itertools.tee)|it, n|it1, it2, … itn splits one iterator into n| |


* [accumulate()](https://docs.python.org/3/library/itertools.html#itertools.accumulate) - returns a running total of values in an iterable

``` py
from itertools import accumulate
nums= list(accumulate(range(8)))
print(nums)
```
```
[0, 1, 3, 6, 10, 15, 21, 28]
```

``` py
# accumulate creates an iterator that accumulates values
vals = [10,20,30,40,50,40,30]
acc = itertools.accumulate(vals, max)
print(list(acc))
```
```
[10, 20, 30, 40, 50, 50, 50]
```

*  [takewhile()](https://docs.python.org/3/library/itertools.html#itertools.takewhile) - takes items from an iterable while a predicate function remains true

``` py
from itertools import accumulate, takewhile
nums= list(accumulate(range(8)))
print(nums)
print(list(takewhile(lambda x:x<=6,nums)))
```
```
[0, 1, 3, 6, 10, 15, 21, 28]
[0, 1, 3, 6]
```

*  [dropwhile()](https://docs.python.org/3/library/itertools.html#itertools.dropwhile) - drops elements from the iterable as long as the predicate is true

``` py
# advanced iteration functions in the itertools package
import itertools

def testFunction(x):
    return x < 40


def main():
    
    # dropwhile and takewhile will return values until
    # a certain condition is met that stops them
    print(list(itertools.dropwhile(testFunction, vals)))
    print(list(itertools.takewhile(testFunction, vals)))
    
    
if __name__ == "__main__":
    main()
    
```
```
[40, 50, 40, 30]
[10, 20, 30]
```

* [chain()](https://docs.python.org/3/library/itertools.html#itertools.chain) - combines several iterables into one long one

``` py
# advanced iteration functions in the itertools package

import itertools
def main():
    # use chain to connect sequences together
    x = itertools.chain("ABCD", "1234")
    print(list(x))
    
if __name__ == "__main__":
    main()
    
```
```
['A', 'B', 'C', 'D', '1', '2', '3', '4']
```

## Combinatoric iterators

* [Product](https://docs.python.org/3/library/itertools.html#itertools.product) : cartesian product, equivalent to a nested for-loop

``` py
print(list(itertools.product('ABC', repeat=2)))
```
```
[('A', 'A'), ('A', 'B'), ('A', 'C'), ('B', 'A'), ('B', 'B'), ('B', 'C'), ('C', 'A'), ('C', 'B'), ('C', 'C')]
```

* [Permutations](https://docs.python.org/3/library/itertools.html#itertools.permutations): r-length tuples, all possible orderings, no repeated elements

``` py
print(list(itertools.permutations('ABC', 2)))
```
```
[('A', 'B'), ('A', 'C'), ('B', 'A'), ('B', 'C'), ('C', 'A'), ('C', 'B')]
```


``` py
from itertools import product, permutations
letters=("A","B")
print(list(product(letters,range(2))))
print(list(permutations(letters)))
```
```
[('A', 0), ('A', 1), ('B', 0), ('B', 1)]
[('A', 'B'), ('B', 'A')]
```

* [Combinations](https://docs.python.org/3/library/itertools.html#itertools.combinations) : r-length tuples, in sorted order, no repeated elements

``` py
print(list(itertools.combinations('ABC', 2)))
```
```
[('A', 'B'), ('A', 'C'), ('B', 'C')]
```

* [combinations_with_replacement](https://docs.python.org/3/library/itertools.html#itertools.combinations_with_replacement) : r-length tuples, in sorted order, with repeated elements

``` py
print(list(itertools.combinations_with_replacement('ABC', 2)))
```
```
[('A', 'A'), ('A', 'B'), ('A', 'C'), ('B', 'B'), ('B', 'C'), ('C', 'C')]
```