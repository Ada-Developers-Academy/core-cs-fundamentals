# Reading Recursive Code

## Learning Goals

- Define base case
- List the parts of a recursive function
- Define stack
- Practice reading recursive function calls

## Vocabulary and Synonyms

| Vocab                        | Definition                                                                                                                                                            | How to Use in a Sentence                                                                                                                               |
| ---------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Recursion (computer science) | A programming technique where a function calls itself                                                                                                                 | "One way to compute the nth fibonacci number is with recursion, where a function `fibonacci` calls itself until it's finished."                        |
| Base Case                    | A condition which will end the recursion. This is case where the solution is concrete                                                                                 | "The base case for computing the nth fibonacci number is when `n` is 1 or 2, as the first two numbers of the fibonacci sequence are always 1 and 1." " |
| Recursive Case               | A situation in a recursive function that will call the function itself                                                                                                | "When computing the nth fibonacci number, if `n` is greater than 2, the `fibonacci` function will call itself."                                        |
| Stack (data structure)       | A data structure that operates as "Last-In-First-Out," where new data is pushed onto the top, and data is popped off from the top                                     |
| System stack                 | A part of memory dedicated to storing the method calls and local variables of a running program. The system stack is responsible for keeping track of function calls. |

## Recursion

In programming, a recursive function is a function that calls itself.

Consider the following recursive function:

```python
def hello_crash():
    print("Hello, crash!")
    hello_crash()
```

Both iteration and recursion are programming techniques used to repeat logic and behavior. There are often iterative and recursive solutions to the same problem!

When would we choose to solve a problem with recursion? Once we're used to thinking about recursion, recursive algorithms may be more readable and understandable compared to iterative solutions.

## Anatomy of a Recursive Function

Functions that call itself, like the imaginary `get_next_item` function, will recurse an infinite number of times.

However, if a function calls itself an infinite number of times, when will we actually get an answer and solve our problem? Recursive functions are more helpful when they actually _do_ stop!

In order to better read and debug recursive functions, let's dissect the anatomy of one.

### Base Cases are Stopping Conditions

Recursive algorithms will usually take in at least one argument. A recursive algorithm handles different situations based on the value of the argument. The algorithm should handle:

- At least one _recursive case_
- At least one _base case_

| Part           | Definition                                                            |
| -------------- | --------------------------------------------------------------------- |
| Recursive Case | A case or situation that depends on the solution of other cases       |
| Base Case      | A case or situation where there is a solution without using recursion |

The responsibility of the _recursive case_ is to divide the problem into a smaller problem.

The responsibility of the _base case_ is to give a solid, immediate solution to the problem.

We can imagine that a recursive function will handle recursive cases by calling itself, until it reaches a base case. Most recursive functions will follow this pattern:

1. If some condition is met and we're handling the base case
   - Solve using the base case's solution
1. Else
   - Solve by recursively calling the same function with different input

The "different input" in the recursive call should be working towards bringing the problem to the base case.

## Example: Exponentiation

Read through this recursive function, `power(num, exponent)`, whose responsibility is to calculate [exponentiation](https://en.wikipedia.org/wiki/Exponentiation) of the form `num`<sup>`exponent`</sup>. It takes in two arguments:

1. `num`, which is the base number
1. `exponent`, which is the exponent

For example, 3<sup>5</sup>, where `3` is `num` and `5` is `exponent`, is expressed and calculated like this:

```
3 * 3 * 3 * 3 * 3
```

And 3<sup>6</sup> is expressed as:

```
3 * 3 * 3 * 3 * 3 * 3
```

```python
def power(num, exponent):
    if exponent == 0:
        return 1

    return num * power(num, exponent - 1)
```

#### Base Case

In exponentiation, any number raised to the power of zero equals one.

```python
if exponent == 0:
    return 1
```

This code snippet is the _base case_. Whenever `power` is called **and** the argument `exponent` is `0`, then we return `1`. This base case gives us an immediate solution to the problem: `1`.

#### Recursive Cases

```python
return num * power(num, exponent - 1)
```

This code snippet handles the recursive cases. Recursive cases _call itself while making the problem smaller_. Recursive cases should move the problem closer and closer to the base case.

The problem gets smaller by calling `power` with a smaller exponent. As the `exponent` shrinks, it will eventually equal `0`.

### Running `power`

How can we visualize the flow of code execution? Let's add some print statements to `power`, and then run it.

```python
def power(num, exponent):
    print("Calling power! num:", num, "exponent:", exponent)
    if exponent == 0:
        return 1

    return num * power(num, exponent - 1)


print(3, "raised to the power of", 5, "is", power(3, 5))

print("-------------")

print(3, "raised to the power of", 6, "is", power(3, 6))
```

We should get the following output:

```
Calling power! num: 3 exponent: 5
Calling power! num: 3 exponent: 4
Calling power! num: 3 exponent: 3
Calling power! num: 3 exponent: 2
Calling power! num: 3 exponent: 1
Calling power! num: 3 exponent: 0
3 raised to the power of 5 is 243
-------------
Calling power! num: 3 exponent: 6
Calling power! num: 3 exponent: 5
Calling power! num: 3 exponent: 4
Calling power! num: 3 exponent: 3
Calling power! num: 3 exponent: 2
Calling power! num: 3 exponent: 1
Calling power! num: 3 exponent: 0
3 raised to the power of 6 is 729
```

We can confirm that the `power` function was called multiple times. Each time, the problem was made smaller, and `exponent` was decremented by one. Eventually, when `exponent` was `0`, it met the conditions for the base case, and returned `1`.

## Infinite Recursion

A function that calls itself without working towards a base case will repeat infinitely.

```python
def infinite_recursion(n):
    return n + infinite_recursion(n)
```

A function without a base case will never have a stopping point! Consider this code which has no base case:

```python
def infinite_recursion(n):
    return n + infinite_recursion(n - 1)
```

Executing both of these functions results in a `RecursionError`!

## Stacks and Function Calls

A running program has a dedicated section of memory called **the system stack**.

The system stack is where method calls and local variables are stored. It's responsible for keeping track of function calls.

The "stack" in "system stack" implies that it uses the _stack_ data structure. The system stack keeps track of function calls using a stack data structure.

### Intro to the Stack Data Structure

How does a stack organize data? A stack organizes data like a stack of plates! When we add a plate to the stack of plates, we add it to the top. When we need a plate from the stack of plates, we remove it from the top.

When a stack adds a new piece of data, it goes on top. When a stack removes one piece of data, it pops off the top item.

### !callout-info

## Stacks Are LIFO

Stacks operate in a Last-In-First-Out (LIFO) manner. They remove things in the reverse order they were added.

### !end-callout

## Tracing Recursive Functions and Illustrating the Stack

Let's read more recursive functions and apply our new knowledge about the _system stack_ in order to visualize it. Consider the following function.

```python
def mystery(num):
    if num <= 1:
        return 1

    return num * mystery(num-1)
```

What happens when we invoke the function when `num` is `5`?

```python
mystery(5)
```

We can begin to illustrate the _system stack_. Because the system stack keeps track of function calls, we add in the function call `mystery(5)` onto the stack.

![Diagram showing the system stack as a box. There is a box labeled "mystery(5)" inside the system stack.](<../assets/recursion_reading-recursion_mystery(5).png>)  
_Fig. Diagram showing the system stack as a box. There is a box labeled "mystery(5)" inside the system stack._

When `mystery(5)` executes, the base case is not met. It will call `mystery(4)`.

The function call `mystery(4)` is added to the _top_ of the stack.

![Diagram showing the system stack. There is a stack of boxes inside the system stack. The boxes are labeled in this order, from top-to-bottom: "mystery(4)", "mystery(5)"](<../assets/recursion_reading-recursion_mystery(4).png>)  
_Fig. Diagram showing the system stack. There is a stack of boxes inside the system stack. The boxes are labeled in this order, from top-to-bottom: "mystery(4)", "mystery(5)"_

Here, `num` is `4`, and the base case is still not met. This will call `mystery(3)`

We add `mystery(3)` to the top of the stack.

![Diagram showing the system stack. There is a stack of boxes inside the system stack. The boxes are labeled in this order, from top-to-bottom: "mystery(3)", "mystery(4)", "mystery(5)"](<../assets/recursion_reading-recursion_mystery(3).png>)  
_Fig. Diagram showing the system stack. There is a stack of boxes inside the system stack. The boxes are labeled in this order, from top-to-bottom: "mystery(3)", "mystery(4)", "mystery(5)"_

This calls `mystery(2)`. Calling `mystery(2)` gets pushed onto the stack.

![Diagram showing the system stack. There is a stack of boxes inside the system stack. The boxes are labeled in this order, from top-to-bottom: "mystery(2)", "mystery(3)", "mystery(4)", "mystery(5)"](<../assets/recursion_reading-recursion_mystery(2).png>)  
_Fig. Diagram showing the system stack. There is a stack of boxes inside the system stack. The boxes are labeled in this order, from top-to-bottom: "mystery(2)", "mystery(3)", "mystery(4)", "mystery(5)"_

The base case is still not met. The function calls `mystery(1)`, which gets pushed onto the stack.

![Diagram showing the system stack. There is a stack of boxes inside the system stack. The boxes are labeled in this order, from top-to-bottom: "mystery(1)", "mystery(2)", "mystery(3)", "mystery(4)", "mystery(5)"](<../assets/recursion_reading-recursion_mystery(1).png>)  
_Fig. Diagram showing the system stack. There is a stack of boxes inside the system stack. The boxes are labeled in this order, from top-to-bottom: "mystery(1)", "mystery(2)", "mystery(3)", "mystery(4)", "mystery(5)"_

At this point, `num` is `1`, which is our base case! The base case provides a solution and `return`s `1`.

As the function finishes and `return`s, it's time on the system stack is over. The system stack pops off the top function call after executing `return 1`.

![Diagram showing a stack of boxes inside the system stack. The boxes are labeled in this order, from top-to-bottom: "mystery(1)", "mystery(2)", "mystery(3)", "mystery(4)", "mystery(5)". There is an arrow pointing from "mystery(1)" to "mystery(2)" labeled "Return 1"](<../assets/recursion_reading-recursion_mystery(1)-return.png>)  
_Fig. Diagram showing a stack of boxes inside the system stack. The boxes are labeled in this order, from top-to-bottom: "mystery(1)", "mystery(2)", "mystery(3)", "mystery(4)", "mystery(5)". There is an arrow pointing from "mystery(1)" to "mystery(2)" labeled "Return 1"_

The system stack returns to `mystery(2)`.

`mystery(2)` takes that return value (`1`), and executes `num * mystery(num-1)`, and then **returns it**. In this case, where `num` is `2`, it **returns** `2 * 1`, or `2`.

The function `mystery(2)` is popped off the system stack. The system stack returns to `mystery(3)` on the stack.

We can summarize the remaining returns like so:

| Frame Executed | `num` | `num * mystery(num-1)` | Return value |
| -------------- | ----- | ---------------------- | ------------ |
| `mystery(3)`   | `3`   | `3 * 2`                | `6`          |
| `mystery(4)`   | `4`   | `4 * 6`                | `24`         |
| `mystery(5)`   | `5`   | `5 * 24`               | `120`        |

![Diagram showing a stack of "mystery()" function calls inside the system stack. There are arrows pointing from one function call to the function below. The arrows are labeled in this order, from top-to-bottom: "Return 1", "Return 2", "Return 6", "Return 24". An arrow leading from "mystery(5)" to empty space below is labeled "Return 120"](../assets/recursion_reading-recursion_mystery-result.png)  
_Fig. Diagram showing a stack of "mystery()" function calls inside the system stack. There are arrows pointing from one function call to the function below. The arrows are labeled in this order, from top-to-bottom: "Return 1", "Return 2", "Return 6", "Return 24". An arrow leading from "mystery(5)" to empty space below is labeled "Return 120"_

As a final result, we see that `mystery(5)` returns `120`!

Illustrating the stack like this can help us visualize recursive calls.

## Check for Understanding

<!-- Question Takeaway -->
<!-- prettier-ignore-start -->
### !challenge
* type: paragraph
* id: Do3G8s
* title: Reading Recursive Code
##### !question

What was your biggest takeaway from this lesson? Feel free to answer in 1-2 sentences, draw a picture and describe it, or write a poem, an analogy, or a story.

##### !end-question
##### !placeholder

My biggest takeaway from this lesson is...

##### !end-placeholder
### !end-challenge
<!-- prettier-ignore-end -->
