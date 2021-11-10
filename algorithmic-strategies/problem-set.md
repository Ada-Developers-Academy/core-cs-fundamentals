# Problem Set 

## Directions

Complete all questions below.

## Practice


<!-- prettier-ignore-start -->

### !challenge

* type: code-snippet
* language: python3.6
* id: 9690c9f6-abd1-4c1c-a4eb-2cee2d7ec3c6
* title: Smallest Missing Element


##### !question

Given a sorted list of non-negative and distinct integers, find the smallest missing non-negative element in the list.

```
Input:  nums[] = [0, 1, 2, 6, 9, 11, 15]
Output: The smallest missing element is 3
 
 
Input:  nums[] = [1, 2, 3, 4, 6, 9, 11, 15]
Output: The smallest missing element is 0
 
 
Input:  nums[] = [0, 1, 2, 3, 4, 5, 6]
Output: The smallest missing element is 7 
```

This problem could be solved with a linear search, but if you examine sample input 3, this could lead to an O(n) runtime.  Instead we can use a divide & conquer approach.  

What algorithm do we know which is faster than O(n) and uses a divide and conquer approach?

Here are the tests:

```python
def test_empty_list():
    assert find_smallest_missing_number([]) == 0

def test_missing_three():
    assert find_smallest_missing_number([0, 1, 2, 4, 5, 6]) == 3

def test_missing_last_number_seven():
        assert find_smallest_missing_number([0, 1, 2, 3, 4, 5, 6]) == 7
```

##### !end-question

##### !placeholder

```py
def find_smallest_missing_number(nums, left=None, right=None):
    """ Returns the smallest non-negative integers.
    """
    if left is None and right is None:
        left = 0
        right = len(nums) - 1
    pass
```

##### !end-placeholder

##### !tests


```py
import unittest
from main import find_smallest_missing_number

class TestPython1(unittest.TestCase):
    def test_empty_list(self):
        self.assertEqual(0,find_smallest_missing_number([]))
    
    def test_missing_three(self):
        self.assertEqual(3,find_smallest_missing_number([0, 1, 2, 4, 5, 6]))

    def test_missing_last_number_seven(self):
        self.assertEqual(7,find_smallest_missing_number([0, 1, 2, 3, 4, 5, 6]))

```
##### !end-tests

##### !hint

Could you use something like binary search?

##### !end-hint

##### !explanation

Our solution:

```python
def find_smallest_missing_number(nums, left=None, right=None):
    """ Returns the smallest non-negative integers.
    """
    if left is None and right is None:
        left = 0
        right = len(nums) - 1
    
    if left > right:
        return left
    mid = (left + right) // 2

    if nums[mid] == mid: # i.e. if `mid` is not at the wrong index
        # Then search the left side for the missing number
        return find_smallest_missing_number(nums, mid + 1, right)
    else:
        return find_smallest_missing_number(nums, left, mid - 1)
```

##### !end-explanation

### !end-challenge

<!-- prettier-ignore-end -->

<!-- prettier-ignore-start -->
### !challenge

* type: code-snippet
* language: python3.6
* id: d6a0c681-4e89-49a1-a3c4-0a8cc5a3dac4
* title: Ugly Numbers

##### !question

Ugly numbers are numbers whose only prime factors are 2, 3, or 5. Essentially if you divide an ugly number by 2, 3, and 5 until they no longer divide evenly, you will end up with a 1.

For example:  6 is ugly because 6 / 2 == 3 and 3 / 3 == 1.
30 is an ugly number because 30 / 2 == 15 and 15 / 3 == 5 and 5 / 5 == 1.

On the other hand 14 is *not* an ugly number because 14 / 2 == 7 and 7 is not evenly divisible by 2, 3, or 5.

The sequence of ugly numbers are 1, 2, 3, 4, 5, 6, 8, 9, 10, 12, 15...  By convention, 1 is included.

**The Problem**:

Given a number `n` find the nth ugly number.

```
Input:  n = 7
Output: 8

Input: n = 1
Output: 1

Input: n = 10
Output: 12

Input:  n = 150
Output: 5832
```

Here are the tests:

```python
def test_n_is_7():
    assert get_nth_ugly_number(7) == 8

def test_n_is_1():
    assert get_nth_ugly_number(1) == 1

def test_n_is_10():
    assert get_nth_ugly_number(10) == 12

def test_n_is_150():
    assert get_nth_ugly_number(150) == 5832
```

##### !end-question

##### !placeholder

```py
def get_nth_ugly_number(n):
    """ Returns the nth ugly number.
        Hint:  use a dynamic programming approach.
    """ 
    pass
```

##### !end-placeholder

##### !tests


```py
import unittest
from main import get_nth_ugly_number

class TestPython1(unittest.TestCase):
  def test_n_is_7(self):
    self.assertEqual(8,get_nth_ugly_number(7))

  def test_n_is_1(self):
    self.assertEqual(1,get_nth_ugly_number(1))

  def test_n_is_10(self):
    self.assertEqual(12,get_nth_ugly_number(10))

  def test_n_is_150(self):
    self.assertEqual(5832,get_nth_ugly_number(150))
```

##### !end-tests

##### !hint

You can start with the first ugly number `1` in a list and use 2, 3, and 5 to calculate the next number.  Then you can append it to the list and repeat the process until you reach the nth ugly number.

```python
last_multiple_of_2 = 0
last_multiple_of_3 = 0
last_multiple_of_5 = 0
ugly_numbers = [1]

# Then find the minimum of:
# ugly_numbers[last_multiple_of_2] * 2,
# ugly_numbers[last_multiple_of_3] * 3,
# ugly_numbers[last_multiple_of_5] * 5,

# And use that to find the next ugly number.
```

##### !end-hint

##### !explanation

Our solution:

```python
def get_nth_ugly_number(n):
    """ Returns the nth ugly number.
        Hint:  use a dynamic programming approach.
    """ 
    last_multiple_of_2 = 0
    last_multiple_of_3 = 0
    last_multiple_of_5 = 0
    ugly_numbers = [1]

    for i in range(1, n):
        multiple_of_2 = ugly_numbers[last_multiple_of_2] * 2
        multiple_of_3 = ugly_numbers[last_multiple_of_3] * 3
        multiple_of_5 = ugly_numbers[last_multiple_of_5] * 5

        next_ugly_number = min(multiple_of_2, multiple_of_3, multiple_of_5)

        if next_ugly_number == multiple_of_2:
            last_multiple_of_2 += 1
        if next_ugly_number == multiple_of_3:
            last_multiple_of_3 += 1
        if next_ugly_number == multiple_of_5:
            last_multiple_of_5 += 1

    # Return the last ugly number in our list
    return ugly_numbers[-1]
```

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->