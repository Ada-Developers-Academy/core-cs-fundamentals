# Problem Set: Git

## Directions

Follow the directions below.

There is no submission for this exercise.

We highly recommend doing Parts 1-3 alongside a partner or group! It will be more fun, and talking through the process and problem with others will help solidify learning.

Using Git is inherently a collaborative endeavor, and this is a great opportunity to practice **talking out loud** about Git. It's better to practice talking about Git out loud now, in anticipation of resolving Git problems with team members later!

## Preparation

Let's start by cloning [the `ada-tax-prep` repo](https://github.com/AdaGold/ada-tax-prep) onto our own local machine to use for Parts 1-3.

## Part 1: Merge a Feature Branch into a Main Branch

The goal of this part is to perform one successful merge between two branches. We will also model the workflow of creating a feature branch, finishing it, and merging it back to a shared `main` branch.

### Build Up the `main` Branch

After cloning this project and `cd`ing into it, we should check that we're on the default `main` branch using `$ git status` or `$ git branch`.

Then we perform our usual steps of creating a virtual environment, activating it, and installing the project requirements.

```bash
$ python3 -m venv venv
$ source venv/bin/activate
$ pip3 install -r requirements.txt
```

Now, let's add a commit to this `main` branch! 

Open the `ada_tax_prep/income_tax.py` file, which contains logic about calculating a graduated income tax. Locate the `TAX_BRACKETS_2020` constant, and replace it with the following data.

```python
TAX_BRACKETS_2020 = (
    { "max": 9875, "rate": 10 },
    { "max": 40125, "rate": 12 },
    { "max": 85525, "rate": 22 },
    { "max": 163300, "rate": 24 },
    { "max": 207350, "rate": 32 },
    { "max": 518400, "rate": 35 },
    { "rate": 37 }
)
```

Run the tests and confirm that they pass, then make a commit with the commit message, `"configures 2020 tax brackets"`.

### Create a Feature Branch

We've received a new project requirement that we must build a feature that calculates income deductions.

- [ ] Let's create a feature branch for this new feature named `income-deductions`.

- [ ] Now, let's switch to that branch using `$ git switch`.

- [ ] Confirm that the current branch has changed with `$ git status` or `$ git branch`.

- [ ] Confirm that the commit history for this current branch includes all commits that are currently also on `main`, including the recent commit.

- [ ] Implement the income deductions feature by adding the following code to the end of `income_tax.py`, after the definition of the `calculate_tax_2020` function.

```python
DEDUCTION_CATEGORIES = (
    "charity",
    "mortgage",
    "child",
    "tuition",
    "healthcare"
)

STANDARD_DEDUCTION_2020 = 10000

def calculate_deducted_income(income, deductions, standard_deduction):
    summed_deductions = sum((
        deductions.get(category, 0)
        for category in DEDUCTION_CATEGORIES
    ))

    total_deductions = (
        standard_deduction
            if standard_deduction > summed_deductions
            else summed_deductions
    )

    adjusted_income = income - total_deductions

    return adjusted_income if adjusted_income > 0 else 0

def calculate_deducted_income_2020(income, deductions):
    return calculate_deducted_income(income, deductions, STANDARD_DEDUCTION_2020)
```

- [ ] Add the following tests to the end of `tests/test_tax_prep.py`, after the test `test_big_bracket_last`.

```python
@pytest.fixture
def all_valid_deductions():
    return {
        "charity": 5000,
        "mortgage": 5000,
        "child": 5000,
        "tuition": 5000,
        "healthcare": 5000
    }    

@pytest.fixture
def some_invalid_deductions():
    return {
        "charity": 5000,
        "mortgage": 5000,
        "child": 5000,
        "invalid": 5000,
        "not_allowed": 5000
    }    

@pytest.fixture
def few_valid_deductions():
    return {
        "charity": 5000,
        "mortgage": 5000,
        "child": 5000
    }    

def test_deducted_income_cannot_fall_below_zero():
    income = 10000

    deducted_income = calculate_deducted_income_2020(income, {})

    assert deducted_income == 0

def test_applies_standard_deduction():
    income = 50000

    deducted_income = calculate_deducted_income_2020(income, {})

    assert deducted_income == 40000

def test_applies_itemized_deductions(all_valid_deductions):
    income = 50000

    deducted_income = calculate_deducted_income_2020(income, all_valid_deductions)

    assert deducted_income == 25000

def test_ignores_invalid_itemized_deductions(some_invalid_deductions):
    income = 50000

    deducted_income = calculate_deducted_income_2020(income, some_invalid_deductions)

    assert deducted_income == 35000
```

- [ ] Modify the `import` statements at the top of `test_tax_prep.py` as follows.

```python
import pytest
from ada_tax_prep.income_tax import (
    calculate_tax_2020, calculate_deducted_income_2020
)
```

- [ ] Run the tests of this project using `$ pytest`, and confirm that our tests are running and passing.

- [ ] Finally, we'll make a commit that records this work on the feature branch. This commit should have the commit message,  `"implements deduction calculation"`.

### Merge the Feature Branch Into `main`

Eventually, we need the commit history of the feature branch to be merged _into_ `main`. This will allow any developer who looks at the latest `main` branch to see the feature. Let's merge our branch now!

- [ ] Switch to the `main` branch using `$ git switch` or `$ git checkout`.

- [ ] Confirm that we are currently on the `main` branch with `$ git status` or `$ git branch`.

- [ ] Confirm that the `main` branch does _not_ have the commits on the feature branch using `$ git log`.

- [ ] Merge the feature branch into the current branch using `$ git merge income-deductions`.

- [ ] Read through the Git output and notice that some code was added.

- [ ] Confirm that the commit history of `main` has changed, and now includes the feature branch commit, with `$ git log`.

### Test `main`

Now that our `main` branch has new code, we should do the work of manually checking that `main` is running and working as intended.

- [ ] Run the tests of this project using `$ pytest`.

- [ ] Confirm that our new tests are included and passing.

## Part 2: Merging Multiple Times

We've received another new project requirement! We need to add functionality to calculate the refund or payment of a tax payer.  We'll need a type that represents a tax payer, and a function to calculate a tax payer's tax liability. Using the payer's liability and withholdings, we can determine the size of their refund.

 Let's start by working on the function that calculates an individual's tax liability: the taxes owed based on their income, less their deductions.

### Create a Feature Branch

We're eager to get started, so let's make our feature branch right now!

- [ ] Make a new feature branch named `tax-refund` from `main`.

- [ ] Switch to the `tax-refund` branch and confirm that we're now on the `tax-refund` branch.

- [ ] Add the following code to the end of `income_tax.py`.

```python
def calculate_tax_liability(income, deductions, standard_deduction, brackets):
    deducted_income = calculate_deducted_income(income, deductions, standard_deduction)
    return calculate_tax_by_bracket(deducted_income, brackets)

def calculate_tax_liability_2020(income, deductions):
    return calculate_tax_liability(income, deductions, STANDARD_DEDUCTION_2020, TAX_BRACKETS_2020)
```

- [ ] Add the following code to the end of `test_tax_prep.py`.

```python
def test_calculate_adjusted_income_tax_burden(all_valid_deductions):
    income = 50000

    adjusted_income_tax = calculate_tax_liability_2020(income, all_valid_deductions)

    assert adjusted_income_tax == 988 + 1815
```

- [ ] Modify the `import` statements at the top of `test_tax_prep.py` as follows.

```python
import pytest
from ada_tax_prep.income_tax import (
    calculate_tax_2020, calculate_deducted_income_2020, calculate_tax_liability_2020
)
```

- [ ] Run the tests of this project using `$ pytest`.

- [ ] Commit this change to the (current) `tax-refund` branch with the message `"implements tax liability calculation"`.

### Bait and Switch (Back to `main`)

An urgent change request has suddenly arrived from our manager! Our income deduction feature is using the wrong standard deduction! We need to fix this in the `main` branch directly.

- [ ] Switch to the `main` branch and confirm that we're back on the `main` branch.

### Fix `main`

Let's fix the issue!

- [ ] In `income_tax.py`, let's change the value of `STANDARD_DEDUCTION_2020` to `12400`. (Use your ⌘F searching skills!)

- [ ] In `test_tax_prep.py`, update the `test_applies_standard_deduction` test as follows.

```python
def test_applies_standard_deduction():
    income = 50000

    deducted_income = calculate_deducted_income_2020(income, {})

    assert deducted_income == 37600
```

- [ ] Run the tests of this project using `$ pytest`.

- [ ] Commit this change to the (current) `main` branch with the message `"HOTFIX: updates standard deduction"`.

We've resolved our urgent issue on `main`!

### Merge `main` Into the Feature Branch

We fixed `main`, but we're not done with our feature yet. Before we resume work on our feature, we should make sure that we have the same hotfix in our feature branch.

We could duplicate this work, and recreate the code we need. Alternatively, we could merge `main` into our feature branch.

We will prefer frequently merging `main` into our feature branches so that they stay as close to the state of `main` as possible. This will help us minimize the chances of large merge conflicts.

- [ ] Switch to the `tax-refund` branch and confirm that we're now back on the `tax-refund` branch.

- [ ] Check our current feature branch's Git log and confirm that we do _not_ have `main`'s commits merged into this branch.

- [ ] Merge `main` into the current branch with `$ git merge main`. If we are prompted to accept a default commit message, we should accept it. This is usually accomplished by closing the editor that displays the suggested message.

- [ ] Check our current branch's Git log now, and confirm that we now **do** have `main`'s commits merged in.

### Build Up the Feature Branch More

Let's continue development of our feature branch!

We had just finished the tax liability calculation, so next is our type to hold all the tax records for a single tax payer, and the functions to calculate their refund!

- [ ] Add the following code to the end of `income_tax.py`.

```python
class TaxPayer:
    def __init__(self, withholdings, income, deductions):
        self.withholdings = withholdings
        self.income = income
        self.deductions = deductions

    def calculate_return(self, standard_deduction, brackets):
        deducted_income = calculate_deducted_income(
            self.income,
            self.deductions,
            standard_deduction
        )

        tax_liability = calculate_tax_by_bracket(deducted_income, brackets)

        return self.withholdings - tax_liability

    def calculate_return_2020(self):
        deducted_income = calculate_deducted_income(
            self.income,
            self.deductions,
            STANDARD_DEDUCTION_2020
        )

        tax_liability = calculate_tax_by_bracket(deducted_income, TAX_BRACKETS_2020)

        return self.withholdings - tax_liability
```

- [ ] Add the following code to the end of `test_tax_prep.py`.

```python
def test_taxpayer_receiving_a_return_gets_a_return(all_valid_deductions):
    taxpayer = TaxPayer(withholdings=3000, income=50000, deductions=all_valid_deductions)

    refund = taxpayer.calculate_return_2020()

    assert refund == 197

def test_taxpayer_owing_tax_has_negative_return(few_valid_deductions):
    taxpayer = TaxPayer(withholdings=3000, income=50000, deductions=few_valid_deductions)

    refund = taxpayer.calculate_return_2020()

    assert refund == -1003
```

- [ ] Modify the `import` statements at the top of `test_tax_prep.py` as follows.

```python
import pytest
from ada_tax_prep.income_tax import (
    calculate_tax_2020, calculate_deducted_income_2020, calculate_tax_liability_2020,
    TaxPayer
)
```

- [ ] Run the tests of this project using `$ pytest`.

- [ ] Commit this change to the (current) `tax-refund` branch with the message `"implements refund calculation for TaxPayer"`.

Our feature is now complete!

### Merge the Feature Branch into `main`

As usual, once we finish a feature branch, we'll want to merge it back into `main`.

- [ ] Switch back to the `main` branch.

- [ ] Merge `tax-refund` into `main` with `$ git merge tax-refund`.

- [ ] Run the tests of this project using `$ pytest`.

## Part 3: Merging Overlapping Changes

We'll finish off our feature work with a few small changes to intentionally force us to resolve a merge conflict.

### Create a Feature Branch

- [ ] Create a feature branch named `new-deductions`.

It's important that we do this before the following work in `main` to achieve the simulated merge conflict. We should _not_ switch into this new branch yet.

### Add Madeline's Work to `main`

For this step, let's pretend that we're a separate developer named Madeline.

Madeline is going to push a commit onto the `main` branch.

- [ ] Make sure we are on the `main` branch, or switch back if we need to

- [ ] In `income_tax.py`, update `DEDUCTION_CATEGORIES` as follows.

```python
DEDUCTION_CATEGORIES = (
    "charity",
    "mortgage",
    "child",
    "tuition",
    "healthcare",
    "home office"
)
```

- [ ] In `test_tax_prep.py`, add the following new fixture after the existing `few_valid_deductions` fixture.

```python
@pytest.fixture
def new_valid_deductions():
    return {
        "charity": 5000,
        "mortgage": 5000,
        "child": 5000,
        "tuition": 5000,
        "healthcare": 5000,
        "home office": 5000
    }
```

- [ ] Also in `test_tax_prep.py`, add the following new test after the existing `test_ignores_invalid_itemized_deductions` test.

```python
def test_applies_new_itemized_deductions(new_valid_deductions):
    income = 50000

    deducted_income = calculate_deducted_income_2020(income, new_valid_deductions)

    assert deducted_income == 20000
```

- [ ] Run the tests of this project using `$ pytest`.

- [ ] Make a commit for this work with the message, `"I'm Madeline and I'm adding the home office deduction"`.

### Switch to the Feature Branch

Let's return to being ourselves. We remember that we were in the middle of development on a feature branch!

- [ ] Switch to the `new-deductions` branch

### Build Up the Feature Branch With Overlap

We need to add our own new deduction category. To do so, we'll take the following steps.

- [ ] In `income_tax.py`, update `DEDUCTION_CATEGORIES` as follows.

```python
DEDUCTION_CATEGORIES = (
    "charity",
    "mortgage",
    "child",
    "tuition",
    "healthcare",
    "sales tax"
)
```

- [ ] In `test_tax_prep.py`, add the following new fixture after the existing `few_valid_deductions` fixture.

```python
@pytest.fixture
def new_valid_deductions():
    return {
        "charity": 5000,
        "mortgage": 5000,
        "child": 5000,
        "tuition": 5000,
        "healthcare": 5000,
        "sales tax": 5000
    }
```

- [ ] Also in `test_tax_prep.py`, add the following new test after the existing `test_ignores_invalid_itemized_deductions` test.

```python
def test_applies_new_itemized_deductions(new_valid_deductions):
    income = 50000

    deducted_income = calculate_deducted_income_2020(income, new_valid_deductions)

    assert deducted_income == 20000
```

- [ ] Run the tests.

- [ ] Make a commit with the message, `"adds sales tax deduction"`.

### Merge `main` Into the Feature Branch

We want Madeline's work on `main` in our current feature branch.

- [ ] Begin to merge with `$ git merge main`

### Resolve Conflicts

- [ ] Notice the output that Git prints to the terminal. Confirm that it says that a merge conflict came up during the process of merging.

- [ ] Run `$ git status` in order to see the message once again.

- [ ] Notice that Git suggests resolving the conflict by adding resolved files to staging.

- [ ] Notice that Git suggests actions to do with the merge, such as running `git merge --continue` or `git merge --abort`.

- [ ] Open the project in VS Code or a similar text editor.

- [ ] Find the location of a conflicting area of code.

Notice that conflicts are marked by _actual changes_ in our code! One of the conflicts should look something like:

```
    "healthcare",
<<<<<<< HEAD
    "sales tax"
=======
    "home office"
>>>>>>> main
)
```

Some editors, like VSCode, will display lines like this with special highlighting, and may even display actions we can take to resolve the conflict.

A simple resolution is to simply accept both changes, either by using a feature in our editor to do so, or by deleting the three special conflict lines that we see in the excerpt above.

In this instance, it turns out this is _not_ enough to resolve this conflict, since these terms appear in a list of items (actually a tuple), and so at minimum, a comma is needed. 

- [ ] In `income_tax.py`, remove the conflict lines, and then update `DEDUCTION_CATEGORIES` as follows.

```python
DEDUCTION_CATEGORIES = (
    "charity",
    "mortgage",
    "child",
    "tuition",
    "healthcare",
    "home office",
    "sales tax"
)
```

There can be multiple merge conflicts, so we need to be sure to find and resolve them all. The next is in `test_tax_prep.py`.

- [ ] In `test_tax_prep.py`, locate the conflict in the `new_valid_deductions` fixture. Accept both changes, and then update the fixture as follows.

```python
@pytest.fixture
def new_valid_deductions():
    return {
        "charity": 5000,
        "mortgage": 5000,
        "child": 5000,
        "tuition": 5000,
        "healthcare": 5000,
        "home office": 5000,
        "sales tax": 5000
    }
```

### !callout-info

## Deciding How to Resolve Conflicts

How did we decide what the code should look like at this point? We needed to use context clues and the situation at hand to decide what lines of code to keep, remove, or modify.

<br />

We can also talk to the other developer with whose code we are conflicting to try to work out the best course of action. Collaboration often will give us the best result!

### !end-callout

At this point, we have resolved all the conflicts. Before we complete the merging process in Git, we should run the tests to be sure our changes still allow the tests to pass. We can still run commands like `pytest` in our terminal, even if we're in the middle of merging in Git!

- [ ] Run the tests.

Notice that `test_applies_new_itemized_deductions` is failing.

```
>       assert deducted_income == 20000
E       assert 15000 == 20000
```

This is the test that was added in each of the branches. It was identical in both branches, so it was not flagged as a conflict. Its assert expected only a single new category, so the result is off by 5000.

- [ ] In `test_tax_prep.py`, update the `test_applies_new_itemized_deductions` test implementation as follows.

```python
def test_applies_new_itemized_deductions(new_valid_deductions):
    income = 50000

    deducted_income = calculate_deducted_income_2020(income, new_valid_deductions)

    assert deducted_income == 15000
```

- [ ] Run the tests again and confirm they pass.

### Complete the Merge

- [ ] Return to the terminal and run `$ git status` again.

- [ ] Add the resolved files to staging.

- [ ] Make a commit **with no commit message** using `$ git commit`.

- [ ] Accept the default commit message for this merge commit.

- [ ] Run `$ git status` to confirm that the merge has concluded.

- [ ] Run `$ git log` to check the current Git history. Check that Madeline's commits, our commits, and the merge commit are all present.

### Merge the Feature Branch into `main`

Once more, we have finished a feature branch, so we should merge it back into `main`.

- [ ] Switch back to the `main` branch.

- [ ] Merge `new-deductions` into `main` with `$ git merge new-deductions`.

- [ ] Run the tests.

### !callout-success

## Congratulations!

We just completed Parts 1-3 of this problem set!

### !end-callout

## Part 4

Work through the following sections of [https://learngitbranching.js.org/](https://learngitbranching.js.org/):

- Introduction Sequence
  - Lessons 1, 2, and 3
- Ramping Up
  - All lessons
