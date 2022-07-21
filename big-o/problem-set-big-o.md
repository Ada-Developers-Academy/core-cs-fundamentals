# Problem Set: Big(O)

## Directions

Complete all questions below.

## Practice

<!-- Question 1 -->
<!-- prettier-ignore-start -->
### !challenge
* type: multiple-choice
* id: rhpVnF
* title: Big O
##### !question

What is the time complexity of the following piece of code?

```python
def does_value_exist(input_list, value):
    for item in input_list:
        if item == value:
            return True
    return False
```

##### !end-question
##### !options

* O(1)
* O(log n)
* O(n)
* O(n log n)
* O(n<sup>2</sup>)
* O(n<sup>3</sup>)

##### !end-options
##### !answer

* O(n)

##### !end-answer
##### !explanation

The provided code _linearly_ searches through each item in the list to check if the value is found. In the worst case scenario, all items in the list are searched. This means if there are _n_ items in the list, all _n_ items will be checked. In the best case scenario, the value to be found would be the first item in the list. In the average case, the number of times the loop will run will be somewhere in between the best case and worst case, but still dependent on the number of items in the list, i.e. _n_.

<br />

The time complexity of this algorithm is therefore _linear_ or _O(n)_ where _n_ is the length of the `input_list`.

##### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

<!-- Question 2 -->
<!-- prettier-ignore-start -->
### !challenge
* type: multiple-choice
* id: fFOaNl
* title: Big O
##### !question

What is the time complexity of the following piece of code?

```python
def repeat_four_times(value):
    for count in range(4):
        print("The value is", value)
```

##### !end-question
##### !options

* O(1)
* O(log n)
* O(n)
* O(n log n)
* O(n<sup>2</sup>)
* O(n<sup>3</sup>)

##### !end-options
##### !answer

* O(1)

##### !end-answer
##### !explanation

Independent of the input parameter value, the loop in this method will always run four times. Because the number of iterations in the loop is constant and independent of input parameter size or value, the time complexity will be _constant_ or _O(1)_.

##### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

<!-- Question 3 -->
<!-- prettier-ignore-start -->
### !challenge
* type: multiple-choice
* id: 2sHTBq
* title: Big O
##### !question

What is the time complexity of the following piece of code?

```python
def repeat_multiple_times(value, num_of_repetitions):
    for count in range(num_of_repetitions):
        print("The value is", value)
```

##### !end-question
##### !options

* O(1)
* O(log n)
* O(n)
* O(n log n)
* O(n<sup>2</sup>)
* O(n<sup>3</sup>)

##### !end-options
##### !answer

* O(n)

##### !end-answer
##### !explanation

This method executes the `print` instruction `num_of_repetitions` times. If the value of `num_of_repetitions` changes, the number of times the `print` instruction is repeated will change _linearly_.

<br />

Therefore, the time complexity of this algorithm is _linear_ or _O(n)_ where _n_ is the supplied number of repetitions.

##### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

<!-- Question 4 -->
<!-- prettier-ignore-start -->
### !challenge
* type: multiple-choice
* id: BAKq4K
* title: Big O
##### !question

What is the time complexity of the following piece of code?

```python
def greet_friends(input_list):
    for num in range(len(input_list)):
        print(f"Hello, Friend #{num + 1}!")
```

##### !end-question
##### !options

* O(1)
* O(log n)
* O(n)
* O(n log n)
* O(n<sup>2</sup>)
* O(n<sup>3</sup>)

##### !end-options
##### !answer

* O(n)

##### !end-answer
##### !explanation

This method will execute the `print` statement as many times as is the length of the `input_list`. If the size of the `input_list` changes, the number of times the `print` statement gets executed will change to match the size.

<br />

Since the number of times the `print` statement gets executed is _linearly_ proportional to the length of the `input_list`, the time complexity is _linear_ or _O(n)_ where _n_ is the length of the `input_list`.

##### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

<!-- Question 5 -->
<!-- prettier-ignore-start -->
### !challenge
* type: multiple-choice
* id: SULbFB
* title: Big O
##### !question

What is the time complexity of the following piece of code?

```python
def greet_friends(input_list):
    i = 0
    while i < 17:
        print(f"Hello, Friend #{i + 1}!")
        i += 1
```

##### !end-question
##### !options

* O(1)
* O(log n)
* O(n)
* O(n log n)
* O(n<sup>2</sup>)
* O(n<sup>3</sup>)

##### !end-options
##### !answer

* O(1)

##### !end-answer
##### !explanation

The loop in this method gets run 17 times regardless of the size or value of the input list.

<br />

Hence, the time complexity of _constant_ or _O(1)_.

##### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

<!-- Question 6 -->
<!-- prettier-ignore-start -->
### !challenge
* type: multiple-choice
* id: 4w506R
* title: Big O
##### !question

What is the time complexity of the following piece of code?

```python
def greet_friends(input_list):
    count = len(input_list)
    i = 0
    while i < count:
        print(f"Hello, Friend #{i + 1}!")
        i += 1
```

##### !end-question
##### !options

* O(1)
* O(log n)
* O(n)
* O(n log n)
* O(n<sup>2</sup>)
* O(n<sup>3</sup>)

##### !end-options
##### !answer

* O(n)

##### !end-answer
##### !explanation

The loop in this method gets run `count` times. `count` is the length of `input_list`. As the length of `input_list` changes, so will the number of times the loop gets executed. The execution of the loop is _linearly_ proportional to the length of `input_list`.

<br />

So, the time complexity is _linear_ or _O(n)_ where _n_ is the length of the input parameter, `input_list`.

##### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

<!-- Question 7 -->
<!-- prettier-ignore-start -->
### !challenge
* type: multiple-choice
* id: bfvZeu
* title: Big O
##### !question

What is the time complexity of the following piece of code?

```python
def greet_friends(input_list):
    count = len(input_list)
    i = 0
    while i < 17:
        for j in range(count):
            print(f"Hello, Friend #{i+1} in {j+1}!")
        i += 1
```

##### !end-question
##### !options

* O(1)
* O(log n)
* O(n)
* O(n log n)
* O(n<sup>2</sup>)
* O(n<sup>3</sup>)

##### !end-options
##### !answer

* O(n)

##### !end-answer
##### !explanation

There are two nested loops in this method. The outer `while` loop gets run 17 times. The inner `for` loop gets run `count` times where `count` is the length of `input_list`. Since the loops are nested, for each iteration of the outer loop, the complete inner loop gets run once. That means, the `print` statement will get executed (17 * `count`) times.

<br />

In Big O terms, the `print` statement will get executed _(17 * n)_ times, where _n_ is the length of `input_list`. While determining time complexity, we drop the constants. So, the time complexity of this algorithm is _O(n)_, where _n_ is the length of `input_list`. In other words, the time complexity is linearly proportional to the input size.

##### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

<!-- Question 8 -->
<!-- prettier-ignore-start -->
### !challenge
* type: multiple-choice
* id: 5qCZ8q
* title: Big O
##### !question

What is the time complexity of the following piece of code?

```python
def greet_friends(input_list):
    count = len(input_list)
    i = 0
    while i < count:
        for j in range(count):
            print(f"Hello, Friend #{i+1} in {j+1}!")
        i += 1
```

##### !end-question
##### !options

* O(1)
* O(log n)
* O(n)
* O(n log n)
* O(n<sup>2</sup>)
* O(n<sup>3</sup>)

##### !end-options
##### !answer

* O(n<sup>2</sup>)

##### !end-answer
##### !explanation

There are two nested loops in this method. Each loop runs _n_ times where _n_ is the length of `input_list`. Since the loops are nested, the loop will run _n * n_ times.

<br />

So, the time complexity of this algorithm is _O(n<sup>2</sup>)_ where _n_ is the length of the input `input_list`. In other words, the time complexity is _quadratic_, which is a _polynomial_ time complexity.

##### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->

<!-- Question 9 -->
<!-- prettier-ignore-start -->
### !challenge
* type: multiple-choice
* id: rkV75c
* title: Big O
##### !question

What is the time complexity of the following piece of code?

```python
def greet_friends(input_list):
    count = len(input_list)
    k = 0
    while k != count:
        i = 0
        while i < count:
            for j in range(count):
                print(f"Hello, Friend #{i+1} in #{j+1}!")
            i += 1
        k += 1
```

##### !end-question
##### !options

* O(1)
* O(log n)
* O(n)
* O(n log n)
* O(n<sup>2</sup>)
* O(n<sup>3</sup>)

##### !end-options
##### !answer

* O(n<sup>3</sup>)

##### !end-answer
##### !explanation

There are three nested loops in this method, each running _n_ times where _n_ is the length of `input_list`. The time complexity will therefore be _n * n * n_ or in Big O terms _O(n<sup>3</sup>)_. In other words, the time complexity will be _cubic_, which is a _polynomial_ time complexity.

##### !end-explanation
### !end-challenge
<!-- prettier-ignore-end -->