Software testing can be divided into two classes, Manual testing and Automated testing. Automated testing is the execution of your tests using a script instead of a human.

There are different Test Runners available in Python. Popular ones are: 

* [unittest](#unitest)
* [nose or nose2](#nose-or-nose2)
* [pytest](#pytest)

## Unitest

It is built into the standard python library. import unittest should be the starting line of code for using it. Depends upon the python version, it should differ as later versions of Python supports unittest and earlier versions supported unittest2.

One of the major problems with manual testing is that it requires time and effort. In manual testing, we test the application over some input, if it fails, either we note it down or we debug the application for that particular test input, and then we repeat the process. With unittest, all the test inputs can be provided at once and then you can test your application. In the end, you get a detailed report with all the failed test cases clearly specified, if any.

The unittest module has both a built-in testing framework and a test runner. A testing framework is a set of rules which must be followed while writing test cases, while a test runner is a tool which executes these tests with a bunch of settings, and collects the results.

## Nose or Nose2

This is an open source application and similar to unittest only.It is compatible with numerous kinds of tests that are written using unittest framework. nose2 is the recent version one, and they are installed by using.

``` py
pip install nose2 
```

## Pytest

t supports unittest test cases execution. It has benefits like supporting built in assert statement, filtering of test cases, returning from last failing test etc

``` py
def test_sum_numbers_using_pytest():
	assert sum([700, 900]) == 1600, "Resultant should be 1600"

def test_sum_tuple_using_pytest():
	assert sum((700,1900)) == 1600, "Resultant should be 1600"
```