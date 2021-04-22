# Recursion and Iteration

## Recursion vs Iteration, Which is Better

Both loops and recursive solutions arrive at the same result, code gets repeated. However recursive methods are often considered more _elegant_ because they can be written with less code. Further some data structures like [binary search trees](https://www.geeksforgeeks.org/binary-search-tree-data-structure/) are naturally recursive and recursive solutions are equally efficient and easier to write.

On the other hand, iterative solutions do not require use of the system stack, saving space, and the overhead of a method call (both a cost in space and time). Thus often an iterative solution will be both faster and more space efficient. Languages that make extensive use of recursion take advantage of tail recursion to make up for this performance penalty.

So why learn recursion? A few reasons:

- Recursive code is sometimes easier to write and shorter
- Some data structures are recursive by nature which makes recursive methods attractive
- Often, if you need a stack-like data structure to store the state, a recursive solution can be nearly as efficient.
- A good portion of interview questions have a recursive solution

## Converting An Iterative Solution to Recursion

If you want to convert an iterative solution to recursion you can:

1. Identify the core, candidate loop in the iterative algorithm. Convert this to a new function.
1. Add parameters to the new function to take the loop variables and local variables as input. (In our example, add index as a parameter.)
1. Adapt the loop condition to an if condition, (if index >= length) in the new function. This will form the base case in the recursive function – returning and ending the recursion.
1. If the condition is not satisfied, we define the recursive case by converting the loop body into a recursive call. The loop variable from iterative version is updated while making the next recursive call.
   Finally, test & check for optimizations in the new recursive function.

Lets convert a linear-search to recursion

```ruby
def search(array, to_find)
  index = 0
  while index < array.length
    if array[index] == to_find
      return index
    end
    index += 1
  end
  return nil
end
```

1. Our core candidate loop is the `while index < array.length`.
1. Our loop control variable is `index`, which we can add as a parameter.
1. We can adapt the loop into an if statement to stop the recursion if we find the item, or if we run past the end of the array.

See below:

```ruby
def recursive_linear_search(array, to_find, current_index = 0)
  # Base Cases
  return nil if current_index > array.length
  return index if array[current_index] == to_find

  # Recursive Case
  return recursive_linear_search(array, to_find, current_index + 1)
end
```