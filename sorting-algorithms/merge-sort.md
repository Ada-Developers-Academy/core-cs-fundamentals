# Merge Sort

<iframe src="https://adaacademy.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=c5c75fd3-abfe-4086-85c3-ad1200243bea&autoplay=false&offerviewer=true&showtitle=true&showbrand=false&start=0&interactivity=all" height="405" width="720" style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>

## Learning Goals

- Describe merge sort and its efficiency

## Vocabulary and Synonyms

| <div style="min-width:200px;">Vocab</div> | Definition                                                                                                                                                         |
| ----------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Recursive Algorithm                       | A method of solving a problem where the solution depends on solving smaller instances of the same problem. This approach can be applied to many types of problems. |
| Divide-And-Conquer Algorithm              | A strategy of solving a big problem by breaking it into smaller, more manageable subproblems. It can also lead to recursive solutions.                             |

## Overview

Merge sort is a _divide-and-conquer_ algorithm. It involves the following three stages:

1. **Divide** the array into two sub-arrays repeatedly until each sub-array is of size one.
1. **Sort** each sub-array. (An array of size one is sorted by default.)
1. **Merge** the sub-arrays into one array by combining two sub-arrays into one at each step.

## Divide

![Merge sort divide example. The list starts with the values (7, 2, 8, 1, 6, 5, 3, 9). This is split into to lists with one having (7, 2, 8, 1), and the other having (6, 5, 3, 9). Each list of four values is split into two lists of 2 value, resulting in 4 total lists. (7, 2), (8, 1), (6, 5), and (3, 9). Finally, each list of two is split into two single item lists for a total of 8 single item lists. (7), (2), (8), (1), (6), (5), (3), (9).](../assets/sorting-algorithms_merge-sort_divide.png)  
_Fig. Steps that merge sort takes when dividing a list containing 7, 2, 8, 1, 6, 5, 3, 9._

Let's reference this image to illustrate the divide step, starting at the top, original array.

In the first _divide_ step, the original array of size eight gets divided into two sub-arrays of size four each. The arrays are divided at a calculated halfway point.

In the next _divide_ step, we have two sub-arrays. Both of these arrays have four elements. They aren't of size one yet! So, the same action gets repeated. We calculate the halfway point, and divide the sub-arrays in half.

This _divide_ stage continues until the original array of size _n_ is reduced to sub-arrays of size _1_ each.

An array of size one is trivially sorted. With only a single item in the list, there is no other item to be out of place!

## Sort and Merge

The _merge_ stage starts by combining two sub-arrays at a time.

While combining the sub-arrays containing `7` and `2` respectively, the values in each are compared and sorted. The merging process continues in this manner.

### Sorting in Detail

![Merge sort merge example. We start with 8 individual lists. (7), (2), (8), (1), (6), (5), (3), (9). Each pair of single value lists is merged into a single list of two values, resulting in four lists of two values. (2, 7), (1, 8), (5, 6), (3, 9). Each pair of two value lists is merged into a single list of four values, resulting in two lists of four values. (1, 2, 7, 8), (3, 5, 6, 9). Finally the two lists of four items are merged into a single list of eight items. (1, 2, 3, 5, 6, 7, 8, 9).](../assets/sorting-algorithms_merge-sort_merge.png)  
_Fig. Steps that merge sort takes when merging the lists it previously divided._

How does the merge sort algorithm merge and sort two sub-arrays into one? The algorithm compares an item from each sub-array, and uses a third, temporary, auxiliary array.

Consider the two sub-arrays `[1, 2, 7, 8]` and `[3, 5, 6, 9]` in the final merge step in our example image above.

| <div style="min-width:100px">Comparing which values (in bold)?</div> | Which is smaller and gets written to the auxiliary array? | <div style="min-width:200px">Auxiliary array</div> |
| -------------------------------------------------------------------- | --------------------------------------------------------- | -------------------------------------------------- |
| [**1**, 2, 7, 8] <br /> [**3**, 5, 6, 9]                             | 1                                                         | [1]                                                |
| [1, **2**, 7, 8] <br /> [**3**, 5, 6, 9]                             | 2                                                         | [1, 2]                                             |
| [1, 2, **7**, 8] <br /> [**3**, 5, 6, 9]                             | 3                                                         | [1, 2, 3]                                          |
| [1, 2, **7**, 8] <br /> [3, **5**, 6, 9]                             | 5                                                         | [1, 2, 3, 5]                                       |
| [1, 2, **7**, 8] <br /> [3, 5, **6**, 9]                             | 6                                                         | [1, 2, 3, 5, 6]                                    |
| [1, 2, **7**, 8] <br /> [3, 5, 6, **9**]                             | 7                                                         | [1, 2, 3, 5, 6, 7]                                 |
| [1, 2, 7, **8**] <br /> [3, 5, 6, **9**]                             | 8                                                         | [1, 2, 3, 5, 6, 7, 8]                              |

At this final point, all elements of the first sub-array have been merged. All remaining elements of the second sub-array get copied over linearly to the auxiliary array.

In this case, only one element is left in the second sub-array. So, _9_ gets copied over to the auxiliary array, for a final `[1, 2, 3, 5, 6, 7, 8, 9]`.

This is the process of sorting and merging at the same time, which repeats until there are no more-sub arrays and the original array is completely sorted.

Finally, the auxiliary array gets linearly copied back to the original array.

## Stability

Let's look at the stability of merge sort before tackling big O, since our complexity discussion will be a bit more involved.

Merge sort is a stable sorting algorithm, though we have to be a little careful to ensure this.

Recall that for a sorting algorithm to be stable, the sorted array must preserve the relative ordering between equivalent values that existed in the unsorted array. To ensure this, we need to guarantee that if there are two items with the same value, that the instance that started on the left, stays on the left.

For the stable _O(n<sup>2</sup>)_ algorithms, we did this bys ensuring that we never swapped "through" an equivalent value. But with all our dividing and merging, how can we ensure this remains true in merge sort?

Notice that when we divide a sub-array, there is always a left side and a right side. Anything that goes into the left array will originally have preceded anything in the right array. This is true all the way down during the divide phase. So if we encounter two equivalent values during the merge phase, one from the left and one from the right, we need only prefer the value from the left. As long as we do this all the way up through the merging, we will preserve the relative ordering required for a stable sort.

## Big O Complexity

The time complexity of merge sort is _O(n log n)_. Let's look closer to understand how we achieved this conclusion.

### Divide Step

Each divide step can be implemented as a straightforward computation to find the array midpoint from a start and end index. This step takes constant time regardless of the size of the sub-array, and there will be _n-1_ total divides. So the divide step would contribute _n-1_, a linear term, to the total complexity. We will be able to ignore this term since it will not dominate the complexity growth.

### Merge Step

Merging a total of _n_ elements takes _O(n)_ time. If there are two sub-arrays of size _n/2_ each, then we will compare one element from one sub-array with another element from the second sub-array and one of the two will get copied. This step will continue until all are copied, taking a total of _O(n)_ time.

As the sub-problems get smaller, the number of sub-problems doubles at each level, but the merging time halves. The doubling and halving cancel each other out and so the merging takes _O(n)_ time at each level of the merge steps. Notice that each row in the merge diagram has _n_ (in this case 8) elements in total.

### Base Case

In the base case, we have sub-arrays of size _1_ and a total of _n_ sub-arrays. It takes _O(1)_ time to sort an array of size one. Overall, merging the base level is _O(n)_ time, just like any other level.

### Count of levels

Starting with _n_ elements, and reducing by half at each level until we reach arrays with a single element each, takes _log n_ steps. Similarly, starting with sub-arrays of one element each and combining two sub-arrays at a time until we reach an array of _n_ elements also takes _log n_ steps.

### Conclusion

Overall, each level takes _O(n)_ time. There are _O(log n)_ such levels.

Therefore, _O(n)_ merges times _O(log n)_ levels results in an overall time complexity of _O(n log n)_.

Notice that were able to arrive at this conclusion purely from a description of the operations that must be performed, and not from a direct inspection of any implementation.

In fact, when we encounter the implementation of merge sort later when discussing recursion, it might not be clear how to derive a big O analysis from it in the same way that we were able to for the _O(n<sup>2</sup>)_ sorting algorithms that used nested loops. In such cases, drawing a diagram of the operations can provide us with a geometric argument for thinking about the algorithm's complexity.

### !callout-info

## Merge Sort Implementation Uses Recursion

Understanding how to implement merge sort is best paired with the topic of recursion. We will revisit merge sort at that time, but if this sounds interesting, follow your curiosity!

### !end-callout

### Performance Considerations

It may seem like we have to do a lot of extra work for merge sort that we don't need to do for something like insertion sort. So how can merge sort have a time complexity of _O(n log n)_ while the simpler insertion sort has a time complexity of _O(n<sup>2</sup>)_?

It is absolutely accurate to say that insertion sort is a simpler algorithm with less bookkeeping overhead. But we should remember that big O is not a measure of absolute performance. It tells us how the performance grows with the size of the input.

This means that for small arrays, insertion sort may absolutely perform better than merge sort. However, as the size of the input grows, merge sort will tend to outperform insertion sort.

### !callout-info

## There Are Other _O(n log n)_ Sorting Algorithms

Other than merge sort, the most well known _O(n log n)_ sorting algorithms include [quick sort](https://www.geeksforgeeks.org/quick-sort/), and [heap sort](https://www.geeksforgeeks.org/heap-sort/). If this introduction to merge sort has been interesting, then diving into these other algorithms may also be rewarding. Follow your curiosity!

### !end-callout

## Check for Understanding

<!-- Question Takeaway -->
<!-- prettier-ignore-start -->
### !challenge
* type: paragraph
* id: d4d6b4de
* title: Merge Sort
##### !question

What was your biggest takeaway from this lesson? Feel free to answer in 1-2 sentences, draw a picture and describe it, or write a poem, an analogy, or a story.

##### !end-question
##### !placeholder

My biggest takeaway from this lesson is...

##### !end-placeholder
### !end-challenge
<!-- prettier-ignore-end -->
