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

## Parking Spot

30 min - Medium

This time you are an Uber driver and you are trying your best to park your car in a parking lot.

Your car has length carDimensions[0] and width carDimensions[1]. You have already picked your lucky spot (rectangle of the same size as the car with upper left corner at (luckySpot[0], luckySpot[1])) and bottom right corner at (luckySpot[2], luckySpot[3]) and you need to find out if it's possible to park there or not.

It is possible to park your car at a given spot if and only if you can drive through the parking lot without any turns to your lucky spot (for safety reasons, the car can only move in two directions inside the parking lot - forwards or backwards along the long side of the car) starting from some side of the lot (all four sides are valid options).

Naturally, you can't park your car if the lucky spot is already occupied. The car can't drive through or park at any of the occupied spots.

**Example**

For carDimensions = [3, 2],
```
parkingLot = [[1, 0, 1, 0, 1, 0],
              [0, 0, 0, 0, 1, 0],
              [0, 0, 0, 0, 0, 1],
              [1, 0, 1, 1, 1, 1]]
```
and
luckySpot = [1, 1, 2, 3], the output should be

solution(carDimensions, parkingLot, luckySpot) = true


![Parking](./Images/parkin.png)

For carDimensions = [3, 2],
```
parkingLot = [[1, 0, 1, 0, 1, 0],
              [1, 0, 0, 0, 1, 0],
              [0, 0, 0, 0, 0, 1],
              [1, 0, 0, 0, 1, 1]]
```
and
luckySpot = [1, 1, 2, 3], the output should be

solution(carDimensions, parkingLot, luckySpot) = false;

For carDimensions = [4, 1],
```
parkingLot = [[1, 0, 1, 0, 1, 0],
              [1, 0, 0, 0, 1, 0],
              [0, 0, 0, 0, 0, 1],
              [1, 0, 0, 0, 1, 1]]
```
and
luckySpot = [0, 3, 3, 3], the output should be

solution(carDimensions, parkingLot, luckySpot) = true.

**Solution**

``` py
def solution(dim, lot, spot):
    if not is_empty(lot,spot[:2],spot[2:]):
        return False
        
    if spot[3] - spot[1] > spot[2] - spot[0]:
        return is_empty(lot, (spot[0],0),(spot[2],spot[1])) or is_empty(lot,(spot[0],spot[3]),(spot[2], len(lot[0]) -1))
    else:
        return is_empty(lot, (0, spot[1]),(spot[0],spot[3])) or is_empty(lot, (spot[2],spot[1]),( len(lot) -1, spot[3]))
    
        
def is_empty(l,p1,p2):
    for i in range(p1[0], p2[0]+1):
        for j in range(p1[1],p2[1]+1):
            if l[i][j] == 1:
                return False
    return True
```

## Fancy Ride

5 min - Easy

Being a new Uber user, you have $20 off your first ride. You want to make the most out of it and drive in the fanciest car you can afford, without spending any out-of-pocket money. There are 5 options, from the least to the most expensive: "UberX", "UberXL", "UberPlus", "UberBlack" and "UberSUV".

You know the length l of your ride in miles and how much one mile costs for each car. Find the best car you can afford.

**Example**

For l = 30 and fares = [0.3, 0.5, 0.7, 1, 1.3], the output should be
solution(l, fares) = "UberXL".

The cost for the ride in this car would be $15, which you can afford, but "UberPlus" would cost $21, which is too much for you.

**Solution**

``` py
def solution(l, fares):
    opt=["UberX", "UberXL", "UberPlus", "UberBlack", "UberSUV"]
    for ride,cost in enumerate(fares):
        if cost*l <= 20:
            ans = opt[ride]
    return ans 
```

## Night Route

15 min - Medium

Consider a big city located on n islands. There are bridges connecting the islands, but they all have only one-way traffic. To make matters worse, most of the bridges are closed at night, so there is at most one bridge with traffic going from any island A to any other island B.

There is a programmer who turns a penny by working nights as an Uber driver. One night his phone dies right after he picks up a rider going from island 0 to island (n - 1). He has the map of the city bridges in his laptop though (stored as a matrix of distances), so he decides to implement an algorithm that calculates the shortest path between those two islands and evaluate the cost based on the distance of the path. Assume that each mile of the trip is 1$.

**Example**

For
```
city = [[-1, 5, 20],
        [21, -1, 10],
        [-1, 1, -1]]
```
the output should be solution(city) = 15.

city[i][j] equals the distance between the ith and the jth islands in miles, or -1 if there is no bridge by which one can move from island i to island j.

solution(city) should be 15, since the shortest distance from the 0th to the 2nd island is 15. The distance from the 0th to the 1st is city[0][1] = 5, and from the 1st to the 2nd is city[1][2] = 10.

![uber1](./Images/uber1.png)

For
```
city = [[-1, 5, 2, 15],
        [2, -1, 0, 3],
        [1, -1, -1, 9],
        [0, 0, 0, -1]]
```
the output should be solution(city) = 8.

The shortest path is 0 -> 1 -> 3 which costs 5 + 3 = 8.

![uber2](./Images/uber2.png)

**Solution**
``` py
#Todo
```
