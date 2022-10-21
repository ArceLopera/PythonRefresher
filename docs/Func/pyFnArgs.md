Python allows to have function with varying number of arguments. Using *args as a function parameter enables you to pass an arbitrary number of arguments to that function. The arguments are then accessible as the tuple args in the body of the function. The parameter *args must come after the named parameters to a function. The name args is just a convention; you can choose to use another. *args is called an argument list.

``` py
def function(named_args, *args):
  print(named_args)
  print(args)
function(1,2,3,4,5,6,7)
```
```
1
(2, 3, 4, 5, 6, 7)
```

## Default Values

Named parameters to a function can be made optional by giving them a default value. These must come after named parameters without a default value. In case the argument is passed in, the default value is ignored. If the argument is not passed in, the default value is used.

``` py
def function(x,y,food="spam"):
  print(food)

function(1,2)
function(2,3,"eggs")
```
```
spam
eggs
```

## Keyword Arguments

kwargs (standing for keyword arguments) allows you to handle named arguments that you have not defined in advance. The keyword arguments return a **dictionary in which the keys are the argument names, and the values are the argument values.

The arguments returned by **kwargs are not included in *args

``` py
def my_func(x,y=7,*args,**kwargs):
  print(kwargs)
my_func(2,3,4,5,6,a=7,b=8) #a and b are the names of the arguments that we passed to the function call.
```
```
{'a': 7, 'b': 8}
```

## Keyword-only Arguments

These are only specifiable via the name of the argument, and cannot be specified as a positional argument.

For example, the following function takes a positional argument and two keyword-only arguments


``` py
def keyword_only_function(parameter, *, option1=False, option2=''):
    pass
```
In this example, option1, and option2 are only specifiable via the keyword argument syntax. The following is valid

``` py
keyword_only_function(3, option1=True, option2='Hello World!')
```
But this example will raise an error

``` py
keyword_only_function(3, True, 'Hello World!')
```

## Passing Arguments By Value and By Reference

Manipulating provided arguments inside the function will leave immutable arguments intact, but will update mutable arguments. Lists are mutable, int is inmutable. Passing List as arguments is similar to passing by reference. Passing int is similar to passing by value.

``` py
def Func(a,b):
  a=1
  b[0]=1

x=0
y=[0]
Func(x,y)
print(x,y)
```
```
0 [1]
```