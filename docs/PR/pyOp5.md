**Boolean type**. There are two Boolean values: True and False.
They can be created by comparing values, for instance by using the equal operator ==.

``` py
a=True
print(a)
b=(1==3)
print(b)
```

```
True
False
-1
```

**Comparison operators** are also called **Relational operators**.
There are != , <, <=, >, >=.  Used to compare strings lexicographically

``` py
print(3!=2)
print(8<=9.0) #different types, no problem!
print('Carlos'>'Ana')
```

```
True
True
True
```
**Boolean logic** is used to make more complicated conditions for if statements that rely on more than one condition. 

Python's **Boolean operators** are *and*, *or*, *not*, *in*, *not in*, *is* and, *is not*.

``` py
print(1==1 and 3>4)
print(1==1 or 3>4)
print(1==2 and not 3>4)
x=('bear','bunny','tree')
y='bear'
print(y in x)
print(y not in x)
print(y is x[0])#same id

print(id(y))
print(id(x[0]))

```
```
False
True
False
True
False
True
140097849021808
140097849021808
```