Docstrings (documentation strings) serve a similar purpose to comments, as they are designed to explain code. However, they are more specific and have a different syntax. They are created by putting a multiline string containing an explanation of the function below the function's first line. Unlike conventional comments, docstrings are retained throughout the runtime of the program. This allows the programmer to inspect these comments at run time.

``` py
def sumt(x,y):
  """
  Multiplies by two the sum of parameters

  Parameters
    ----------
    x : int
      First Number.
    y : int
      Second Number.
  Returns
    -------
    z : int
      Result of the operation

  Examples
    --------
    >>> sumt(2, 3)
    12 

  """
  return (x+y)*2
```
The docstring is a triple-quoted string (which may span multiple lines) that comes immediately after the header of a function. When we call help() or .doc on a function, it shows the docstring.

``` py
help(sumt)
```
```
Help on function sumt in module __main__:

sumt(x, y)
    Multiplies by two the sum of parameters
    
    Parameters
      ----------
      x : int
        First Number.
      y : int
        Second Number.
    Returns
      -------
      z : int
        Result of the operation
    
    Examples
      --------
      >>> sumt(2, 3)
      12

```

``` py
print(sumt.__doc__)
```
```
  Multiplies by two the sum of parameters

  Parameters
    ----------
    x : int
      First Number.
    y : int
      Second Number.
  Returns
    -------
    z : int
      Result of the operation

  Examples
    --------
    >>> sumt(2, 3)
    12 
```