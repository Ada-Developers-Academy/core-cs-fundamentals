# Problem Set: Lists and Memory

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: multiple-choice
* id: 55890920-cfd1-47e0-96e8-4e2b1caa3ada
* title: Lists and References
* points: 1
* topics: python-lists

##### !question

True or False, a list variable directly references it's elements.

##### !end-question

##### !options

* True
* False

##### !end-options

##### !answer

* False

##### !end-answer

<!-- other optional sections -->
##### !hint

Think about side effects and functions.

##### !end-hint
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->
<!-- !explanation - !end-explanation (markdown, students can see after answering correctly) -->

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: short-answer
* id: f00befa4-e25a-40b6-b235-618bb0fca09a
* title: Side Effects
* points: 1
* topics: python-lists

##### !question

What is printed by this code segment?

```python
def mystery(numbers):
    index = 0
    while index < len(numbers):
        numbers[index] *= 2
        index += 1
    
    return numbers

nums = [1, 2, 3, 4, 5]
mystery(nums)

print(nums[3])
```


##### !end-question

##### !placeholder

What is printed by print(nums[3])?

##### !end-placeholder

##### !answer

/8/

##### !end-answer

<!-- other optional sections -->
<!-- !hint - !end-hint (markdown, hidden, students click to view) -->
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->
##### !explanation

The loop traverses the list multiplying each number by 2.  Since lists are mutable objects, changing things in `numbers`, the parameter impacts the array referenced by `nums`.


##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: multiple-choice
* id: 5a39abda-3557-49e7-bd9a-409dccc9e1a8
* title: Time complexity of a function
* points: 1
* topics: python-lists, Big-O

##### !question

What is the **time** complexity of the following function?

```python
def max(numbers):
    if len(numbers) == 0:
        return None

    max_num = numbers[0]

    for num in numbers:
        if num > max_num:
            max_num = num
    
    return max_num
```

##### !end-question

##### !options

* O(1)
* O(log n)
* O(n)
* O(n<sup>2</sup>)

##### !end-options

##### !answer

* O(n)

##### !end-answer

<!-- other optional sections -->
##### !hint

What determines the length of the loop?


##### !end-hint

##### !explanation

This loop will **always** traverse the entire length of the list (size n).

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: multiple-choice
* id: 5bbb9400-054c-4667-a82c-86d5b3642e2b
* title: Space complexity of a function
* points: 1
* topics: python-lists, Big-O

##### !question

What is the **space** complexity of the following function?

```python
def max(numbers):
    if len(numbers) == 0:
        return None

    max_num = numbers[0]

    for num in numbers:
        if num > max_num:
            max_num = num
    
    return max_num
```

##### !end-question

##### !options

* O(1)
* O(log n)
* O(n)
* O(n<sup>2</sup>)

##### !end-options

##### !answer

* O(1)

##### !end-answer

<!-- other optional sections -->
##### !hint

Are you building a data structure?

##### !end-hint

##### !explanation

No data structure is created in this function, it just always returns 1 number. 

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: multiple-choice
* id: 727f7ca4-61e8-418d-803f-106c1841367a
* title: Space Complexity Question 2
* points: 1
* topics: python-lists, big-o

##### !question

What is the space complexity of the following function?

```python
def long_words(words):
    big_words = []
    for word in words:
        if len(word) > 5:
            big_words.append(word)
    
    return big_words
```

##### !end-question

##### !options

* O(1)
* O(log n)
* O(n)
* O(n<sup>2</sup>)

##### !end-options

##### !answer

* O(n)

##### !end-answer

<!-- other optional sections -->
##### !hint

Are you creating any data structures?

##### !end-hint
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->
##### !explanation

As the loop executes with each iteration you may add an element to the `big_words` list.  If the `words` list is of size n, worst-case the new list will also be of size n.

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->
