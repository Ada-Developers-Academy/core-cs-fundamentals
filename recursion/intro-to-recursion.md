# Intro to Recursion

## Learning Goals

- Define recursion

## Introduction

Life is full of problems. Big problems. But sometimes big problems are based on a smaller version of the same problem. And that smaller problem is itself based on a yet smaller version of the same problem. And that yet smaller problem is itself based on an even smaller version of the same problem, all the way down until we reach a size of the problem that isn't so big, and that we know how to solve.

Such problems are said to be recursive.

But recursion applies to more than just problems. Recursion happens around us all the time. Observing and naming recursion in the real world is a great way to begin thinking about recursion in our programs!

## Vocabulary and Synonyms

| Vocab     | Definition                                           | How to Use in a Sentence                                                                                     |
| --------- | ---------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| Recursion | The process of defining something in terms of itself | "The acronym GNU means "GNU's Not Unix." This is a recursive acronym, because its meaning refers to itself." |

## Recursion

Recursion is what happens when something's definition refers to itself. This could mean that something is constructed using itself, or that its construction is based on itself.

A recursive algorithm solves a problem by solving a smaller version of the same problem.

## Examples from Mathematics

The [Sierpiński triangle](https://en.wikipedia.org/wiki/Sierpi%C5%84ski_triangle) is a triangle which contains smaller triangles. These smaller triangles contain other smaller triangles... which contain other smaller triangles. This pattern goes on infinitely.

The Sierpiński triangle is recursive because it is made up of other Sierpiński triangles.

The [Koch snowflake](https://en.wikipedia.org/wiki/Koch_snowflake) (also known as Koch curve) is a shape made using a recursive algorithm.

A Koch snowflake is created by starting with an equilateral triangle, and applying the following algorithm for each line segment in the shape:

1. Divide the line segment into three segments of equal length
1. Draw an equilateral triangle, whose base is the middle segment from step one
1. Remove the line segment that is the base of the triangle from step two

The [Fibonacci sequence](https://en.wikipedia.org/wiki/Fibonacci_number) is a sequence of numbers where each next number is defined in terms of previous numbers in the sequence. As the sequence grows, the ratios between consecutive terms approaches the golden ratio **𝛗**, which is often considered a marker of natural beauty.

## Examples from Nature

- Romanesco broccoli, where each bud is made up of smaller buds
- Sourdough bread that was made from leftover sourdough
- Branching behavior in certain plants and algae, where a branch branches off another branch

We can observe many fractal patterns—patterns which have internal similarity—in nature. They can often be described recursively.

Many claim to find the golden ratio (related to the recursive Fibonacci sequence) hidden within numerous natural structures.

- Sunflower seed heads
- Pinecone seeds
- Flower petals

## Examples from Art

- Matryoshka dolls
  - Wooden dolls that contain other matryoshka dolls within itself
- Droste effect
  - An effect where an image contains the image itself
- Infinity mirrors

## Check for Understanding

<!-- Question 1 -->
<!-- prettier-ignore-start -->
### !challenge
* type: checkbox
* id: sE7nhe
* title: Thinking Recursively
##### !question

Which of the following are examples of recursion?

##### !end-question
##### !options

* A triangle which contains another triangle
* A Sierpiński triangle made up of other Sierpiński triangles
* Calculating the Fibonacci sequence, in which the next number in the sequence is the sum of the last two numbers in the sequence
* A row of similar jars and containers on a shelf
* A painted self-portrait

##### !end-options
##### !answer

* A Sierpiński triangle made up of other Sierpiński triangles
* Calculating the Fibonacci sequence, in which the next number in the sequence is the sum of the last two numbers in the sequence

##### !end-answer
##### !explanation

A Sierpiński triangle made up of other Sierpiński triangles is defined by referring to itself.

<br />

Calculating the Fibonacci sequence follows a recursive algorithm. Its solution depends on the solutions of smaller versions of the same problem.

<br />

Putting a triangle in another triangle doesn't necessarily make it recursive. If that inner triangle also had an inner triangle, and _that_ inner triangle also had an inner triangle, and so on, then it could be recursive.

<br />

Similar jars aren't defined in terms of each other, so would not be recursive. They just happen to be similar.

<br />

A painted self-portrait where the artist was painting a self-portrait of themselves painting a self-portrait, and so on, could be recursive, as in the Droste effect. But a typical self-portrait would not be recursive.

##### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

<!-- Question Takeaway -->
<!-- prettier-ignore-start -->
### !challenge
* type: paragraph
* id: xFPTHi
* title: Intro to Recursion
##### !question

What was your biggest takeaway from this lesson? Feel free to answer in 1-2 sentences, draw a picture and describe it, or write a poem, an analogy, or a story.

##### !end-question
##### !placeholder

My biggest takeaway from this lesson is...

##### !end-placeholder
### !end-challenge
<!-- prettier-ignore-end -->
