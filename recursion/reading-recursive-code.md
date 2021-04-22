#

## Learning Goals

- Trace through a recursive function call and understand time and space comlexities

## Introduction

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

## Parts of a Recursive Function

A Recursive algorithm has two parts:

1. If the problem is easy, solve it immediately.
1. If the problem can't be solved immediately, divide it into smaller problems, then: Solve the smaller problems by applying this procedure to each of them.

We call a problem that can be solved immediately a _base case_ and a problem that divides the problem into a smaller problem a _recursive case_.

So a recursive algorithm is really made up of:

- At least one base case.
- At least one recursive case.

Most recursive methods will follow the following pattern:

- If [some condition]
  - Solve using the base case
- Else
  - Solve by recursively calling the same function with smaller input

### Example: Power

Examine the following method:

```ruby
def pow(base, exponent)
  return 1 if exponent == 0

  return base * pow(base, exponent - 1)
end
```

The method above calculates one number `base` taken to a given power `exponent`. The method starts with a condition to end the recursion called a _base case_, `return 1 if exponent == 0`. If the base case is met the method returns 1. The next line takes one step toward solving the problem (calculating `base` to the given exponent) by multiplying `base` times a _smaller_ version of the original problem (taking `base` to a power which is one smaller). This is called a _recursive case_.

### Without A Base Case

If you have a recursive function without a recursive case... well you just have a function. However if a method has a recursive call without a base case like this:

```ruby
def infinite_recursion(n)
  return n + infinite_recursion(n - 1)
end
```

The recursive calls will continue until the stack runs out of space resulting in what's called a _Stack Overflow Error_.

## Tracing Recursive Methods

Consider the following recursive method.

```ruby
def mystery(num)
  return 1 if num <= 1

  return num * mystery(num - 1)
end
```

How could you determine the result of mystery(5)?

You can trace through it by working through the problem just like Ruby executes it. You start by drawing a stack with `mystery(5)` on it.

![Mystery 5](<images/mystery(5).png>)

To solve that you need to find `mystery(4) because the base case is not true.

So you add `mystery(4)` to the stack.

![Mystery 4](<images/mystery(4).png>)

To solve that you need to find `mystery(3) because the base case is not true.

So you add `mystery(3)` to the stack.

![Mystery 3](<images/mystery(3).png>)

To solve that you need to find `mystery(2) because the base case is not true.

So you add `mystery(2)` to the stack.

![Mystery 3](<images/mystery(2).png>)

To solve that you need to find `mystery(1) because the base case is not true.

So you add `mystery(1)` to the stack.

![Mystery 3](<images/mystery(1).png>)

**Ah Ha!** now the base-case is met and it will return 1

![Mystery return 1](<images/mystery(1)-return.png>)

`mystery(2)` takes that return value multiplies it by 2 and returns 2. That method then takes 2 and multiplies it by 3 and returns the product 6. mystery(4) then takes that and multiples it by 4 and returns the product of 24. The last `mystery(5)` takes 24 and multiplies it by 5 and returns the product 120.

![mystery result](images/mystery-result.png)

You can use this manner to trace through and work through a recursive method.

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
