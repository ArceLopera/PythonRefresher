Looping statements allow for the repeated execution of a section of code. For instance, suppose we wanted to add up all of the integers between zero (0) and ten (10), not including ten. We could, of course, do this in one line, but we could also use a loop to add each integer one at a time. Below is the code for a simple accumulator that accomplishes this:

``` py
sum = 0
for i in range(10):
    sum = sum + i
print(sum)
alternative_sum = 0+1+2+3+4+5+6+7+8+9
print(alternative_sum==sum)
```

```
45
True
```
###Range function
The *range*() built-in function generates the sequence of values that we loop over, and notice that range(10) does not include 10 itself. In order to output the range as a list, we need to explicitly convert it to a list, using the list() function. If range is called with one argument, it produces an object with values from 0 to that argument. If it is called with two arguments, it produces values from the first to the second. range can have a third argument, which determines the interval of the sequence produced, also called the step. We can also create list of decreasing numbers, using a negative number as the third argument.

``` py
numbers=list(range(10))
print(numbers)

numbers=list(range(5,10))
print(numbers)

numbers=list(range(5,10,2))
print(numbers)

print(list(range(20, 5, -2)))
```
```
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
[5, 6, 7, 8, 9]
[5, 7, 9]
[20, 18, 16, 14, 12, 10, 8, 6]
```
###elements in lists
In addition to looping over a sequence of integers using the range() function, we can also loop over the elements in a list, which is shown below:

``` py
ingredients = ["flour", "sugar", "eggs", "oil", "baking soda"]
for ingredient in ingredients:
    print(ingredient)
```

```
flour
sugar
eggs
oil
baking soda
```
Above, the for-loop iterates over the elements of the list *ingredients*, and within the loop each of those elements is referred to as *ingredient*. The use of singular/plural nouns to handle this iteration is a common Python motif, but is by no means necessary to use in your own programming. 

###Break and Continue

Similar to while loops, the break and continue statements can be used in for loops, to stop the loop or jump to the next iteration.

``` py
# use the break and continue statements
for x in range(5,10):
    if (x == 7): break
    if (x % 2 == 0): continue
    print (x)
  
  #using the enumerate() function to get index 
days = ["Mon","Tue","Wed","Thu","Fri","Sat","Sun"]
for i, d in enumerate(days):
  print (i, d)
```

```
5
0 Mon
1 Tue
2 Wed
3 Thu
4 Fri
5 Sat
6 Sun
```


``` py

```

```

```