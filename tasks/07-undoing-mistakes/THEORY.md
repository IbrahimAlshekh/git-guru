# Theory: Task 07

Read each section only when the task tells you to.

---

## Section 1: Amend = Rewrite

`git commit --amend` doesn't "edit" a commit. It **replaces** it with a new one. The old commit gets a different hash, which means it's a different object in Git's eyes.

This is safe when the commit is only on your local machine. But if you've already pushed it to a shared remote, amending creates a divergence, your local history and the remote history disagree. That causes problems for everyone else on the team.

Rule of thumb: **amend freely before pushing. Never after.**

---

## Section 2: Reset vs Revert

These two commands both "undo" things, but in fundamentally different ways.

### Reset, Rewrite History

`git reset` moves the branch pointer backward. It's like the commit never happened.

```
Before:  A ← B ← C ← D  (main)
                          ↑ HEAD

After git reset --hard C:
         A ← B ← C  (main)
                     ↑ HEAD

D still exists in Git's object store but no branch points to it.
```

Three flavors:
- `--soft`, moves the pointer, keeps changes staged
- `--mixed` (default), moves the pointer, keeps changes in working directory but unstaged
- `--hard`, moves the pointer, *discards all changes*. Gone.

`--hard` is destructive. Use it with intention.

### Revert, Add Corrective History

`git revert` creates a **new commit** that undoes a previous commit's changes.

```
Before:  A ← B ← C ← D  (main)

After git revert D:
         A ← B ← C ← D ← D'  (main)

D' has the opposite changes of D. The history still shows D happened.
```

This is safe for shared branches because you're not rewriting anything, you're adding to history. Everyone can pull D' and the mistake is undone.

### When to Use Which

| Situation | Tool |
|-----------|------|
| Last commit, not yet pushed | `amend` |
| Last few commits, not yet pushed | `reset` |
| Any commit that's already pushed | `revert` |
| Staged file you want to unstage | `restore --staged <file>` |
| Working directory changes to discard | `restore <file>` |
