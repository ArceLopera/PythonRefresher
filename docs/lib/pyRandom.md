Python Random module is an in-built module of Python which is used to generate random numbers. These are pseudo-random numbers means these are not truly random. This module can be used to perform random actions such as generating random numbers, print random a value for a list or string, etc.

``` py
# import random
import random

# prints a random value from the list
list1 = [1, 2, 3, 4, 5, 6]
print(random.choice(list1))
```
```
3
```

``` py
import random

random.seed(5)

print(random.random())
print(random.random())
```
```
0.6229016948897019
0.7417869892607294

```

``` py
# import the random module
import random


# declare a list
sample_list = [1, 2, 3, 4, 5]

print("Original list : ")
print(sample_list)

# first shuffle
random.shuffle(sample_list)
print("\nAfter the first shuffle : ")
print(sample_list)

# second shuffle
random.shuffle(sample_list)
print("\nAfter the second shuffle : ")
print(sample_list)
```
```
Original list : 
[1, 2, 3, 4, 5]

After the first shuffle : 
[3, 4, 2, 1, 5]

After the second shuffle : 
[2, 1, 5, 4, 3]
```

``` py
# Functions for generating random data sequences
import random
import string

# Use the choice function to randomly select from a sequence
moves = ["rock", "paper", "scissors"]
print(random.choice(moves))

# Use the choices function to create a list of random elements
roulette_wheel = ["black", "red", "green"]
weights = [18, 18, 2]
print(random.choices(roulette_wheel, weights, k=10))

# The sample function randomly selects elements from a population
# without replacement (the chosen items are not replaced)
chosen = random.sample(string.ascii_uppercase, 6)
print(chosen)

# The shuffle function shuffles a sequence in place
players = ["Bill", "Jane", "Joe", "Sally", "Mike", "Lindsay"]
random.shuffle(players)
print(players)

# to shuffle an immutable sequence, use the sample function first
result = random.sample(string.ascii_uppercase, k=len(string.ascii_uppercase))
random.shuffle(result)
print(''.join(result))
```
```
paper
['red', 'black', 'black', 'black', 'red', 'black', 'black', 'red', 'black', 'red']
['C', 'E', 'T', 'X', 'O', 'Y']
['Lindsay', 'Joe', 'Sally', 'Mike', 'Bill', 'Jane']
EJYQHGKSUNCVBIFTZPWORXLDAM
```

## Criptographic random

The secrets module is used for generating random numbers for managing important data such as passwords, account authentication, security tokens, and related secrets, that are cryptographically strong. This module is responsible for providing access to the most secure source of randomness. This module is present in Python 3.6 and above.

``` py
# Using cryptographic-appropriate methods to generate random data
# that may be sensitive. secrets module introduced in Python 3.6
import os
import secrets


# the urandom() function in the OS module produces random numbers that
# are cryptographically safe to use for sensitive purposes
result = os.urandom(8)
print([hex(b) for b in result])


# secrets.choice is the same as random.choice but more secure
moves = ["rock", "paper", "scissors"]
print(secrets.choice(moves))


# secrets.token_bytes generates random bytes
result = secrets.token_bytes()
print(result)


# secrets.token_hex creates a random string in hexadecimal
result = secrets.token_hex()
print(result)


# secrets.token_urlsafe generates characters that can be in URLs
result = secrets.token_urlsafe()
print(result)
```
```
['0x54', '0xd8', '0xb2', '0xf3', '0x68', '0xed', '0x35', '0xab']
scissors
b'\xbc\x14\xf5\xc6\x02\xe5\xd3W\xcc9\x88\xddk\xc7\xb7\xc4\xc9\x9a\xcd\xf0N\x94\x95\xdd\xfe\xac\xa1\x07\x80|L,'
4db4b731c2de8d0af94fe8563fc21f00aae04e41ba52ce56c5b9467583d3e57d
tYBwYVYQXVdsXdeztE2-ki-osvgvsNnnWT2ZVLj3kng
```

``` py
# Create a temporary password using Python
import secrets
import string


# Function to return a temporary password given a length
def generateTempPass(numChars=8):
    potentialChars = string.ascii_letters + string.digits + "+=?/!@#$%*"
    result = ''.join(secrets.choice(potentialChars) for i in range(numChars))
    return result


# Function to return a temporary password and enforce 1 number and 1 uppercase
def generateBetterPass(numChars=8):
    potentialChars = string.ascii_letters + string.digits + "+=?/!@#$%*"
    while True:
        result = ''.join(secrets.choice(potentialChars)
                         for i in range(numChars))

        # if the password has at least one number and one uppercase char we can stop
        if (any(c.isupper() for c in result)
                and any(c.isdigit() for c in result)):
            break

    return result


# create a temporary password
print(generateTempPass(10))

# create a stronger temporary password
print(generateBetterPass(10))

# create a temporary, hard-to-guess URL
resultUrl = "https://my.example.com?reset="
resultUrl += secrets.token_urlsafe(15)
print(resultUrl)
```
```
p9oV1vn?eJ
A2*Mlp7p!l
https://my.example.com?reset=DhpaK2rfeYIbFs73nbl1
```

## UUID

UUID, Universal Unique Identifier, is a python library which helps in generating random objects of 128 bits as ids. It provides the uniqueness as it generates ids on the basis of time, Computer hardware (MAC etc.)

+ Can be used as general utility to generate unique random id.
+ Can be used in cryptography and hashing applications.
+ Useful in generating random documents, addresses etc.

``` py
# Generating unique identifiers
import uuid


# use the uuid4 function to create a random sequence using
# the underlying os.urandom() function
result = uuid.uuid4()
print("UUID4: ")
print(result)
print(result.hex)
print(result.urn)
print("~~~~~~~~~~~~~~~~~~~~~~~\n")


# create a UUID using uuid5, which takes a namespace and
# name value. Note that this version is not crypto-safe
result = uuid.uuid5(uuid.NAMESPACE_DNS, "example.com")
print("UUID5: ")
print(result)
print(result.hex)
print(result.urn)
print("~~~~~~~~~~~~~~~~~~~~~~~\n")
```
```
UUID4: 
dfbf3df5-8647-4a91-8e51-81e1a3465ec3
dfbf3df586474a918e5181e1a3465ec3
urn:uuid:dfbf3df5-8647-4a91-8e51-81e1a3465ec3
~~~~~~~~~~~~~~~~~~~~~~~

UUID5: 
cfbff0d1-9375-5685-968c-48ce8b15ae17
cfbff0d193755685968c48ce8b15ae17
urn:uuid:cfbff0d1-9375-5685-968c-48ce8b15ae17
~~~~~~~~~~~~~~~~~~~~~~~
```