# Bubble Sort

<iframe src="https://adaacademy.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=45dab937-de88-4987-8539-ad11018a382c&autoplay=false&offerviewer=true&showtitle=true&showbrand=false&start=0&interactivity=all" height="405" width="720" style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>

## Learning Goals

- Describe bubble sort and its efficiency

## Overview

The bubble sort algorithm works by repeatedly looping through a list of data. With each pass through the list, the "next" sorted value will "bubble up" to its proper place in the list.

### Detailed Explanation

Bubble sort works by repeatedly

- Stepping through the list to be sorted
- Comparing each pair of adjacent items, and
- Swapping the adjacent items if they are in the wrong order

As the algorithm proceeds, the largest element gets _bubbled_ to the top of the array after each iteration through the outer loop.

The algorithm repeats this process until it makes a pass all the way through the list.

![Bubble sort example. The list starts with 9, 6, 4, 8, 3. 9 bubbles all the way to the end. 6, 4, 8, 3, 9. 6 starts to bubble, but hits 8 which bubbles to its spot. 4, 6, 3, 8, 9. 4 starts to bubble, but immediately hits 6, which bubbles to its spot. 4, 3, 6, 8, 9. 4 bubbles to its spot. 3, 4, 6, 8, 9. Only one unsorted item remains, so the list is sorted.](../assets/sorting-algorithms_bubble-sort_small-example.png)  
_Fig. Steps that bubble sort takes when sorting a list containing 9, 6, 4, 8, 3._

Here is a more detailed explanation of the bubble sort algorithm:

- For each pass, start from one end of the list.
- Compare each pair of adjacent items.
- Swap the adjacent items if they are out of order.
- Continue to the end of the list, checking each pair and swapping as needed.
- Repeat from the beginning until we make an entire pass through the list without swapping any items. This means all the items are in the right order, and the list is sorted.

We can make a few small optimizations to this process. Both are applied in the diagram above.

- We can consider the length of the unsorted list to shorten by one with each pass. After each pass, one more item is guaranteed to be in the proper order at the end of the list.
- If we track the unsorted list length, we never have to perform the final bubble pass (when the unsorted list has one item). There is nothing else left unsorted with which to swap that item!

## Example

Consider the initial unsorted array `[99, 45, 35, 40, 16, 50, 11, 7, 90]`.

This table shows the first pass through the array, demonstrating how the bubble sort algorithm performs the comparison and swapping of adjacent values from one end to the other.

| <div style="min-width:300px;">Array</div> | What is happening?                                                                                                         |
| ----------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| [**99, 45**, 35, 40, 16, 50, 11, 7, 90]   | The pair of adjacent items is **99** and **45**. The algorithm compares them. 99 is larger, and should be placed after 45. |
| [45, **99, 35**, 40, 16, 50, 11, 7, 90]   | The adjacent items are **99** and **35**. The algorithm compares them. 99 is larger, and should be placed after 35.        |
| [45, 35, **99, 40**, 16, 50, 11, 7, 90]   | The algorithm compares **99** and **40**, and swaps their positions.                                                       |
| [45, 35, 40, **99, 16**, 50, 11, 7, 90]   | The algorithm compares **99** and **16**, and swaps their positions.                                                       |
| [45, 35, 40, 16, **99, 50**, 11, 7, 90]   | The algorithm compares **99** and **50**, and swaps their positions.                                                       |
| [45, 35, 40, 16, 50, **99, 11**, 7, 90]   | The algorithm compares and swaps **99** and **11**.                                                                        |
| [45, 35, 40, 16, 50, 11, **99, 7**, 90]   | The algorithm compares and swaps **99** and **7**.                                                                         |
| [45, 35, 40, 16, 50, 11, 7, **99, 90**]   | The algorithm compares and swaps **99** and **90**.                                                                        |

Because the list is still relatively short, we (as humans) can easily pick out 99 as being the largest item. We should expect 99 to be moved to the last position in the list after the first pass. We see that by carefully performing the side-by-side checks and swaps that this is indeed the outcome we observe.

The bubble sort algorithm continues with pass two:

| <div style="min-width:300px;">Array</div>   | What is happening?                                                                                                                                                                                                                                           |
| ------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [**45**, **35**, 40, 16, 50, 11, 7, 90, 99] | 45 and 35 are compared, and must swap.                                                                                                                                                                                                                       |
| [35, **45**, **40**, 16, 50, 11, 7, 90, 99] | 45 continues to win a number of comparisons, so continues to bubble up.                                                                                                                                                                                      |
| [35, 40, **45**, **16**, 50, 11, 7, 90, 99] |
| [35, 40, 16, **45**, **50**, 11, 7, 90, 99] | 45 and 50 are compared, but since 45 is less than 50, they are not swapped.                                                                                                                                                                                  |
| [35, 40, 16, 45, **50**, **11**, 7, 90, 99] | The next pair check resumes with 50 being compared to 11. 50 is larger, so they are swapped.                                                                                                                                                                 |
| [35, 40, 16, 45, 11, **50**, **7**, 90, 99] | 50 continues to be compared, swapping as it wins.                                                                                                                                                                                                            |
| [35, 40, 16, 45, 11, 7, **50**, **90**, 99] | 50 and 90 are compared, and don't swap, since they are already in the proper order.                                                                                                                                                                          |
| -                                           | We do not compare 90 and 99. As pointed out, we can consider 99 as being in an already sorted part of the list. We can think of the unsorted portion as shortening by one with each additional pass, which reduces the total number of comparisons required. |

Let's step through one more pass—the third pass—in detail. We will see that this will _not_ be the final pass, as bubble sort will continue until no swaps are made.

| <div style="min-width:300px;">Array</div>   | What is happening?                                                                                                                                                  |
| ------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [**35**, **40**, 16, 45, 11, 7, 50, 90, 99] | We perform pairwise comparisons as before. Swapping as needed. 40 is the initial winner.                                                                            |
| [35, **40**, **16**, 45, 11, 7, 50, 90, 99] |
| [35, 16, **40**, **45**, 11, 7, 50, 90, 99] | 45 starts winning.                                                                                                                                                  |
| [35, 16, 40, **45**, **11**, 7, 50, 90, 99] |
| [35, 16, 40, 11, **45**, **7**, 50, 90, 99] |
| [35, 16, 40, 11, 7, **45**, **50**, 90, 99] | 50 wins.                                                                                                                                                            |
| -                                           | We do not compare 50 and 90. We think of the unsorted list as having shortened again. We do not need to compare 50 to the values in the sorted region of the array. |

Since swaps were still made during this pass, bubble sort will continue to run.

<br />

<details style="max-width: 700px; margin: auto;">
  <summary>
      Click to view a summary of the remaining passes.
  </summary>

| Pass 4                                      |
| ------------------------------------------- |
| [**35**, **16**, 40, 11, 7, 45, 50, 90, 99] |
| [16, **35**, **40**, 11, 7, 45, 50, 90, 99] |
| [16, 35, **40**, **11**, 7, 45, 50, 90, 99] |
| [16, 35, 11, **40**, **7**, 45, 50, 90, 99] |
| [16, 35, 11, 7, **40**, **45**, 50, 90, 99] |

| Pass 5                                      |
| ------------------------------------------- |
| [**16**, **35**, 11, 7, 40, 45, 50, 90, 99] |
| [16, **35**, **11**, 7, 40, 45, 50, 90, 99] |
| [16, 11, **35**, **7**, 40, 45, 50, 90, 99] |
| [16, 11, 7, **35**, **40**, 45, 50, 90, 99] |

| Pass 6                                      |
| ------------------------------------------- |
| [**16**, **11**, 7, 35, 40, 45, 50, 90, 99] |
| [11, **16**, **7**, 35, 40, 45, 50, 90, 99] |
| [11, 7, **16**, **35**, 40, 45, 50, 90, 99] |

| Pass 7                                      |
| ------------------------------------------- |
| [**11**, **7**, 16, 35, 40, 45, 50, 90, 99] |
| [7, **11**, **16**, 35, 40, 45, 50, 90, 99] |

| Pass 8                                      |
| ------------------------------------------- |
| [**7**, **11**, 16, 35, 40, 45, 50, 90, 99] |

Notice that for our nine value list, eight passes through the data were required, and that each pass checked one fewer set of pairs than the previous pass.

</details>

## Big O Complexity

There are two basic operations in which we are interested when analyzing sorting algorithms:

1. the number of comparisons
1. the number of swaps

In our big O analysis of sorting algorithms, we will typically focus on the number of comparisons. In some languages, the number of swaps will also be important and could provided a reason to favor an algorithm with fewer swaps over an algorithm with many swaps.

Also, recall that big O analysis considers the worst case for an algorithm! Although it's possible for bubble sort to finish after a single pass (_O(n)_) if the array happened to be sorted already, we are less interested in that situation.

Noticing best case performance can be useful if we are choosing between multiple algorithms that otherwise have the same complexity, or if we have forehand knowledge about the data with which we will be working.

In the worst case, we would need to perform the check and swap with each pair, and everything would be out of order so that we don't finish early. This would require about as many passes through the array as there are values.

This gives us a time complexity for bubble sort of _O(n<sup>2</sup>)_, where _n_ is the array length.

We conclude this by considering:

- The outer loop (overall number of passes) must run _n_ times
- The inner loop (performing comparisons and swapping) must also run _n_ times

We can even be a little more precise with our counting.

The inner loop runs _n-1_ times during the first iteration of the outer loop, _n-2_ times during the second iteration through the outer loop, and so on. i.e. _n-1 + n-2 + n-3 + ... + 3 + 2 + 1_.

There is a mathematical identity which states this summation is the same as _n(n-1)/2_. When multiplied out this results in _1⁄2n<sup>2</sup>-1⁄2n_, for _O(n<sup>2</sup>)_.

Notice that _n(n-1)/2_ does _not_ equal _n<sup>2</sup>_. Recall that when performing big O analysis, we are interested in the rate of growth in the algorithm rather than the exact number of operations. The growth rate will be dominated by the largest term in the equation.

After multiplying out the expression, the largest term is _1⁄2n<sup>2</sup>_. After dropping the constant, this allows us to say that bubble sort is _O(n<sup>2</sup>)_.

### !callout-info

## Mathematical Proofs Out of Scope

In general, full mathematical proofs for the algorithms we discuss are out of scope for the curriculum. We will often apply analyses that are more intuitive than rigorous. However, there are great resources online that explain the math in-depth! Follow your curiosity!

### !end-callout

## Stability

Bubble sort is a stable sorting algorithm. Since we only shift values by one position, and even then only if they are strictly out of order, equivalent values will never "jump" over one another.

That is, if the value 10 appeared in the list twice, the leftmost instance would always remain to the left, while the rightmost would remain to the right.

As discussed in the Sorting Algorithms lesson, stability can be a useful property for a sorting algorithm to have. If our values were more complex records that we would like to sort based on multiple attributes, then we can simply apply a stable sort multiple times. Or if the initial ordering of a list isn't entirely random, a stable sort will preserve the ordering between records that are otherwise equivalent.

## Example Implementation

Consider this example implementation of bubble sort.

```python
def bubble_sort(array):
    i = 0
    # Begin the outer loop
    while i < len(array) - 1:
        j = 0
        # Begin the inner loop
        while j < (len(array) - i - 1):
            # Compare two adjacent items
            if array[j] > array[j+1]:
                # Swap
                temp = array[j]
                array[j] = array[j+1]
                array[j+1] = temp
            j += 1
        i += 1
```

Compare this code with this detailed explanation of the algorithm:

- Start a variable `i` at `0`
- Create an outer loop that loops while `i` is smaller than the length of the `array - 1` since we don't need to bubble the final value
  - Start a variable `j` at `0`
  - Create an inner loop that loops while `j` is smaller than `len(array) - i - 1` since we want to avoid the `i` sorted elements at the end, and we need to leave one extra value for the pairwise comparisons
    - Compare the items at index `j` and `j+1`. If they're out of order:
      - Swap the items at `array[j]` and `array[j+1]` using a temporary variable, `temp`
    - Increment `j`
  - Repeat until `j` reaches its limit
  - Increment `i`
- Repeat until `i` reaches its limit

This implementation does _not_ explicitly track whether a swap has been made (which could allow early termination). But when we get down to a single item in the unsorted portion, this is implicitly true, as there is nothing left with which we can compare.

This implementation sorts the array in-place. That is, it uses only a small amount of constant extra memory (just a few local variables), and the original array itself is updated. Because the original array is modified, no return statement is needed.

Note that the presented implementation used a temporary variable to perform the swap. This is a common pattern in languages that don't support multiple values in a single assignment. This implementation has been written in a general manner to emphasize that the algorithm—the steps for performing bubble sort—are not specific to any one language.

We will follow this same style when discussing other sorting algorithms. But we should feel free to modify the presented implementation to make better use of language-specific features!

## Check for Understanding

<!-- Question Takeaway -->
<!-- prettier-ignore-start -->
### !challenge
* type: paragraph
* id: Ym2Y2e
* title: Bubble Sort
##### !question

What was your biggest takeaway from this lesson? Feel free to answer in 1-2 sentences, draw a picture and describe it, or write a poem, an analogy, or a story.

##### !end-question
##### !placeholder

My biggest takeaway from this lesson is...

##### !end-placeholder
### !end-challenge
<!-- prettier-ignore-end -->
