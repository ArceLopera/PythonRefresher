The else statement is most commonly used along with the if statement, but it can also follow a for or while loop, which gives it a different meaning. With the for or while loop, the code within it is called if the loop finishes normally (when a break statement does not cause an exit from the loop).

``` py
for i in range(10):
  if i==999:
    break
else:
  print("Unbroken 1")  
for i in range(10):
  if i==5:
    break
else:
  print("Unbroken 2")  
```

```
Unbroken 1
```
The else statement can also be used with try/except statements. In this case, the code within it is only executed if no error occurs in the try statement.
``` py
try:
  print(1)
except ZeroDivisionError:
  print(2)
else:
  print(3)

print("*********")
try:
  print(1/0)
except ZeroDivisionError:
  print(2)
else:
  print(3)
```

```
1
3
*********
2
```