The help() function is possibly the most important Python function you can learn. If you can remember how to use help(), you hold the key to understanding most other functions.

``` py
help(round)
```
```
Help on built-in function round in module builtins:

round(number, ndigits=None)
    Round a number to a given precision in decimal digits.
    
    The return value is an integer if ndigits is omitted or None.  Otherwise
    the return value has the same type as the number.  ndigits may be negative.
```

You can create your own functions by using the def statement. The code block within every function starts with a colon (:) and is indented. You must define functions before they are called, in the same way that you must assign variables before using them.

``` py
def my_func():
  print("spam ")
  print("spam ")

my_func()

def excla(word):
  print("Spam with " + word + "!")

excla("eggs")

def sumtwice(x,y):
  return (x+y)*2
print(sumtwice(3,4))
```
```
spam 
spam 
Spam with eggs!
14
```