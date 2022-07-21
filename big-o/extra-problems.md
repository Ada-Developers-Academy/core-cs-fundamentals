# O(10<sup>n</sup>) and n! Problems

<!-- Question 11 -->
<!-- prettier-ignore-start -->
### !challenge
* type: multiple-choice
* id: RIvnUW
* title: Big O
##### !question

Imagine a password of length _n_ that can contain only digit values (numbers).

What will be the time complexity for [a brute force solution](https://en.wikipedia.org/wiki/Brute-force_attack) to break the password?

##### !end-question
##### !options

* O(1)
* O(log n)
* O(n)
* O(n log n)
* O(n<sup>2</sup>)
* O(n<sup>3</sup>)
* O(n!)
* O(10<sup>n</sup>)

##### !end-options
##### !answer

* O(10<sup>n</sup>)

##### !end-answer
##### !explanation

To break a password of size _n_ where each value could be one of ten digits, 0 through 9, we will need to try out each possibility starting with all _n_ values being _0_. Then we systematically advance each value so that we test every possible combination of values.

<br />

Imagine a case where _n_ is 3. We start at 000, then 001, 002, 003, all the way through all ten digits. Then 010, 011, 012, and so on. Notice that we are basically counting up in numerical order, starting from 000, and ending at 999, for a total of 1000 passwords to check, which is _10 * 10 * 10_, or _10<sup>3</sup>_.

<br />

More generally, the first of the _n_ values could be any of 0 through 9. For each of these, we try the 10 possible values for the second of the _n_ values and so on. This would lead to _10 * 10 * ... n times_ or in other words _10<sup>n</sup>_ possibilities to explore. Hence the time complexity will be _O(10<sup>n</sup>)_ or _exponential_.

##### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

<!-- Question 12 -->
<!-- prettier-ignore-start -->
### !challenge
* type: multiple-choice
* id: GdZGf5
* title: Big O
##### !question

A traveling salesperson wants to visit _n_ cities. They can start the journey at any city and must visit each city once.

How many different possibilities exist for the order in which they could visit all _n_ cities?

##### !end-question
##### !options

* O(1)
* O(log n)
* O(n)
* O(n log n)
* O(n<sup>2</sup>)
* O(n<sup>3</sup>)
* O(n!)
* O(10<sup>n</sup>)

##### !end-options
##### !answer

* O(n!)

##### !end-answer
##### !explanation

We start with choosing one of the _n_ cities to be the starting city. There are _n_ possible options for this. For each choice of first city, there are _n - 1_ options to select the second city to visit. Then, _n - 2_ options to select the third city to visit, and so on until only one city remains to visit.

<br />

Let's consider an example: Let's say _n_ is 3 and the possible cities are Atlanta, Boston and Chicago. Here's how we can explore the problem. We pick one of the three cities to be the first city. Let's say Atlanta. Then, for the next city to visit, there are two options: Boston or Chicago. Let's say we pick Boston. Then only one city remains unvisited: Chicago. To try out all possible options would look like to following:

1. Atlanta → Boston → Chicago
1. Atlanta → Chicago → Boston
1. Boston → Atlanta → Chicago
1. Boston → Chicago → Atlanta
1. Chicago → Atlanta → Boston
1. Chicago → Boston → Atlanta

<br />

This is a total of 6 possibilities, which is the same as _3 * 2 * 1_ or _3!_, i.e. _3 factorial_.

<br />

Generalizing to _n_ cities, this would be _n * (n-1) * (n-2) * ... * 1_ or _n!_, i.e. _n factorial_. In Big O terms, the time complexity will be _O(n!)_ or _factorial_.

##### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->
