# [Optional] Dynamic Programming Problems

## Directions

Complete all questions below. Be aware, these problems can be very hard.

## Practice

<!-- prettier-ignore-start -->
### !challenge
* type: code-snippet
* language: python3.6
* id: ff66fd15
* title: Algorithmic Strategies
### !question

The **0-1 Knapsack Problem** poses a question of vital importance to cat burglars the world over! Assume we are in a room of \(n\) treasures. Each of the treasures has a weight and a value. We have a knapsack to put these items in, and we can carry up to `max_weight` units of weight. We're only a moderately successful cat burglar, so once we leave the room, an alarm will trigger, alerting security.

We only have one chance to pull off this heist, and make our getaway!

What is the maximum value of the items that we can fit in our knapsack?

Notice that this problem does _not_ ask which items those are, although some variations will do so. **We are only interested in the total maximum value.**

Sourced from: [GeeksforGeeks](https://www.geeksforgeeks.org/0-1-knapsack-problem-dp-10/)

As an example, let's consider the case where there are three items:
| Item | Weight | Value  |
|------|--------|--------|
| 1    | 10     | 60     |
| 2    | 20     | 100    |
| 3    | 30     | 120    |

If we are able to carry 50 units of weight, what is the maximum value of the items we can fit in our knapsack?

In this case, we can take items 2 and 3, which have a combined weight of 50, and a combined value of 220. So our maximum value is 220.

Here are the tests:

```python
def test_empty_knapsack():
    assert knapsack([], [], 0) == 0

def test_small_knapsack(self):
    assert knapsack([10, 20, 30], [60, 100, 120], 50) == 220

def test_medium_knapsack(self):
    assert knapsack(
        [99, 60, 70, 68, 50, 65, 48, 31, 52, 29],
        [104, 105, 138, 135, 82, 73, 103, 52, 57, 136],
        75
    ) == 188
```

### !end-question
### !placeholder

```python
def knapsack(weights, values, max_weight):
    pass
```
### !end-placeholder
### !tests
```python
import unittest
from main import *

class TestZeroOneKnapsack(unittest.TestCase):
    def test_empty_knapsack(self):
        self.assertEqual(knapsack([], [], 0), 0)

    def test_small_knapsack(self):
        self.assertEqual(knapsack([10, 20, 30], [60, 100, 120], 50), 220)

    def test_medium_knapsack(self):
        self.assertEqual(knapsack([99, 60, 70, 68, 50, 65, 48, 31, 52, 29], [104, 105, 138, 135, 82, 73, 103, 52, 57, 136], 75), 188)
```
### !end-tests
### !hint

- Is there a way we can think of this problem as resembling the structure of the longest common subsequence problem?
- What limits are there on whether we are _allowed_ to take an item?
- If we are _able_ to take an item, what aspects around taking or not taking the item do we need to consider?

### !end-hint
### !hint

- If we decide to take an item, what quantity contributes to our overall calculation?
- If we decide to take an item, what effect does that have on our `max_weight`?
- If the weight of the current item exceeds the current `max_weight`, are we allowed to take it? What impact does that have on the recursive calls we would make for that case?

### !end-hint
### !hint

- What conditions would allow us to halt further recursion? What are the base cases?

<br />

The next hint provides a solution skeleton.

### !end-hint
### !hint

Solution skeleton:

```python
def knapsack(weights, values, max_weight):
    # if there are no more items or no more room, the remaining max value is 0

    # get the current weight and remaining weights
    # get the current value and remaining values

    # if there is room for the current item weight
        # we can either:
            # 1. take the current item, which contributes its value to our
            #    possible total, plus the total of the rest of the items with
            #    the max weight diminished by the weight of the current item
            # 2. not take the current item, in which case the total would
            #    be the total of the rest of the items. The max weight is not
            #    affected since we didn't take the current item
        # our max value is the max of these two options
    # otherwise there is no room for the current item
        # our max value must be the max value of the rest of the items

    # return the result
```

### !end-hint

### !explanation

An example of a working implementation:

<br />

```python
def knapsack(weights, values, max_weight):
    if not weights or max_weight <= 0:
        return 0

    weight, rest_weight = weights[0], weights[1:]
    value, rest_value = values[0], values[1:]
    
    if weight <= max_weight:
        result = max(
            value + knapsack(rest_weight, rest_value, max_weight - weight),
            knapsack(rest_weight, rest_value, max_weight)
        )
    else:
        result = knapsack(rest_weight, rest_value, max_weight)

    return result
```

<br />

The following lines use tuple unpacking to create four distinct local variables.

<br />

```python
    weight, rest_weight = weights[0], weights[1:]
    value, rest_value = values[0], values[1:]
```

<br />

The right sides of the assignments create temporary anonymous tuples which are immediately unpacked into the positionally corresponding variables on the left sides of the assignments.

<br />

This could have been similarly accomplished with code such as:

<br />

```python
    weight = weights[0]
    rest_weight = weights[1:]
    value = values[0]
    rest_value = values[1:]
```

<br />

Or by foregoing the use of temporaries entirely. The use of named local variables to refer to the first value and the remaining values of each list is purely for readability.

### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

<!-- prettier-ignore-start -->
### !challenge
* type: code-snippet
* language: python3.6
* id: e3ae7d4e
* title: Algorithmic Strategies
### !question

Let's continue working on the **0-1 Knapsack Problem**. For this challenge, the scenario is the same, and the tests are the same, with one addition:

The new test checks a large, complicated scenario, which is unlikely to complete in the test timeout period unless we apply some dynamic programming strategies to improve the performance!

Here are the tests:

```python
def test_empty_knapsack():
    assert knapsack([], [], 0) == 0

def test_small_knapsack(self):
    assert knapsack([10, 20, 30], [60, 100, 120], 50) == 220

def test_medium_knapsack(self):
    assert knapsack(
        [99, 60, 70, 68, 50, 65, 48, 31, 52, 29],
        [104, 105, 138, 135, 82, 73, 103, 52, 57, 136],
        75
    ) == 188

def test_large_knapsack(self):
    assert knapsack(
        [92, 39, 56, 81, 59, 38, 71, 91, 73, 34, 13, 27, 10, 49, 56, 90, 66, 91, 47, 52, 46, 43, 69, 53, 90, 99, 84, 41, 33, 89, 46, 78, 29, 16, 58, 44, 11, 87, 26, 13, 11, 63, 81, 51, 12, 90, 29, 100, 93, 43, 52, 65, 45, 46, 45, 98, 74, 58, 60, 100, 42, 66, 56, 37, 80, 68, 91, 63, 65, 73, 59, 10, 41, 30, 88, 79, 11, 94, 20, 89, 83, 70, 47, 75, 19, 15, 33, 34, 94, 65, 66, 44, 62, 95, 45, 17, 92, 93, 27, 43],
        [96, 56, 143, 123, 96, 83, 82, 117, 82, 52, 66, 126, 122, 90, 128, 149, 149, 116, 55, 145, 111, 145, 63, 137, 85, 148, 70, 125, 57, 72, 82, 124, 107, 137, 127, 139, 125, 94, 111, 108, 117, 142, 121, 103, 140, 54, 82, 55, 104, 50, 98, 82, 50, 64, 105, 112, 70, 113, 91, 72, 108, 112, 132, 141, 85, 138, 94, 117, 137, 104, 54, 135, 105, 95, 135, 150, 143, 144, 143, 132, 52, 90, 100, 119, 59, 147, 125, 55, 101, 90, 72, 90, 58, 131, 123, 76, 109, 130, 138, 77],
        200
    ) == 1657
```

### !end-question
### !placeholder

```python
def knapsack(weights, values, max_weight):
    pass
```
### !end-placeholder
### !tests
```python
import unittest
from main import *

class TestZeroOneKnapsack(unittest.TestCase):
    def test_empty_knapsack(self):
        self.assertEqual(knapsack([], [], 0), 0)

    def test_small_knapsack(self):
        self.assertEqual(knapsack([10, 20, 30], [60, 100, 120], 50), 220)

    def test_medium_knapsack(self):
        self.assertEqual(knapsack([99, 60, 70, 68, 50, 65, 48, 31, 52, 29], [104, 105, 138, 135, 82, 73, 103, 52, 57, 136], 75), 188)

    def test_large_knapsack(self):
        self.assertEqual(knapsack([92, 39, 56, 81, 59, 38, 71, 91, 73, 34, 13, 27, 10, 49, 56, 90, 66, 91, 47, 52, 46, 43, 69, 53, 90, 99, 84, 41, 33, 89, 46, 78, 29, 16, 58, 44, 11, 87, 26, 13, 11, 63, 81, 51, 12, 90, 29, 100, 93, 43, 52, 65, 45, 46, 45, 98, 74, 58, 60, 100, 42, 66, 56, 37, 80, 68, 91, 63, 65, 73, 59, 10, 41, 30, 88, 79, 11, 94, 20, 89, 83, 70, 47, 75, 19, 15, 33, 34, 94, 65, 66, 44, 62, 95, 45, 17, 92, 93, 27, 43], [96, 56, 143, 123, 96, 83, 82, 117, 82, 52, 66, 126, 122, 90, 128, 149, 149, 116, 55, 145, 111, 145, 63, 137, 85, 148, 70, 125, 57, 72, 82, 124, 107, 137, 127, 139, 125, 94, 111, 108, 117, 142, 121, 103, 140, 54, 82, 55, 104, 50, 98, 82, 50, 64, 105, 112, 70, 113, 91, 72, 108, 112, 132, 141, 85, 138, 94, 117, 137, 104, 54, 135, 105, 95, 135, 150, 143, 144, 143, 132, 52, 90, 100, 119, 59, 147, 125, 55, 101, 90, 72, 90, 58, 131, 123, 76, 109, 130, 138, 77], 200), 1657)
```
### !end-tests
### !hint

- We probably need to add an additional parameter to be able to store and pass memoized data.
- What data type would be appropriate for storing the memoized data?
- How can we initialize the storage for the memoized data?
- Where do we need to update our memoized data?
- Where do we need to pass our memoized data?
  
### !end-hint

### !hint

- What piece or pieces of data coming into the function call can be used to uniquely mark _this_ function call? The weights? The values? The max weight? Are any of these redundant?
- If multiple pieces of data are required, how can we use those as keys into our memoized data? Can we use multi-dimensional storage? Is there a way to pack multiple pieces of data into a single piece of data?
- If any of the data we would like to use as keys is mutable, can that be used? Is there a way to convert it to immutable data?

<br />

The next hint will show some examples of a possible key to use for our memoization.
  
### !end-hint
### !hint

We might define a key for our memoized storage as follows:

```python
key = (tuple(weights), max_weight)
```

or

```python
key = (len(weights), max_weight)
```

- What do parentheses mean in Python when used this way? How does this allow us to use these multiple data items as a single key?
- Why would we convert the list of weights to a tuple of weights?
- Why would using the length of the weights list be enough?

<br />

The next hint provides a solution skeleton.

### !end-hint
### !hint

Solution skeleton:

```python
def knapsack(weights, values, max_weight, memo=None):
    # initialize the memo storage object if needed

    # determine whether a result for the current function call is already in the memo
    # if the current call is already memoized
        # return the memoized value

    # if there are no more items or no more room, the remaining max value is 0

    # get the current weight and remaining weights
    # get the current value and remaining values

    # if there is room for the current item weight
        # we can either:
            # 1. take the current item, which contributes its value to our
            #    possible total, plus the total of the rest of the items with
            #    the max weight diminished by the weight of the current item.
            #    Be sure to supply the memoized data to the recursive call!
            # 2. not take the current item, in which case the total would
            #    be the total of the rest of the items. The max weight is not
            #    affected since we didn't take the current item.
            #    Be sure to supply the memoized data to the recursive call!
        # our max value is the max of these two options
    # otherwise there is no room for the current item
        # our max value must be whatever the max value is of the rest of the items.
        # Be sure to supply the memoized data to the recursive call!

    # store whatever result we arrived at in our memoized storage

    # return the result
```

### !end-hint
### !explanation

An example of a working implementation:

<br />

```python
def knapsack(weights, values, max_weight, memo=None):
    if memo is None:
        memo = {}

    key = (len(weights), max_weight)
    if key in memo:
        return memo[key]

    if not weights or max_weight <= 0:
        return 0

    weight, rest_weight = weights[0], weights[1:]
    value, rest_value = values[0], values[1:]
    
    if weight <= max_weight:
        result = max(
            value + knapsack(rest_weight, rest_value, max_weight - weight, memo),
            knapsack(rest_weight, rest_value, max_weight, memo)
        )
    else:
        result = knapsack(rest_weight, rest_value, max_weight, memo)        

    memo[key] = result

    return result
```
### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->
