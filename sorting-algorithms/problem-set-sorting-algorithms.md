# Problem Set: Sorting Algorithms

## Directions

Complete all questions below.

## Practice

<!-- Question 1 -->
<!-- prettier-ignore-start -->
### !challenge
* type: paragraph
* id: fN9PLJ
* title: Sorting Algorithms
##### !question

Describe the algorithm for Insertion Sort in your own words. Make sure to touch on:

- What makes this algorithm unique?
- What is its time and space complexity?
- What factors contribute to its time complexity?

Answer in 3-6 sentences, draw a picture and describe it, or write a poem, an analogy, or a story.

##### !end-question
##### !placeholder

The insertion sort algorithm is unique because...

##### !end-placeholder
### !end-challenge
<!-- prettier-ignore-end -->

<!-- Question 2 -->
<!-- prettier-ignore-start -->
### !challenge
* type: paragraph
* id: oIbAq4
* title: Sorting Algorithms
##### !question

Describe the algorithm for Merge Sort in your own words. Make sure to touch on:

- What makes this algorithm unique?
- What is its time complexity?
- What factors contribute to its time complexity?

Answer in 3-6 sentences, draw a picture and describe it, or write a poem, an analogy, or a story.

##### !end-question
##### !placeholder

The merge sort algorithm is unique because...

##### !end-placeholder
### !end-challenge
<!-- prettier-ignore-end -->

<!-- Question 3 -->
<!-- prettier-ignore-start -->
### !challenge
* type: code-snippet
* language: python3.6
* id: P2sZ7P
* title: Sorting Algorithms
### !question

There's nothing like getting familiar with sorting algorithms than to implement it yourself!

Without using Python's `sort()` method (or anything like that), implement `sort_by_length` based on insertion sort.

`sort_by_length` is a function that takes in one string. It returns a list of strings, where the items are the words from the string, ordered by length. Words with shorter length are placed before words with longer length.

When words are tied for length, maintain the order they appeared in the original string.

Here are the tests:

```python
def test_sort_by_length_with_empty_string():
    assert sort_by_length("") == []


def test_sort_by_length():
    assert sort_by_length("I love great awesome words") == [
        "I", "love", "great", "words", "awesome"]


def test_sort_by_length_checks_smallest_word_last():
    assert sort_by_length("love great awesome words I") == [
        "I", "love", "great", "words", "awesome"]


def test_sort_by_length_equal_length_maintains_order():
    assert sort_by_length("words of equal length") == [
        "of", "words", "equal", "length"]
```

### !end-question
### !placeholder

```python
def sort_by_length(sentence):
    pass
```
### !end-placeholder
### !tests
```python
import unittest
from main import *

class TestPython1(unittest.TestCase):
    def test_sort_by_length_with_empty_string(self):
        self.assertEqual(sort_by_length(""), [])

    def test_sort_by_length(self):
        self.assertEqual(sort_by_length("I love great awesome words"),
                         ["I", "love", "great", "words", "awesome"])

    def test_sort_by_length_checks_smallest_word_last(self):
        self.assertEqual(sort_by_length("love great awesome words I"),
                         ["I", "love", "great", "words", "awesome"])

    def test_sort_by_length_equal_length_maintains_order(self):
        self.assertEqual(sort_by_length("words of equal length"),
                         ["of", "words", "equal", "length"])
```
### !end-tests
### !explanation

An example of a working implementation:

```python
def sort_by_length(sentence):
    array = sentence.split()
    i = 1
    while i < len(array):
        to_insert = array[i]
        j = i
        # Search in the sorted portion of the list
        # for the correct position to insert sentence[i]
        while j > 0 and len(array[j-1]) > len(to_insert):
            array[j] = array[j-1]
            j -= 1
        array[j] = to_insert
        i += 1
    return array
```

### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

<!-- Question 4 -->
<!-- prettier-ignore-start -->
### !challenge
* type: paragraph
* id: U2QaR9
* title: Sorting Algorithms
##### !question

Describe the time and space complexity of your implementation of `sort_by_length`.

##### !end-question
##### !placeholder

The time complexity is... The space complexity is...

##### !end-placeholder
### !end-challenge
<!-- prettier-ignore-end -->
