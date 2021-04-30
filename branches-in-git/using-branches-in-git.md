# Using Branches

<!-- ## Learning Goals -->

<!-- ## Introduction -->

## Checking Your Current Branch

Whenever we work on a Git project, we are always located inside a branch. All commits made will belong to the branch we're located in.

We can determine what branch we're located in using either:

- `git status`
- `git branch`

When we run

```bash
$ git status
```

We'll get output such as

```
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
```

This output tells us that we are on the branch named `main`.

When we run

```bash
$ git branch
```

We'll get output such as

```
  add-deployment-config
  convert-to-hooks
* main
  rename-task-model
```

In this example, there are four branches that exist: `add-deployment-config`, `convert-to-hooks`, `main`, and `rename-task-model`.

The asterisk `*` indicates the current branch; in this example, we're currently on the `main` branch.

## Creating Branches

When we create a branch, we should first and foremost be aware of our _current_ location. What branch are we currently on? What is the most recent commit?

When we create a branch, the new branch will have the same commit history as the current branch.

After we've established that we want our new branch to branch off the current branch, we can create a new branch with:

```bash
$ git branch <new-branch-name>
```

Where `<new-branch-name>` is the name of the new branch.

## Switching Branches

We can switch our current branch to a different existing branch with:

```bash
$ git switch <destination-branch-name>
```

Where `<destination-branch-name>` is the name of the destination branch.

### !callout-info

## `git switch` Replaces `git checkout`

The following command also changes our location to a different branch:

```bash
$ git checkout <destination-branch-name>
```

This command was the dominant way for switching branches for a long time, so it's important to recognize this syntax.

### !end-callout

### Sometimes Switching Is "Unsafe"

When we switch branches, Git will attempt to preserve the unstaged changes and the staged changes.

On occasion, Git will recognize that there isn't a way to keep the unstaged and staged changes intact in another branch. Git will ask us to change our situation if we still want to switch branches. We recommend any of the following:

- Create a commit with the unstaged and/or staged changes. This way, these changes will stay on the current branch before switching.
- Use Git's stash feature, which will save unstaged and staged changes in the _stash_, instead of a commit.

Both strategies are equally valid depending on the situation. For more information about Git stash, follow your curiosity!

## Deleting Branches

We can delete an existing branch with:

```bash
$ git branch -d <branch-name>
```

Where `<branch-name>` is the name of the branch to be deleted.

### !callout-info

## Prune Old, Stale Branches

Because branches are made and finished so frequently (ideally), projects will accumulate a _lot_ of branches. It's worthwhile to organize branches and delete them after they've been merged into `main`, or are no longer actively used.

### !end-callout
