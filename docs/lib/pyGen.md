Modules are pieces of code that other people have written to fulfill common tasks, such as generating random numbers, performing mathematical operations, etc. There are three main types of modules in Python, those you write yourself, those you install from external sources, and those that are preinstalled with Python.
The last type is called the [standard library](https://docs.python.org/3/library/), and contains many useful modules. Some of the standard library's useful modules include string, re, datetime, math, random, os, multiprocessing, subprocess, socket, email, json, doctest, unittest, pdb, argparse and sys. 

Many third-party Python modules are stored on the [Python Package Index (PyPI)](https://pypi.org/).

The best way to install these is using a program called pip.
It's important to enter pip commands at the command line, not the Python interpreter.
The basic way to use a module is to add import module_name at the top of your code, and then using module_name.var to access functions and values with the name var in the module. Use a comma separated list to import multiple objects.