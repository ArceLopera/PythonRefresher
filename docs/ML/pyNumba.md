Numba is a just-in-time compiler for Python that works best on code that uses NumPy arrays and functions, and loops. The most common way to use Numba is through its collection of decorators that can be applied to your functions to instruct Numba to compile them. When a call is made to a Numba decorated function it is compiled to machine code “just-in-time” for execution and all or part of your code can subsequently run at native machine code speed!

GPU’s have more cores than CPU and hence when it comes to parallel computing of data, GPUs perform exceptionally better than CPU even though GPU has lower clock speed and it lacks several core managements features as compared to the CPU. Thus, running a python script on GPU can prove out to be comparatively faster than CPU, however, it must be noted that for processing a data set with GPU, the data will first be transferred to the GPU’s memory which may require additional time so if data set is small then GPU may perform better than GPU.

``` py
from numba import jit, cuda
import numpy as np
# to measure exec time
from timeit import default_timer as timer

# normal function to run on cpu
def func(a):							
	for i in range(10000000):
		a[i]+= 1	

# function optimized to run on gpu
@jit(target ="cuda")						
def func2(a):
	for i in range(10000000):
		a[i]+= 1
if __name__=="__main__":
	n = 10000000						
	a = np.ones(n, dtype = np.float64)
	b = np.ones(n, dtype = np.float32)
	
	start = timer()
	func(a)
	print("without GPU:", timer()-start)
	
	start = timer()
	func2(a)
	print("with GPU:", timer()-start)

```
