## File Management
### **Opening Files**
The argument of the open function is the path to the file. If the file is in the current working directory of the program, you can specify only its name. You can specify the mode used to open a file by applying a second argument to the open function.
Sending "r" means open in read mode, which is the default.
Sending "w" means write mode, for rewriting the contents of a file.
Sending "a" means append mode, for adding new content to the end of the file.

Adding "b" to a mode opens it in binary mode, which is used for non-text files (such as image and sound files). Once a file has been opened and used, you should close it.
This is done with the close method of the file object.

### **Reading Files**
* file.read(): returns all the contents
* file.readlines():To retrieve each line in a file, you can use the readlines method to return a list in which each element is a line in the file.

### **Writing Files**
* To write to files you use the write method
* The write method returns the number of bytes written to a file, if successful.

``` py
try:
  myfile=open("filename.txt", 'r+') #mode read and write
  #read all content
  cont=myfile.read()
  myfile.write("New line to insert in file")
  print(cont)
finally:
  myfile.close()
```
``` py
myfile=open("textfile.txt", 'r+') #mode read and write
#print each line
for line in myfile:
  print(line.rstrip())
myfile.close()
```
```
This is line 1
This is line 2
This is line 3
This is line 4
This is line 5
This is line 6
This is line 7
This is line 8
This is line 9
This is line 10
```

An alternative way of doing this is using with statements. This creates a temporary variable (often called f), which is only accessible in the indented block of the with statement. The file is automatically closed at the end of the with statement, even if exceptions occur within it.

``` py
with open("filename.txt") as f:
   print(f.read())
```
``` py
# Open a file for writing and create it if it doesn't exist
f = open("textfile.txt","w+")
  
  # Open the file for appending text to the end
  # f = open("textfile.txt","a+")

  # write some lines of data to the file
for i in range(10):
    f.write("This is line %d\r\n" % (i+1))
  
  # close the file when done
f.close()
  
  # Open the file back up and read the contents
f = open("textfile.txt","r")
if f.mode == 'r': # check to make sure that the file was opened
    # use the read() function to read the entire file
    # contents = f.read()
    # print (contents)
    
  fl = f.readlines() # readlines reads the individual lines into a list
  for x in fl:
     print (x)
```
```
This is line 1

This is line 2

This is line 3

This is line 4

This is line 5

This is line 6

This is line 7

This is line 8

This is line 9

This is line 10
```
## Fast Input/Output

``` py
# Program to show time taken in fast
# I / O and normal I / O in python
from sys import stdin, stdout
import time

# Function for fast I / O
def fastIO():

	# Stores the start time
	start = time.perf_counter()

	# To read single integer
	n = stdin.readline()

	# To input array
	arr = [int(x) for x in stdin.readline().split()]

	# Output integer
	stdout.write(str(n))

	# Output array
	stdout.write(" ".join(map(str, arr)) + "\n")

	# Stores the end time
	end = time.perf_counter()
	print("Time taken in fast IO", end-start)

# Function for normal I / O
def normalIO():
	# Stores the start time
	start = time.perf_counter()

	# Input integer
	n = int(input())

	# Input array
	arr = [int(x) for x in input().split()]

	# Output integer
	print(n)

	# Output array
	for i in arr:
		print(i, end =" ")
	print()

	# Stores the end time
	end = time.perf_counter()
	print("Time taken in normal IO: ", end-start)


# Driver Code
if __name__ == '__main__':
	fastIO()
	normalIO()

```
```
Time taken in fast IO 0.001823046999994915
23
23
23
23 
Time taken in normal IO:  5.173487307000002
```
## OS Path Module
``` py
import os
from os import path
import datetime
from datetime import date, time, timedelta
import time

# Print the name of the OS
print (os.name)
  
  # Check for item existence and type
print ("Item exists: ", path.exists("textfile.txt"))
print ("Item is a file: ", path.isfile("textfile.txt"))
print ("Item is a directory: ", path.isdir("textfile.txt"))
  
  # Work with file paths
print ("Item's path: ",path.realpath("textfile.txt"))
print ("Item's path and name: ",path.split(path.realpath("textfile.txt")))
  
  # Get the modification time
t = time.ctime(path.getmtime("textfile.txt"))
print (t)
print (datetime.datetime.fromtimestamp(path.getmtime("textfile.txt")))
  
  # Calculate how long ago the item was modified
td= datetime.datetime.now() - datetime.datetime.fromtimestamp(path.getmtime("textfile.txt"))
print ("It has been " + str(td) + " since the file was modified")
print ("Or, " + str(td.total_seconds()) + " seconds")
```
```
posix
Item exists:  True
Item is a file:  True
Item is a directory:  False
Item's path:  /content/textfile.txt
Item's path and name:  ('/content', 'textfile.txt')
Mon Jul 19 14:31:57 2021
2021-07-19 14:31:57.728190
It has been 0:06:55.454337 since the file was modified
Or, 415.454337 seconds
```
## GLOB Module

Glob module searches all path names looking for files matching a specified pattern according to the rules dictated by the Unix shell. Results so obtained are returned in arbitrary order. Some requirements need traversal through a list of files at some location, mostly having a specific pattern. Python’s glob module has several functions that can help in listing files that match a given pattern under a specified folder.

### **Pattern Rules**

+ Follow standard Unix path expansion rules.
+ Special characters supported : two different wild-cards-  *, ?  and character ranges expressed in [].
+ The pattern rules are applied to segments of the filename (stopping at the path separator, /).
+ Paths in the pattern can be relative or absolute.

### **Application**

+ It is useful in any situation where your program needs to look for a list of files on the file system with names matching a pattern.
+ If you need a list of filenames that have a certain extension, prefix, or any common string in the middle, use glob instead of writing code to scan the directory contents yourself.

``` py
import glob

# search .py files
# in the current working directory
for py in glob.glob("*.py"):
	print(py)
```
``` py
import glob

# Using character ranges []
print('Finding file using character ranges [] :- ')
print(glob.glob('./[0-9].*'))

# Using wildcard character *
print('\n Finding file using wildcard character * :- ')
print(glob.glob('*.gif'))

# Using wildcard character ?
print('\n Finding file using wildcard character ? :- ')
print(glob.glob('?.gif'))

# Using recursive attribute
print('\n Finding files using recursive attribute :- ')
print(glob.glob('**/*.txt', recursive=True))

```
## Shutil Module: Filesystem Shell Methods

``` PY
import os
from os import path
import shutil
from shutil import make_archive
from zipfile import ZipFile

  # make a duplicate of an existing file
if path.exists("textfile.txt"):
    # get the path to the file in the current directory
    src = path.realpath("textfile.txt");
        
    # # let's make a backup copy by appending "bak" to the name
    dst = src + ".bak"
    # # now use the shell to make a copy of the file
    shutil.copy(src,dst)
    
    # # copy over the permissions, modification times, and other info
    shutil.copystat(src, dst)
    
    # # rename the original file
    os.rename("textfile.txt", "newfile.txt")
    
    # now put things into a ZIP archive
    root_dir,tail = path.split(src)
    shutil.make_archive("archive", "zip", root_dir)

    # more fine-grained control over ZIP files
    with ZipFile("testzip.zip","w") as newzip:
      newzip.write("newfile.txt")
      newzip.write("textfile.txt.bak")
```
## PyFileSystem

``` py
pip install fs
pip show fs
```
```
Name: fs
Version: 2.4.14
Summary: Python's filesystem abstraction layer
Home-page: https://github.com/PyFilesystem/pyfilesystem2
Author: Will McGugan
Author-email: will@willmcgugan.com
License: MIT
Location: /usr/local/lib/python3.7/dist-packages
Requires: appdirs, six, setuptools, pytz
Required-by: 
```


``` PY
# import the PyFilesystem library for OS files
from fs.osfs import OSFS


# TODO: open a local filesystem for the current directory
with OSFS(".") as myfs:
    if (not myfs.exists("testdir")):
        # create a sample data directory
        myfs.makedir("testdir")

        # create a file
        with myfs.open("testdir/samplefile.txt", mode='w') as f:
            f.write("This is some text")

        # read the file contents
        with myfs.open("testdir/samplefile.txt") as f:
            content = f.read()
            print(content)

    # TODO: use the getinfo() function to return resource information
    info = myfs.getinfo("testdir/samplefile.txt", namespaces=['details'])
    print(info.name)
    print(info.is_dir)
    print(info.size)
    print(info.type)
    print(info.modified)

```
```
samplefile.txt
False
17
ResourceType.file
2021-12-23 04:09:10.571525+00:00
```

``` PY
# TODO: try opening and reading a ZIP archive

from fs.zipfs import ZipFS

with ZipFS("FileExamples.zip") as thezip:
    if (thezip.exists("FileExamples/File1.txt")):
        with thezip.open("FileExamples/File1.txt") as f:
            content = f.read()
            print(content)
```
``` py
from fs.osfs import OSFS

# TODO: print a directory tree listing
with OSFS(".") as myfs:
    myfs.tree()
```
```
|-- .config
|   |-- configurations
|   |   `-- config_default
|   |-- logs
|   |   `-- 2021.12.03
|   |       |-- 14.32.30.027140.log
|   |       |-- 14.32.50.522723.log
|   |       |-- 14.33.09.955489.log
|   |       |-- 14.33.16.964195.log
|   |       |-- 14.33.36.903459.log
|   |       `-- 14.33.37.701606.log
|   |-- .last_opt_in_prompt.yaml
|   |-- .last_survey_prompt.yaml
|   |-- .last_update_check.json
|   |-- active_config
|   |-- config_sentinel
|   `-- gce
|-- sample_data
|   |-- anscombe.json
|   |-- california_housing_test.csv
|   |-- california_housing_train.csv
|   |-- mnist_test.csv
|   |-- mnist_train_small.csv
|   `-- README.md
`-- testdir
    `-- samplefile.txt
```



``` PY
# TODO: use directory operation functions
# with OSFS(".") as myfs:
#     dirlist = myfs.listdir("testdir")
#     print(dirlist)

# with OSFS(".") as myfs:
#     dirlist = list(myfs.scandir("testdir"))
#     print(dirlist)

with OSFS(".") as myfs:
    dirlist = list(myfs.filterdir("testdir", files=["*.txt"]))
    print(dirlist)

# TODO: Use resource info with scandir
with OSFS(".") as myfs:
    dirlist = myfs.scandir("testdir", namespaces=["details"])
    for info in dirlist:
        print(info.name, info.size)

# TODO: make a copy of a directory
# with OSFS(".") as myfs:
#     myfs.copydir("testdir", "CopyOftestdir", create=True)

# TODO: remove a directory
# with OSFS(".") as myfs:
#     if (myfs.exists("CopyOftestdir")):
#         # myfs.removedir("CopyOftestdir")
#         myfs.removetree("CopyOftestdir")
```
```
[<file 'samplefile.txt'>]
samplefile.txt 17
```

``` PY
# Example file for using the File System walker

from fs.osfs import OSFS
from fs.zipfs import ZipFS

# create a basic file walker
with OSFS(".") as myfs:
    print("-- Files --")
    # TODO: use the files walker to process files
    for path in myfs.walk.files(filter=["*.txt"]):
        print(path)

    print("-- Directories --")
    # TODO: use the dirs walker for directories
    for path in myfs.walk.dirs():
        print(path)

# TODO: use the info property to step through items
# with OSFS(".") as myfs:
#     for path, info in myfs.walk.info(namespaces=["details"]):
#         print(path, info.is_dir, info.size)

# TODO: Use the walk object by itself:
# with OSFS("FileExamples") as myfs:
#     for step in myfs.walk():
#         print(step.path)
#         print(step.files)
#         print(step.dirs)

# TODO: Use the walker with a ZIP
# with ZipFS("FileExamples.zip") as thezip:
#     print("-- Zip Contents --")
#     for path in thezip.walk.files():
#         print(path)
```
```
-- Files --
/testdir/samplefile.txt
-- Directories --
/.config
/testdir
/sample_data
/.config/logs
/.config/configurations
/.config/logs/2021.12.03
```

``` py
from fs.osfs import OSFS

# Challenge - figure out the total size of all text files in a folder structure
totalsize = 0

# Create a file walker to walk the FileExamples directory
with OSFS(".") as myfs:
    # We need to specify the details namespace to get size info
    for path, info in myfs.walk.info(namespaces=["details"]):
        # Check for an ending extension of .txt
        if path.endswith(".txt") and not info.is_dir:
            totalsize += info.size

    # print the final results
    print("Total size of files is: {0}".format(totalsize))
```
```
Total size of files is: 17
```

## CSV IO

``` py
# importing the csv module
import csv

# my data rows as dictionary objects
mydict =[{'branch': 'COE', 'cgpa': '9.0', 'name': 'Nikhil', 'year': '2'},
		{'branch': 'COE', 'cgpa': '9.1', 'name': 'Sanchit', 'year': '2'},
		{'branch': 'IT', 'cgpa': '9.3', 'name': 'Aditya', 'year': '2'},
		{'branch': 'SE', 'cgpa': '9.5', 'name': 'Sagar', 'year': '1'},
		{'branch': 'MCE', 'cgpa': '7.8', 'name': 'Prateek', 'year': '3'},
		{'branch': 'EP', 'cgpa': '9.1', 'name': 'Sahil', 'year': '2'}]

# field names
fields = ['name', 'branch', 'year', 'cgpa']

# name of csv file
filename = "university_records.csv"

# writing to csv file
with open(filename, 'w') as csvfile:
	# creating a csv dict writer object
	writer = csv.DictWriter(csvfile, fieldnames = fields)
	
	# writing headers (field names)
	writer.writeheader()
	
	# writing data rows
	writer.writerows(mydict)

```
``` py
# importing csv module
import csv

# csv file name
filename = "university_records.csv"

# initializing the titles and rows list
fields = []
rows = []

# reading csv file
with open(filename, 'r') as csvfile:
	# creating a csv reader object
	csvreader = csv.reader(csvfile)
	
	# extracting field names through first row
	fields = next(csvreader)

	# extracting each data row one by one
	for row in csvreader:
		rows.append(row)

	# get total number of rows
	print("Total no. of rows: %d"%(csvreader.line_num))

# printing the field names
print('Field names are:' + ', '.join(field for field in fields))

# printing first 5 rows
print('\nFirst 5 rows are:\n')
for row in rows[:5]:
	# parsing each column of a row
	for col in row:
		print("%10s"%col),
	print('\n')

```
```
Total no. of rows: 7
Field names are:name, branch, year, cgpa

First 5 rows are:

    Nikhil
       COE
         2
       9.0


   Sanchit
       COE
         2
       9.1


    Aditya
        IT
         2
       9.3


     Sagar
        SE
         1
       9.5


   Prateek
       MCE
         3
       7.8

```

## ConfigParse Module
