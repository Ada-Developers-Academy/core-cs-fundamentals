# Intro to Recursion

## Learning Goals

- Define recursion

## Introduction

A powerful problem-solving technique in computer science is to use recursion. It takes advantage of operations that computers excel at.

However, recursion happens around us all the time! Observing and naming recursion is a great way to begin thinking about recursion.

## Vocabulary and Synonyms

| Vocab     | Definition                                           | How to Use in a Sentence                                                                                     |
| --------- | ---------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| Recursion | The process of defining something in terms of itself | "The acronym GNU means "GNU's Not Unix." This is a recursive acronym, because its meaning refers to itself." |

## Recursion

Recursion is what happens when something's definition refers to itself. This could mean that something is constructed using itself, or that its construction is based on itself.

A recursive algorithm solves a problem by using the solving a smaller version of the same problem.

## Examples from Mathematics

The [Sierpiński triangle](https://en.wikipedia.org/wiki/Sierpi%C5%84ski_triangle) is a triangle which contains smaller triangles. These smaller triangles contain other smaller triangles... which contain other smaller triangles. This pattern goes on infinitely.

The Sierpiński triangle is recursive because it is made up of other Sierpiński triangles.

The [Koch snowflake](https://en.wikipedia.org/wiki/Koch_snowflake) (also known as Koch curve) is a shape made using a recursive algorithm.

A Koch snowflake is created by starting with an equilateral triangle, and following this algorithm for each line segment in the shape:

1. Divide the line segment into three segments of equal length
1. Draw an equilateral triangle, whose base is the middle segment from step one
1. Remove the line segment that is the base of the triangle from step two

## Examples from Nature

- Romanesco broccoli, where each bud is made up of smaller buds
- Sourdough bread that was made from leftover sourdough
- Branching behavior in certain plants and algae, where a branch branches off another branch

We can observe many fractals and fibonacci sequences, both of which are recursive in nature.

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

Which of the following are obvious examples of recursion?

##### !end-question
##### !options

* A triangle which contains other triangles
* A Sierpiński triangle made up of other Sierpiński triangles
* Calculating the fibonacci sequence, in which the next number in the sequence is the sum of the last two numbers in the sequence
* A row of similar jars and containers on a shelf
* A painted self-portrait

##### !end-options
##### !answer

* A Sierpiński triangle made up of other Sierpiński triangles
* Calculating the fibonacci sequence, in which the next number in the sequence is the sum of the last two numbers in the sequence

##### !end-answer
##### !explanation

A Sierpiński triangle made up of other Sierpiński triangles is defined by referring to itself.

Calculating the fibonacci sequence follows a recursive algorithm. Its solution depends on the solutions of smaller versions of the same problem.

##### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

<!-- Question Takeaway -->
<!-- prettier-ignore-start -->
### !challenge
* type: paragraph
* id: xFPTHi
* title: Thinking Recursively
##### !question

What was your biggest takeaway from this lesson? Feel free to answer in 1-2 sentences, draw a picture and describe it, or write a poem, an analogy, or a story.

##### !end-question
##### !placeholder

My biggest takeaway from this lesson is...

##### !end-placeholder
### !end-challenge
<!-- prettier-ignore-end -->
