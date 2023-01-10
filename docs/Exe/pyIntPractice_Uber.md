## Fare Estimator

5 min - Easy

Uber is building a Fare Estimator that can tell you how much your ride will cost before you request it. It works by passing approximated ride distance and ride time through this formula:

(Cost per minute) * (ride time) + (Cost per mile) * (ride distance)

where Cost per minute and Cost per mile depend on the car type.

You are one of the engineers building the Fare Estimator, so knowing cost per minute and cost per mile for each car type, as well as ride distance and ride time, return the fare estimates for all car types.

**Example**

For
ride_time = 30,

ride_distance = 7,

cost_per_minute = [0.2, 0.35, 0.4, 0.45], and

cost_per_mile = [1.1, 1.8, 2.3, 3.5], the output should be

solution(ride_time, ride_distance, cost_per_minute, cost_per_mile) = [13.7, 23.1, 28.1, 38].

Since:

```
30 * 0.2 + 7 * 1.1 = 6 + 7.7 = 13.7
30 * 0.35 + 7 * 1.8 = 10.5 + 12.6 = 23.1
30 * 0.4 + 7 * 2.3 = 12 + 16.1 = 28.1
30 * 0.45 + 7 * 3.5 = 13.5 + 24.5 = 38
```

**Solution**
``` py
def solution(ride_time, ride_distance, cost_per_minute, cost_per_mile):
    return [ride_time*i+ride_distance*j for (i,j) in zip(cost_per_minute,cost_per_mile)]
```

## Perfect City

30 min - Medium

Consider a city where the streets are perfectly laid out to form an infinite square grid. In this city finding the shortest path between two given points (an origin and a destination) is much easier than in other more complex cities. As a new Uber developer, you are tasked to create an algorithm that does this calculation.

Given user's departure and destination coordinates, each of them located on some street, find the length of the shortest route between them assuming that cars can only move along the streets. Each street can be represented as a straight line defined by the x = n or y = n formula, where n is an integer.

**Example**

For departure = [0.4, 1] and destination = [0.9, 3], the output should be
solution(departure, destination) = 2.7.

0.6 + 2 + 0.1 = 2.7, which is the answer.

![PerfectCity](./Images/perfCity.png)

**Solution**

``` py
def solution(departure, destination):
    if int(departure[1])==departure[1]:
        x = math.ceil(min(departure[0],destination[0]))
        y = math.floor(max(departure[0],destination[0]))
        return abs(departure[1]-destination[1])+min(abs(x-departure[0])+abs(x-destination[0]),abs(y-departure[0])+abs(y-destination[0]))
    else:
        x = math.ceil(min(departure[1],destination[1]))
        y = math.floor(max(departure[1],destination[1]))
        return abs(departure[0]-destination[0])+min(abs(x-departure[1])+abs(x-destination[1]),abs(y-departure[1])+abs(y-destination[1]))
```