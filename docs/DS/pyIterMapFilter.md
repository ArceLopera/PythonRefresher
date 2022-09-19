
The built-in functions map and filter are very useful higher-order functions that operate on lists (or similar objects called iterables).

## Map

The function map takes a function and an iterable as arguments, and returns a new iterable with the function applied to each argument.

``` py
def add_five(x):
  return x+5
nums=[11,22,33,44,55]
result= list(map(add_five,nums))
print(result)
```
```
<class 'list'>
[16, 27, 38, 49, 60]
```
``` py
#the same using lambda syntax
result= list(map(lambda x:x+5,nums))
print(result)
```
```
[16, 27, 38, 49, 60]
```

## Filter

The function filter filters an iterable by removing items that don't match a predicate (a function that returns a Boolean). Like map, the result has to be explicitly converted to a list if you want to print it.

``` py
nums=[11,22,33,44,55]
res= list(filter(lambda x:x%2==0,nums))
print(res)
```

```
[22, 44]
```
``` py
# use transform functions like sorted, filter, map

def filterFunc(x):
    if x % 2 == 0:
        return False
    return True


def filterFunc2(x):
    if x.isupper():
        return False
    return True


def squareFunc(x):
    return x**2


def toGrade(x):
    if (x >= 90):
        return "A"
    elif (x >= 80 and x < 90):
        return "B"
    elif (x >= 70 and x < 80):
        return "C"
    elif (x >= 65 and x < 70):
        return "D"
    return "F"


def main():
    # define some sample sequences to operate on
    nums = (1, 8, 4, 5, 13, 26, 381, 410, 58, 47)
    chars = "abcDeFGHiJklmnoP"
    grades = (81, 89, 94, 78, 61, 66, 99, 74)

    # use filter to remove items from a list
    odds = list(filter(filterFunc, nums))
    print(odds)

    # use filter on non-numeric sequence
    lowers = list(filter(filterFunc2, chars))
    print(lowers)

    # use map to create a new sequence of values
    squares = list(map(squareFunc, nums))
    print(squares)

    # use sorted and map to change numbers to grades
    grades = sorted(grades)
    letters = list(map(toGrade, grades))
    print(letters)


if __name__ == "__main__":
    main()

```
```
[1, 5, 13, 381, 47]
['a', 'b', 'c', 'e', 'i', 'k', 'l', 'm', 'n', 'o']
[1, 64, 16, 25, 169, 676, 145161, 168100, 3364, 2209]
['F', 'D', 'C', 'C', 'B', 'B', 'A', 'A']
```