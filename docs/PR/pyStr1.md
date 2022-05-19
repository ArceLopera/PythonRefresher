**Backslashes** can also be used to escape tabs or arbitrary Unicode characters. \n represents a new line. Similarly, \t represents a tab. Newlines will be automatically added for strings that are created using three quotes. This makes it easier to format long, multi-line texts without the need to explicitly put \n for line breaks.

``` py
print("Hugo\'s house \n Jane\'s mother \t Diana\'s dog")
print("""This
is
multline
text""")
print("That's \"cool\"")
print("Look, a mountain: /\\")
print("1\n2 3")
```
```
Hugo's house 
 Jane's mother 	 Diana's dog
This
is
multline
text
That's "cool"
Look, a mountain: /\
1
2 3
```