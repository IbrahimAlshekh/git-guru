# Task 11: Rebasing

## The Scenario

You've been working on a documentation improvements branch for a couple of days. Meanwhile, the team merged other changes into `main`. Your branch is now "behind." Before merging your work, you want to bring it up to date, but instead of a merge commit that clutters the history, you'll use **rebase** to replay your commits on top of the latest `main`.

---

## What to Do

### Step 1, Set Up the Divergence

Make sure you're on `main` and up to date:

```bash
git switch main
git pull
```

Create a branch for documentation improvements:

```bash
git switch -c docs/improve-readme
```

Open `README.md` and add a section above the "Contributing" section:

```
## Quick Reference

| Task | Command |
|------|---------|
| See current status | `git status` |
| See what changed | `git diff` |
| Save a snapshot | `git add . && git commit -m "message"` |
| Create a branch | `git switch -c branch-name` |
| Merge a branch | `git merge branch-name` |
```

```bash
git add README.md
git commit -m "Add Git quick reference table to README"
```

Now add one more commit on this branch, update `ONBOARDING.md` to mention the quick reference:

Open `ONBOARDING.md` and add to the Day 1 list:

```
- Check the Quick Reference section in the README for common Git commands
```

```bash
git add ONBOARDING.md
git commit -m "Reference quick reference table in onboarding guide"
```

### Step 2, Simulate Changes on Main

Switch to `main` and add a commit (simulating a teammate's merged PR):

```bash
git switch main
```

Open `CHANGELOG.md` and add entries:

```
- Security guidelines
- Git workflow documentation
- Pull request process
```

```bash
git add CHANGELOG.md
git commit -m "Update changelog with recent additions"
```

### Step 3, See the Divergence

```bash
git log --oneline --graph --all
```

Both `main` and `docs/improve-readme` have commits the other doesn't. If you merged now, you'd get a merge commit. Instead, let's rebase.

### Step 4, Rebase

```bash
git switch docs/improve-readme
git rebase main
```

> 📖 **Stop and read** [THEORY.md](THEORY.md) **, Section 1: What Rebase Does**

Now check:

```bash
git log --oneline --graph --all
```

Your two commits are now sitting *on top of* the latest main commit. The history is a straight line. No merge commit.

### Step 5, Merge (Fast-Forward)

```bash
git switch main
git merge docs/improve-readme
```

Because you rebased, this is a fast-forward merge, clean and linear.

```bash
git branch -d docs/improve-readme
```

### Step 6, Push

```bash
git push
```

### Step 7, Interactive Rebase

Let's try one more thing. Create a branch and make some messy commits:

```bash
git switch -c docs/cleanup
```

Open `GIT_WORKFLOW.md` and fix something small (add a period at the end of a sentence). Commit:

```bash
git add GIT_WORKFLOW.md
git commit -m "Fix typo"
```

Open it again, fix another small thing. Commit:

```bash
git add GIT_WORKFLOW.md
git commit -m "Another typo fix"
```

Open it again, add a blank line or minor formatting. Commit:

```bash
git add GIT_WORKFLOW.md
git commit -m "Fix formatting"
```

Three trivial commits that should really be one. Fix it with interactive rebase:

```bash
git rebase -i HEAD~3
```

Your editor opens showing three commits. Change the second and third from `pick` to `squash` (or `s`):

```
pick abc1234 Fix typo
squash def5678 Another typo fix
squash ghi9012 Fix formatting
```

Save and close. A new editor opens for the combined commit message. Write:

```
Fix typos and formatting in Git workflow guide
```

Save and close. Check:

```bash
git log --oneline -3
```

Three commits became one. Clean history.

```bash
git switch main
git merge docs/cleanup
git branch -d docs/cleanup
git push
```

---

## Verify

```bash
# History should be linear, no merge diamonds for recent work
git log --oneline --graph -10

# README has the quick reference
grep "Quick Reference" README.md

# The squashed commit exists
git log --oneline | grep "Fix typos"
```

---

## What You Just Learned

- `git rebase main` replays your branch commits on top of the latest main
- Rebase produces linear history, cleaner than merge commits for small branches
- `git rebase -i HEAD~N` lets you squash, reorder, or edit recent commits
- **Golden rule:** never rebase commits that have been pushed and shared. Rebase rewrites history, if others have those commits, you'll cause conflicts.
- Rebase vs merge is a team decision, not a right/wrong question

Interactive rebase is one of the most useful tools for keeping history honest. Before opening a pull request, a quick `rebase -i` to clean up your "wip" and "fix typo" commits costs five minutes and makes your teammates' review much easier.

---

**Congratulations, you've completed Tier 2!** You can now collaborate with a team using Git.

→ Next: [Task 12: Gitflow Introduction](../12-gitflow-intro/TASK.md) (Tier 3: Gitflow)
