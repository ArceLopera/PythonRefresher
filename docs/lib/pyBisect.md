The purpose of Bisect algorithm is to find a position in list where an element needs to be inserted to keep the list sorted.

Python in its definition provides the bisect algorithms using the module “bisect” which allows to keep the list in sorted order after insertion of each element. This is essential as this reduces overhead time required to sort the list again and again after insertion of each element.

Important Bisection Functions

1. bisect(list, num, beg, end) :- This function returns the position in the sorted list, where the number passed in argument can be placed so as to maintain the resultant list in sorted order. If the element is already present in the list, the right most position where element has to be inserted is returned. This function takes 4 arguments, list which has to be worked with, number to insert, starting position in list to consider, ending position which has to be considered.
2. bisect_left(list, num, beg, end) :- This function returns the position in the sorted list, where the number passed in argument can be placed so as to maintain the resultant list in sorted order. If the element is already present in the list, the left most position where element has to be inserted is returned. This function takes 4 arguments, list which has to be worked with, number to insert, starting position in list to consider, ending position which has to be considered.

3. bisect_right(list, num, beg, end) :- This function works similar to the “bisect()” and mentioned above.
4. insort(list, num, beg, end) :- This function returns the sorted list after inserting number in appropriate position, if the element is already present in the list, the element is inserted at the rightmost possible position. This function takes 4 arguments, list which has to be worked with, number to insert, starting position in list to consider, ending position which has to be considered.

5. insort_left(list, num, beg, end) :- This function returns the sorted list after inserting number in appropriate position, if the element is already present in the list, the element is inserted at the leftmost possible position. This function takes 4 arguments, list which has to be worked with, number to insert, starting position in list to consider, ending position which has to be considered.

6. insort_right(list, num, beg, end) :- This function works similar to the “insort()” as mentioned above.

``` py
# use the bisection functions to maintain a list in sorted order
import bisect

values = [5, 7, 13, 20, 25, 31, 36, 43, 47, 49, 50, 75]

# exercise the left and right bisection routines
print(bisect.bisect(values, 25))
print(bisect.bisect_right(values, 25))

print(bisect.bisect_left(values, 25))

# use insort to insert new items
bisect.insort_right(values, 25)  # will insert to the right
print(values)

# bisect can be used as an array lookup using breakpoints
breakpoints = [60, 70, 80, 90]
gradeLetters = 'FDCBA'
scores = [81, 68, 53, 91, 90, 82, 76, 71, 84]


def calcGrade(score):
    # use the bisect function to identify cutoff points for the letter grades
    i = bisect.bisect(breakpoints, score)
    return gradeLetters[i]


results = [calcGrade(score) for score in scores]
print(results)
```
```
5
5
4
[5, 7, 13, 20, 25, 25, 31, 36, 43, 47, 49, 50, 75]
['B', 'D', 'F', 'A', 'A', 'B', 'C', 'C', 'B']
```