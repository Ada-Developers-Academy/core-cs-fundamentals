# Overview of Hash Tables

<iframe src="https://adaacademy.hosted.panopto.com/Panopto/Pages/Embed.aspx?pid=280bb441-7d57-4ec1-82b9-ad2a018a559c&autoplay=false&offerviewer=true&showtitle=true&showbrand=false&start=0&interactivity=all" height="405" width="720" style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>

## Learning Goals

- Define hash table
- Define hash function
- Describe how hash tables resolve collisions

## Introduction

Python dictionaries are fascinating!

Let's say we had a list of names `["Mickey", "Kermit", "Garfield"]`. If we let a user enter a name as input, and wanted to check whether that name was in this list, we would need to iterate over the array and check whether the user input matched each name. This is a O(n) operation.

Note that using the `in` operator on lists only helps the readability, not the performance. Internally, it still needs to check whether the value we are looking for matches any of the values in the array, one by one!

But what if we used a dictionary? Let's store our list of names as the keys of a dictionary like `{"Mickey": 1, "Kermit": 1, "Garfield": 1}`. The values don't really matter, but are required since dictionaries store key-value pairs. Here, `1` works just as well as any other value we might pick.

By storing our "list" in this way, we can now use the `in` operator on dictionaries to ask whether the user input is a key in our dictionary in a time complexity of O(1), constant time!

How do Python dictionaries achieve this performance? How are keys and values allocated in memory?

Under the hood, Python dictionaries are _hash tables_.

When we consider how hash tables are designed and implemented, we will:

- Practice algorithmic and design thinking around data structures
- Consider how complex data structures are implemented
- Learn powerful problem-solving techniques for problems often encountered in interviews
- Appreciate dictionaries more!

## Vocabulary and Synonyms

| Vocab         | Definition                                                                                          | Synonyms         | How to Use in a Sentence                                                                                                                                                                                      |
| ------------- | --------------------------------------------------------------------------------------------------- | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Hash Table    | A data structure that implements an associative array, which maps unique key identifiers to values. | Hash Map         | "Hash tables have an O(1) lookup time."                                                                                                                                                                       |
| Hash Function | A function used by a hash table to map a key to an index.                                           | Hashing function | "The hash function converts a key into an index in an associative array"                                                                                                                                      |
| Collision     | When multiple keys map to the same element in a hash table's internal array.                        | -                | "The hash function result caused a value to be inserted into an index where a different value already existed, which is a collision. The hash table needs to handle this collision in order to keep both pieces of data." |

# Hash Tables

A _hash table_ is a data structure designed to store key-value pairs. They have a method to look up a value by its key (find), add a key-value pair (insert), and delete a key-value pair (remove).

Hash tables have the ability to look up values by key with a time complexity of O(1). With our current knowledge of programming, how is it possible for a data structure to achieve this, even though searching for an item in an array using linear search has a time complexity of O(n)?

Hash tables achieve their speedy lookup times of O(1) by storing their key-value pairs in an array. They take advantage of how arrays have O(1) lookup operations when given an index.

Each hash table has an _internal array_ that it uses for its storage. When a hash table inserts a key-value pair, it stores the pair in the _internal array_ at a particular position.

To determine the position, hash tables use _hash functions_ to convert a given key into an index in the internal array. Hash tables use this computed index as the location to store the key-value pair.

Hash functions themselves are designed to be fast. And since their result is used to perform constant time array lookups, the overall lookup can also be very quick!


### !callout-info

## Hash Tables Implement Associative Arrays

One reason why hash tables are interesting is because they implement an _abstract data type_ known as an _associative array_. An _abstract data type_ is any theoretical data structure that is described not by its concrete implementation, but by its behavior and how it's used. An _associative array_ is a theoretical data structure that describes collections that store key-value pairs.

### !end-callout

## Time Complexity

For all three operations of inserting, finding, and deleting values, hash tables have a O(1) time complexity, which occurs if each pair in the table is stored at a distinct index.

| Action                        | Average Case | Worst Case |
| ----------------------------- | ------------ | ---------- |
| Finding a value by key        | O(1)         | O(n)       |
| Removing a value by key       | O(1)         | O(n)       |
| Inserting a new key and value | O(1)         | O(n)       |

The worst case occurs if all pairs are stored at the same index. As we will see, this degrades to linear search.

### !callout-info

## We Describe Hash Table Big O by Average Case

Normally, when we estimate the runtime of a data structure's methods with Big O, we assume the worst case. However, a well-designed hash table will attempt to prevent the worst-case scenario from occurring. Therefore when we work with hash tables we **assume the average case**. The likelihood of the worst case occurring depends on how well the **hash function** is implemented.

### !end-callout

## Hash Function

**Hash functions** are functions responsible for mapping a given key into an integer index in the internal array.

### Example Hash Function

Imagine that we have a hash table which holds "name"-"job title" key-value pairs. This hash table needs a hash function to transform the "name" into an index.

![Applying a hashing algorithm to several names. There are 5 steps: Key, Numeric Conversion, Numeric Value, mod by Array Length, and Index. The first key is Debbie Nguyen. An arrow indicates that we perform a numeric conversion on the name, resulting in 13 for the numeric value. Another arrow indicates the mod step (mod 4 since there are 4 indices) resulting in index 1. This will end up being a collision and is shown in fuchsia. The remaining 4 sets of data are Carlton Griffith→16→0 which will be a collision, Eddie Bowers→12→0 which is a collision with Carlton Griffith, Kaye Campbell→13→1 which is a collision with Debbie Nguyen, and Jeanette Barker→15→3 which is not a collision and is shown in yellow.](../assets/hash-tables_hash-tables_hash-function.png)  
_Fig. Mapping names to indices. Here, we used `len()` to convert each name to a number, then performed a mod by 4 to find the index in the internal array, since the internal array currently has 4 slots. Collisions can happen as a result of either the initial numeric conversion, or as a result of the squeezing forced by the modulo operation._

An example hash function could use the following algorithm:

- Convert the key to a string
- Convert the string to a numeric value by grabbing its length
- Calculate the length of the string modulo the length of the internal array
- Use this result as the index

```python
def hash_code(key):
  return len(str(key)) % len(hash_array)
```

### !callout-info

## Why Modulo in This Example?

When arrays get created, they have a fixed size in memory. Trying to read or write beyond the end would result in an `IndexError`. Using `len(str(key)) % len(hash_array)` will always result in an index between `0` and the length of the array, meaning it will always be a valid index!

<br />

In practice, the class representing the key type will be responsible for converting the key to some initial numeric value (Python classes can implement the `__hash__` method for this purpose), and the hash table performs the additional steps to make sure the numeric value refers to a valid index in its internal storage.

### !end-callout

### !callout-danger

## Production Hash Functions Are More Complicated

The hypothetical hash function presented in this example is _not_ a good hash function. Words in languages tend to cluster around certain lengths, so there will tend to be many keys with the same length, and hence the same index in the internal array after squeezing to the array length. Production hash functions tend to perform a variety of manipulations to "stir" the bits representing our data into more varied ranges.

### !end-callout

## Collisions

There is practically no limit to the number of possible keys would could use in our hash table. By contrast, it stores our pair data in a limited-size array. At some point, any hash function will result in some keys being mapped to the same index. When this occurs, it is called a _collision_.

### !callout-info

## Collisions Are Predicted by the Pigeon Hole Principle

Any time we try to put `n + 1` items into `n` positions, we will be unable to put each item into a unique position. If we had only `n` items, each item could go into each of the `n` positions perfectly. But as soon as we add one more item, it must now go into the same position as a previous item! This observation is referred to as the _pigeon hole principle_ and can be useful for thinking about the performance of certain algorithms.

### !end-callout

### Example Collision

Let's use the same hash function from before:

```python
def hash_code(key):
  return len(str(key)) % len(hash_array)
```

Imagine a hash table that stores "name"-"job title" key-value pairs. The hash table's internal `hash_array` has a length of `15`. Imagine inserting the following pairs, which have the following indices after applying the above hash function:

| Key (Name) | Value (Job Title)     | Index (`hash_code(key)`) |
| ---------- | --------------------- | ------------------------ |
| `"Nora"`   | `"Devops Engineer"`   | `4`                      |
| `"Aubrey"` | `"Web Developer"`     | `6`                      |
| `"Kirk"`   | `"Systems Analyst"`   | `4`                      |

If we insert Nora first, and then eventually Kirk, our hash function will attempt to add Kirk at the index `4`, even though Nora already exists there.

### Resolving Collisions

There are many ways to resolve a collision! One way is to make each element of the hash array a collection itself, and then store new elements in the collection rather than directly in the hash array.

### Example Resolution

If our elements are stored in these supplemental collections, we could end up with a hash which looks like this:

![The internal array in a hash table. Indices 0 through 7 are shown, all of which contain None, other than indices 4 and 6. Index 4 refers to a list with two key-value pairs: Nora - a Devops Engineer, and Kirk - a Systems Analyst. Index 6 refers to a list with one key-value pair: Aubrey - a Web Developer. Indices 8 through 14 are not shown, but can be presumed to all contain None.](../assets/hash-tables_hash-tables_collision.png)  
_Fig. The internal array of the hash table for the data given above, with collisions resolved by adding all pairs with the same hash value to a collection stored at the index matching the hash value._

In this example, we resolve collisions by creating an array at each index of the main array, then adding the key-value pair to the end of the list.

### !callout-info

## Effective Hash Functions

What would happen if we inserted 600 items, and our hash function happened to calculate the same hash value for all 600 of them? If the hash function does not adequately spread values out over the length of the array, we'll have long chains of key-value pairs and a O(n) worst case runtime to find items.

<br />

Effective hash functions attempt to spread all possible values over the entire data structure to avoid assigning multiple keys to the same index. Most libraries use well-proven hashing functions which normally avoid high numbers of collisions.

### !end-callout

## Summary

Hash tables are a data structure which allow quick lookup of a value by using a key. Each key is mapped to an index of an internal array with a specialized method called a _hash function_. The average-case lookup is O(1) and the worst-case is O(n). However, most good implementations use a _hash function_ which attempts to uniformly distribute elements and prevent collisions.

This means that for _practical purposes_ we can treat the time complexity of lookup, deletion and insertion as O(1), despite the worst-case O(n) time complexity.  This is because, the implementations we use in languages like Python, so rarely encounter worst-case scenarios.
