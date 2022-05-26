**The Operator, @**

In the context of matrix multiplication, a @ b invokes **a.\_\_matmul\_\_(b)** - making this syntax:

`a @ b`

equivalent to

`dot(a, b)`

and

`a @= b`

equivalent to

`a = dot(a, b)`

where dot is, for example, the numpy matrix multiplication function and a and b are matrices.