#

## Learning Goals

- Author a recursive algorithm

## Introduction


## Vocabulary and Synonyms

| Vocab | Definition | Synonyms | How to Use in a Sentence
| --- | --- | --- | ---


### Writing A Recursive Method

When writing a recursive method, try the following:

- Think about the recursive case: How are we going to break the problem into a smaller problem (by calling out method again) and get closer to the base case?
- Think about how you can reduce the problem to one or more smaller sub-problems of the same form.
- Think about what information you need to give to the sub-problems (the parameters).
- Think about what information you want back from the sub-problems (the return type).
- Write the method header.
- Think about the base case: When is the answer so simple that we know the answer without recursing?
- Write a method specification (like the static view of the problem) that explains exactly what it will do in terms of the parameters. Include any preconditions.
- Write the code.
- Test out your code with several different cases. Ensure all of them terminate with a base case and yield the right results.

## Walk-through: Summing Natural Numbers

Consider this programming problem.

```
Devise an algorithm for a function that takes a natural number as input parameter and computes the sum of all natural number up to and including the input parameter.

E.g.
natural_numbers_sum(3) should return 6 = 3 + 2 + 1
natural_numbers_sum(4) should return 10 = 4 + 3 + 2 + 1
```

Note:

In mathematics, the natural numbers are those used for counting and ordering. Natural numbers start with 0 or 1. (aka positive integers).

You could write an iterative solution like this:

```ruby
def natural_numbers_sum(num)
  sum = 0
  while num > 0 # While num is greater than zero
    sum += num  # Add the current num to sum
    num -= 1    # decrement num
  end

  return sum
end
```

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

- type: multiple-choice
- id: f645e9bd-6140-4712-8666-3d942b313630
- title: Base Case
- points: 1
- topics: recursion

##### !question

If you did this recursively, what could be the base case?

##### !end-question

##### !options

- Either num == 1 or num == 0. In that case return num.
- num > 0
- num % 2 == 0

##### !end-options

##### !answer

- Either num == 1 or num == 0. In that case return num.

##### !end-answer

<!-- other optional sections -->
<!-- !hint - !end-hint (markdown, users can see after a failed attempt) -->
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->

##### !explanation

Generally, we make the base-case the condition which should **end** the recursion. In this case the recursion should end when `num` is 1 or 0. It would continue as long as num > 0.

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

- type: multiple-choice
- id: 4a1395c2-3b77-4983-83ed-a3a8c9510871
- title: Recursive Case
- points: 1
- topics: recursion

##### !question

If you did this recursively, what do you do in the recursive case?

##### !end-question

##### !options

- num > 3
- return num + natural_numbers_sum(num - 1)
- return num

##### !end-options

##### !answer

- return num + natural_numbers_sum(num - 1)

##### !end-answer

<!-- other optional sections -->
<!-- !hint - !end-hint (markdown, users can see after a failed attempt) -->
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->

##### !explanation

The recursive case is the section of code which would have the method call itself.

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->


**Write the recursive solution**

If you want the solution you can take a look [at our example](recursion.resource.md).


## Debugging Infinite Recursion


### !challenge

- type: short-answer
- id: 5d36668e-4b91-48f3-b9a4-8f00cda5b44d
- title: What's wrong
  <!-- * points: [1] (optional, the number of points for scoring as a checkpoint) -->
  <!-- * topics: [python, pandas] (optional the topics for analyzing points) -->

##### !question

What is wrong with this code:

```ruby
def fibonacci(num)
  return fibonacci(num - 1) + fibonacci(num - 2)
end
```

What could be wrong with the above code?

##### !end-question

##### !placeholder

What's wrong?

##### !end-placeholder

##### !answer

/.+/

##### !end-answer

<!-- other optional sections -->
<!-- !hint - !end-hint (markdown, users can see after a failed attempt) -->
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->

##### !explanation

This code produces a Stack Overflow Error because it performs **infinite recursion.** The method needs a base case like return 1 if num <= 1

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

## Check for Understanding

Given the following binary search method, convert it to recursion. You can use the starter code below.

```ruby
def binary_search(array, to_find)
  high = array.length - 1
  low = 0
  while high >= low
    mid = (high + low) / 2
    if array[mid] == to_find
      return mid
    elsif array[mid] > to_find
      high = mid - 1
    else
      low = mid + 1
    end
  end

  return nil
end
```

```ruby
def recursive_binary_search(array, to_find, low = 0, high = array.length - 1)


end
```

You can see a solution in our [recursion examples page](recursion.resource.md)

