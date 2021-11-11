# Instructor: Algorithmic Strategies

## Dynamic Programming O(1) Space Fibonacci

```python
def fibonacci(n):
    if n == 0 or n == 1:
        return n

    n_minus_2 = 0
    n_minus_1 = 1
    current = 2

    while current <= n:
        next_fib = n_minus_2 + n_minus_1

        # shift down
        n_minus_2 = n_minus_1
        n_minus_1 = next_fib

        current += 1

    return n_minus_1
```

A similar change cannot bring the forward recursive approach down to O(1) due to stack growth.

## Dynamic Programming for LCS

The memoization can be accomplished a little more nicely using tuples to store the arguments of a call as an immutable structure (also some other python niceties)

```python
def lcs(str1, str2, memo=None):
    if not str1 or not str2:
        return 0

    call = (str1, str2)
    if memo is None:
        memo = {}
    elif call in memo:
        return memo[call]

    first1, rest1 = str1[0], str1[1:]
    first2, rest2 = str2[0], str2[1:]

    current_score = 1 if first1 == first2 else 0

    result = max(
        current_score + lcs(rest1, rest2, memo),
        lcs(rest1, str2, memo),
        lcs(str1, rest2, memo)
    )

    memo[call] = result

    return result
```

It turns out this style of memoization is so common, that python has a decorator to help with this!

```python
import functools

@functools.cache
def lcs(str1, str2):
    if not str1 or not str2:
        return 0

    first1, rest1 = str1[0], str1[1:]
    first2, rest2 = str2[0], str2[1:]

    current_score = 1 if first1 == first2 else 0

    result = max(
        current_score + lcs(rest1, rest2),
        lcs(rest1, str2),
        lcs(str1, rest2)
    )

    return result
```

## Problem set hint discussions

### Challenge 1: Implement 0-1 knapsack
- Is there a way we can think of this problem as resembling the structure of the longest common subsequence problem?
  - The structure is very similar. The core of the problem is given the current item we are looking at, what's the best we can do if we include it in our solution and what's the best we can do if we _don't_ include it in our solution. In lcs(), the choices were, do we consume both of the current characters (either take as part of the subsequence and add 1 to our count if they match), do we advance only the first string, or do we advance only the second string. In knapsack(), the choices are does the current item "fit" in the sack, and if it does, what's the maximum value we can attain if we take it, compared to the max we can attain if we don't. So in either case, the core is to generate all possible options (we go for a brute force approach) and then pick the best for this situation.
- What limits are there on whether we are _allowed_ to take an item?
  - We may only take an item if the addition of it's weight does not cause us to exceed our max weight (alternatively, the current weight does not exceed the available remaining weight).
- If we are _able_ to take an item, what aspects around taking or not taking the item do we need to consider?
  - Which gives us a better result, adding this item's value to our total and analyzing the remaining items with the reduced available weight, or skipping this item and analyzing the remaining items without reducing the available weight.
- If we decide to take an item, what quantity contributes to our overall calculation?
  - The item's value would get added to our value tally
- If we decide to take an item, what effect does that have on our `max_weight`?
  - The available max weight would be decreased by the weight of the item
- If the weight of the current item exceeds the current `max_weight`, are we allowed to take it? What impact does that have on the recursive calls we would make for that case?
  - No, we can't take it, so the only thing we can do is choose not to take it, calculating the value we can get from the remaining items with an un-reduced max weight.
- What conditions would allow us to halt further recursion? What are the base cases?
  - Whether we have reached the end of the list.
  - Whether we have reduced our remaining max weight to 0.

### Challenge 2: Memoize 0-1 knapsack

- We probably need to add an additional parameter to be able to store and pass memoized data.
  - We should add a `memo` parameter, defaulted to `None`
- What data type would be appropriate for storing the memoized data?
  - Dictionary because we need to store the max value (the result of a knapsack call) for some list of values and a remaining weight. These keys are not consecutive numbers (not obvious how we would make them so—at least not immediately) so going with a dictionary is a good strategy.
- How can we initialize the storage for the memoized data?
  - If memo isn't initialized (it's None), initialize it to empty dict. Note that we cannot simply do a Falsy check since that would constantly re-initialize the dictionary if it were empty, so the stack frames would not be sharing the same memo object.
- Where do we need to update our memoized data?
  - Towards the end of the function, once we've found the max for this sub-problem.
- Where do we need to pass our memoized data?
  - Into the recursive knapsack calls
- What piece or pieces of data coming into the function call can be used to uniquely mark _this_ function call? The weights? The values? The max weight? Are any of these redundant?
  - The weights and the max weight (remaining available weight) are the best candidates. The values will contribute to max value stored in the memo, so won't contribute to the key lookup.
- If multiple pieces of data are required, how can we use those as keys into our memoized data? Can we use multi-dimensional storage? Is there a way to pack multiple pieces of data into a single piece of data?
  - We could use a two-dimensional dictionary as was done in the lcs solution. The first dimension would be related to the weight list, and the second to the remaining weight. We would still need to do something about the list of weights being mutable (see below). Or we can pack the multiple values into a hashable object. We could build our own, or make use of a built-in Python type (this is the approach presented in the example solution).
- If any of the data we would like to use as keys is mutable, can that be used? Is there a way to convert it to immutable data?
  - The list of weights is mutable, so cannot be used as a dict key. But we could convert the list of weights into a tuple of weights!
- What do parentheses mean in Python when used this way? How does this allow us to use these multiple data items as a single key?
  - The parentheses are creating a tuple literal. Tuples are immutable, and can be used as a dict key as long as all the value within them are also immutable.
- Why would we convert the list of weights to a tuple of weights?
  - If we simply put the list of weights into our tuple key, it would be mutable, rendering the entire tuple unfit for use as a dict key. By converting the list of weights to a tuple of weights, it can serve as part of an immutable key.
- Why would using the length of the weights list be enough?
  - The contents of the list of weights don't change. If we have a list of 3 weights `[10, 20, 30]`, then if we have processed the first item (whether taken or not), the remaining 2 items in the list are `[20, 30]`. And the last 1 item left in the list would always be `[30]`. So the length of the list acts like a proxy to the position of the item we are considering. Note that we cannot use the weight itself, since multiple items could have the same weight. If we use the length as our key for the items, it _would_ be more feasible to use nested arrays rather than nested dicts, but given the compound key is more convenient and frees us from needing to worry about pre-allocating the array (it's a little tricky to deal with the remaining weight dimension), there's little reason to do so for this example.
