Modules are pieces of code that other people have written to fulfill common tasks, such as generating random numbers, performing mathematical operations, etc. There are three main types of modules in Python, those you write yourself, those you install from external sources, and those that are preinstalled with Python.
The last type is called the [standard library](https://docs.python.org/3/library/), and contains many useful modules. Some of the standard library's useful modules include [string](https://docs.python.org/3/library/string.html), [re](https://docs.python.org/3/library/re.html), [datetime](https://docs.python.org/3/library/datetime.html), [math](https://docs.python.org/3/library/math.html), [random](https://docs.python.org/3/library/random.html), [os](https://docs.python.org/3/library/os.html), [multiprocessing](https://docs.python.org/3/library/multiprocessing.html), [subprocess](https://docs.python.org/3/library/subprocess.html), [socket](https://docs.python.org/3/library/socket.html), [email](https://docs.python.org/3/library/email.html), [json](https://docs.python.org/3/library/json.html), [doctest](https://docs.python.org/3/library/doctest.html), [unittest](https://docs.python.org/3/library/unittest.html), [pdb](https://docs.python.org/3/library/pdb.html), [argparse](https://docs.python.org/3/library/argparse.html) and [sys](https://docs.python.org/3/library/sys.html). 

[Python 3 Module of the Week](https://pymotw.com/3/) shows how to use the modules of the Python 3 standard library.

 Many third-party Python modules are stored on the [Python Package Index (PyPI)](https://pypi.org/).

The best way to install these is using a program called pip.
It's important to enter pip commands at the command line, not the Python interpreter.
The basic way to use a module is to add import module_name at the top of your code, and then using module_name.var to access functions and values with the name var in the module. Use a comma separated list to import multiple objects.



+ [Text Processing Services](https://docs.python.org/3/library/text.html)
    + [string](../PR/pyStr1.md) — Common string operations
    + [re](../Func/pyRegex.md) — Regular expression operations
+ [Functional Programming Modules](https://docs.python.org/3/library/functional.html)
    + [itertools](pyIter.md) — Functions creating iterators for efficient looping
    + [functools](../Func/pyFnTools.md) — Higher-order functions and operations on callable objects
    + [operator](https://docs.python.org/3/library/operator.html) — Standard operators as functions
+ [DataTypes](https://docs.python.org/3/library/datatypes.html)
    + [datetime](pydatetime.md) — Basic date and time types
    + [calendar](pydatetime.md#calendar) — General calendar-related functions 
    + [Collections](../DS/pyDS.md) — Container datatypes
    + [heapq](../DS/pyHeapQueue.md) — Heap queue algorithm
    + [bisect](../lib/pyBisect.md) — Array bisection algorithm
    + [array](../DS/pyArray.md) — Efficient arrays of numeric values
    + pprint — Data pretty printer
    + [enum](../Cls/pyEnum.md) — Support for enumerations
+ [Numeric and Mathematical Modules](https://docs.python.org/3/library/numeric.html)
    + numbers — Numeric abstract base classes
    + [math](../Func/pyNumFunc.md#mathematical-functions) — Mathematical functions
    + [cmath](../Func/pyNumFunc.md#mathematical-functions) — Mathematical functions for complex numbers
    + [decimal](../PR/pyOp1.md#decimal) — Decimal fixed point and floating point arithmetic
    + fractions — Rational numbers
    + [random](./pyRandom.md) — Generate pseudo-random numbers
    + [statistics](../Func/pyNumFunc.md#statistics) — Mathematical statistics functions
+ [File Management](pyIO.md)
    + [Fast IO](pyIO.md#fast-inputoutput)
    + [OS.path](pyIO.md#os-path-module) — Common pathname manipulations
    + [glob](pyIO.md#glob-module) — Unix style pathname pattern expansion
    + [shutil](pyIO.md#shutil-module-filesystem-shell-methods) — High-level file operations 
    + [PyFileSystem](pyIO.md#pyfilesystem) — Common interface to any filesystem.
+ [Data Persistence](https://docs.python.org/3/library/persistence.html)
    + [pickle](pySerial.md) — Python object serialization
    + [json](pySerial.md#serialization-with-json) — JSON encoder and decoder
    + [csv](pyIO.md#csv-io) — CSV File Reading and Writing 
+ Graphic User Interface
    + [GUI with Tk](https://docs.python.org/3/library/tk.html)
    + [emoji](pyEmoji.md) — Several ways to print emojis
    + [Interactivity with ipywidgets](https://ipywidgets.readthedocs.io/en/latest/) —  Interactive browser controls for Jupyter notebooks
+ [Networking and Internet]()
    + [requests](https://requests.readthedocs.io/en/latest/) — HTTP for humans
    + [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/) — Parsing HTML and XML documents
+ [Machine Learning](../ML/pyGen.md)
    + [Pandas](../ML/pyPandas.md) — Read and manipulate data
    + [Numpy](../ML/pyNumpy.md) — Manipulating lists and tables of numerical data
        + [Numba](../ML/pyNumba.md) — Makes Python code fast
    + [Matplotlib](../ML/pyPlot.md) — For creating static, animated, and interactive visualizations in Python
    + [Scikit-learn](../ML/pyGen.md) — Machine learning in Python
+ Parallel Computing
    + Threads
    + Processes
    + Asyncio
+ [Development Tools](https://docs.python.org/3/library/development.html)
    + [Debugging and Profiling]()
        + pdb — The Python debugger
        + [Time Profiling](pyTimeP.md)
        + [Memory Profiling](pyMemP.md)
    + [Testing Software](pyTest.md)
    + [Logging](pylog.md)
    + [Software Packaging and Distribution](pyPack.md)