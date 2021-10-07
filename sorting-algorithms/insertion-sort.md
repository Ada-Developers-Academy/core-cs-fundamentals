# Insertion Sort

<iframe src="https://adaacademy.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=69c2ff66-1bff-43c1-ac03-ad120019dac4&autoplay=false&offerviewer=true&showtitle=true&showbrand=false&start=0&interactivity=all" height="405" width="720" style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>

## Learning Goals

- Describe insertion sort and its efficiency

## Overview

The insertion sort algorithm works by considering each item in an unsorted list, and inserting them one-by-one into their proper places in a sorted list.

### Detailed Explanation

Conceptually, insertion sort works with two list structures:

1. The unsorted source list
2. A list into which sorted items are inserted

We can iterate over the items in the unsorted list and insert each into the sorted list (which starts empty).

To save memory, most insertion sort implementations use an in-place sort that works by treating a portion of the existing list as sorted (often the beginning) and moving each item in the unsorted portion to its proper location in the sorted portion.

![Insertion Sort Example. The list starts with 9, 4, 8, 6, 3. Treat the left-most value as sorted. 4 belongs before 9, so shift it there. 4, 9, 8, 6, 3. 8 belongs between 4 and 9, so shift it there. 4, 8, 9, 6, 3. 6 belongs between 4 and 8, so shift it there. 4, 6, 8, 9, 3. 3 belongs before 4, so shift it there. 3, 4, 6, 8, 9. The list is sorted.](../assets/sorting-algorithms_insertion-sort_small-example.png)  
*Fig. Steps that insertion sort takes when sorting a list containing 9, 4, 8, 6, 3.*

Consider this more detailed explanation of insertion sort:

- Treat the first item as a list of length one, which is sorted by definition.
- Consider each item in the unsorted portion of the list.
- Step backwards through the sorted list, swapping the new item, until we find a value less than the current item. This item is now in its proper location (for the time being).
- Continue with the next unsorted item, swapping it forward into the sorted portion until we find its proper location.
- Continue with the remainder of the unsorted list, until the entire list has become sorted.

We can also explain insertion sort this way:

- Treat the first item as a list of length one, which is sorted by definition.
- Expand the portion of the sorted list by one, which may mean it is no longer sorted. The final item, and _only_ the final item, might be in the wrong position.
- Perform swaps towards the front of the list to move the final item to its proper location.
- Continue by expanding the items included in the sorted list by one, swapping as necessary to move the final item to its proper location.
- Continue with the remainder of the unsorted list, until the entire list has become sorted.

## Example

Consider the initial unsorted array `[99, 45, 35, 40, 16, 50, 11, 7, 90]`.

The simplified loop table below shows the arrangement of the array after moving each new item to its place in the sorted portion. Again, we shift the new item to its proper place by repeatedly swapping it forward with adjacent items until we encounter a value less than the new value.

The sorted sub-array is **bolded**. The next value to be inserted is always the value adjacent to the end of the sorted sub-array.

| Pass | Array                                   |
| ---- | --------------------------------------- |
| 1    | [**99**, 45, 35, 40, 16, 50, 11, 7, 90] |
| 2    | [**45, 99**, 35, 40, 16, 50, 11, 7, 90] |
| 3    | [**35, 45, 99**, 40, 16, 50, 11, 7, 90] |
| 4    | [**35, 40, 45, 99**, 16, 50, 11, 7, 90] |
| 5    | [**16, 35, 40, 45, 99**, 50, 11, 7, 90] |
| 6    | [**16, 35, 40, 45, 50, 99**, 11, 7, 90] |
| 7    | [**11, 16, 35, 40, 45, 50, 99**, 7, 90] |
| 8    | [**7, 11, 16, 35, 40, 45, 50, 99**, 90] |
| 9    | [**7, 11, 16, 35, 40, 45, 50, 90, 99**] |

## Big O Complexity

As with the other sorting algorithms we have considered, with insertion sort we examine the number of comparisons performed in the inner loop.

The insertion sort algorithm requires (in the worst case):

- 0 comparisons to insert the first element
- 1 comparison to insert the second element
- 2 comparisons to insert the third element
- ... and so on
- _n-1_ comparisons to insert the last element

Overall, this is _1 + 2 + 3 + ... + (n-1)_, the same expression we saw for bubble sort and selection sort.

Therefore insertion sort has a complexity of _O(n<sup>2</sup>)_.

We might also notice that insertion sort, like bubble sort, has a best case time complexity of _O(n)_ if the list is already sorted. As we expand the sorted sub-part of the array, each new item is already in its correct spot, which we can determine with a single check per item. Since there are _n_ items, this gives a best case of _O(n)_.

Insertion sort generally improves in complexity the closer the list is to being sorted, that is, the more items are already relatively in their correct places. In other words, insertion sort runs in _nearly_ linear time on a _nearly_ sorted list of elements.

## Stability

Insertion sort is a stable sorting algorithm. Like bubble sort, we only move items in the list using adjacent swaps, and then only when they are strictly out of order.

## Example Implementation

Consider this example implementation of insertion sort.

```python
def insertion_sort(array):
    i = 1
    while i < len(array):
        to_insert = array[i]
        j = i
        # Search in the sorted portion of the array
        # for the correct position to insert array[i]
        while j > 0 and array[j-1] > to_insert:
            array[j] = array[j-1]
            j -= 1
        array[j] = to_insert
        i += 1
```

Compare this code with this detailed explanation of the algorithm:

- Loop through the entire list with `i` representing the first position of the unsorted sub-array
- Store the first element of the unsorted list in a temporary variable called `to_insert`
- Find the correct index to insert the value `to_insert`
  - Loop through the sorted list from back to front
  - Compare the values between the item at the position we're inspecting, and `to_insert`
  - Swap if needed
- Increase the outer index `i` so that the sorted list grows, and the unsorted list shrinks

This implementation sorts the array in-place. Because the original array is modified, no return statement is needed.

## Check for Understanding

<!-- Question Takeaway -->
<!-- prettier-ignore-start -->
### !challenge
* type: paragraph
* id: TAl2E7
* title: Insertion Sort
##### !question

What was your biggest takeaway from this lesson? Feel free to answer in 1-2 sentences, draw a picture and describe it, or write a poem, an analogy, or a story.

##### !end-question
##### !placeholder

My biggest takeaway from this lesson is...

##### !end-placeholder
### !end-challenge
<!-- prettier-ignore-end -->
