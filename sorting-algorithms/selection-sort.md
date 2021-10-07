# Selection Sort

<iframe src="https://adaacademy.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=facbdf57-b727-40c6-9b40-ad120019daed&autoplay=false&offerviewer=true&showtitle=true&showbrand=false&start=0&interactivity=all" height="405" width="720" style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>

## Learning Goals

- Describe selection sort and its efficiency

## Overview

The selection sort algorithm works by selecting the smallest unsorted item in the list, and swapping it with index 0, then finding the next smallest and swapping it into index 1, and so on.

### Detailed Explanation

![Selection sort example. The list starts with 9, 4, 8, 6, 3. 3 is the smallest, so 3 and 9 swap. 3, 4, 8, 6, 9. 4 is the smallest, so it remains where it is. 3, 4, 8, 6, 9. 6 is the smallest, so 6 and 8 swap. 3, 4, 6, 8, 9. 8 is the smallest, so it remains where it is. 3, 4, 6, 8, 9. Only one unsorted item remains, so the list is sorted.](../assets/sorting-algorithms_selection-sort_small-example.png)  
_Fig. Steps that selection sort takes when sorting a list containing 9, 4, 8, 6, 3._

Here is a more detailed explanation of the selection sort algorithm:

- We look through the entire array for the smallest element.
- Once we find it, we swap this smallest element found with the first element of the array.
- Then we look for the smallest element in the remaining array (the sub-array without the first element) and swap this element found with the second element.
- Then we look for the smallest element in the remaining array (the sub-array without the first and second elements) and swap that element with the third element, and so on.

## Example

Consider the initial unsorted array `[99, 45, 35, 40, 16, 50, 11, 7, 90]`.

The simplified loop table below shows some of the key values during each pass of the outer loop through the array.

- `i` is the index that starts at 0, and increments until the length of the array.
- `min_index` is a variable that holds the index of the smallest element remaining in the unsorted portion of the list. To locate this item, we use an inner loop through the remaining unsorted values for each pass of the outer loop.

The array in each row is shown _before_ the swap for that pass is performed, so that the index under consideration `i` and the index of the minimum found value `min_index` line up with the displayed array values. The array shown on each following line has the previously identified swap applied.

| Pass | <div style="min-width: 300px;">Array</div>  | `i` | `min_index` |
| ---- | ------------------------------------------- | --- | ----------- |
| 1    | [**99**, 45, 35, 40, 16, 50, 11, **7**, 90] | 0   | 7           |
| 2    | [7, **45**, 35, 40, 16, 50, **11**, 99, 90] | 1   | 6           |
| 3    | [7, 11, **35**, 40, **16**, 50, 45, 99, 90] | 2   | 4           |
| 4    | [7, 11, 16, **40**, **35**, 50, 45, 99, 90] | 3   | 4           |
| 5    | [7, 11, 16, 35, **40**, 50, 45, 99, 90]     | 4   | 4           |
| 6    | [7, 11, 16, 35, 40, **50**, **45**, 99, 90] | 5   | 6           |
| 7    | [7, 11, 16, 35, 40, 45, **50**, 99, 90]     | 6   | 6           |
| 8    | [7, 11, 16, 35, 40, 45, 50, **99**, **90**] | 7   | 8           |
| 9    | [7, 11, 16, 35, 40, 45, 50, 90, 99]         | -   | -           |

Note that we do not actually run the 9th pass for this 9 value array. Since there is only one item left in the unsorted portion of the array and no available swap locations, we can end one pass "early."

## Big O Complexity

The time complexity of selection sort is _O(n<sup>2</sup>)_.

The way by which we reach this conclusion is very similar to our discussion of bubble sort.

Our outer loop runs about _n_ times. The first pass through, we must perform _n-1_ comparisons to find the minimum value, and then perform a single swap for that value.

Note this minor improvement over bubble sort, as bubble sort would perform both _n-1_ comparisons, as well as _n-1_ swaps. This does not affect our overall complexity analysis since the inner loop does still run _n-1_ times. But again, in some languages this could be important.

Each successive pass requires one fewer comparison, so we end up with the same decreasing summation as we did in bubble sort, which gives us a complexity of _O(n<sup>2</sup>)_.

For a more intuitive argument. Consider that both the outer loop (tracking the position to place the minimum) and the inner loop (looking for the current minimum) are related to the size of the array _n_, and since they are nested, we multiply their bounds together for _n*n_ or _O(n<sup>2</sup>)_.

## Stability

Selection sort is _not_ a stable sorting algorithm. The swaps that we perform can result in equivalent values jumping over one another, losing the information about their relative initial orderings.

If we need a stable sorting algorithm, we should select a different algorithm, or think about how we could modify the base selection sort algorithm to enforce stability.

## Example Implementation

Consider this example implementation of selection sort.

```python
def selection_sort(array):
    i = 0
    while i < len(array) - 1:
        min_index = i
        j = i + 1
        while j < len(array):
            if array[j] < array[min_index]:
                min_index = j
            j += 1
        if min_index != i:
            temp = array[min_index]
            array[min_index] = array[i]
            array[i] = temp
        i += 1
```

Compare this code with this detailed explanation of the algorithm:

- Start a variable `i` at `0`
- Create an outer loop that loops while `i` is smaller than the length of the `array - 1` since we don't need to swap the final value
  - Start with the assumption that the minimum value is already in the right place by setting `min_index` to `i` 
  - Start a variable `j` at the position one past `i` to look for the smallest element in the rest of the array
  - Create an inner loop that loops `j` over the remainder of the array
    - If the current inspected value is smaller than the current smallest value, update `min_index` with the current index `j`
    - Increase `j`
  - Repeat until `j` reaches the end of the list
  - If `i` and `min_index` are not the same, then
    - Swap the elements at index `i` and index `min_index` using a temporary variable `temp`
  - Increase `i`
- Repeat until `i` reaches the end of the list

This implementation sorts the array in-place. Because the original array is modified, no return statement is needed.

## Check for Understanding

<!-- Question Takeaway -->
<!-- prettier-ignore-start -->
### !challenge
* type: paragraph
* id: WcmHej
* title: Selection Sort
##### !question

What was your biggest takeaway from this lesson? Feel free to answer in 1-2 sentences, draw a picture and describe it, or write a poem, an analogy, or a story.

##### !end-question
##### !placeholder

My biggest takeaway from this lesson is...

##### !end-placeholder
### !end-challenge
<!-- prettier-ignore-end -->
