# Theory: Task 04

---

## Section 1: What Is a Branch?

Here's the thing that surprises everyone: **a branch is just a 40-character text file** that contains a commit hash. That's it.

When you ran `git branch coding-standards`, Git created a tiny file at `.git/refs/heads/coding-standards` containing the hash of the current commit. You can actually see it:

```bash
cat .git/refs/heads/coding-standards
```

That's why branches are "cheap", creating one doesn't copy any files, doesn't duplicate history, doesn't take up meaningful disk space. It's one 40-byte pointer.

When you make a commit on a branch, Git moves that pointer forward to the new commit. When you switch branches, Git moves HEAD and swaps your working directory to match.

Compare this to what some people imagine: "a branch is a separate copy of the whole project." That model would make branching slow and expensive. In Git, it's instantaneous because it's just pointer manipulation.

---

## Section 2: The Graph with Branches

After your work, the graph looks like this:

```
A ← B ← C ← D ← E  (main)
                    ↖
                      F ← G  (coding-standards)
                             ↑
                            HEAD
```

Actually, since no new commits were added to `main` while you worked, it's more accurately:

```
A ← B ← C ← D ← E ← F ← G
                  ↑           ↑
                main    coding-standards
                               ↑
                              HEAD
```

`main` still points at commit E. `coding-standards` points at G. They share the history A through E. F and G are *only* on `coding-standards`.

HEAD points to `coding-standards`, which means "you are on that branch." When you switch to `main`, HEAD moves, and Git restores your working directory to what it looked like at commit E, which didn't include `CODING_STANDARDS.md`.

This is the graph in action. Once you can picture this, everything else in Git makes sense.
