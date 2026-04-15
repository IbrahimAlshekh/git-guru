# Task 08: Stashing Work

## The Scenario

You're halfway through writing an onboarding guide when an urgent message comes in: "There's a typo on the main page, can you fix it right now?" You can't switch branches with uncommitted work (well, sometimes you can, but it's messy). You don't want to commit half-finished work either.

Solution: **stash** it.

---

## What to Do

### Step 1, Start Work on a Branch

```bash
git switch main
git switch -c onboarding-guide
```

Create `ONBOARDING.md`:

```
# Onboarding Guide

Welcome to the team! This guide helps you get set up in your first week.

## Day 1

- Get access to the code repository
- Set up your local development environment
- Read the Code of Conduct and Coding Standards
- Meet your onboarding buddy
```

Don't commit. This is intentionally in-progress.

Check:

```bash
git status
```

You see `ONBOARDING.md` as untracked.

### Step 2, Stage It (But Don't Commit)

```bash
git add ONBOARDING.md
git status
```

It's staged, but halfway done. Now you need to switch to `main` for that urgent fix.

### Step 3, Stash

```bash
git stash
```

Check:

```bash
git status
ls
```

Clean. `ONBOARDING.md` is gone, it's on the stash. Now you can safely switch branches.

### Step 4, Do the Urgent Fix

```bash
git switch main
```

Open `README.md`. Find the maintainer line at the bottom and fix a "typo", change the date to today's actual date, or change "Last Updated" to "Last Reviewed."

```bash
git add README.md
git commit -m "Fix maintainer info on README"
```

### Step 5, Go Back and Restore Your Work

```bash
git switch onboarding-guide
git stash pop
```

Check:

```bash
git status
cat ONBOARDING.md
```

Your half-written onboarding guide is back, exactly as you left it.

> 📖 **Stop and read** [THEORY.md](THEORY.md) **, Section 1: The Stash**

### Step 6, Finish and Commit

Add more content to `ONBOARDING.md`:

```

## Day 2-3

- Complete the first tutorial project
- Shadow a team member on a code review
- Submit your first small pull request (even a typo fix counts)

## Day 4-5

- Pick up your first real task from the backlog
- Pair program with a senior developer
- Write a short "what I learned this week" note for the team
```

Commit:

```bash
git add ONBOARDING.md
git commit -m "Add onboarding guide"
```

### Step 7, Merge Back to Main

```bash
git switch main
git merge onboarding-guide
git branch -d onboarding-guide
```

Update `README.md`, add to the "What's Inside" section:

```
- [Onboarding Guide](ONBOARDING.md), First week setup for new team members
```

```bash
git add README.md
git commit -m "Add onboarding guide link to table of contents"
```

---

## Verify

```bash
# Should show clean working directory
git status

# ONBOARDING.md exists
cat ONBOARDING.md

# Stash should be empty
git stash list
# Should return nothing

# Full history
git log --oneline --graph -10
```

---

## What You Just Learned

- `git stash` saves uncommitted work and cleans your working directory
- `git stash pop` restores the most recent stash
- `git stash list` shows all stashes
- Stash is perfect for "save my spot" moments, quick interruptions, branch switches
- It's a temporary shelf, not a long-term storage system

---

**Congratulations, you've completed Tier 1!** You can now work solo with Git confidently.

→ Next: [Task 09: Working with Remotes](../09-working-with-remotes/TASK.md) (Tier 2: Collaboration)
