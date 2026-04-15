# Theory: Task 11

Read each section only when the task tells you to.

---

## Section 1: What Rebase Does

Merge and rebase both integrate changes from one branch into another. They just do it differently.

### Merge: Combine Histories

```
Before:
A ← B ← C ← F  (main)
           ↖
             D ← E  (feature)

After merge:
A ← B ← C ← F ← M  (main)
           ↖     ↗
             D ← E
```

Creates a merge commit (M). Preserves the fact that work happened in parallel. The branch structure is visible in the graph.

### Rebase: Replay Commits

```
Before:
A ← B ← C ← F  (main)
           ↖
             D ← E  (feature)

After rebase (on feature branch):
A ← B ← C ← F  (main)
                ↖
                  D' ← E'  (feature)

After merge (fast-forward):
A ← B ← C ← F ← D' ← E'  (main, feature)
```

Rebase takes your commits (D and E), detaches them, moves the branch to the tip of main (F), and **replays** your commits one by one on top. The result is D' and E', they have the same changes as D and E, but different hashes because they have a different parent.

The history becomes linear. It looks like you wrote D and E *after* F, even though you didn't.

### Why "Replay" Matters

D' is not the same commit as D. It has a new parent, so it has a new hash. This is why the golden rule exists: if you've pushed D to a shared remote, other people might have it. If you rebase and create D', your history and theirs diverge. This causes real problems.

Rebase local, unpushed commits freely. Never rebase commits others are building on.

### When to Use Which

| Situation | Recommended |
|-----------|-------------|
| Small feature branch, 1-3 commits | Rebase onto main, then fast-forward merge |
| Long-running branch with many contributors | Merge, preserving the branch history has value |
| Cleaning up your own messy commits | Interactive rebase (`rebase -i`) |
| Shared branches (develop, main) | Never rebase, always merge |

Many teams use a hybrid: rebase your local feature branch to keep it up-to-date, then merge (with `--no-ff`) to main so the merge commit serves as a record that a feature was completed.
