## Datetime

``` py
from datetime import date
from datetime import time
from datetime import datetime

## DATE OBJECTS
  # Get today's date from the simple today() method from the date class
today = date.today()
print ("Today's date is ", today)
  
  # print out the date's individual components
print ("Date Components: ", today.day, today.month, today.year)
  
  # retrieve today's weekday (0=Monday, 6=Sunday)
print ("Today's Weekday #: ", today.weekday())
days = ["monday","tuesday","wednesday","thursday","friday","saturday","sunday"]
print ("Which is a " + days[today.weekday()])
  
  ## DATETIME OBJECTS
  # Get today's date from the datetime class
today = datetime.now()
print  ("The current date and time is ", today)
  
  # Get the current time
t = datetime.time(datetime.now())
print ("The current time is ", t)
```
```
Today's date is  2021-12-22
Date Components:  22 12 2021
Today's Weekday #:  2
Which is a wednesday
The current date and time is  2021-12-22 20:01:50.628110
The current time is  20:01:50.631578
```
## Pendulum

The pendulum is one of the popular Python DateTime libraries to ease DateTime manipulation. It provides a cleaner and easier to use API. It simplifies the problem of complex date manipulations involving timezones which are not handled correctly in native datetime instances.

It inherits from the standard datetime library but provides better functionality. So you can introduce Pendulums Datetime instances in projects which are already using built-in datetime class (except for the libraries that check the type of the objects by using the type function like sqlite3).

``` py
from datetime import date
from datetime import time
from datetime import datetime
!pip install pendulum
import pendulum
```
``` py
dt1 = pendulum.datetime(2021,12,24)

print(dt1)

#local() creates datetime instance with local timezone
local = pendulum.local(2020, 11,27)
print(local)
print(local.timezone.name)

# Importing library
import pendulum

# Getting current UTC time
utc_time = pendulum.now('UTC')

# Switching current timezone to
# Kolkata timezone using in_timezone().
kolkata_time = utc_time.in_timezone('Asia/Kolkata')
print('Current Date Time in Kolkata =', kolkata_time)

# Generating Sydney timezone
sydney_tz = pendulum.timezone('Australia/Sydney')

# Switching current timezone to
# Sydney timezone using convert().
sydney_time = sydney_tz.convert(utc_time)
print('Current Date Time in Sydney =', sydney_time)

```
```
2021-12-24T00:00:00+00:00
2020-11-27T00:00:00+00:00
Etc/UTC
Current Date Time in Kolkata = 2021-12-23T01:36:55.336688+05:30
Current Date Time in Sydney = 2021-12-23T07:06:55.336688+11:00
```

``` py
# Importing the library
import pendulum
# creating datetime instance
dt = pendulum.datetime(2020, 11, 27)
print(dt)

# Manipulating datetime object using add()
dt = dt.add(years=5)
print(dt)

# Manipulating datetime object using subtract()
dt = dt.subtract(months = 1)
print(dt)

# Similarly you can add or subtract
# months,weeks,days,hours,minutes
# individually or all at a time.
dt = dt.add(years=3, months=2, days=6,
			hours=12, minutes=30, seconds=45)

print(dt)
```
```
2020-11-27T00:00:00+00:00
2025-11-27T00:00:00+00:00
2025-10-27T00:00:00+00:00
2029-01-02T12:30:45+00:00

```

``` py
dt_here=pendulum.now()
dt_there=dt_here.in_timezone("Europe/London")
print(dt_there)
```
```
2021-12-22T20:27:11.672167+00:00
```

## Formatting

``` py
# Times and dates can be formatted using a set of predefined string
  # control codes 
now = datetime.now() # get the current date and time
  
  #### Date Formatting ####
  
  # %y/%Y - Year, %a/%A - weekday, %b/%B - month, %d - day of month
print (now.strftime("The current year is: %Y")) # full year with century
print (now.strftime("%a, %d %B, %y")) # abbreviated day, num, full month, abbreviated year
  
  # %c - locale's date and time, %x - locale's date, %X - locale's time
print (now.strftime("Locale date and time: %c"))
print (now.strftime("Locale date: %x"))
print (now.strftime("Locale time: %X"))
  
  #### Time Formatting ####
  
  # %I/%H - 12/24 Hour, %M - minute, %S - second, %p - locale's AM/PM
print (now.strftime("Current time: %I:%M:%S %p")) # 12-Hour:Minute:Second:AM
print (now.strftime("24-hour time: %H:%M")) # 24-Hour:Minute
```
```
The current year is: 2021
Mon, 19 July, 21
Locale date and time: Mon Jul 19 14:22:20 2021
Locale date: 07/19/21
Locale time: 14:22:20
Current time: 02:22:20 PM
24-hour time: 14:22
```

``` py
import pendulum
# Creating new DateTime instance
dt = pendulum.datetime(2021, 12, 27, 12, 30, 15)
print(dt)

# Formatting date-time
dt.to_day_datetime_string()
formatted_str = dt.format('dddd Do [of] MMMM YYYY HH:mm:ss A', locale='fr')
print(formatted_str)

new_str = dt.strftime('%Y-%m-%d %H:%M:%S %Z%z')
print(new_str)
```
```
2021-12-27T12:30:15+00:00
lundi 27e of décembre 2021 12:30:15 PM
2021-12-27 12:30:15 UTC+0000
```

``` py
import pendulum
dt = pendulum.parse('1997-11-21T22:00:00',
					tz = 'Asia/Calcutta')
print(dt)

# parsing of non standard string
dt = pendulum.from_format('2020/11/21',
						'YYYY/MM/DD')

print(dt)
```
```
1997-11-21T22:00:00+05:30
2020-11-21T00:00:00+00:00
```
## Time Deltas

``` py
from datetime import date
from datetime import time
from datetime import datetime
from datetime import timedelta

# construct a basic timedelta and print it
print (timedelta(days=365, hours=5, minutes=1))

# print today's date
now = datetime.now()
print(now)
print("today is: ",now)

# print today's date one year from now
print ("one year from now it will be: ", now + timedelta(days=365))

# create a timedelta that uses more than one argument
print ("in two weeks and 3 days it will be: ",now + timedelta(weeks=2, days=3))

# calculate the date 1 week ago, formatted as a string
t = datetime.now() - timedelta(weeks=1)
s = t.strftime("%A %B %d, %Y")
print ("one week ago it was " + s)

### How many days until April Fools' Day?

today = date.today()  # get today's date
afd = date(today.year, 4, 1)  # get April Fool's for the same year
# use date comparison to see if April Fool's has already gone for this year
# if it has, use the replace() function to get the date for next year
if afd < today:
  print ("April Fool's day already went by %d days ago" % ((today-afd).days))
  afd = afd.replace(year=today.year + 1)  # if so, get the date for next year

# Now calculate the amount of time until April Fool's Day  
time_to_afd = afd - today
print ("It's just", time_to_afd.days, "days until next April Fools' Day!")
```
```
365 days, 5:01:00
2021-07-19 14:28:46.250025
today is:  2021-07-19 14:28:46.250025
one year from now it will be:  2022-07-19 14:28:46.250025
in two weeks and 3 days it will be:  2021-08-05 14:28:46.250025
one week ago it was Monday July 12, 2021
April Fool's day already went by 109 days ago
It's just 256 days until next April Fools' Day!
```

``` py
import pendulum
time_delta = pendulum.duration(days = 2,
							hours = 10,
							years = 2)
print(time_delta)

# Date when i am writing this code is 2020-11-27.
print('future date =',
	pendulum.now() + time_delta)
```
```
2 years 2 days 10 hours
future date = 2023-12-25T06:10:31.649124+00:00
```

``` py
dt9=pendulum.datetime(2022,10,13)
di=dt9.diff_for_humans(pendulum.today())
print(di)
```
```
9 months after
```

## Calendar

``` py
import calendar

# create a plain text calendar
c = calendar.TextCalendar(calendar.SUNDAY)
str_te = c.formatmonth(2017, 1, 0, 0)
print (str_te)

# loop over the days of a month
# zeroes mean that the day of the week is in an overlapping month
for i in c.itermonthdays(2017, 8):
  print (i)
  
# The Calendar module provides useful utilities for the given locale,
# such as the names of days and months in both full and abbreviated forms
for name in calendar.month_name:
  print (name)

for day in calendar.day_name:
  print (day)

# Calculate days based on a rule: For example, consider
# a team meeting on the first Friday of every month.
# To figure out what days that would be for each month,
# we can use this script:
print ("Team meetings will be on:")
for m in range(1,13):
  # returns an array of weeks that represent the month
  cal = calendar.monthcalendar(2017, m)
  # The first Friday has to be within the first two weeks
  weekone = cal[0]
  weektwo = cal[1]
   
  if weekone[calendar.FRIDAY] != 0:
    meetday = weekone[calendar.FRIDAY]
  else:
    # if the first friday isn't in the first week, it must be in the second
    meetday = weektwo[calendar.FRIDAY]
      
  print ("%10s %2d" % (calendar.month_name[m], meetday))

```
```
January 2017
Su Mo Tu We Th Fr Sa
 1  2  3  4  5  6  7
 8  9 10 11 12 13 14
15 16 17 18 19 20 21
22 23 24 25 26 27 28
29 30 31

0
0
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
0
0

January
February
March
April
May
June
July
August
September
October
November
December
Monday
Tuesday
Wednesday
Thursday
Friday
Saturday
Sunday
Team meetings will be on:
   January  6
  February  3
     March  3
     April  7
       May  5
      June  2
      July  7
    August  4
 September  1
   October  6
  November  3
  December  1

```