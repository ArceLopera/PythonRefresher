Comprehensions are a handy way to run a loop within a single line of code and to collect the results of the loop in a collection such as a list

##List Comprehension

List comprehensions are a useful way of quickly creating lists whose contents obey a simple rule. Python allows for list comprehension in which the elements of a list are iterated over all in one line of code. List comprehensions are inspired by set-builder notation in mathematics.

``` py
even_list = [2, 4, 6, 8]
odd_list = [even+1 for even in even_list]
print(odd_list)

cubes = [i**3 for i in range(5)]
print(cubes)
```

```
[3, 5, 7, 9]
[0, 1, 8, 27, 64]
```

Note from above the similarities between list comprehension and a for-loop; Python has list comprehension as a compact, "pythonic" way of performing operations that could be done within a for-loop. A list comprehension can also contain an if statement to enforce a condition on values in the list.

``` py
a=[i**2 for i in range(10)]
evens=[i**2 for i in range(10) if i**2 % 2 == 0]
print(a)
print(evens)
```

```
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
[0, 4, 16, 36, 64]
```
Trying to create a list in a very extensive range will result in a MemoryError. This code shows an example where the list comprehension runs out of memory. This issue is solved by generators.

``` py
results = []

for city, year in zip(cities,years):
  #int () needed because year is a string
  if int(year) >1945:
    results.append(city+': '+year)
```

To do it better and more Pythonic

Use List comprehensions
``` py
#List comprehension:
# [f(element) for element in iterator if condition(element)]

results = [(city+': '+year)
            for city, year in zip(cities,years) 
            if int(year) >1945]

results = [(city+': '+year) for city, year in zip(cities,years) if int(year) >1945]
```
##Dictionary comprehension

``` py
cities_by_year = {year:city for city, year in zip(cities,years)}
```
``` py
# Demonstrate how to use dictionary comprehensions

def main():
    # define a list of temperature values
    ctemps = [0, 12, 34, 100]

    # Use a comprehension to build a dictionary
    tempDict = {t: (t * 9/5) + 32 for t in ctemps if t < 100}
    print(tempDict)
    print(tempDict[12])

    # Merge two dictionaries with a comprehension
    team1 = {"Jones": 24, "Jameson": 18, "Smith": 58, "Burns": 7}
    team2 = {"White": 12, "Macke": 88, "Perce": 4}
    newTeam = {k: v for team in (team1, team2) for k, v in team.items()}
    print(newTeam)


if __name__ == "__main__":
    main()
```

```
{0: 32.0, 12: 53.6, 34: 93.2}
53.6
{'Jones': 24, 'Jameson': 18, 'Smith': 58, 'Burns': 7, 'White': 12, 'Macke': 88, 'Perce': 4}
```
##Set Comprehension

``` py
cities_after_1930 = {city for year, city in cities_by_year.items() if int(year)>1930 }
```

``` py
def main():
    # define a list of temperature data points
    ctemps = [5, 10, 12, 14, 10, 23, 41, 30, 12, 24, 12, 18, 29]

    # build a set of unique Fahrenheit temperatures
    ftemps1 = [(t * 9/5) + 32 for t in ctemps]
    ftemps2 = {(t * 9/5) + 32 for t in ctemps}
    print(ftemps1)
    print(ftemps2)

    # build a set from an input source
    sTemp = "The quick brown fox jumped over the lazy dog"
    chars = {c.upper() for c in sTemp if not c.isspace()}
    print(chars)


if __name__ == "__main__":
    main()
```
```
[41.0, 50.0, 53.6, 57.2, 50.0, 73.4, 105.8, 86.0, 53.6, 75.2, 53.6, 64.4, 84.2]
{64.4, 73.4, 41.0, 105.8, 75.2, 50.0, 84.2, 53.6, 86.0, 57.2}
{'G', 'M', 'E', 'B', 'J', 'U', 'R', 'N', 'W', 'P', 'Y', 'T', 'O', 'H', 'Z', 'Q', 'V', 'X', 'F', 'K', 'L', 'D', 'I', 'A', 'C'}
```