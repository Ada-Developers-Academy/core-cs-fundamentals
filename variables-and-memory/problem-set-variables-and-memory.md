# Problem Set: Variables and Memory

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: multiple-choice
* id: 45bbfac6-3851-461a-9ef2-36832f43459d
* title: Variable Scope
<!-- * points: [1] (optional, the number of points for scoring as a checkpoint) -->
<!-- * topics: [python, pandas] (optional the topics for analyzing points) -->

##### !question

What is the value of `result` after the function `is_letter_in_word` is invoked as shown below?

```py
def is_letter_in_word(word, letter):
    """
    input: word (string) and letter (single character)
    output: boolean
    """
    if letter not in word:
        result = False
    else: 
        result = True

    return result

result = True
is_letter_in_word("hello", "x"):
```

##### !end-question

##### !options

* `True`
* `False`
* `"hello"`
* `"x"`

##### !end-options

##### !answer

* `True`

##### !end-answer

##### !explanation 

The variable `result` on line `7` is defined in function scope. The variable `result` on line `13` is defined in global scope. When we invoke `is_letter_in_word` on line `14` we do not assign its return value to a variable, so `result = True` is unchanged.

##### !end-explanation

<!-- other optional sections -->
<!-- !hint - !end-hint (markdown, hidden, students click to view) -->
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->
<!-- !explanation - !end-explanation (markdown, students can see after answering correctly) -->

### !end-challenge

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: multiple-choice
* id: b56446e2-22dc-47b3-901c-e3510dbbcbfb
* title: Variable Scope
<!-- * points: [1] (optional, the number of points for scoring as a checkpoint) -->
<!-- * topics: [python, pandas] (optional the topics for analyzing points) -->

##### !question

What is the value of `result` after the function `is_letter_in_word` is invoked as shown below?

```py
def is_letter_in_word(word, letter):
    """
    input: word (string) and letter (single character)
    output: boolean
    """
    if letter not in word:
        result = False
    else: 
        result = True

    return result

result = True
result = is_letter_in_word("hello", "x"):
```

##### !end-question

##### !options

* `True`
* `False`
* `"hello"`
* `"x"`

##### !end-options

##### !answer

* `False`

##### !end-answer

##### !explanation 

When we invoke `is_letter_in_word` on line `14` we assign its return value to the global variable `result`. As such, the value of `result` is overwritten with `False` (the value returned by the function).

##### !end-explanation

<!-- other optional sections -->
<!-- !hint - !end-hint (markdown, hidden, students click to view) -->
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->
<!-- !explanation - !end-explanation (markdown, students can see after answering correctly) -->

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: multiple-choice
* id: c8a41151-3eb4-4a4f-ac8d-cab3b1e869c3
* title: Variables Are References
<!-- * points: [1] (optional, the number of points for scoring as a checkpoint) -->
<!-- * topics: [python, pandas] (optional the topics for analyzing points) -->

##### !question

What are the values of `a` and `b` after the following code snippet is run?

```py
a = "hello"
b = a
a = "world"
```

##### !end-question

##### !options

* `a = "hello"`, `b = "hello"`
* `a = "hello"`, `b = "world"`
* `a = "world"`, `b = "hello"`
* `a = "world"`, `b = "world"`

##### !end-options

##### !answer

* `a = "world"`, `b = "hello"`

##### !end-answer

##### !explanation

Strings are an immutable datatype. In this example, the variables "a" and "b" point to where a string value is stored in memory. When `a` is reassigned to the value `"world"`, `b` still points to the value `"hello"`.

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: multiple-choice
* id: bf869b3d-23f9-4643-b1a4-9c661c865ac1
* title: Variables Are References
<!-- * points: [1] (optional, the number of points for scoring as a checkpoint) -->
<!-- * topics: [python, pandas] (optional the topics for analyzing points) -->

##### !question

What are the values of `before_tax` and `after_tax` after the following code snippet is run?

```py
before_tax = 10
after_tax = before_tax  * 1.1
before_tax = 20
```

##### !end-question

##### !options

* `before_tax = 10`, `after_tax = 11`
* `before_tax = 20`, `after_tax = 11`
* `before_tax = 20`, `after_tax = 22`

##### !end-options

##### !answer

* `before_tax = 20`, `after_tax = 11`

##### !end-answer

##### !explanation

Integers are an immutable datatype. If we want to update the `after_tax` value after we reassign the `before_tax` to `20`, we need another line `after_tax = before_tax  * 1.1`.

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: checkbox
* id: 9c70af03-8c71-4995-8c02-46d32e6a2e10
* title: Variables Are References
<!-- * points: [1] (optional, the number of points for scoring as a checkpoint) -->
<!-- * topics: [python, pandas] (optional the topics for analyzing points) -->

##### !question

What are the values of `all_stores` and `book_stores` after the following code snippet is run?

```py
all_stores = [
    {"name": "Ada's Technical Books", "type": "book"},
    {"name": "Elliott Bay", "type": "book"},
    {"name": "Central Co-op", "type": "grocery"} 
]

book_stores = all_stores
book_stores.pop()
```

##### !end-question

##### !options

*
```python
all_stores = [
    {"name": "Ada's Technical Books", "type": "book"},
    {"name": "Elliott Bay", "type": "book"},
    {"name": "Central Co-op", "type": "grocery"} 
]
book_stores = [
    {"name": "Ada's Technical Books", "type": "book"},
    {"name": "Elliott Bay", "type": "book"},
    {"name": "Central Co-op", "type": "grocery"} 
]
```
*   
```python
all_stores = [
    {"name": "Ada's Technical Books", "type": "book"},
    {"name": "Elliott Bay", "type": "book"},
    {"name": "Central Co-op", "type": "grocery"} 
]
book_stores = [
    {"name": "Ada's Technical Books", "type": "book"},
    {"name": "Elliott Bay", "type": "book"},
]
```
*   
```python
all_stores = [
    {"name": "Ada's Technical Books", "type": "book"},
    {"name": "Elliott Bay", "type": "book"},
]
book_stores = [
    {"name": "Ada's Technical Books", "type": "book"},
    {"name": "Elliott Bay", "type": "book"},
]
```

##### !end-options

##### !answer

*   
```python
all_stores = [
    {"name": "Ada's Technical Books", "type": "book"},
    {"name": "Elliott Bay", "type": "book"},
]
book_stores = [
    {"name": "Ada's Technical Books", "type": "book"},
    {"name": "Elliott Bay", "type": "book"},
]
```

##### !end-answer

##### !explanation

Lists are a mutable datatype. `all_stores` and `book_stores` point to the same place in memory. When we modify `book_stores`, we also modify `all_stores`. 

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: checkbox
* id: 861b3fdf-8339-4031-897b-0e7f41f1c6ee
* title: Variables Are References
<!-- * points: [1] (optional, the number of points for scoring as a checkpoint) -->
<!-- * topics: [python, pandas] (optional the topics for analyzing points) -->

##### !question

What are the values of `ada`, `elliott`, and `book_stores` after the following code snippet is run?

```py
ada = {"name": "Ada's Technical Books", "type": "book"}
elliott = {"name": "Elliott Bay", "type": "book"}

book_stores = [ada, elliott]

ada["city"] = "Seattle"
elliott["city"] = "Seattle"
```

##### !end-question

##### !options

*
```python
ada = {
    "name": "Ada's Technical Books", 
    "type": "book",
    }
elliot = {
    "name": "Elliott Bay", 
    "type": "book", 
    }

book_stores = [
    {
        "name": "Ada's Technical Books", 
        "type": "book", 
    },
    {
        "name": "Elliot Bay", 
        "type": "book",
    }
]
```

*
```python
ada = {
    "name": "Ada's Technical Books", 
    "type": "book", 
    "city": "Seattle"
    }
elliot = {
    "name": "Elliott Bay", 
    "type": "book", 
    "city": "Seattle"
    }

book_stores = [
    {
        "name": "Ada's Technical Books", 
        "type": "book", 
    },
    {
        "name": "Elliot Bay", 
        "type": "book", 
    },
]
```

*
```python
ada = {
    "name": "Ada's Technical Books", 
    "type": "book", 
    "city": "Seattle"
    }
elliot = {
    "name": "Elliott Bay", 
    "type": "book", 
    "city": "Seattle"
    }

book_stores = [
    {
        "name": "Ada's Technical Books", 
        "type": "book", 
        "city": "Seattle"
    },
    {
        "name": "Elliot Bay", 
        "type": "book", 
        "city": "Seattle"
    },
]
```

##### !end-options

##### !answer

*
```python
ada = {
    "name": "Ada's Technical Books", 
    "type": "book", 
    "city": "Seattle"
    }
elliot = {
    "name": "Elliott Bay", 
    "type": "book", 
    "city": "Seattle"
    }

book_stores = [
    {
        "name": "Ada's Technical Books", 
        "type": "book", 
        "city": "Seattle"
    },
    {
        "name": "Elliot Bay", 
        "type": "book", 
        "city": "Seattle"
    },
]
```

##### !end-answer

##### !explanation

Lists and dictionaries are a mutable datatypes. When we add a key-value pair to a dictionary, the variable that points to this dictionary has the new key-value pair. With a list of dictionaries, when the contents of the dictionaries are updated, the updated content is in the list.

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->
