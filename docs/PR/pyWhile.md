
A while loop is used to repeat a block of code multiple times. The while loop is used in cases when the number of iterations is not known and depends on some calculations and conditions in the code block of the loop. To end a while loop prematurely, the break statement can be used. Another statement that can be used within loops is continue. Unlike break, continue jumps back to the top of the loop, rather than stopping it. Basically, the continue statement stops the current iteration and continues with the next one.

``` py
i=1
while i <=5:
  print(i)
  i+=1
print("the end")
```

```
1
2
3
4
5
the end
```