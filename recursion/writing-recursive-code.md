# Writing Recursive Code

## Learning Goals

- Construct a recursive solution from a word problem

## Considerations for a Recursive Function

The following prompts will help us construct different parts of a recursive function.

- What is the base case? What is the version of the problem where we know the answer without recursing?
- How can we describe the repeated problem that gets divided into smaller versions of the problem?
- What information does each smaller problem need?
- What information do we want back from each problem?
- How do we expect examples to behave?

### Determine the Base Case

The base case is the the version of the problem where we can determine the answer without recursing. Without a base case, our recursion will never end!

We may be able to determine the base case directly from the given problem statement. Sometimes we may have additional understanding that lets us determine the base case. Other times we may need to ask clarifying questions, or experiment with a few sample situations to get a feel for what might be a workable base case.

### Describe the Repeated Smaller Problem

What is the problem that needs to be solved? What do "smaller" versions of the problem look like? The answers to these questions will help us determine when and how to make the recursive function call.

We'll use this answer to help us visualize the solution, as we'll use the remaining prompts to determine details.

### Determine the Information the Smaller Problem Needs

Each version of the smaller problem needs input. What pieces of input are needed?

The answer to this question will help us determine the _parameters_ of our recursive function.

We should also consider how the parameters move towards the base case. Recall that if the parameters never move towards the base case, we'll end up with infinite recursion.

### Determine the Information We Want Back

Given the problem statement, what is the information that each problem should give back?

The answer to this question will determine the _return_ value of our function.

### Create Example Tables

When we have a draft of our recursive function, we can create example tables to check our work.

Here is a set of sample headers that we could use to build an example table. Each row in the table should represent a function call that is on the call stack.

| Function Call | Argument(s) | Return value |
| ------------- | ----------- | ------------ |

## Walk-through: Summing Natural Numbers

In mathematics, _natural numbers_ are numbers used for counting and ordering. For this situation, we will use the definition of the natural numbers as being all positive integers starting at 1.

Let's consider this programming problem:

Create a function named `sum_natural_numbers` that is responsible for summing all natural numbers up to and including the input, `num`. We will assume that `num` is always a positive integer. This function should return the sum.

Examples:

| `num` | Example           | Sum  |
| ----- | ----------------- | ---- |
| `3`   | 3 + 2 + 1         | `6`  |
| `4`   | 4 + 3 + 2 + 1     | `10` |
| `5`   | 5 + 4 + 3 + 2 + 1 | `15` |
| `1`   | 1                 | `1`  |

### Determine the Base Case

The problem states that natural numbers begin at 1.

We can determine the return value of `sum_natural_numbers(1)` without using recursion! This algorithm needs to stop when `num` is `1`.

Therefore, our base case is when `num == 1`.

### Describe the Repeated Smaller Problem

The problem states that the function "computes the sum of all natural number up to and including `num`."

<!-- Question 1 -->
<!-- prettier-ignore-start -->
### !challenge
* type: paragraph
* id: 7lIVkd
* title: Writing Recursive Code
##### !question

Consider the `sum_natural_numbers` problem.

What is one way we describe the repeated problem? What is the problem that gets divided into smaller versions of itself?

##### !end-question
##### !placeholder

The repeated problem for sum_natural_numbers is...

##### !end-placeholder
##### !explanation

We might describe the repeated problem like so:

The repeated problem is addition. We need to add the sum of all natural numbers calculated so far and a new number.

##### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

### Determine the Information the Smaller Problem Needs

Each smaller version of the problem needs an input number, `num`.

Each recursive call should bring the number closer to the base case, `1`. Because `1` is the smallest natural number, and all other integers are greater than `1`, we should start our recursion from a larger integer and decrement `num`.

By starting `num` greater than `1`, and decrementing by `1` at each level of recursion, we can be certain that `num` will eventually become `1` and end the recursion.

### Determine the Information We Want Back

The value we need to `return` from each call is the sum of all natural numbers up to and including `num`.

### Create Example Tables

The following table represents the call stack when calling `sum_natural_numbers(4)`. The top of the stack is the first row, `sum_natural_numbers(1)`. This function call is at the top of the stack because it is the base case, so it is the final function call. With stacks, the last item pushed in is the first item popped out (LIFO!).

| Function Call            | `num` | Return value |
| ------------------------ | ----- | ------------ |
| `sum_natural_numbers(1)` | `1`   | `1`          |
| `sum_natural_numbers(2)` | `2`   | `3`          |
| `sum_natural_numbers(3)` | `3`   | `6`          |
| `sum_natural_numbers(4)` | `4`   | `10`         |

### Putting It Together

Here is an example implementation of `sum_natural_numbers`:

```python
def sum_natural_numbers(num):
    print("Calling sum_natural_numbers! num:", num)

    # Base Case: When num is 1, the sum is 1
    if num == 1:
        return 1

    # Return the sum of all natural numbers so far plus the
    # current num.
    # Decrementing num by 1 brings us closer to the base case.
    return sum_natural_numbers(num-1) + num


print("The sum of all natural numbers up to and including 4 is",
      sum_natural_numbers(4))

print("-------------")

print("The sum of all natural numbers up to and including 5 is",
      sum_natural_numbers(5))

print("-------------")

print("The sum of all natural numbers up to and including 1 is",
      sum_natural_numbers(1))
```

### !callout-info

## Writing Recursive Code Takes Practice

After reading through this lesson, it's okay if it's not entirely clear how we arrive at recursive algorithms. Writing them often depends on having a bit of an "Aha!" moment. Sometimes, charting the data in an iterative solution can reveal a self-similarity in the calculations that provides that moment of recognition. Other times, thinking about a problem in terms like, "I want to do _X_, but to do so, first I need to do _Y_," where _Y_ is somehow a "smaller" version of _X_ can also be helpful.

<br />

In any case, we shouldn't get discouraged if the that key recursive step doesn't immediately leap out at us. Practice will help us develop the knack for seeing it!

### !end-callout

## Check for Understanding

<!-- Question Takeaway -->
<!-- prettier-ignore-start -->
### !challenge
* type: paragraph
* id: ukzYK2
* title: Writing Recursive Code
##### !question

What was your biggest takeaway from this lesson? Feel free to answer in 1-2 sentences, draw a picture and describe it, or write a poem, an analogy, or a story.

##### !end-question
##### !placeholder

My biggest takeaway from this lesson is...

##### !end-placeholder
### !end-challenge
<!-- prettier-ignore-end -->
