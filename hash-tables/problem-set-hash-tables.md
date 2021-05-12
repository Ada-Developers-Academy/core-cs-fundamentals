# Problem Set: Hash Table

## Directions

Complete all questions below. **Solve all questions using a hash table** (Python dictionary).

## Practice

<!-- Question 1 -->
<!-- prettier-ignore-start -->
### !challenge
* type: code-snippet
* language: python3.6
* id: 9U2j0J
* title: Hash Tables
* points: 3
### !question

Write a function `get_intersection` that takes two integer lists with unique values and returns their intersection in a new array.

Be sure to use a dictionary in your solution. Do not use any built-in intersection functions.

Here are the tests:

```python
def test_get_intersection_one_match():
    red = [2, 3, 4]
    blue = [4, 5, 6]
    assert get_intersection(red, blue) == [4]


def test_get_intersection_no_matches():
    red = [9, 30, 42]
    blue = [56, 34, 90, 32]
    assert get_intersection(red, blue) == []


def test_get_intersection_many_matches():
    red = [50, 43, 25, 72]
    blue = [25, 36, 43, 50, 80]
    result = get_intersection(red, blue)
    assert 25 in result
    assert 43 in result
    assert 50 in result
    assert len(result) == 3
```

### !end-question
### !tests
```python
import unittest
from main import get_intersection
class TestChallenge(unittest.TestCase):
    # Note: Written with these asserts to mimic the pytest assertions we give students

    def test_get_intersection_one_match(self):
        red = [2, 3, 4]
        blue = [4, 5, 6]
        self.assertEqual(get_intersection(red, blue), [4])

    def test_get_intersection_no_matches(self):
        red = [9, 30, 42]
        blue = [56, 34, 90, 32]
        self.assertEqual(get_intersection(red, blue), [])

    def test_get_intersection_many_matches(self):
        red = [50, 43, 25, 72]
        blue = [25, 36, 43, 50, 80]
        result = get_intersection(red, blue)
        self.assertTrue(25 in result)
        self.assertTrue(43 in result)
        self.assertTrue(50 in result)
        self.assertEqual(len(result), 3)
```
### !end-tests
### !explanation

An example of a working implementation:

```python
def get_intersection(red, blue):
    frequency_hash = {}

    for list in [red, blue]:
        for item in list:
            if item in frequency_hash:
                frequency_hash[item] += 1
            else:
                frequency_hash[item] = 1

    intersections = []
    for item, quantity in frequency_hash.items():
        if quantity > 1:
            intersections.append(item)

    return intersections
```

<br/>

Another example of a working implementation:

```python
def get_intersection(red, blue):
    frequency_hash = {}

    for list in [red, blue]:
        for item in list:
            count = frequency_hash.get(item, 0)
            frequency_hash[item] = count + 1

    intersections = []
    for item, quantity in frequency_hash.items():
        if quantity > 1:
            intersections.append(item)

    return intersections
```

### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

<!-- Question 2 -->
<!-- prettier-ignore-start -->
### !challenge
* type: code-snippet
* language: python3.6
* id: LbtYXn
* title: Hash Tables
* points: 3
### !question

Write a function `is_permutation` that takes two strings and returns `True` if one string is a permutation of the other.

Here are the tests:

```python
def test_is_permutation():
    assert is_permutation("hello", "ehllo")


def test_is_permutation_false_different_qty_letters():
    assert not is_permutation("heelo", "ehllo")


def test_is_permutation_false_different_letters():
    assert not is_permutation("pizza", "pasta")


def test_is_permutation_unmatching_lengths():
    assert not is_permutation("pizza", "piza")


def test_is_permutation_same_word():
    assert is_permutation("pizza", "pizza")


def test_is_permutation_empty_strings():
    assert is_permutation("", "")
```

### !end-question
### !tests
```python
import unittest
from main import *
class TestChallenge(unittest.TestCase):
    # Note: Written with these asserts to mimic the pytest assertions we give students

    def test_is_permutation(self):
        self.assertTrue(is_permutation("hello", "ehllo"))

    def test_is_permutation_false_different_qty_letters(self):
        self.assertTrue(not is_permutation("heelo", "ehllo"))

    def test_is_permutation_false_different_letters(self):
        self.assertTrue(not is_permutation("pizza", "pasta"))

    def test_is_permutation_unmatching_lengths(self):
        self.assertTrue(not is_permutation("pizza", "piza"))

    def test_is_permutation_same_word(self):
        self.assertTrue(is_permutation("pizza", "pizza"))

    def test_is_permutation_empty_strings(self):
        self.assertTrue(is_permutation("", ""))
```
### !end-tests
### !hint
Many problems that use dictionaries to solve problems related to strings involve counting the available letters. What must be true about the counts of the letters in two different words in order for them to be permutations of one another?
### !end-hint

### !explanation

An example of a working implementation:

```python
def populate_frequency_map(text):
    frequency_hash = {}
    for char in text:
        if char in frequency_hash:
            frequency_hash[char] += 1
        else:
            frequency_hash[char] = 1
    return frequency_hash


def is_permutation(red, blue):
    red_frequency_hash = populate_frequency_map(red)
    blue_frequency_hash = populate_frequency_map(blue)

    return red_frequency_hash == blue_frequency_hash
```

<br/>

Another example of a working implementation:

```python
def populate_frequency_map(text):
    frequency_hash = {}
    for char in text:
        count = frequency_hash.get(char, 0)
        frequency_hash[char] = count + 1
    return frequency_hash


def is_permutation(red, blue):
    red_frequency_hash = populate_frequency_map(red)
    blue_frequency_hash = populate_frequency_map(blue)

    return red_frequency_hash == blue_frequency_hash
```

### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

<!-- Question 3 -->
<!-- prettier-ignore-start -->
### !challenge
* type: code-snippet
* language: python3.6
* id: 9LkdRV
* title: Hash Tables
* points: 3
### !question

Write a function `is_palindrome_permutation` that takes a string as an argument and returns `True` if the letters could be re-arranged into a palindrome.

Here are the tests:

```python
def test_is_palindrome_permutation_simple():
    assert is_palindrome_permutation("lool")


def test_is_palindrome_permutation_palindrome():
    assert is_palindrome_permutation("racecar")


def test_is_palindrome_permutation_rearranged_palindrome():
    assert is_palindrome_permutation("carrace")


def test_is_palindrome_permutation_incomplete():
    assert not is_palindrome_permutation("raceca")


def test_is_palindrome_permutation_unmatching_letters():
    assert not is_palindrome_permutation("hello")


def test_is_palindrome_permutation_empty_string():
    assert is_palindrome_permutation("")
```

### !end-question
### !tests
```python
import unittest
from main import *
class TestChallenge(unittest.TestCase):
    # Note: Written with these asserts to mimic the pytest assertions we give students

    def test_is_palindrome_permutation_simple(self):
        self.assertTrue(is_palindrome_permutation("lool"))

    def test_is_palindrome_permutation_palindrome(self):
        self.assertTrue(is_palindrome_permutation("racecar"))

    def test_is_palindrome_permutation_rearranged_palindrome(self):
        self.assertTrue(is_palindrome_permutation("carrace"))

    def test_is_palindrome_permutation_incomplete(self):
        self.assertTrue(not is_palindrome_permutation("raceca"))

    def test_is_palindrome_permutation_unmatching_letters(self):
        self.assertTrue(not is_palindrome_permutation("hello"))

    def test_is_palindrome_permutation_empty_string(self):
        self.assertTrue(is_palindrome_permutation(""))
```
### !end-tests
### !hint
Many problems that use dictionaries to solve problems related to strings involve counting the available letters. What must be true about the counts of the letters in a string in order for it to be a palindrome? From the previous problem, can we say that the same must be true about a _permutation_ of a palindrome?
### !end-hint
### !explanation

An example of a working implementation:

```python
def is_palindrome_permutation(text):
    frequency_hash = {}
    for char in text:
        if char in frequency_hash:
            frequency_hash[char] += 1
        else:
            frequency_hash[char] = 1

    odd_matches_count = 0
    for frequency in frequency_hash.values():
        if frequency % 2:
            odd_matches_count += 1

    return odd_matches_count <= 1
```

### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->
