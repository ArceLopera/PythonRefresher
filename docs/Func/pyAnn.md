[PEP 3107](https://www.python.org/dev/peps/pep-3107/)

PEP stands for Python Enhancement Proposal. It is a design document that describes new features for Python or its processes or environment. It also provides information to the python community.

PEP-3107 introduced the concept and syntax for adding arbitrary metadata annotations to Python. There's no preconceived use case, but the PEP suggests several. One very handy one is to allow you to annotate parameters with their expected types; it would then be easy to write a decorator that verifies the annotations or coerces the arguments to the right type. Another is to allow parameter-specific documentation instead of encoding it into the docstring.

Function annotations are only supported in python 3x.

[Details here](https://www.geeksforgeeks.org/function-annotations-python/)

the -> marks the return function annotation.

``` py
def kinetic_energy(m:'in KG', v:'in M/S')->'Joules': 
    return 1/2*m*v**2
 
kinetic_energy.__annotations__
```
```
{'m': 'in KG', 'return': 'Joules', 'v': 'in M/S'}
```
Annotations are dictionaries, so you can do this:
``` py
'{:,} {}'.format(kinetic_energy(12,30),
      kinetic_energy.__annotations__['return'])
```
```
5,400.0 Joules
```
You can also have a python data structure rather than just a string:

``` py
rd={'type':float,'units':'Joules',
    'docstring':'Given mass and velocity returns kinetic energy in Joules'}
def f()->rd:
    pass
```
``` py
f.__annotations__['return']['type']
```
```
float
```

``` py
f.__annotations__['return']['units']
```
```
Joules
```

``` py
f.__annotations__['return']['docstring']
```
```
Given mass and velocity returns kinetic energy in Joules
```

Or, you can use function attributes to validate called values:

``` py
def validate(func, locals):
    for var, test in func.__annotations__.items():
        value = locals[var]
        try: 
            pr=test.__name__+': '+test.__docstring__
        except AttributeError:
            pr=test.__name__   
        msg = '{}=={}; Test: {}'.format(var, value, pr)
        assert test(value), msg

def between(lo, hi):
    def _between(x):
            return lo <= x <= hi
    _between.__docstring__='must be between {} and {}'.format(lo,hi)       
    return _between

def f(x: between(3,10), y:lambda _y: isinstance(_y,int)):
    validate(f, locals())
    print(x,y)

```
``` py
f(2,2) 
```
```
---------------------------------------------------------------------------
AssertionError                            Traceback (most recent call last)
<ipython-input-8-e43489394a12> in <module>()
----> 1 f(2,2)

1 frames
<ipython-input-7-b73806aca747> in validate(func, locals)
      7             pr=test.__name__
      8         msg = '{}=={}; Test: {}'.format(var, value, pr)
----> 9         assert test(value), msg
     10 
     11 def between(lo, hi):

AssertionError: x==2; Test: _between: must be between 3 and 10
```

``` py
f(3,2.1)
```
```
---------------------------------------------------------------------------
AssertionError                            Traceback (most recent call last)
<ipython-input-9-d705e73c1fc6> in <module>()
----> 1 f(3,2.1)

1 frames
<ipython-input-7-b73806aca747> in validate(func, locals)
      7             pr=test.__name__
      8         msg = '{}=={}; Test: {}'.format(var, value, pr)
----> 9         assert test(value), msg
     10 
     11 def between(lo, hi):

AssertionError: y==2.1; Test: <lambda>
```
``` py
f(3,4)
```
```
3 4
```