# Task 05: Merging

## The Scenario

Your coding standards are ready. Time to bring that work into `main` so the whole team has access. This is a **merge** , combining two branches.

---

## What to Do

### Step 1 , Prepare for a Fast-Forward Merge

First, make sure your coding standards branch is complete:

```bash
git switch coding-standards
git log --oneline
```

Now switch to `main` , the branch you want to merge *into*:

```bash
git switch main
```

Before merging, visualize the graph:

```bash
git log --oneline --graph --all
```

Notice that `main` hasn't moved since you created the branch. This means Git can do a **fast-forward merge** , it just moves the `main` pointer forward.

### Step 2 , Merge

```bash
git merge coding-standards
```

Read the output. It should say "Fast-forward." Now check:

```bash
git log --oneline --graph --all
```

Both branch pointers now point to the same commit. The graph is a straight line again.

> 📖 **Stop and read** [THEORY.md](THEORY.md) **, Section 1: Fast-Forward vs Three-Way Merge**

### Step 3 , Update the README

Now add the coding standards link to `README.md`'s "What's Inside" section:

```
- [Coding Standards](CODING_STANDARDS.md) , Code style and best practices
```

Commit:

```bash
git add README.md
git commit -m "Add coding standards link to table of contents"
```

### Step 4 , Set Up a Three-Way Merge

Let's create a situation where a fast-forward isn't possible.

Create a new branch and add content:

```bash
git switch -c testing-guidelines
```

(`git switch -c` creates *and* switches in one step)

Create `TESTING.md`:

```
# Testing Guidelines

## Philosophy

Every feature should have tests. Tests are not a burden , they are documentation that verifies itself.

## What to Test

- **Happy path** , Does the feature work when used correctly?
- **Edge cases** , What happens with empty input, huge numbers, special characters?
- **Error cases** , Does it fail gracefully?

## Test Naming

Name tests as sentences that describe behavior:
- `it should return the user when given a valid ID`
- `it should throw an error when the ID does not exist`

Do NOT name tests after the function they test:
- Bad: `testGetUser`
- Good: `it should return null for a deleted user`
```

Commit:

```bash
git add TESTING.md
git commit -m "Add testing guidelines"
```

### Step 5 , Make a Competing Commit on Main

Switch back to `main` and make a *different* change:

```bash
git switch main
```

Open `README.md` and add below the last item in "What's Inside":

```
- [Testing Guidelines](TESTING.md) , How we write and organize tests
```

Commit:

```bash
git add README.md
git commit -m "Add testing guidelines placeholder to table of contents"
```

### Step 6 , Look at the Graph

```bash
git log --oneline --graph --all
```

Now you can see the fork: `main` and `testing-guidelines` have diverged. Neither is ahead of the other , they both have commits the other doesn't.

### Step 7 , Three-Way Merge

```bash
git merge testing-guidelines
```

Git will open your editor with a merge commit message. Accept the default (or write your own) and save.

This time the output says "Merge made by the 'ort' strategy" (or "recursive" in older Git). That's a three-way merge , Git combined two divergent histories.

```bash
git log --oneline --graph --all
```

You can see the merge commit , it has *two parents*, creating a diamond shape in the graph.

---

## Verify

```bash
# Should show the merge commit at the top
git log --oneline -1

# Should show the diamond/fork in the graph
git log --oneline --graph --all

# TESTING.md should exist
cat TESTING.md

# README should have the testing link
grep "Testing" README.md
```

---

## What You Just Learned

- `git merge <branch>` combines another branch into your current branch
- **Fast-forward:** when main hasn't moved, Git just slides the pointer forward , no merge commit
- **Three-way merge:** when both branches have new commits, Git creates a merge commit that has two parents
- Always switch to the *receiving* branch first (`git switch main`), then merge the other one in

---

→ Next: [Task 06: Merge Conflicts](../06-merge-conflicts/TASK.md)
