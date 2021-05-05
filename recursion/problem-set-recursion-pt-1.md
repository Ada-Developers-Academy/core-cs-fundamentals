# Problem Set: Recursion Pt. 1

## Directions

Complete all questions below. **Solve all questions using recursion**, and not iteration.

## Practice

<!-- Question 1 -->
<!-- prettier-ignore-start -->
### !challenge
* type: code-snippet
* language: python3.6
* id: E3lY0n
* title: Recursion
* points: 3
### !question

Write a function `factorial` that accepts an integer parameter `n`. It uses recursion to compute and return the value of `n` factorial (also written as `n!`).

Here are the tests:

```python
def test_factorial_zero():
    assert factorial(0) == 1


def test_factorial_positive_num():
    assert factorial(5) == 5 * 4 * 3 * 2 * 1


def test_factorial_negative_num():
    with pytest.raises(ValueError):
        factorial(-1)
```

### !end-question
### !tests
```python
import unittest
from main import *

class TestChallenge(unittest.TestCase):
    def test_factorial_zero(self):
        self.assertEqual(factorial(0), 1)

    def test_factorial_positive_num(self):
        self.assertEqual(factorial(5), 5 * 4 * 3 * 2 * 1)

    def test_factorial_negative_num(self):
        with self.assertRaises(ValueError):
            factorial(-1)
```
### !end-tests
### !explanation

An example of a working implementation:

```python
def factorial(num):
    if num < 0:
        raise ValueError("Number must be greater than zero")
    if num == 0:
        return 1
    return num * factorial(num-1)
```

### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

<!-- Question 2 -->
<!-- prettier-ignore-start -->
### !challenge
* type: code-snippet
* language: python3.6
* id: DvBKYq
* title: Recursion
* points: 3
### !question

Write a function `reverse` that accepts a string `text` as a parameter. It returns the reverse of `text` by reversing all characters in the string.

Here are the tests:

```python
def test_reverse_word():
    assert reverse("cat") == "tac"


def test_reverse_single_character():
    assert reverse("a") == "a"


def test_reverse_empty_string():
    assert reverse("") == ""
```

### !end-question
### !tests
```python
import unittest
from main import *

class TestChallenge(unittest.TestCase):
    def test_reverse_word(self):
        self.assertEqual(reverse("cat"), "tac")

    def test_reverse_single_character(self):
        self.assertEqual(reverse("a"), "a")

    def test_reverse_empty_string(self):
        self.assertEqual(reverse(""), "")
```
### !end-tests
### !explanation

An example of a working implementation:

```python
def reverse(text):
    if len(text) <= 1:
        return text
    # Use Python string slicing to get the
    # first character of text and the
    # remaining characters
    first_char = text[:1]
    remaining_chars = text[1:]
    return reverse(remaining_chars) + first_char
```

### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

<!-- Question 3 -->
<!-- prettier-ignore-start -->
### !challenge
* type: code-snippet
* language: python3.6
* id: i99SZO
* title: Recursion
* points: 3
### !question

Write a function `bunny` that accepts an integer parameter `count`. `count` represents a number of bunnies and each bunny has two big floppy ears. We want to compute the total number of ears across all the bunnies recursively (without loops or multiplication).

Here are the tests:

```python
def test_bunny_zero_bunnies():
    assert bunny(0) == 0


def test_bunny_one_bunny_has_two_ears():
    assert bunny(1) == 2


def test_bunny_fifty_bunnies_have_100_ears():
    assert bunny(50) == 100
```

### !end-question
### !tests
```python
import unittest
from main import *

class TestChallenge(unittest.TestCase):
    def test_bunny_zero_bunnies(self):
        self.assertEqual(bunny(0), 0)

    def test_bunny_one_bunny_has_two_ears(self):
        self.assertEqual(bunny(1), 2)

    def test_bunny_fifty_bunnies_have_100_ears(self):
        self.assertEqual(bunny(50), 100)
```
### !end-tests
### !explanation

An example of a working implementation:

```python
def bunny(count):
    if not count:
        return count
    else:
        return 2 + bunny(count-1)
```

### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

<!-- Question 4 -->
<!-- prettier-ignore-start -->
### !challenge
* type: code-snippet
* language: python3.6
* id: hhiNnl
* title: Recursion
* points: 3
### !question

Write a function `is_nested_parens` that accepts a string `parens` of only parentheses. It returns `True` if those parentheses are properly nested, and `False` if they are not. You may assume that no non-parenthesis characters will be passed to this function.

| Example `parens` | Expected Output |
| --------------- | --------------- |
| `"((()))"`      | `True`          |
| `""`            | `True`          |
| `"(())))"`      | `False`         |

Here are the tests:

```python
def test_is_nested_parens():
    parens = "((()))"

    assert is_nested_parens(parens)


def test_is_nested_parens_empty_str():
    assert is_nested_parens("")


def test_is_nested_parens_not_matching_length():
    parens = "(())))"

    assert not is_nested_parens(parens)
```
### !end-question
### !tests
```python
import unittest
from main import *

class TestChallenge(unittest.TestCase):
    def test_is_nested_parens(self):
        parens = "((()))"

        self.assertTrue(is_nested_parens(parens))

    def test_is_nested_parens_empty_str(self):
        self.assertTrue(is_nested_parens(""))

    def test_is_nested_parens_not_matching_length(self):
        parens = "(())))"

        self.assertFalse(is_nested_parens(parens))
```
### !end-tests
### !explanation

An example of a working implementation:

```python
def is_nested_parens(parens):
    if len(parens) == 0:
        return True
    elif parens[:1] != "(" or parens[-1:] != ")":
        return False
    else:
        return is_nested_parens(parens[1:-1])
```

### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

### !callout-info

## Challenge for `is_nested_parens`

For an additional challenge, implement `is_nested_parens` without creating new strings in the process of solving the problem.

<br />

<details>
    <summary>Hint</summary>

<br />

Sometimes we create extra helper functions that can store more information in their parameters than we might use in the main solution function.

</details>

### !end-callout
