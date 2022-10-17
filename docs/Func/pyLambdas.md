Creating a function normally (using def) assigns it to a variable automatically. This is different from the creation of other objects - such as strings and integers - which can be created on the fly, without assigning them to a variable. The same is possible with functions, provided that they are created using lambda syntax. Functions created this way are known as **anonymous**. This approach is most commonly used when passing a simple function as an argument to another function. The syntax is shown in the next example and consists of the lambda keyword followed by a list of arguments, a colon, and the expression to evaluate and return.

``` py
def my_func(f, arg):
  return f(arg)

my_func(lambda x: 2*x*x, 5)
```
```
50
```
Lambda functions aren't as powerful as named functions. They can only do things that require a single expression - usually equivalent to a single line of code. Lambda functions can be assigned to variables, and used like normal functions.

``` py
#It is usually better to define a function with def instead.
ec=lambda x: x*x*2+4*x+3
print(ec(8))
```
```
163
```