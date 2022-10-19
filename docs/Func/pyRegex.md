Regular expressions are a powerful tool for various kinds of string manipulation.
They are a domain specific language (DSL) that is present as a library in most modern programming languages, not just Python.

They are useful for two main tasks:
- verifying that strings match a pattern (for instance, that a string has the format of an email address),
- performing substitutions in a string (such as changing all American spellings to British ones).

Domain specific languages are highly specialized mini programming languages.
Regular expressions are a popular example, and SQL (for database manipulation) is another.
Private domain-specific languages are often used for specific industrial purposes.

Regular expressions in Python can be accessed using the re module, which is part of the standard library.
After you've defined a regular expression, the re.match function can be used to determine whether it matches at the beginning of a string.
If it does, match returns an object representing the match, if not, it returns None.
To avoid any confusion while working with regular expressions, we would use raw strings as r"expression".
Raw strings don't escape anything, which makes use of regular expressions easier.

``` py
import re
pattern = r"spam"
if re.match(pattern,"spamspamspam"):
  print("Match")
else:
  print("No match")
```
```
Match
```

* The function re.search finds a match of a pattern anywhere in the string.
* The function re.findall returns a list of all substrings that match a pattern.
+ The function re.finditer does the same thing as re.findall, except it returns an iterator, rather than a list.

``` py
import re
pattern = r"spam"
if re.match(pattern,"eggspamsausagespam"):
  print("Match")
else:
  print("No match")
if re.search(pattern,"eggspamsausagespam"):
  print("Match")
else:
  print("No match")
print(re.findall(pattern,"eggspamsausagespam"))
```
```
No match
Match
['spam', 'spam']
```
The regex search returns an object with several methods that give details about it. These methods include group which returns the string matched, start and end which return the start and ending positions of the first match, and span which returns the start and end positions of the first match as a tuple.

``` py
import re
pattern = r"pam"
match = re.search(pattern,"eggspamsausage")
if match:
  print(match.group())
  print(match.start())
  print(match.end())
  print(match.span())
```
```
pam
4
7
(4, 7)
```

One of the most important re methods that use regular expressions is sub.

``` re.sub(pattern, repl, string, count=0) ```

This method replaces all occurrences of the pattern in string with repl, substituting all occurrences, unless count provided. This method returns the modified string.



``` py
import re
hello="My name is Carlos, Hi Carlos"
pattern=r"Carlos"
newstr=re.sub(pattern,"Diana",hello, count =1)
print(newstr)
```
```
My name is Diana, Hi Carlos
```
## Metacharacters

Metacharacters are what make regular expressions more powerful than normal string methods.
They allow you to create regular expressions to represent concepts like "one or more repetitions of a vowel".

The existence of metacharacters poses a problem if you want to create a regular expression (or regex) that matches a literal metacharacter, such as "$". You can do this by escaping the metacharacters by putting a backslash in front of them.
However, this can cause problems, since backslashes also have an escaping function in normal Python strings. This can mean putting three or four backslashes in a row to do all the escaping.

To avoid this, you can use a raw string, which is a normal string with an "r" in front of it.

*  . (dot) : This matches any character, other than a new line.
*  ^ and $ : These match the start and end of a string, respectively.


``` py
import re

pattern=r"gr.y"
pattern2=r"...." #Any four character string with no newlines
patt3 = r"^gr.y$"

if re.match(pattern,"grey"):
  print("Match 1")
if re.match(pattern,"gray"):
  print("Match 2")
if re.match(pattern,"blue"):
  print("Match 3")
if re.match(patt3,"gray"):
  print("Match 4")
if re.match(patt3,"Stingray"):
  print("Match 5")
```
```
Match 1
Match 2
Match 4
```
## Character Classes

Character classes provide a way to match only one of a specific set of characters. A character class is created by putting the characters it matches inside square brackets. The pattern [aeiou] in the search function matches all strings that contain any one of the characters defined.


``` py
import re
patt=r"[aeiou]"
if re.search(patt,"grey"):
  print("Match 1")
if re.search(patt,"qwertyuiop"):
  print("Match 2")
if re.search(patt,"rhythm myths"):
  print("Match 3")
```
```
Match 1
Match 2
```
Character classes can also match ranges of characters. Some examples: The class [a-z] matches any lowercase alphabetic character. The class [G-P] matches any uppercase character from G to P. The class [0-9] matches any digit. Multiple ranges can be included in one class. For example, [A-Za-z] matches a letter of any case.

``` py
import re
#strings that contain two alphabetic uppercase letters followed by a digit.
patt=r"[A-Z][A-Z][0-9]"
if re.search(patt,"LS8"):
  print("Match 1")
if re.search(patt,"E3"):
  print("Match 2")
if re.search(patt,"1ab"):
  print("Match 3")
```
```
Match 1
```
Place a ^ at the start of a character class to invert it. This causes it to match any character other than the ones included. Other metacharacters such as $ and ., have no meaning within character classes. The metacharacter ^ has no meaning unless it is the first character in a class.

The pattern [^A-Z] excludes uppercase strings. Note, that the ^ should be inside the brackets to invert the character class.

``` py
import re
patt=r"[^A-Z]"
if re.search(patt,"this is all quiet"):
  print("Match 1")
if re.search(patt,"E31hsDD"):
  print("Match 2")
if re.search(patt,"SHOUT"):
  print("Match 3")
```
```
Match 1
Match 2
```
## Metacharacters for Repetition

Some more metacharacters are * + ? { and }.
These specify numbers of repetitions.
* The metacharacter * means "zero or more repetitions of the previous thing". It tries to match as many repetitions as possible. The "previous thing" can be a single character, a class, or a group of characters in parentheses. * matches 0 or more occurrences of the preceding expression.
* The metacharacter + is very similar to *, except it means "one or more repetitions", as opposed to "zero or more repetitions". + matches 1 or more occurrence of the preceding expression.
* The metacharacter ? means "zero or one repetitions".
* Curly braces can be used to represent the number of repetitions between two numbers.
The regex {x,y} means "between x and y repetitions of something".
Hence {0,1} is the same thing as ?.
If the first number is missing, it is taken to be zero. If the second number is missing, it is taken to be infinity.

``` py
import re
# strings that start with "egg" and follow with zero or more "spam"s
patt=r"egg(spam)*"
patt1=r"[a^]*" #Zero or more repetitions of "a" or "^"
patt2=r"g+"
patt3=r"(42)+$" #One or more 42s
patt4=r"ice(-)?cream"
patt5=r"colo(u)?r"#Matches both color and colour
patt6=r"9{1,3}$"# matches string that have 1 to 3 nines.
if re.match(patt,"egg"):
  print("Match 1")
if re.match(patt,"eggspamspamegg"):
  print("Match 2")
if re.match(patt,"spam"):
  print("Match 3")
if re.match(patt2,"g"):
  print("Match 4")
if re.match(patt2,"gggggg"):
  print("Match 5")
if re.match(patt2,"abcde"):
  print("Match 6")
if re.match(patt4,"ice-cream"):
  print("Match 7")
if re.match(patt4,"icecream"):
  print("Match 8")
if re.match(patt4,"ice--cream"):
  print("Match 9")
if re.match(patt6,"9"):
  print("Match 10")
if re.match(patt6,"999"):
  print("Match 11")
if re.match(patt6,"9999"):
  print("Match 12")
```
```
Match 1
Match 2
Match 4
Match 5
Match 7
Match 8
Match 10
Match 11
```

## Groups

A group can be created by surrounding part of a regular expression with parentheses. This means that a group can be given as an argument to metacharacters such as * and ?. (spam) represents a group in the example pattern shown below.

The content of groups in a match can be accessed using the group function. A call of group(0) or group() returns the whole match. A call of group(n), where n is greater than 0, returns the nth group from the left. The method groups() returns all groups up from 1. Groups can be nested

``` py
import re
# strings that start with "egg" and follow with zero or more "spam"s
patt=r"egg(spam)*"
patt1=r"([^aeiou][aeiou][^aeiou])+"#one or more repetitions of a nonvowel, a vowel and nonvowel
patt2=r"a(bc)(de)(f(g)h)i"
if re.match(patt,"egg"):
  print("Match 1")
if re.match(patt,"eggspamspamegg"):
  print("Match 2")
if re.match(patt,"spam"):
  print("Match 3")
match=re.match(patt2,"abcdefghijklmnop")
if match:
  print(match.group())
  print(match.group(0))
  print(match.group(1))
  print(match.group(2))
  print(match.groups())
```
```
Match 1
Match 2
abcdefghi
abcdefghi
bc
de
('bc', 'de', 'fgh', 'g')
```

There are several kinds of special groups.
Two useful ones are named groups and non-capturing groups.
* Named groups have the format (?P<name>...), where name is the name of the group, and ... is the content. They behave exactly the same as normal groups, except they can be accessed by group(name) in addition to its number.
* Non-capturing groups have the format (?:...). They are not accessible by the group method, so they can be added to an existing regular expression without breaking the numbering.

``` py
import re
patt=r"(?P<first>abc)(?:def)(ghi)"
match=re.match(patt,"abcdefghijklmnop")
if match:
  print(match.group("first"))
  print(match.groups())
```
```
abc
('abc', 'ghi')
```

Another important metacharacter is |. This means "or", so red|blue matches either "red" or "blue".

``` py
import re
patt=r"gr(a|e)y"
match=re.match(patt,"gray")
if match:
  print("Match 1")
match=re.match(patt,"grey")
if match:
  print("Match 2")
match=re.match(patt,"griy")
if match:
  print("Match 3")
```
```
Match 1
Match 2
```

## Special Sequences

There are various special sequences you can use in regular expressions. They are written as a backslash followed by another character. One useful special sequence is a backslash and a number between 1 and 99, e.g., \1 or \17. This matches the expression of the group of that number.

Note, that "(.+) \1" is not the same as "(.+) (.+)", because \1 refers to the first group's subexpression, which is the matched expression itself, and not the regex pattern.

More useful special sequences are \d, \s, and \w. These match digits, whitespace, and word characters respectively. In ASCII mode they are equivalent to [0-9], [ \t\n\r\f\v], and [a-zA-Z0-9_]. In Unicode mode they match certain other characters, as well. For instance, \w matches letters with accents. Versions of these special sequences with upper case letters - \D, \S, and \W - mean the opposite to the lower-case versions. For instance, \D matches anything that isn't a digit.

Additional special sequences are \A, \Z, and \b. The sequences \A and \Z match the beginning and end of a string, respectively. The sequence \b matches the empty string between \w and \W characters, or \w characters and the beginning or end of the string. Informally, it represents the boundary between words. The sequence \B matches the empty string anywhere else.

``` py
import re
#[\w\.-]+ matches one or more word character, dot or dash.
emailpattern = r"([\w\.-]+)@([\w\.-]+)(\.[\w\.]+)"
patt=r"(.+) \1"
match=re.match(patt,"word word")
if match:
  print("Match 1")
match=re.match(patt,"?! ?!")
if match:
  print("Match 2")
match=re.match(patt,"abc def")
if match:
  print("Match 3")

patt=r"(\D+\d)" # matches one or more non-digits followed by a digit.
match=re.match(patt,"Hi 999!")
if match:
  print("Match 4")
match=re.match(patt,"1, 23, 456!!")
if match:
  print("Match 5")
match=re.match(patt," ! $?")
if match:
  print("Match 6")

patt=r"\b(cat)\b" # matches the word "cat" surrounded by word boundaries.
match=re.search(patt,"The cat sat!") #needs search not match
if match:
  print("Match 7")
match=re.search(patt,"we s>cat<tered?")
if match:
  print("Match 8")
match=re.search(patt,"We scattered.")
if match:
  print("Match 9")
patt=r"\B(cat)\B"
match=re.search(patt,"We scattered.")
if match:
  print("Match 10")
#[\w\.-]+ matches one or more word character, dot or dash. the dot is preceded by \ to treat it as a character
emailpattern = r"([\w\.-]+)@([\w\.-]+)(\.[\w\.]+)"
match=re.search(emailpattern,"Please contact car.ar@laposte.net for any assitance") #needs search not match
if match:
  print(match.group())
```
```
Match 1
Match 2
Match 4
Match 7
Match 8
Match 10
car.ar@laposte.net
```

Regexes can be more readable with the verbose flag

```py 
#The usual compact way:
email_rx = r"^[^@ ]+@[^@ ]+\.[^@ ]+$"
```
``` py
import re
#The verbose way:
email_rx = r"""(?x)     #verbose flag
    ^                   #beginning of string
    [^@ ]+              #stuff without @ or space (name)
    @                   #an @ sign
    [^@ ]+              #more stuff (domain)
    \.                  #a dot
    [^@ ]+              #final stuff(com, org,..)
    $                   #end of string
    """

print(re.match(email_rx,"carlos@pollo.com"))
```
```
<re.Match object; span=(0, 16), match='carlos@pollo.com'>
```