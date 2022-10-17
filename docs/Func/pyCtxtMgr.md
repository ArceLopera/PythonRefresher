## The **with** Keyword

Context managers are a really helpful structure in Python. Each context manager executes specific code before and after the statements you specify. To use one, you use the with keyword:



```
with <context manager> as <var>:
    <statements>
```


Using with gives you a way to define code to be executed within the context manager’s scope. The most basic example of this is when you’re working with file I/O in Python.

If you wanted to open a file, do something with that file, and then make sure that the file was closed correctly, then you would use a context manager. Consider this example in which names.txt contains a list of names, one per line:

``` py
with open("names.txt") as input_file:
  for name in input_file:
    print(name.strip())
```

The file I/O context manager provided by open() and initiated with the with keyword opens the file for reading, assigns the open file pointer to input_file, then executes whatever code you specify in the with block. Then, after the block is executed, the file pointer closes. Even if your code in the with block raises an exception, the file pointer would still close.

## The **as** Keyword
If you want access to the results of the expression or context manager passed to with, you’ll need to alias it using as. You may have also seen as used to alias imports and exceptions, and this is no different. The alias is available in the with block:

```
with <expr> as <alias>:
    <statements>
```
Most of the time, you’ll see these two Python keywords, with and as, used together.