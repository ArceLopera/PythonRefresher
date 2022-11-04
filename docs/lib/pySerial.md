[Data Persistence](http://pymotw.com/2/persistence.html)

The standard library includes a variety of modules for persisting data. The most common pattern for storing data from Python objects for reuse is to serialize them with pickle and then either write them directly to a file or store them using one of the many key-value pair database formats available with the dbm API. If you don’t care about the underlying dbm format, the best persistence interface is provided by shelve. If you do care, you can use one of the other dbm-based modules directly.

* anydbm – Access to DBM-style databases
* dbhash – DBM-style API for the BSD database library
* dbm – Simple database interface
* dumbdbm – Portable DBM Implementation
* gdbm – GNU’s version of the dbm library
* [pickle](pySerial.md#serialization-with-pickle) and cPickle – Python object serialization
* shelve – Persistent storage of arbitrary Python objects
* whichdb – Identify DBM-style database formats
* sqlite3 – Embedded Relational Database

For serializing over the web, the [json](#serialization-with-json) module may be a better choice since its format is more portable.

## Serialization with Pickle

The pickle module is used for implementing binary protocols for serializing and de-serializing a Python object structure. 
 

**Pickling:** It is a process where a Python object hierarchy is converted into a byte stream. 
 
**Unpickling:** It is the inverse of Pickling process where a byte stream is converted into an object hierarchy. 

Module Interface : 
 

* dumps() – This function is called to serialize an object hierarchy.
* loads() – This function is called to de-serialize a data stream.

``` py
# Python program to illustrate
#Picle.dumps()
import pickle

data = [ { 'a':'A', 'b':2, 'c':3.0 } ]
data_string = pickle.dumps(data)
print ('PICKLE:', data_string )
```
```
PICKLE: b'\x80\x03]q\x00}q\x01(X\x01\x00\x00\x00aq\x02X\x01\x00\x00\x00Aq\x03X\x01\x00\x00\x00bq\x04K\x02X\x01\x00\x00\x00cq\x05G@\x08\x00\x00\x00\x00\x00\x00ua.'
```

``` py
# Python program to illustrate
# pickle.loads()
import pickle
import pprint

data1 = [ { 'a':'A', 'b':2, 'c':3.0 } ]
print ('BEFORE:',)
pprint.pprint(data1)

data1_string = pickle.dumps(data1)

data2 = pickle.loads(data1_string)
print ('AFTER:',)
pprint.pprint(data2)

print ('SAME?:', (data1 is data2))
print ('EQUAL?:', (data1 == data2))
```
```
BEFORE:
[{'a': 'A', 'b': 2, 'c': 3.0}]
AFTER:
[{'a': 'A', 'b': 2, 'c': 3.0}]
SAME?: False
EQUAL?: True
```
Python pickle module is used for serializing and de-serializing a Python object structure. Any object in Python can be pickled so that it can be saved on disk. What pickle does is that it “serializes” the object first before writing it to file. Pickling is a way to convert a python object (list, dict, etc.) into a character stream. The idea is that this character stream contains all the information necessary to reconstruct the object in another python script.

``` py
# Python3 program to illustrate store
# efficiently using pickle module
# Module translates an in-memory Python object
# into a serialized byte stream—a string of
# bytes that can be written to any file-like object.

import pickle

def storeData():
	# initializing data to be stored in db
	Omkar = {'key' : 'Omkar', 'name' : 'Omkar Pathak',
	'age' : 21, 'pay' : 40000}
	Jagdish = {'key' : 'Jagdish', 'name' : 'Jagdish Pathak',
	'age' : 50, 'pay' : 50000}

	# database
	db = {}
	db['Omkar'] = Omkar
	db['Jagdish'] = Jagdish
	
	# Its important to use binary mode
	dbfile = open('examplePickle', 'ab')
	
	# source, destination
	pickle.dump(db, dbfile)					
	dbfile.close()

def loadData():
	# for reading also binary mode is important
	dbfile = open('examplePickle', 'rb')	
	db = pickle.load(dbfile)
	for keys in db:
		print(keys, '=>', db[keys])
	dbfile.close()

if __name__ == '__main__':
	storeData()
	loadData()

```
```
Omkar => {'key': 'Omkar', 'name': 'Omkar Pathak', 'age': 21, 'pay': 40000}
Jagdish => {'key': 'Jagdish', 'name': 'Jagdish Pathak', 'age': 50, 'pay': 50000}
```
### Without a File

``` py
# initializing data to be stored in db
Omkar = {'key' : 'Omkar', 'name' : 'Omkar Pathak',
'age' : 21, 'pay' : 40000}
Jagdish = {'key' : 'Jagdish', 'name' : 'Jagdish Pathak',
'age' : 50, 'pay' : 50000}

# database
db = {}
db['Omkar'] = Omkar
db['Jagdish'] = Jagdish

# For storing
b = pickle.dumps(db)	 # type(b) gives <class 'bytes'>

# For loading
myEntry = pickle.loads(b)
print(myEntry)
```
```
{'Omkar': {'key': 'Omkar', 'name': 'Omkar Pathak', 'age': 21, 'pay': 40000}, 'Jagdish': {'key': 'Jagdish', 'name': 'Jagdish Pathak', 'age': 50, 'pay': 50000}}
```

### Advantages of Using Pickle

1. **Recursive objects** (objects containing references to themselves): Pickle keeps track of the objects it has already serialized, so later references to the same object won’t be serialized again. (The marshal module breaks for this.)
2. **Object sharing** (references to the same object in different places): This is similar to self- referencing objects; pickle stores the object once, and ensures that all other references point to the master copy. Shared objects remain shared, which can be very important for mutable objects.
3. **User-defined classes and their instances:** Marshal does not support these at all, but pickle can save and restore class instances transparently. The class definition must be importable and live in the same module as when the object was stored.

## Serialization with JSON

``` py
# import module
import json

# Data to be written
data = {
	"user": {
		"name": "satyam kumar",
		"age": 21,
		"Place": "Patna",
		"Blood group": "O+"
	}
}

# Serializing json and
# Writing json file
with open( "datafile.json" , "w" ) as write:
	json.dump( data , write )
```
``` py
# importing the module
import json

# creating the JSON data as a string
data = '{"Name" : "Romy", "Gender" : "Female"}'

print("Datatype before deserialization : "
	+ str(type(data)))

# deserializing the data
data = json.loads(data)

print("Datatype after deserialization : "
	+ str(type(data)))
```
```
Datatype before deserialization : <class 'str'>
Datatype after deserialization : <class 'dict'>
```