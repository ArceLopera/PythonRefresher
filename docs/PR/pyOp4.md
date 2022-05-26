Walrus operator := allows you to assign values to variables within an expression, including variables that do not exist yet. Let's suppose we want to take an integer from the user, assign it to a variable num and output it. The walrus operator accomplishes these operations at once. The walrus operator makes code more readable and can be useful in many situations.

``` py
num=int(input())
print(num)
#The same but using Walrus operator #Python 3.8 up
print(num:=int(input()))
```
