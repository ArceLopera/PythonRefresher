Oftentimes while programming, one will want to only execute portions of code when certain conditions are met, for instance, when a variable has a certain value. This is accomplished using conditional statements: if, elif, and else. Indentation is used to define the level of nesting, for nested conditionals. Multiple if/else statements make the code long and not very readable. The elif statement is equivalent to an else/if statement. It is used to make the code shorter, more readable, and avoid indentation increase.

``` py
for i in range(10):
    if i % 2 == 0: # % -- modulus operator -- returns the remainder after division
        print("{} is even".format(i))
    else:
        print("{} is odd".format(i))
```

```
0 is even
1 is odd
2 is even
3 is odd
4 is even
5 is odd
6 is even
7 is odd
8 is even
9 is odd
```

``` py
# Example using elif as well
# Print the meteorological season for each month (loosely, of course, and in the Northern Hemisphere)
print("In the Northern Hemisphere: \n")
month_integer = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12] # i.e., January is 1, February is 2, etc...
for month in month_integer:
    if month < 3:
        print("Month {} is in Winter".format(month))
    elif month < 6:
        print("Month {} is in Spring".format(month))
    elif month < 9:
        print("Month {} is in Summer".format(month))
    elif month < 12:
        print("Month {} is in Fall".format(month))
    else: # This will put 12 (i.e., December) into Winter
        print("Month {} is in Winter".format(month))
```

```
In the Northern Hemisphere: 

Month 1 is in Winter
Month 2 is in Winter
Month 3 is in Spring
Month 4 is in Spring
Month 5 is in Spring
Month 6 is in Summer
Month 7 is in Summer
Month 8 is in Summer
Month 9 is in Fall
Month 10 is in Fall
Month 11 is in Fall
Month 12 is in Winter
```

###Ternary operator
Conditional expressions provide the functionality of if statements while using less code. They shouldn't be overused, as they can easily reduce readability, but they are often useful when assigning variables. Conditional expressions are also known as applications of the ternary operator. The ternary operator checks the condition and returns the corresponding value. The ternary operator is so called because, unlike most operators, it takes three arguments.

``` py
a = 3
b=1 if a>=5 else 42
print(b) #42
```
###Match case (Switch)
``` py
##For 3.10 up
value = "one"
match value:
  case "one":
      result = 1
  case "two":
      result = 2
  case "three" | "four":
      result =(3, 4)
  case _:
      result =-1

print(result)
```