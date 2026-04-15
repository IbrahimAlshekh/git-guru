# Theory: Task 08

---

## Section 1: The Stash

The stash is a special storage area in Git, think of it as a stack of temporary snapshots that live outside the normal commit history.

When you run `git stash`, Git:

1. Takes your staged and unstaged changes
2. Saves them in a special stash object
3. Resets your working directory to the last commit (clean state)

When you run `git stash pop`, Git:

1. Takes the most recent stash
2. Applies those changes back to your working directory
3. Removes the stash from the stack

### Multiple Stashes

You can stash more than once. Each `git stash` pushes onto the stack:

```
stash@{0} ← most recent
stash@{1}
stash@{2} ← oldest
```

Useful commands:

| Command | What It Does |
|---------|-------------|
| `git stash` | Save and clean |
| `git stash pop` | Restore most recent, remove from stack |
| `git stash apply` | Restore most recent, keep on stack |
| `git stash list` | Show all stashes |
| `git stash drop` | Delete most recent stash |
| `git stash pop stash@{2}` | Restore a specific stash |

### When NOT to Use Stash

Stash is for short interruptions, minutes to hours. If you stash something and forget about it for a week, you'll have trouble remembering what it was. For longer-term "not ready yet" work, just commit it on a branch with a message like "WIP: half-done onboarding guide." A WIP commit on a branch is better than a forgotten stash.

### Stash Can Conflict Too

If the code changed while your work was stashed, `git stash pop` might produce a conflict, just like a merge. Resolve it the same way: edit the file, remove markers, `git add`.

---

## Tier 1 Complete, What You Know Now

You've finished the solo tier. Here's what you can do:

- Initialize a repo and make commits
- See what changed with `diff` and `log`
- Branch, merge, and resolve conflicts
- Undo mistakes with amend, reset, and revert
- Stash work temporarily

This covers about 90% of daily Git usage for a solo developer. Tier 2 adds the collaboration layer, pushing, pulling, and working with others.
