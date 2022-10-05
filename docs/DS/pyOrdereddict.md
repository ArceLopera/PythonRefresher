An OrderedDict is a dictionary subclass that remembers the order that keys were first inserted. The only difference between dict() and OrderedDict() is that:

OrderedDict preserves the order in which the keys are inserted. A regular dict doesn’t track the insertion order, and iterating it gives the values in an arbitrary order. By contrast, the order the items are inserted is remembered by OrderedDict.

``` py
# A Python program to demonstrate working
# of OrderedDict

from collections import OrderedDict

print("This is a Dict:\n")
d = {}
d['a'] = 1

d['b'] = 2
d['c'] = 3
d['d'] = 4

for key, value in d.items():
	print(key, value)

print("\nThis is an Ordered Dict:\n")
od = OrderedDict()

od['a'] = 1
od['b'] = 2
od['c'] = 3
od['d'] = 4

for key, value in od.items():
	print(key, value)
```
```
This is a Dict:

a 1
b 2
c 3
d 4

This is an Ordered Dict:

a 1
b 2
c 3
d 4
```
## Key value Change 

If the value of a certain key is changed, the position of the key remains unchanged in OrderedDict.
``` py
# A Python program to demonstrate working of key
# value change in OrderedDict
from collections import OrderedDict

print("Before:\n")
od = OrderedDict()
od['a'] = 1
od['b'] = 2
od['c'] = 3
od['d'] = 4
for key, value in od.items():
	print(key, value)

print("\nAfter:\n")
od['c'] = 5
for key, value in od.items():
	print(key, value)
```
```
Before:

a 1
b 2
c 3
d 4

After:

a 1
b 2
c 5
d 4
```
## Deletion and Re-Inserting 

Deleting and re-inserting the same key will push it to the back as OrderedDict, however, maintains the order of insertion.
``` py
# A Python program to demonstrate working of deletion
# re-insertion in OrderedDict
from collections import OrderedDict

print("Before deleting:\n")
od = OrderedDict()
od['a'] = 1
od['b'] = 2
od['c'] = 3
od['d'] = 4

for key, value in od.items():
	print(key, value)

print("\nAfter deleting:\n")
od.pop('c')
for key, value in od.items():
	print(key, value)

print("\nAfter re-inserting:\n")
od['c'] = 3
for key, value in od.items():
	print(key, value)
```
```
Before deleting:

a 1
b 2
c 3
d 4

After deleting:

a 1
b 2
d 4

After re-inserting:

a 1
b 2
d 4
c 3
```


``` py
from collections import OrderedDict


def main():
    # list of sport teams with wins and losses
    sportTeams = [("Royals", (18, 12)), ("Rockets", (24, 6)), 
                ("Cardinals", (20, 10)), ("Dragons", (22, 8)),
                ("Kings", (15, 15)), ("Chargers", (20, 10)), 
                ("Jets", (16, 14)), ("Warriors", (25, 5))]

    # sort the teams by number of wins
    sortedTeams = sorted(sportTeams, key=lambda t: t[1][0], reverse=True)

    # create an ordered dictionary of the teams
    teams = OrderedDict(sortedTeams)
    print(teams)

    # Use popitem to remove the top item
    tm, wl = teams.popitem(False)
    print("Top team: ", tm, wl)

    # What are next the top 4 teams?
    for i, team in enumerate(teams, start=1):
        print(i, team)
        if i == 4:
            break

    # test for equality
    a = OrderedDict({"a": 1, "b": 2, "c": 3})
    b = OrderedDict({"a": 1, "c": 3, "b": 2})
    print("Equality test: ", a == b)


if __name__ == "__main__":
    main()
```
```
OrderedDict([('Warriors', (25, 5)), ('Rockets', (24, 6)), ('Dragons', (22, 8)), ('Cardinals', (20, 10)), ('Chargers', (20, 10)), ('Royals', (18, 12)), ('Jets', (16, 14)), ('Kings', (15, 15))])
Top team:  Warriors (25, 5)
1 Rockets
2 Dragons
3 Cardinals
4 Chargers
Equality test:  False
```