###str.format() 

String formatting uses a string's format method to substitute a number of arguments in the string. Each argument of the format function is placed in the string at the corresponding position, which is determined using the curly braces { }.
``` py
# String formatting
nums=[1,2,3]
msg="Numbers {0} {1} {2} ".format(nums[1],nums[0],nums[2])
print(msg)
``` 

``` 
Numbers 2 1 3 
``` 
String formatting can also be done with named arguments.
``` py
a="{x} , {y}".format(y=12,x=4)
print(a)
``` 
``` 
4 , 12
``` 

``` py
x=42
print('The number is {:b}'.format(x))
``` 

``` 
The number is 101010
``` 

- **count(str)** returns how many times the str substring appears in the given string.
- **upper()** converts the string to uppercase.
- **lower()** converts the string to lowercase.
- **replace(old, new)** replaces all occurrences of old with new.
- **len(str)** returns the length of the string (number of characters).

Note, that these functions return a new string with the corresponding manipulation

###**Fstrings (Literal String Interpolation)**
After Python 3.6, to create an f-string, prefix the string with the letter “ f ”. The string itself can be formatted in much the same way that you would with str.format(). F-strings provide a concise and convenient way to embed python expressions inside string literals for formatting. Simply it is a shortcut for the format method.

``` py
# Prints today's date with help
# of datetime library
import datetime
 
today = datetime.datetime.today()
print(f"{today:%B %d, %Y}")
``` 

``` 
July 30, 2021
``` 

``` py
name = "Eric Idle"
f"{name.lower()} is funny."
```

```
eric idle is funny.
```
``` py
x=42
print(f'The number is {x:b}')
```
```
The number is 101010
```
``` py
name = 'CarPool'
age = 23
print(f"Hello, My name is {name} and I'm {age} years old.")
```
``` 
Hello, My name is CarPool and I'm 23 years old.
```

###Template string
``` py
from string import Template

def main():
    # Usual string formatting with format()
    str1 = "Love {0} and {1}".format("Pollo", "Pitas")
    print(str1)
    
    # create a template with placeholders
    templ = Template("Love ${title} and ${author}")
    
    # use the substitute method with keyword arguments
    str2 = templ.substitute(title="Pollo", author="Pitas")
    print(str2)
    
    # use the substitute method with a dictionary
    data = { 
        "author": "Pitas",
        "title": "Pollo"
    }
    str3 = templ.substitute(data)    
    print(str3)

    
if __name__ == "__main__":
    main()
```

```
Love Pollo and Pitas
Love Pollo and Pitas
Love Pollo and Pitas
```