# \[Optional\] Problem Set: Recursion Pt. 2

## Directions

Complete all questions below. **Solve all questions using recursion**, and not iteration.

## Practice

<!-- Question 1 -->
<!-- prettier-ignore-start -->
### !challenge
* type: code-snippet
* language: python3.6
* id: nCv8Qu
* title: Recursion
* points: 3
### !question

Write a function `search` that accepts an unsorted array of strings, `array`, and a string value to find, `query`. It returns `True` if `query` is found in `array`, and `False` otherwise. Make the algorithm recursive.

Be sure to implement `search` using recursion.

Here are the tests:

```python
def test_search_success_unsorted():
    assert search(["b", "c", "a"], "a")


def test_search_empty_array():
    assert not search([], "a")


def test_search_success_first_item():
    assert search(["a", "b", "c"], "a")


def test_search_not_found():
    assert not search(["a", "b", "c"], "🌈")
```

### !end-question
### !tests
```python
import unittest
from main import *

class TestChallenge(unittest.TestCase):
    def test_search_success_unsorted(self):
        self.assertTrue(search(["b", "c", "a"], "a"))

    def test_search_empty_array(self):
        self.assertFalse(search([], "a"))

    def test_search_success_first_item(self):
        self.assertTrue(search(["a", "b", "c"], "a"))

    def test_search_not_found(self):
        self.assertFalse(search(["a", "b", "c"], "🌈"))
```
### !end-tests
### !explanation

An example of a working implementation:

```python
def search(array, query):
    if not len(array):
        return False
    elif array[0] == query:
        return True
    # Use Python slicing to get all items
    # besides the first item
    return search(array[1:], query)
```

### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

<!-- Question 2 -->
<!-- prettier-ignore-start -->
### !challenge
* type: code-snippet
* language: python3.6
* id: 0PjlSp
* title: Recursion
* points: 3
### !question

Write a recursive function `is_palindrome` that accepts a string `text` as a parameter. It returns a boolean value indicating whether or not that string is a [palindrome](https://en.wikipedia.org/wiki/Palindrome).

| Input `text` | Return value |
| ------------ | ------------ |
| `"racecar"`  | `True`       |
| `"raecar"`   | `False`      |

Here are the tests:

```python
def test_is_palindrome_success():
    assert is_palindrome("racecar")


def test_is_palindrome_not_palindrome():
    assert not is_palindrome("raecar")
```

### !end-question
### !tests
```python
import unittest
from main import *

class TestChallenge(unittest.TestCase):
    def test_is_palindrome_success(self):
        self.assertTrue(is_palindrome("racecar"))

    def test_is_palindrome_not_palindrome(self):
        self.assertFalse(is_palindrome("raecar"))
```
### !end-tests
### !explanation

An example of a working implementation:

```python
def is_palindrome(text):
    if len(text) <= 1:
        return True
    # Use Python slicing to check if
    # the first character is equal to
    # the last character
    elif text[:1] != text[-1:]:
        return False
    else:
        # Use Python slicing to pass in
        # the substring between the first
        # and last characters of text
        return is_palindrome(text[1:-1])
```

### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

### !callout

## Challenge for `is_palindrome`

For an additional challenge, implement `is_palindrome` without creating new strings in the process of solving the problem.

### !end-callout

<!-- Question 3 -->
<!-- prettier-ignore-start -->
### !challenge
* type: code-snippet
* language: python3.6
* id: lkW6SO
* title: Recursion
* points: 3
### !question

Write a recursive function named `digit_match`. It accepts two non-negative integers as parameters. It returns the number of digits that match in the two integers.

Two digits match if they are equal _and_ have the same position relative to the end of the number (i.e. starting with the ones digit).

In other words, the function should compare the last digits of each number, the second-to-last digits of each number, the third-to-last digits of each number, and so fort, counting how many pairs match.

Example:

- First number: `1072503891`
- Second number: `62530841`
- Number of matches: `4`
    - Matching pairs: 2-2, 5-5, 8-8, 1-1

```
1 0 7 2 5 0 3 8 9 1
    | | | | | | | |
    6 2 5 3 0 8 4 1
```

Here are the tests:

```python
def test_digit_match_large_inputs():
    apples = 1072503891
    oranges = 62530841

    assert digit_match(apples, oranges) == 4


def test_digit_match_no_matches():
    apples = 0
    oranges = 62530841

    assert digit_match(apples, oranges) == 0


def test_digit_match_clustered_matches():
    apples = 841
    oranges = 62530841

    assert digit_match(apples, oranges) == 3


def test_digit_match_single_digits():
    apples = 0
    oranges = 0

    assert digit_match(apples, oranges) == 1


def test_digit_match_small_inputs():
    apples = 10
    oranges = 20

    assert digit_match(apples, oranges) == 1
```

### !end-question
### !tests
```python
import unittest
from main import *

class TestChallenge(unittest.TestCase):
    def test_digit_match_large_inputs(self):
        apples = 1072503891
        oranges = 62530841

        self.assertEqual(digit_match(apples, oranges), 4)

    def test_digit_match_no_matches(self):
        apples = 0
        oranges = 62530841

        self.assertEqual(digit_match(apples, oranges), 0)

    def test_digit_match_clustered_matches(self):
        apples = 841
        oranges = 62530841

        self.assertEqual(digit_match(apples, oranges), 3)

    def test_digit_match_single_digits(self):
        apples = 0
        oranges = 0

        self.assertEqual(digit_match(apples, oranges), 1)

    def test_digit_match_small_inputs(self):
        apples = 10
        oranges = 20

        self.assertEqual(digit_match(apples, oranges), 1)

```
### !end-tests
### !explanation

An example of a working implementation:

```python
def digit_match(apples, oranges):
    # Base cases:
    # If both apples and oranges are 0 return 1
    if apples == 0 and oranges == 0:
        return 1
    # If one or both are 1-digit numbers
    elif apples < 10 or oranges < 10:
        if apples % 10 == oranges % 10:
            return 1
        
        return 0
    
    # Recursive Cases
    if apples % 10 == oranges % 10:
        return 1 + digit_match(apples // 10, oranges // 10)
        
    return digit_match(apples // 10, oranges // 10)

```

### !end-explanation
### !hint

Our solution uses Python's _floor division operator_, `//`.

When Python divides two numbers, it will give you the answer:

```python
19 / 10
# 1.9
12 / 10
# 1.2
9 / 10
# 0.9
3 / 10
# 0.3
```

With floor division, Python returns the answer, rounded down to a whole number. Observe:

```python
19 // 10
# 1
12 // 10
# 1
9 // 10
# 0
3 // 10
# 0
```

Any number less than 10 `//` by `10` will return `0`.

### !end-hint
### !end-challenge
<!-- prettier-ignore-end -->
