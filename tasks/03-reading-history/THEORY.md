# Theory: Task 03

Read each section only when the task tells you to.

---

## Section 1: The Commit Graph

Every commit points to its parent, the commit that came before it. This creates a chain:

```
A ← B ← C ← D  (main)
                  ↑
                 HEAD
```

Right now, your history is a straight line. Commit D (your most recent) points back to C, which points to B, which points to A (your first commit). This is the **commit graph**.

Two important pointers:

**`main`** (or `master`), This is a branch. A branch is just a pointer to a commit. Right now, `main` points to your latest commit, D.

**`HEAD`**, This is "where you are right now." It usually points to a branch name (like `main`), which in turn points to a commit. When you make a new commit, the branch pointer moves forward, and HEAD follows.

```
A ← B ← C ← D
                ↑
              main
                ↑
              HEAD
```

When you make a new commit E:

```
A ← B ← C ← D ← E
                    ↑
                  main
                    ↑
                  HEAD
```

Both `main` and `HEAD` moved forward. The old commits didn't change, E simply joined the chain.

In the next task, you'll create a second branch. That's when the graph stops being a straight line, and that's when Git gets interesting.

---

## Why This Matters

Understanding the graph is the single most important thing in Git. When you hear "rebase," "merge," "cherry-pick," or "reset," every one of them is an operation on this graph. If you can picture the graph in your head, you can predict what any Git command will do.
