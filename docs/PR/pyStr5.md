

Python contains many useful built-in functions and methods to accomplish common tasks.

### join 
joins a list of strings with another string as a separator.
``` py
print(", ".join(["spam","eggs","ham"]))
```
```
spam, eggs, ham
```
### replace
replaces one substring in a string with another.
``` py
print("Hello Me".replace("Me", "Ham"))
```
```
Hello Ham
```
### startswith and endswith 
determine if there is a substring at the start and end of a string, respectively.

### find and rfind
search for a substr in a larger str. returns the index or -1 if not found. rfind starts from the right end to search. (Use the in operator for boolean result)
``` py
print("Hello Me".find('lo'))
print("Hello Me".find('lop'))
print("Hello Me".rfind('lo'))
print("lo" in "Hello Me")
```
```
3
-1
3
True
```
### lower and upper 
To change the case of a string, you can use lower and upper.
### split 
is the opposite of join turning a string with a certain separator into a list.
``` py
print("spam, eggs, ham".split(", "))
```
```
['spam', 'eggs', 'ham']
```
### count 
to count the number of times a substring is present.
``` py
print("Me Hello Me".count("Me"))
print("Me Hello Me".count("Meh"))
```
```
2
0
```
