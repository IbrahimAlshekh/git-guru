# Theory: Task 05

Read each section only when the task tells you to.

---

## Section 1: Fast-Forward vs Three-Way Merge

There are two types of merges, and Git picks automatically based on the graph shape.

### Fast-Forward

```
Before:
A ← B ← C  (main)
           ↖
             D ← E  (feature)

After merge:
A ← B ← C ← D ← E  (main, feature)
```

No divergence. `main` never got new commits while `feature` was being developed. Git just moves the `main` pointer forward to where `feature` is. No merge commit needed, the history stays linear.

### Three-Way Merge

```
Before:
A ← B ← C ← F  (main)
           ↖
             D ← E  (feature)

After merge:
A ← B ← C ← F ← M  (main)
           ↖     ↗
             D ← E  (feature)
```

Both branches have commits the other doesn't. Git looks at three things: the common ancestor (C), the tip of main (F), and the tip of feature (E). It combines the changes from both sides into a new **merge commit** (M) that has *two parents*.

The merge commit is special, it's the only type of commit with more than one parent. It represents the moment two lines of work came together.

### Which Is Better?

Neither. Fast-forwards make linear history, which is simpler to read. Three-way merges preserve the fact that work happened in parallel, which can be informative. Teams choose their preference, some use `git merge --no-ff` to *always* create merge commits even when fast-forward is possible, because they want the branch history visible.
