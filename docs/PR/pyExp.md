##**Exceptions**
*   ImportError: an import fails;
* IndexError: a list is indexed with an out-of-range number;
* NameError: an unknown variable is used;
* SyntaxError: the code can't be parsed properly;
* TypeError: a function is called on a value of an inappropriate type;
* ValueError: a function is called on a value of the correct type, but with an inappropriate value.

##**Exception Handling**
To handle exceptions, and to call code when an exception occurs, you can use a try/except statement. Multiple exceptions can also be put into a single except block using parentheses, to have the except block handle all of them. An except statement without any exception specified will catch all errors.

##**Finally**
To ensure some code runs no matter what errors occur, you can use a finally statement. The finally statement is placed at the bottom of a try/except statement.

``` py
try:
  a=0
  b=1
  print(a/b)
  #print(b/a)
  print(a+"a")
except ZeroDivisionError:
  print ("Error!")
except (ValueError,TypeError):
  print ("Error 2!")
except:
  print(f'Unknown error: {sys.exc_info()}')
else:
  print('No errors')
finally:
  print("Bye bye")


```

```
0.0
Error 2!
Bye bye
```
##**Raising Exceptions** 
Use raise statement
Exceptions can be raised with arguments that give detail about them.

``` py
print(1)
raise ValueError
print(2)
```
```
1
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
<ipython-input-75-990863ff3a0f> in <module>()
      1 print(1)
----> 2 raise ValueError
      3 print(2)

ValueError: 
```

``` py
try:
  name = "123"
  raise NameError("Invalid Name!")
except NameError as e:
  print(f'Name error: {e}')
print (2)
```
```
Name error: Invalid Name!
2
```