Most Python code is either a module to be imported, or a script that does something. However, sometimes it is useful to make a file that can be both imported as a module and run as a script. To do this, place script code inside if name == "main". This ensures that it won't be run if the file is imported. When the Python interpreter reads a source file, it executes all of the code it finds in the file. Before executing the code, it defines a few special variables. For example, if the Python interpreter is running that module (the source file) as the main program, it sets the special name variable to have a value "main". If this file is being imported from another module, name will be set to the module's name.

``` py
def function():
  print("This is a module function!")
if __name__=="__main__":
  print("This is a script")
```
```
This is a script
```

If we save the code from our previous example as a file called example.py, we can then import it to another script as a module, using the name example.

``` py
import example
example.function()
```
And the result will be
```
This is a module function
```

Before executing code, Python interpreter reads source file and define few special variables/global variables. 
If the python interpreter is running that module (the source file) as the main program, it sets the special \__name__ variable to have a value “\__main__”. If this file is being imported from another module, \__name__ will be set to the module’s name. Module’s name is available as value to \__name__ global variable. 

A module is a file containing Python definitions and statements. The file name is the module name with the suffix .py appended.

``` py
# Python program to execute
# function directly
def my_function():
	print ("I am inside function")

# We can test function by calling it.
my_function()
```
Now if we want to use that module by importing we have to comment out our call. Rather than that approach best approach is to use following code:

``` py
# Python program to use
# main for function call.
if __name__ == "__main__":
	my_function()

import myscript

myscript.my_function()
```
Advantages : 

1. Every Python module has it’s \__name__ defined and if this is ‘\__main__’, it implies that the module is being run standalone by the user and we can do corresponding appropriate actions.

2. If you import this script as a module in another script, the \__name__ is set to the name of the script/module.

3. Python files can act as either reusable modules, or as standalone programs.

4. if \__name__ == “main”: is used to execute some code only if the file was run directly, and not imported.