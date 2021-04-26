# Overview of Hash Tables

## Learning Goals

- Define Hash Table
- Define Hash Function
- Describe how hash tables
- Compare

## Introduction

In our programs we often need to store data with a quick way to look up specific items. We could store elements in an array, but finding specific entries in an array requires looping through potentially the entire list an O(n) operation, or maintaining the list in order.

## Vocabulary and Synonyms

| Vocab         | Definition                                                                                          | Synonyms | How to Use in a Sentence                |
| ------------- | --------------------------------------------------------------------------------------------------- | -------- | --------------------------------------- |
| Hash Table    | A data structure that implements an associative array, which maps unique key identifiers to values. | Hash Map | "Hash tables have an O(1) lookup time." |
| Hash Function | A function used by a hash table to map a key to an index.                                           |
| Collision     | When multiple keys map to the same element in a hash table's internal array.                        |

## Old Content

# Hash Tables

## Hash Tables Overview

A _hash table_, is an implementation of an _abstract data type_ known as an _associative array_ a data structure designed to store key-value pairs and provide a method to look up a value from its key.

A hash table applies keys to a special method known as a _hash function_ which converts the key into an index of an internal array used for storage. The hash table then stores the key-value pair into that internal array. Because the hash function can quickly convert a key to an array index this operation can result in very quick lookup times.

<!-- Lucidchart link  https://www.lucidchart.com/invitations/accept/5fdcf503-7d8b-4139-94d4-795bfed27883 -->

![Hash Function Example](images/hash-function.png)

<!-- Hash function image source: https://en.wikipedia.org/wiki/Hash_function -->

## Time Complexity

One of the most appealing traits of the hash table is its efficiency.

| Action                        | Average Case | Worst Case |
| ----------------------------- | ------------ | ---------- |
| Finding a value by key        | O(1)         | O(n)       |
| Removing a value by key       | O(1)         | O(n)       |
| Inserting a new key and value | O(1)         | O(n)       |

For all three operations of finding, removing, and inserting values, hash tables have an O(1) time complexity.

### !callout-info

## We Describe Hash Table Big O by Average Case

Normally, when we estimate the runtime of a data structure's methods with Big O, we assume the worst case. However, a well-designed hash table will attempt to prevent the worst-case scenario from occurring. Therefore when we work with hash tables we **assume the average-case**. The likelihood of the worst case from occurring depends on how well the **hash function** is implemented.

### !end-callout

## Hash Function

All **hash functions** are used to map keys to indices in the storage array. Good hash functions attempt to spread all possible values over the entire data structure and avoid assigning multiple keys to the same index.

Designing a good hash function is something of a black art as there is no mathematical formula that will work perfectly in all cases. Instead we use practical general-purpose functions which work well in most cases. This type of algorithm is often called a _heuristic_. A heuristic in Computer Science is a practical solution which works in most cases, but is not mathematically proven to work well in all cases.

### Example Hash Function

For example if I calculated a hash function by converting any key to a string and calculated the length, I could use that number to find an index in my array. However since the length can be of arbitrary size I can divide the length by the size of my array and take the remainder. Then the number would be between 0 and the length of the array.

```python
def hash_code(key):
  return len(str(key)) % len(hash_array)
```


## Collisions

However, there is an enormous number of possible keys and a limited-size array. At some point, a hash function will result in some keys mapped to the same index. When this occurs, it is called a _collision_.

### Example Collision

### Resolving Collisions

There are many ways to resolve a collision. One way is to make each element of the hash array a collection and store new elements in the next field in the collection.

If I attempted the following:

```ruby
  my_hash = MyHash.new
  my_hash["Dan"] = "Lead Instructor"
  my_hash["Chris"] = "CS Fun Instructor"
  my_hash["Simon"] = "Instructor Extraordinaire"
  my_hash[356] = "A big number"
```



### Example Resolution

We will end up with a hash which looks like this:

![Bad hash function example](images/Example-hash.png)


In this example, we resolve collisions by creating an array at each index of the main array and adding the key-value pair to the end of the list.

### !callout-info

## title

As you can see if the hash function does not adequately spread values out over the length of the array, this can result in long chains of key-value pairs and an O(n) worst-case runtime to find items. Luckily most libraries use well-proven hashing functions which normally prevent high numbers of collisions.

### !end-callout

## Summary

Hash Tables are a data structure which allows quick lookup of a value by using a key. Each key is mapped to an index of an internal array with a special method called a _hash function_. The average-case lookup is O(1) and worst-case is O(n). However most good implementations use a _hash function_ which attempts to uniformly distribute elements and prevent collisions.

## Key Terms
