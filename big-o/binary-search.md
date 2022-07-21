# Binary Search

## Learning Goals

* Explain the steps in an binary search algorithm
* Understand the iterative implementation of binary search
* Apply time and space complexity analysis to binary search


## Introduction

<!-- Question 10 -->
<!-- prettier-ignore-start -->
### !challenge
* type: multiple-choice
* id: b9HqKs
* title: Big O
##### !question

What is the time complexity of the following piece of code? Assume that `input_list` is in sorted order.

```python
def binary_search(input_list, value):
    low = 0
    high = len(input_list) - 1
    while low <= high:
        mid = int((low + high) / 2)
        if input_list[mid] > value:
            high = mid - 1
        elif input_list[mid] < value:
            low = mid + 1
        else:
            return mid

    if input_list[low] == value:
        return low

    return None
```

##### !end-question
##### !options

* O(1)
* O(log n)
* O(n)
* O(n log n)
* O(n<sup>2</sup>)
* O(n<sup>3</sup>)

##### !end-options
##### !answer

* O(log n)

##### !end-answer
##### !explanation

There is one loop in this method. The number of times the loop runs is proportional to the length of `input_list`. With each iteration through the loop, half of the items in `input_list` are eliminated (either the first half or the second half) until either the value is found or the loop ends. Since with each iteration through the loop, half of the values in the remaining sub-array are eliminated, the time complexity of this algorithm is _logarithmic_ or _O(log n)_ where _n_ is the length of the input parameter, `input_list`.

##### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

