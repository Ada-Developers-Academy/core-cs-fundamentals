# Binary Search

## Learning Goals

* Explain the steps in an binary search algorithm
* Understand the iterative implementation of binary search
* Apply time and space complexity analysis to binary search

## Introduction

Binary search is an efficient algorithm for finding an item in a sorted list. It works by repeatedly dividing in half the portion of the list that could contain the item, until you've narrowed down the possible locations to just one [source](https://www.khanacademy.org/computing/computer-science/algorithms/binary-search/a/binary-search#:~:text=Binary%20search%20is%20an%20efficient,game%20in%20the%20introductory%20tutorial.).


## Binary Search Steps

### Real World Example

The steps to the binary search algorithm can be best understand through an example. Let's imagine searching for a specific person in an address book. [reference](https://www.bbc.co.uk/bitesize/guides/z7kkw6f/revision/8), [stackoverflow example](https://stackoverflow.com/questions/2307283/what-does-olog-n-mean-exactly/2307314#2307314).
1. Start by picking a point in the middle of the address book.
2. If that is the person, the search ends.
3. If the person at the midpoint is alphabetically before the person you are searching for, divide the book in half, ignore the first half, and continue the search with the later half.
4. Alternatively, if the  person at the midpoint is alphabetically after the person you are searching for, divide the book in half, ignore the later half, and continue the search with the first half.
5. Steps 2-4 continue until the person if found or there are no more items.

### Code Implementation

The steps described above are implemented in code in the `binary_search` function below.

```py
def binary_search(array, value):
    low = 0
    high = len(array) - 1
    while low <= high:
        mid = (low + high)//2
        if array[mid] > value:
            high = mid - 1
        elif array[mid] < value:
            low = mid + 1
        else:
            return mid

        if array[low] == value:
            return low

    return None
```

Let's analyze this algorithm by using a loop table with a concrete example of searching for a `value` in an `array` of integers. Imagine a `array` of eight elements `[1, 2, 3, 4, 5, 6, 7, 8]`. The `value` we are searching for is `2`:

| Iteration | `low` | `high` |`low <= high`| `mid` | 
|--|--|--|--|--|
|1| `0` | `7` | `True` | `3` | 
|2| `0` | `2` | `True` | `1` |

On the second iteration, the line `return mid` is executed because `array[1] = 2`

Notice with each iteration the size of the input involved in the search (`low` to `high`) is halved. So worst-case a list of 8 items would take 3 iterations to find the value. We could double the size of `numbers` to 16 items and it would only take 4 iteration to find the value and for 32 items it would only take 5 iterations. Thus while the function *does* take longer as the input size increases it does not increase very rapidly.

The table below summarizes the number of iterations in the worst case scenario required to find a `value` with the `binary_search` algorithm for list of length `n`.

|   n |   Number of iterations |
|--- |--- |
|   8 |   3 |
|   16 |   4 |
|   32 |   5 |
|   64 |   6 |
| 1,048,576 | 20 |

*Table. Number of iterations for each input size.*

## Big-O Analysis

### Time Complexity

Recall that time complexity is the measurement of how the amount of time an algorithm takes to run as the size of the input changes. Time complexity is usually measured in _number of operations._

The relationship between the number of operations and the input size for `binary_search` described above is a logarithmic relationship. In Big O notation, this is `O(log n)`.

#### Logorithms

**What is a log?**?

A logarithm is a quantity representing the power to which a fixed number (the base) must be raised to produce a given number. 

| Logarithmic Equation | Equivalent Power Equation | How it is Read | 
|--|--|--|
| log <sub>2</sub>8 = 3 | 2<sup>3</sup> = 8 | **log base 2 of 8 equals 3** is equivalent to **2 to the power of 3 equals 8** |
| log <sub>10</sub>10000 = 4 | 10<sup>4</sup> = 10000 | **log base 10 of 10000 equals 4** is equivalent to **10 to the power of 4 equals 10000** |

In a coding problem if we reduce the size of a problem by dividing the remaining input with each iteration we often get a time complexity involving a logarithm.

In general, in a coding problem:

* If the size of the input is *divided* by some value with each iteration, the time complexity involves a logarithm with a base equal to the divisor.
* By far, the most common logarithmic base is 2 because our algorithms often, like binary search, divide the input size by two with each iteration.
  * Often we drop the base of the logarithm since all logarithms can be [converted into base 2 using constants](https://www.khanacademy.org/math/algebra2/x2ec2f6f830c9fb89:logs/x2ec2f6f830c9fb89:change-of-base/a/logarithm-change-of-base-rule-intro).


### Space Complexity

Recall that space complexity is the measurement of how much memory an algorithm uses as the size of the input changes. 

In the iterative `binary_search` algorithm we analyzed above, there are no additional memory allocations. As such, the space complexity is `O(1)`.

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

