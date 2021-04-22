# Reading Recursive Code

## Learning Goals

- Trace through a recursive function call and understand time and space comlexities

## Introduction

Recursion solves plenty of computational problems. However, recursive functions may be interesting to read because they call itself.

Should we ever come across recursive functions.

## Vocabulary and Synonyms

| Vocab                        | Definition                                                                            | Synonyms | How to Use in a Sentence                                                                                                    |
| ---------------------------- | ------------------------------------------------------------------------------------- | -------- | --------------------------------------------------------------------------------------------------------------------------- |
| Recursion (computer science) | A programming technique where a function calls itself                                 | -        | "One way to calculate a fibonacci number is with recursion, where a function `fibonacci` calls itself until it's finished." |
| Base Case                    | A condition which will end the recursion. This is case where the solution is concrete | -        | ""                                                                                                                          |

| Base Case | A condition which will end the recursion. This is the case where the solution is straightforward to solve. |
| Recursive Case | The part of a recursive method which makes a recursive call. |
| Tail Recursion | A tail recursive function is a recursive function where the function calls itself at the end ("tail") of the function in which no computation is done after the return of recursive call. |
Infinite Recursion
| Stack Overflow Error | An error caused when the system stack memory is exhausted, usually from infinite recursion. |

##

In programming, a recursive function is a function that calls itself.

We can imagine a recursive function named `get_next_item`. When we call `get_next_item`, it will invoke itself, `get_next_item`. Of course, when _this_ function calls begins execution, it will also invoke itself.

Iteration and recursion are both programming techniques used to repeat logic and behavior. Often, the same problems that iteration solves can be solved with recursion!

When would we solve a problem with recursion? Once we're used to thinking about recursion, recursive algorithms may be more readable and understood compared to iterative solutions.

## Anatomy of a Recursive Function

Functions that call itself, like the imaginary `get_next_item` function, will recurse an infinite number of times.

However, if a function calls itself an infinite number of times, when will we actually get an answer and solve our problem? Recursive functions are more helpful when they actually _do_ stop!

In order to properly handle recursive functions, let's dissect the anatomy of one. Dissecting the anatomy of a recursive function will help us read and debug them.

### Base Cases are Stopping Conditions

Recursive algorithms will usually take in at least one argument. A recursive algorithm handles different situations based on what that argument is. The algorithm should handle:

- At least one _recursive case_
- At least one _base case_

| Part           | Definition                                                            |
| -------------- | --------------------------------------------------------------------- |
| Recursive Case | A case or situation that depends on the solution of other cases       |
| Base Case      | A case or situation where there is a solution without using recursion |

The responsibility of the _recursive case_ is to divide the problem into a smaller problem.

The responsibility of the _base case_ is to give a solid, immediate solution to the problem.

We can imagine that a recursive function will handle recursive cases by calling itself, until it reaches a base case. Most recursive functions will follow this pattern:

1. If some condition is met
   - Solve using the base case
1. Else
   - Solve by recursively calling the same function with different input

The "different input" in the recursive call should be working towards bringing the problem to the base case.

## Example: Exponentiation

Read through this recursive function, `pow`, whose responsibility is to calculate [exponentiation](https://en.wikipedia.org/wiki/Exponentiation), otherwise known as `num`<sup>`exponent`</sup>. It takes in two arguments:

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
def pow(num, exponent):
    if exponent == 0:
        return 1

    return num * pow(num, exponent - 1)
```

#### Base Case

In exponentiation, any number raised to the power of zero equals one.

```python
if exponent == 0:
    return 1
```

This code snippet is the _base case_. Whenever `pow` is called **and** the argument `exponent` is `0`, then we return `1`. This base case gives us an immediate solution to the problem: `1`!

#### Recursive Cases

```python
return num * pow(num, exponent - 1)
```

This code snippet handles the recursive cases. Recursive cases _call itself while making the problem smaller_. Recursive cases should move the problem closer and closer to the base case.

The problem gets smaller by calling `pow` with a smaller exponent. As the `exponent` shrinks, it will eventually equal `0`!

### Running `pow`

How can we visualize the flow of code execution? Let's imagine the same `pow` function with several print statements, and then run it.

```python
def pow(num, exponent):
    print("Calling pow! num:", num, "exponent:", exponent)
    if exponent == 0:
        return 1

    return num * pow(num, exponent - 1)


print(3, "raised to the power of", 5, "is", pow(3, 5))

print("-------------")

print(3, "raised to the power of", 6, "is", pow(3, 6))
```

We should get the following output:

```
Calling pow! num: 3 exponent: 5
Calling pow! num: 3 exponent: 4
Calling pow! num: 3 exponent: 3
Calling pow! num: 3 exponent: 2
Calling pow! num: 3 exponent: 1
Calling pow! num: 3 exponent: 0
3 raised to the power of 5 is 243
-------------
Calling pow! num: 3 exponent: 6
Calling pow! num: 3 exponent: 5
Calling pow! num: 3 exponent: 4
Calling pow! num: 3 exponent: 3
Calling pow! num: 3 exponent: 2
Calling pow! num: 3 exponent: 1
Calling pow! num: 3 exponent: 0
3 raised to the power of 6 is 729
```

We can confirm that the `pow` function was called multiple times. Each time, the problem was made smaller, and `exponent` decremented by one. Eventually, when `exponent` was `0`, it met the conditions for the base case, and returned `1`.

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

A running program has a dedication section of memory called **the system stack**.

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

![Diagram showing the system stack as a box. There is a box labeled "mystery(5)" inside the system stack.](../assets/recursion_reading-recursion_mystery(5).png)  
_Fig. Diagram showing the system stack as a box. There is a box labeled "mystery(5)" inside the system stack._

When `mystery(5)` executes, the base case is not met. It will call `mystery(4)`.

The function call `mystery(4)` is added to the _top_ of the stack.

![Diagram showing the system stack. There is a stack of boxes inside the system stack. The boxes are labeled in this order, from top-to-bottom: "mystery(4)", "mystery(5)"](../assets/recursion_reading-recursion_mystery(4).png)  
_Fig. Diagram showing the system stack. There is a stack of boxes inside the system stack. The boxes are labeled in this order, from top-to-bottom: "mystery(4)", "mystery(5)"_

Here, `num` is `4`, and the base case is still not met. This will call `mystery(3)`

We add `mystery(3)` to the top of the stack.

![Diagram showing the system stack. There is a stack of boxes inside the system stack. The boxes are labeled in this order, from top-to-bottom: "mystery(3)", "mystery(4)", "mystery(5)"](../assets/recursion_reading-recursion_mystery(3).png)  
_Fig. Diagram showing the system stack. There is a stack of boxes inside the system stack. The boxes are labeled in this order, from top-to-bottom: "mystery(3)", "mystery(4)", "mystery(5)"_

This calls `mystery(2)`. Calling `mystery(2)` gets pushed onto the stack.

![Diagram showing the system stack. There is a stack of boxes inside the system stack. The boxes are labeled in this order, from top-to-bottom: "mystery(2)", "mystery(3)", "mystery(4)", "mystery(5)"](../assets/recursion_reading-recursion_mystery(2).png)  
_Fig. Diagram showing the system stack. There is a stack of boxes inside the system stack. The boxes are labeled in this order, from top-to-bottom: "mystery(2)", "mystery(3)", "mystery(4)", "mystery(5)"_

The base case is still not met. The function calls `mystery(1)`, which gets pushed onto the stack.

![Diagram showing the system stack. There is a stack of boxes inside the system stack. The boxes are labeled in this order, from top-to-bottom: "mystery(1)", "mystery(2)", "mystery(3)", "mystery(4)", "mystery(5)"](../assets/recursion_reading-recursion_mystery(1).png)  
_Fig. Diagram showing the system stack. There is a stack of boxes inside the system stack. The boxes are labeled in this order, from top-to-bottom: "mystery(1)", "mystery(2)", "mystery(3)", "mystery(4)", "mystery(5)"_

At this point, `num` is `1`, which is our base case! The base case provides a solution and `return`s `1`.

As the function finishes and `return`s, it's time on the system stack is over. The system stack pops off the top function call after executing `return 1`.

![Diagram showing a stack of boxes inside the system stack. The boxes are labeled in this order, from top-to-bottom: "mystery(1)", "mystery(2)", "mystery(3)", "mystery(4)", "mystery(5)". There is an arrow pointing from "mystery(1)" to "mystery(2)" labeled "Return 1"](../assets/recursion_reading-recursion_mystery(1)-return.png)  
_Fig. Diagram showing a stack of boxes inside the system stack. The boxes are labeled in this order, from top-to-bottom: "mystery(1)", "mystery(2)", "mystery(3)", "mystery(4)", "mystery(5)". There is an arrow pointing from "mystery(1)" to "mystery(2)" labeled "Return 1"_

The system stack returns to `mystery(2)`.

`mystery(2)` takes that return value (`1`), and executes `num * mystery(num-1)`, and then **returns it**. In this case, where `num` is `2`, it **returns** `2 * 1`, or `2`.

The function `mystery(2)` is popped off the system stack. The system stack returns to `mystery(3)` on the stack.

We can summarize the remaining returns like so:

| Frame Executed | `num` | `num * mystery(num-1)` | Return value |
| -------------- | ----- | ---------------------- | ------------ |
| `mystery(3)`   | `3`   | `2`                    | `6`          |
| `mystery(4)`   | `4`   | `6`                    | `24`         |
| `mystery(5)`   | `5`   | `24`                   | `120`        |

![Diagram showing a stack of "mystery()" function calls inside the system stack. There are arrows pointing from one function call to the function below. The arrows are labeled in this order, from top-to-bottom: "Return 1", "Return 2", "Return 6", "Return 24". An arrow leading from "mystery(5)" to empty space below is labeled "Return 120"](../assets/recursion_reading-recursion_mystery-result.png)  
_Fig. Diagram showing a stack of "mystery()" function calls inside the system stack. There are arrows pointing from one function call to the function below. The arrows are labeled in this order, from top-to-bottom: "Return 1", "Return 2", "Return 6", "Return 24". An arrow leading from "mystery(5)" to empty space below is labeled "Return 120"_

As a final result, we see that `mystery(5)` returns `120`!

Illustrating the stack like this can help us visualize recursive calls.

## Reading the `factorial` Function

Let’s consider the mathematical concept factorial. In order to calculate a factorial of a number _n_, denoted as _n!_, you multiply all the numbers from _n_ down to 1. The base case is for number 1. The Factorial of 1 is 1.

So,
5! = 5 _ 4 _ 3 _ 2 _ 1
10! = 10 _ 9 _ 7 _ 6 _ 5 _ 4 _ 3 _ 2 _ 1
3000! = 3000 _ 2999 _ 2998 _ 2997 _ … _ 3 _ 2 \* 1

We could also state 5! = 5 _ 4 _ 3 _ 2 _ 1 as:
5! = 5 _ 4!
4! = 4 _ 3!
3! = 3 _ 2!
2! = 2 _ 1! And we know 1! = 1

So, in general:
n! = n _ (n-1) _ (n-2) _ (n-3) _ … \* 1

Which broken down to model a recursive algorithm is:

- If simple, Solve it immediately --> 1! = 1
- If not simple, solve a small piece and then try to solve the rest --> n! = n \* (n-1)!

If we were to divide this concept into a recursive definition, we might say:

- If n = 1, return 1
- If n > 1, return n \* (n-1)!

We call this the _static view_ of a recursive method. Basically the **static view** is the mathematical way of looking at a recursive problem.

Mathematically, factorial can be explained as:

- _1! = 1_
- _n! = n × (n-1)!_ if _n > 1_

The second statement shows the **recurrence relationship** while computing factorial of a number.

### Code it

Once we know what the base case(s) and the recursive case(s) of a problem are, we can then write the code.

**Given**:
Factorial

- factorial(1) = 1
- factorial(n) = n \* factorial(n-1), where n > 1

We can code this as:

```ruby
def factorial(n)
  if n == 1
    return 1
  else
    return n * factorial(n-1)
  end
end
```

or

```ruby
def factorial(n)
  return 1 if n == 1
  return n * factorial(n-1)
end
```

### How Factorial Works

Each time the factorial function is called Ruby places a _stack frame_ on the call stack. This is the memory storing the method's local variables, parameters and the location to return to when the method finishes. Since most factorial calls where n > 1 result in multiple items placed on the system stack, this incurs a cost in terms of space complexity.

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

- type: multiple-choice
- id: a4455fe4-7766-461c-b8bc-b4132b5cf5f5
- title: Space complexity of Factorial
- points: 1
- topics: recursion

##### !question

What is the **Space** complexity of factorial?

```ruby
def factorial(n)
  return 1 if n == 1
  return n * factorial(n-1)
end
```

##### !end-question

##### !options

- O(1)
- O(log n)
- O(n)
- O(nlog n)
- O(n^2)

##### !end-options

##### !answer

- O(n)

##### !end-answer

<!-- other optional sections -->
<!-- !hint - !end-hint (markdown, users can see after a failed attempt) -->
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->
<!-- !explanation - !end-explanation (markdown, students can see after answering correctly) -->

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

### Tracing Through Factorial

If you have `factorial(5)` first this method call gets put on the call stack.

![Factorial(5)](images/factorial-5.png)

Then `factorial(5)` calls `factorial(4)`, which calls `factorial(3)`, and that calls `factorial(2)` and this calls `factorial(1)`.

![Factorial 5 -> 1 ](images/factorial5-1.png)

`factorial(1)` returns 1, which is plugged into `factorial(2)` which multiplies 2 \* that returned result and carries on down in this fashion.

![factorial(5) completely executed](images/factorial-5-complete.png)

So you can trace a recursive function by walking through it's function calls, placing them on a simulated stack and then unwinding the stack as methods complete returning their result to the calling method.

### Understanding space and time complexities for the example

To compute _factorial(n)_, n operations will be needed. Therefore, the time complexity will be _O(n)_.</br>
Each recursive call will end up with a stack frame on the call stack. There will be _n_ such stack frames by the time the base case is reached and the stack starts unwinding. Stack frames take up space in memory. So, the space complexity will be _O(n)_.

### Time & Space Complexity

How can you determine the time and space complexity of a recursive method.

For the time complexity you can use the number of recursive calls, just like you would use the number of loop iterations. So the above method has a time complexity of O(n).

## Summary

Recursion is when a method calls itself. This works like a loop and can lead to similar issues. If a recursive method does not have a condition to end the recursion, called a _base case_, then the recursion will continue until memory is exhasted in a _stack overflow error_. This kind of unbounded recursion is called _infinite recursion_.

Typically recursive methods will have a base case which can be solved quickly and a recursive case which involves a recursive call on a smaller version of the larger problem. By reducing the problem with each call you approach the base-case.

Recursive methods often have a space-complexity cost. This is do to the call-stack using memory.

Interpreters/compilers in many languages can look at a recursive method and convert it into a loop behind the scenes. They require a method to have no additional work needed after the recursive call. By structuring a method this way you get the space/time benefits of a loop and the simplicity of a recursive method. This kind of recursion is called _tail recursion_. Ruby does **not** have tail recursion turned on by default.
