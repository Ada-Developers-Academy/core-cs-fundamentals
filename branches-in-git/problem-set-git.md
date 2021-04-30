# Problem Set: Git

## Directions

Follow the directions below.

There is no submission for these exercises.

We highly recommend doing Parts 1-3 alongside a partner or group! It will be funner, and talking through the process and problem with others will help solidify learning.

Using Git is inherently a collaborative thing, and this is a great opportunity to practice **talking out loud** about Git. It's better to practice talking about Git out loud now, in anticipation of resolving Git problems with team members later!

## Preparation

Clone this repo onto your own local machine to use during Parts 1-3.

## Part 1: Merge a Feature Branch into a Main Branch

The goal of this part is to witness one successful merge between two branches. It should also mimic the workflow of creating a feature branch, finishing it, and merging it back to a shared `main` branch.

### Build Up the `main` Branch

After cloning this project and `cd`ing into it, we should check that we're on the default `main` branch using `$ git status` or `$ git branch`.

Now, let's add a commit to this `main` branch! Implement and then make a commit with the commit message, "TODO"

### Create a Feature Branch

We've received the new project requirement that we must build a feature that TODO.

- [ ] Let's create a feature branch for this new feature named `TODO`.

- [ ] Now, let's switch to that branch using `$ git switch`.

- [ ] Confirm that the current branch has changed with `$ git status` or `$ git branch`.

- [ ] Confirm that the commit history for this current branch includes all commits that are currently also on `main`, including the recent commit.

- [ ] Implement the TODO feature by adding this code:

TODO

- [ ] Run the tests of this project using `$ python3 -m pytest `. Then, confirm that our tests are running and passing.

- [ ] Finally, make a commit that contains this work on the feature branch. This commit should have the commit message, "TODO"

### Merge the Feature Branch Into `main`

We want the commit history of the feature branch to be merged _into_ `main`. This way, every developer who looks at the latest `main` branch will also see the feature.

- [ ] Switch to the `main` branch using `$ git switch` or `$ git checkout`.

- [ ] Confirm that you are currently on the `main` branch with `$ git status` or `$ git branch`.

- [ ] Confirm that the `main` branch does _not_ have the commits on the feature branch using `$ git log`.

- [ ] Merge the feature branch into the current branch using `$ git merge `.

- [ ] Read through the Git output and notice that some code was added.

- [ ] Confirm that the commit history of `main` has changed, and now includes the feature branch commit, with `$ git log`.

### Test `main`

Now that our `main` branch has new code, we should do the work of manually checking that `main` is running and working as intended.

- [ ] Run the tests of this project using `$ python3 -m pytest `.

- [ ] Confirm that our new tests are included and passing.

## Part 2: Merging Multiple Times

We've received another new project requirement! We need to build TODO.

### Create a Feature Branch

We're ambitious and speedy, and we want to make our feature branch right now.

- [ ] Make a new feature branch named `TODO` from `main`.

### Switch to `main`

Our manager contacted us and needs us to change some code urgently. Our TODO feature needs to handle TODO, and we're asked to change the `main` branch directly.

- [ ] Switch to the `main` branch and confirm that you're on the `main` branch.

### Build Up `main`

Let's create that change!

- [ ] Adjust TODO to add this test and this implementation code:

TODO

- [ ] Commit this change to the (current) `main` branch.

We've accomplished our urgent issue on `main`!

### Switch to the Feature Branch

Now, let's return to our feature branch, TODO.

- [ ] Switch to our feature branch and confirm that you're on this branch.

### Build Up the Feature Branch

Let's focus on building this TODO feature now.

- [ ] Adjust TODO to add this test and this implementation code:

TODO

- [ ] Commit this change to the (current) TODO branch.

### Merge `main` Into the Feature Branch

During our development, we'll see that our feature should ALSO handle TODO, just like what our manager asked us to commit on `main`.

We could duplicate this work, and recreate the code we need. Alternatively, we could also merge `main` into our feature branch.

- [ ] Check our current feature branch's Git log and confirm that we do _not_ have `main`'s commits merged into this branch.

- [ ] Merge `main` into the current branch with `$ git merge main`.

- [ ] Check our current branch's Git log now, and confirm that we now **do** have `main`'s commits merged in.

### Build Up the Feature Branch More

Let's continue development of our feature branch!

- [ ] Adjust TODO to add this test and this implementation code:

TODO

Our feature is now complete!

### Merge the Feature Branch into `main`

As usual, once we finish a feature branch, we'll want to merge it back into `main`.

- [ ] Switch back to the `main` branch.

- [ ] Merge TODO into `main` with `$ git merge TODO`.

## Part 3: Merging Overlapping Changes

We're assigned yet another feature to build:

TODO

For this part, we will follow some directions to force us to resolve a merge conflict.

### Create a Feature Branch

- [ ] Create a feature branch named TODO.

### Add Simon's Work to `main`

For this step, let's pretend that we're a separate developer named Simon.

Simon is going to push a commit onto the `main` branch.

- [ ] Switch to the `main` branch

- [ ] Add this content to TODO:

TODO

- [ ] Make a commit with this work with the message, "I'm Simon and I'm adding TODO"

### Switch to the Feature Branch

Return to being yourself, who was in the middle of development on a feature branch!

- [ ] Switch to the TODO branch

### Build Up the Feature Branch With Overlap

- [ ] Add this content to TODO:

TODO

- [ ] Make a commit with the message, "TODO."

### Merge `main` Into the Feature Branch

We want Simon's work on `main` in our current feature branch.

- [ ] Begin to merge with `$ git merge main`

### Resolve Conflicts

- [ ] Notice the output that Git prints to the terminal. Confirm that it says that a merge conflict came up during the process of merging.

- [ ] Run `$ git status` in order to see the message once again.

- [ ] Notice that Git suggests resolving the conflict by adding resolved files to staging.

- [ ] Notice that Git suggests actions to do with the merge, such as running `git merge --continue` or `git merge --abort`.

- [ ] Open the project in VS Code or a similar text editor.

- [ ] Find the location of the conflicting code. Change the lines of code to this compromise of code:

TODO

### !callout-info

## Deciding How to Resolve Conflicts

How did we decide what the code should look like at this point? We needed to use context clues and the situation at hand to decide what lines of code to keep, remove, or modify.

### !end-callout

- [ ] Return to the terminal and run `$ git status` again.

- [ ] Add the TODO file to staging.

- [ ] Make a commit **with no commit message** using `$ git commit`.

- [ ] Accept the default commit message for this merge commit.

- [ ] Run `$ git status` to confirm that the merge has concluded.

- [ ] Run `$ git log` to check the current git history. Check that Simon's commits, your commits, and the merge commit are all present.

### !callout-success

## Congratulations!

You just completed Parts 1-3 of this problem set!

### !end-callout

## Part 4

Work through the following sections of [https://learngitbranching.js.org/](https://learngitbranching.js.org/):

- Introduction Sequence
  - All lessons
- Ramping Up
  - All lessons
- Moving Work Around
  - Lesson 1: Cherry-pick Intro
