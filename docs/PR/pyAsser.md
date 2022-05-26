An **assertion** is a sanity-check that you can turn on or turn off when you have finished testing the program.
An expression is tested, and if the result comes up false, an exception is raised.
Assertions are carried out through use of the assert statement. Programmers often place assertions at the start of a function to check for valid input, and after a function call to check for valid output.

``` py

print (1)
assert 2 + 2 == 4
print (2)
assert 1 + 1 == 3
print (3)
```
```
1
2
---------------------------------------------------------------------------
AssertionError                            Traceback (most recent call last)
<ipython-input-77-c678df5c3c33> in <module>()
      2 assert 2 + 2 == 4
      3 print (2)
----> 4 assert 1 + 1 == 3
      5 print (3)

AssertionError: 
```

The assert can take a second argument that is passed to the AssertionError raised if the assertion fails. AssertionError exceptions can be caught and handled like any other exception using the try-except statement, but if not handled, this type of exception will terminate the program.

``` py
temp=-10
assert (temp>=0), "Colder than absolute zero!"
```

```
---------------------------------------------------------------------------
AssertionError                            Traceback (most recent call last)
<ipython-input-78-f713a352d793> in <module>()
      1 temp=-10
----> 2 assert (temp>=0), "Colder than absolute zero!"

AssertionError: Colder than absolute zero!
```

