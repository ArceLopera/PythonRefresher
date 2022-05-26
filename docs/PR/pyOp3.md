**In-place operators** allow you to write code like 'x = x + 3' more concisely, as 'x += 3'.
In-place operators can be used for any numerical operation (+, -, *, /, %, **, //). These operators can be used on types other than numbers, as well, such as strings.

``` py
x = 2
x+=3
print(x)
x*=7
print(x)
y="spam "
y*=3
print(y)
```

```
5
35
spam spam spam 
```