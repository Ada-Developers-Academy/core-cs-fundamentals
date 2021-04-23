# Problem Set: Recursion Pt. 2

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

Write a function `search` that accepts an unsorted array of integers, `array`, and an integer value to find, `needle`. It returns `True` if `needle` is found in `array`, and `False` otherwise. Make the algorithm recursive.

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
def search(array, needle):
    if not len(array):
        return False
    elif array[0] == needle:
        return True
    # Use Python slicing to get all items
    # besides the first item
    return search(array[1:], needle)
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

Write a recursive function `is_palindrome` that accepts a string `text` as a parameter. It returns a boolean value indicating if that string is a [palindrome](https://en.wikipedia.org/wiki/Palindrome) or not.

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
