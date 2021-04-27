# Branches

## Goals

The goal of this lesson is to introduce the definition and overall concept to Git branches.

## Vocabulary and Synonyms

| Vocab  | Definition                                                                          | Synonyms | How to Use in a Sentence                                                                                                                                                                                                                                                                   |
| ------ | ----------------------------------------------------------------------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Branch | A feature in Git that captures a snapshot of code changes as one Git commit history | -        | "We worked on the `mark_complete` feature in a new branch `mark_complete`. We finished the `mark_complete` feature and pushed three commits to the branch. During this time, no other branch saw the commits for `mark_complete`. Then, we merged the `mark_complete` branch into `main`." |

## Commits Are on Branches

As we use Git, we know we are creating a Git commit history by building commits.

Each commit has:

- A diff of changes
- A commit message
- A commit hash (to identify it)
- A sense of the commit that comes before it (its parent commit(s))

Commits are also on _branches_. **Git branches** are like named commit histories. A Git branch keeps track of a commit history. Add a new commit extends that branch by another commit.

All of our Git work so far has been on a branch.

There is always at least one default branch in every Git project. The default name for the default branch is `main`; all of our commits we've made so far have been on the `main` branch.

### !callout-info

## Default Name Before `main`

[Before the default branch was named `main`, it was named `master`](https://github.com/github/renaming). This is useful to know because:

- It shows the current conversation around shared language and culture in the tech community
- Many tutorials will refer to the `master` branch

<br/>

We can assume that for any modern software, renaming the branch `master` to `main` will operate identically.

### !end-callout

## Branches Shares a Commit History Until Branching

Each branch has a name and a commit history.

The naming conventions of Git branches depends on the use, context, and team. Some example branch names include:

- `main`
- `click-button-feature`
- `ada/click-button-feature`
- `broken_payment_hot_fix`
- `payment-logic-refactor`
- `payment-logic_patch`
- `development`
- `staging`
- `production`
- `release-0875`

Branches are created **from** another branch's commit. Therefore, a new branch and an old branch share the exact same commit history until the point that the branch is created and branches off.

For example, we can have a `main` branch with the following Git log (and these commit hashes):

```
1d1kl "Refactors payment endpoint to use make_payment helper"
034g3 "Adds payment endpoint to create payments"
```

We can create a `click-button-feature` branch while on the `main` branch. When that happens, the `click-button-feature` will have the following Git log:

```
1d1kl "Refactors payment endpoint to use make_payment helper"
034g3 "Adds payment endpoint to create payments"
```

The `click-button-feature` starts with the same Git history as the `main` branch at the time of creation.

## Adding Commits to One Branch Doesn't Affect the Others

When we add commits to one branch, the commit isn't included in the Git histories of other branches.

We can add a commit to the `main` branch and change its commit history:

```
2pgs7 "Adjusts payment logic for calculating shipping cost"
1d1kl "Refactors payment endpoint to use make_payment helper"
034g3 "Adds payment endpoint to create payments"
```

And, assuming the `click-button-feature` branch was created earlier, the Git history for `click-button-feature` remains:

```
1d1kl "Refactors payment endpoint to use make_payment helper"
034g3 "Adds payment endpoint to create payments"
```

Similarly, we can add a commit to the `click-button-feature` branch:

```
3gtqq "Enables button when form is complete"
1d1kl "Refactors payment endpoint to use make_payment helper"
034g3 "Adds payment endpoint to create payments"
```

And it won't affect the Git history of the `main` branch:

```
2pgs7 "Adjusts payment logic for calculating shipping cost"
1d1kl "Refactors payment endpoint to use make_payment helper"
034g3 "Adds payment endpoint to create payments"
```

## Merging Branches is Merging Commit Histories

We can combine the work represented on two different branches by _merging_ them.

**Merging branches** results in two branches combining their Git histories. More specifically, merging `branch-a` **_into_** `branch-b` means merging the commit history of `branch-a` **_into_** the commit history of `branch-b`.

The actual act of merging `branch-a` into `branch-b` takes this process:

- Rewinding the histories of `branch-a` and `branch-b` to their common commit
- Looking through the commits of `branch-a` and `branch-b` and applying the diffs one at a time until all of commits are applied

This process may re-order some commits out of necessity. Git ultimately applies one of several algorithms to determine the order of applied commits.

The ultimate result is that `branch-b` has one unified Git history that we can follow!

For our above example, we can merge `main` into `click-button-feature`. Then, the history of `click-button-feature` may look like:

```
3gtqq "Enables button when form is complete"
2pgs7 "Adjusts payment logic for calculating shipping cost"
1d1kl "Refactors payment endpoint to use make_payment helper"
034g3 "Adds payment endpoint to create payments"
```

This merge doesn't effect the Git history of the `main` branch:

```
2pgs7 "Adjusts payment logic for calculating shipping cost"
1d1kl "Refactors payment endpoint to use make_payment helper"
034g3 "Adds payment endpoint to create payments"
```

## Branches Have Various Use Cases

Git branches are merely a tool, and how they're used depends on the context and practices of the project at hand and the team working on it.

However, some common patterns for using branches are:

1. Feature branches
1. Experimental proof-of-concept branches

### Feature Branches

A feature branch strategy to software development usually means:

- Designating one branch to represent the ultimate branch of "working" software, usually the `main` branch
- Agreeing that all active development and work-in-progress happens on branches other than `main`
- Each branch is dedicated to making commits solely for one feature at a time

Feature branches can be responsible for:

- Building a new feature and the tests for the new feature
- Modifying an existing feature and updating the tests for this feature
- Bug fixes
- Making small, isolated changes, such as fixing typos

In this strategy, each feature in development will get its own branch. When the feature development is complete, the developer will merge the feature branch _into_ `main`, so that `main` gets the unified, merged commit history.

Then, the feature branch will be deleted.

### Proof of Concept Branches

Branches can be used for small, temporary experiments.

Sometimes, there is a task or a piece of work that prioritizes exploration and understanding over writing clean code or using tests for a short amount of time. When we need to work on an experiment rather than on project requirements directly, we can designate a specific short amount of time exploring solutions and possibilities, and make these changes on a branch.

These experimental branches tend to have an attitude making a "proof of concept," with the intention to write potentially messy code now, and spend time writing more intentional (better, TDD, more readable, usable, flexible) code later.

Sometimes it's necessary to work on an experiment for a brief amount of time. However, when you begin on this endeavor, keep the following things in mind:

- Determine what the goal of the exploration at the beginning
- Create a time limit of less than one day
- Decide to delete the branch at the end of the experiment, and create a separate new branch with clean commits after the research is over
