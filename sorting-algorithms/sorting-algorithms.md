# Sorting Algorithms

## Goals

The goal for this lesson is to introduce sorting algorithms.

Sorting algorithms:

- improve our algorithmic problem-solving skills
- improve our code reading skills
- practice our ability to think abstractly
- practice our ability to explain algorithms

## Vocabulary and Synonyms

| <div style="min-width:150px;">Vocab</div> | Definition                                                                                                                                                                          | How to Use in a Sentence                                                                                                                                                                                                                 |
| ----------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Sorting                                   | Organizing a collection of elements into order                                                                                                                                      | "By sorting my list, I can present the data in a more understandable fashion."                                                                                                                                                           |
| In-place Sorting                          | Sorting an array using only a small, constant amount—O(1)—of extra storage space. Sorting in place modifies the array to be sorted directly rather than making a new, sorted array. | "Our system is memory-constrained, so we should use an in-place sorting strategy so we don't have to duplicate our data." "Copy the array before using that in-place sort. We don't want to modify our original data in this situation." |
| Stable                                    | A sorting algorithm is _stable_ if it guarantees that the relative ordering of two values having the same sort key is the same after the sort as it was before the sort.            | "Since that sorting algorithm is stable, we can apply it multiple times to the same data to sort records based on multiple attributes!"                                                                                                  |

## Introduction

Imagine a stack of index cards, where each index card has the numbers 1 through 100. Imagine that these cards are shuffled in a random, unknowable order.

If you're given the task to sort these index cards in ascending order, what would you do?

Picture yourself. Do you scan through the pile over and over again, slowly changing the order until it's all sorted? Do you use a table and make two separate piles? Do you fan through the cards comparing each card to its neighbor in the pile?

If you take two people and ask them to sort the same pile of cards, they will likely take different approaches.

Machines need to be told how to think through these questions too, but with fewer index cards and more data. The strategies we tell a computer to use for sorting a list of values are called _sorting algorithms_.

## Sorting Algorithms

Sorting is a common feature of applications, such as:

- Sorting last names alphabetically
- Listing sports game scores in descending order
- Sorting employees by ID in an ascending order

Also, certain algorithms improve significantly when working with a sorted array! Consider these examples:

- Finding an element with a minimum or maximum value
  - Unsorted array: O(n)
  - Sorted array: O(1)
- Searching for an element in an array
  - Unsorted array with linear search: O(n)
  - Sorted array with binary search: O(log n)

For each sorting algorithm, we should:

1. Define and describe the sorting strategy
1. Visualize at least one example of this algorithm
1. Learn and understand the Big O complexity of this algorithm
1. Practice reading the code of an example implementation

## In-Place Sorting and Stable Sorting

Some secondary goals we might keep in mind when studying sorting algorithms are recognizing which can be done _in-place_, and which are _stable_.

### In-Place Sorting

_In-place sorting_ lets us sort a list by using only a small, constant amount of extra memory. It primarily uses the array itself for any workspace needed during the process of sorting.

In-place sorting saves on space, but may take more time, and ends up modifying the initial list.

If we don't want our initial list modified, then we will either need to copy the list first, or use a strategy that makes a sorted copy.

### Stable Sorting

_Stable sorting_ describes sorting that maintains the relative order of items after sorting. It is very useful if we want to sort a collection of records on multiple attributes.

Let's say we want to sort a list of people by their ages, and if two people have the same age, by their name. Consider the following list of names and ages.

```
Jean (25), Vickie (39), Karla (33), Patricia (25), Becky (39)
```

If we first sort this list by name we get the following:

```
Becky (39), Jean (25), Karla (33), Patricia (25), Vickie (39)
```

And then sorting further by age, we get the desired outcome of people sorted by age, where tied ages are sorted by name.

```
Jean (25), Patricia (25), Karla (33), Becky (39), Vickie (39)
```

Notice that the order of the names with identical ages is preserved between the second and third lists. For names that were tied in the second list, the one that was on the left is still on the left in the third list. This property is only true for stable sorts, and allows for sorting by an arbitrary number of attributes.

## O(n<sup>2</sup>) Algorithms

Several commonly introduced sorting algorithms have time complexities of O(n<sup>2</sup>). These include _bubble sort_, _selection sort_, and _insertion sort_, which will be discussed in detail in the following lessons.

These algorithms are fine when the array length _n_ is small, but quickly cease to be useful as the size of the array increases. Bubble sort and insertion sort can perform well in the best case, but they do not scale well.

They **do** have the advantage of being approachable for discussion.

Moving beyond these O(n<sup>2</sup>) algorithms, we will discuss _merge sort_, a O(n log n) algorithm with a beautiful symmetry!

## Summary

There are many sorting algorithms that have been developed. We will discuss four of them in the coming lessons, but we can learn more about other sorting methods at [geeksforgeeks.org/sorting-algorithms/](http://www.geeksforgeeks.org/sorting-algorithms/).

Not all sorting algorithms are created equally, so we will want to keep the performance characteristics of each algorithm in mind when selecting one to use.

Most modern programming languages provide a standard sorting algorithm that will work well for many kinds of data, but we should take time to understand it's properties. In certain situations, it might still be worthwhile to provide our own sort implementations.

And keeping the goals presented at the beginning of this lesson in mind, the study of sorting algorithms has many benefits, even if we never end up needing to write our own sorting algorithm.

## Resources

- [Sorting algorithms comparison demo](https://www.youtube.com/watch?v=ZZuD6iUe3Pc)
- [Sorting algorithms visualization](https://www.cs.usfca.edu/~galles/visualization/ComparisonSort.html)
- [Selection sort on Khan Academy](https://www.khanacademy.org/computing/computer-science/algorithms/sorting-algorithms/a/sorting)
- [Insertion sort on Khan Academy](https://www.khanacademy.org/computing/computer-science/algorithms/insertion-sort/a/insertion-sort)
- [Merge sort on Khan Academy](https://www.khanacademy.org/computing/computer-science/algorithms/merge-sort/a/divide-and-conquer-algorithms)
- [Merge Sort Visual Analysis](https://www.youtube.com/watch?v=w4LRRn7GgqU)
- [Eugene Wang's blog post on "Not all sort algorithms are created equal"](http://eewang.github.io/blog/2013/04/22/sort-algorithms/)
- [MIT Open Courseware on MergeSort](https://www.youtube.com/watch?v=g1AwUYauqgg)
- [Why is Merge Sort O(n log(n)? The **really** long answer)](https://www.youtube.com/watch?v=alJswNJ4P3U)
