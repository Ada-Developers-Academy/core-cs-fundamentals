# Problem Set: Lists - Memory and Sorting

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: multiple-choice
* id: 55890920-cfd1-47e0-96e8-4e2b1caa3ada
* title: Lists and References
* points: 1
* topics: python-lists

##### !question

True or False, a list variable directly references it's elements.

##### !end-question

##### !options

* True
* False

##### !end-options

##### !answer

* False

##### !end-answer

<!-- other optional sections -->
##### !hint

Think about side effects and functions.

##### !end-hint
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->
<!-- !explanation - !end-explanation (markdown, students can see after answering correctly) -->

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: short-answer
* id: f00befa4-e25a-40b6-b235-618bb0fca09a
* title: Side Effects
* points: 1
* topics: python-lists

##### !question

What is printed by this code segment?

```python
def mystery(numbers):
    index = 0
    while index < len(numbers):
        numbers[index] *= 2
        index += 1
    
    return numbers

nums = [1, 2, 3, 4, 5]
mystery(nums)

print(nums[3])
```


##### !end-question

##### !placeholder

What is printed by print(nums[3])?

##### !end-placeholder

##### !answer

/8/

##### !end-answer

<!-- other optional sections -->
<!-- !hint - !end-hint (markdown, hidden, students click to view) -->
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->
##### !explanation

The loop traverses the list multiplying each number by 2.  Since lists are mutable objects, changing things in `numbers`, the parameter impacts the array referenced by `nums`.


##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: multiple-choice
* id: 5a39abda-3557-49e7-bd9a-409dccc9e1a8
* title: Time complexity of a function
* points: 1
* topics: python-lists, Big-O

##### !question

What is the **time** complexity of the following function?

```python
def max(numbers):
    if len(numbers) == 0:
        return None

    max_num = numbers[0]

    for num in numbers:
        if num > max_num:
            max_num = num
    
    return max_num
```

##### !end-question

##### !options

* O(1)
* O(log n)
* O(n)
* O(n<sup>2</sup>)

##### !end-options

##### !answer

* O(n)

##### !end-answer

<!-- other optional sections -->
##### !hint

What determines the length of the loop?


##### !end-hint

##### !explanation

This loop will **always** traverse the entire length of the list (size n).

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: multiple-choice
* id: 5bbb9400-054c-4667-a82c-86d5b3642e2b
* title: Space complexity of a function
* points: 1
* topics: python-lists, Big-O

##### !question

What is the **space** complexity of the following function?

```python
def max(numbers):
    if len(numbers) == 0:
        return None

    max_num = numbers[0]

    for num in numbers:
        if num > max_num:
            max_num = num
    
    return max_num
```

##### !end-question

##### !options

* O(1)
* O(log n)
* O(n)
* O(n<sup>2</sup>)

##### !end-options

##### !answer

* O(1)

##### !end-answer

<!-- other optional sections -->
##### !hint

Are you building a data structure?

##### !end-hint

##### !explanation

No data structure is created in this function, it just always returns 1 number. 

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: multiple-choice
* id: 727f7ca4-61e8-418d-803f-106c1841367a
* title: Space Complexity Question 2
* points: 1
* topics: python-lists, big-o

##### !question

What is the space complexity of the following function?

```python
def long_words(words):
    big_words = []
    for word in words:
        if len(word) > 5:
            big_words.append(word)
    
    return big_words
```

##### !end-question

##### !options

* O(1)
* O(log n)
* O(n)
* O(n<sup>2</sup>)

##### !end-options

##### !answer

* O(n)

##### !end-answer

<!-- other optional sections -->
##### !hint

Are you creating any data structures?

##### !end-hint
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->
##### !explanation

As the loop executes with each iteration you may add an element to the `big_words` list.  If the `words` list is of size n, worst-case the new list will also be of size n.

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- prettier-ignore-start -->
### !challenge
* type: paragraph
* id: fN9PLJ
* title: Sorting Algorithms
##### !question

Describe the algorithm for Insertion Sort in your own words. Make sure to touch on:

- What makes this different from other algorithms we've seen?
- What is its time and space complexity?
- What factors contribute to its time complexity?

Answer in 3-6 sentences, draw a picture and describe it, or write a poem, an analogy, or a story.

##### !end-question
##### !placeholder

Insertion sort is different from other algorithms we've seen because...

##### !end-placeholder
### !end-challenge
<!-- prettier-ignore-end -->


<!-- prettier-ignore-start -->
### !challenge
* type: code-snippet
* language: python3.6
* id: P2sZ7P
* title: Sorting Algorithms
### !question

There's no better way to get familiar with sorting algorithms than to implement one yourself!

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
