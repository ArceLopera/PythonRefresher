# Zip
Python zip() method takes iterable or containers and returns a single iterator object, having mapped values from all the containers.

It is used to map the similar index of multiple containers so that they can be used just using a single entity.

``` py
name = [ "Manjeet", "Nikhil", "Shambhavi", "Astha" ]
roll_no = [ 4, 1, 3, 2 ]

# using zip() to map values
mapped = zip(name, roll_no)

print(set(mapped))
```
```
{('Shambhavi', 3), ('Nikhil', 1), ('Astha', 2), ('Manjeet', 4)}

```
``` py
names = ['Mukesh', 'Roni', 'Chari']
ages = [24, 50, 18]

for i, (name, age) in enumerate(zip(names, ages)):
	print(i, name, age)

```

```
0 Mukesh 24
1 Roni 50
2 Chari 18
```

``` py
stocks = ['reliance', 'infosys', 'tcs']
prices = [2175, 1127, 2750]

new_dict = {stocks: prices for stocks,
			prices in zip(stocks, prices)}
print(new_dict)

```
```
{'reliance': 2175, 'infosys': 1127, 'tcs': 2750}

```
# Unzip

How to unzip? 
Unzipping means converting the zipped values back to the individual self as they were. This is done with the help of “*” operator.

``` py
# Python code to demonstrate the working of
# unzip

# initializing lists
name = ["Manjeet", "Nikhil", "Shambhavi", "Astha"]
roll_no = [4, 1, 3, 2]
marks = [40, 50, 60, 70]

# using zip() to map values
mapped = zip(name, roll_no, marks)

# converting values to print as list
mapped = list(mapped)

# printing resultant values
print("The zipped result is : ", end="")
print(mapped)

print("\n")

# unzipping values
namz, roll_noz, marksz = zip(*mapped)

print("The unzipped result: \n", end="")

# printing initial lists
print("The name list is : ", end="")
print(namz)

print("The roll_no list is : ", end="")
print(roll_noz)

print("The marks list is : ", end="")
print(marksz)
```

```
The zipped result is : [('Manjeet', 4, 40), ('Nikhil', 1, 50), ('Shambhavi', 3, 60), ('Astha', 2, 70)]


The unzipped result: 
The name list is : ('Manjeet', 'Nikhil', 'Shambhavi', 'Astha')
The roll_no list is : (4, 1, 3, 2)
The marks list is : (40, 50, 60, 70)
```
