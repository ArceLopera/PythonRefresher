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