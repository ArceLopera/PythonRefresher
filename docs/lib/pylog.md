Logging is a means of tracking events that happen when some software runs. Logging is important for software developing, debugging and running. If you don’t have any logging record and your program crashes, there are very little chances that you detect the cause of the problem. And if you detect the cause, it will consume a lot of time. With logging, you can leave a trail of breadcrumbs so that if something goes wrong, we can determine the cause of the problem.
Python has a built-in module logging which allows writing status messages to a file or any other output streams. 

## The Basics

Basics of using the logging module to record the events in a file are very simple.
For that, simply import the module from the library.

1. Create and configure the logger. It can have several parameters. But importantly, pass the name of the file in which you want to record the events.
2. Here the format of the logger can also be set. By default, the file works in append mode but we can change that to write mode if required.
3. Also, the level of the logger can be set which acts as the threshold for tracking based on the numeric values assigned to each level.
4. There are several attributes which can be passed as parameters.
5. The list of all those parameters is given in Python Library. The user can choose the required attribute according to the requirement.
6. After that, create an object and use the various methods as shown in the example.

``` py
#importing module
import logging

#Create and configure logger
logging.basicConfig(filename="newfile.log",
					format='%(asctime)s %(message)s',
					filemode='w')

#Creating an object
logger=logging.getLogger()

#Setting the threshold of logger to DEBUG
logger.setLevel(logging.DEBUG)

#Test messages
logger.debug("Harmless debug Message")
logger.info("Just an information")
logger.warning("Its a Warning")
logger.error("Did you try to divide by zero")
logger.critical("Internet is down")

```
``` py
import logging

extData = {'user': 'caal@example.com'}


def anotherFunction():
    logging.debug("This is a debug-level log message", extra=extData)


def main():
    # set the output file and debug level, and
    # use a custom formatting specification
    fmtStr = "%(asctime)s: %(levelname)s: %(funcName)s Line:%(lineno)d User:%(user)s %(message)s"
    dateStr = "%m/%d/%Y %I:%M:%S %p"
    logging.basicConfig(filename="output.log",
                        level=logging.DEBUG,
                        format=fmtStr,
                        datefmt=dateStr)

    logging.info("This is an info-level log message", extra=extData)
    logging.warning("This is a warning-level message", extra=extData)
    anotherFunction()


if __name__ == "__main__":
    main()
```