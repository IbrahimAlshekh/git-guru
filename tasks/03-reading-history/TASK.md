# Task 03: Reading History

## The Scenario

A new team member just joined. Before they start contributing, they want to understand what's been done so far. Your job: add a new file to the handbook, then show the new member how to read the project's history using Git.

---

## What to Do

### Step 1, Add a New File

Create a new file called `CODE_OF_CONDUCT.md` in the `handbook/` directory:

```
# Code of Conduct

## Our Pledge

We are committed to making participation in this project a respectful and harassment-free experience for everyone, regardless of experience level, background, or identity.

## Standards

Positive behaviors include:
- Using welcoming and inclusive language
- Respecting differing viewpoints and experiences
- Accepting constructive criticism gracefully
- Focusing on what's best for the team

Unacceptable behaviors include:
- Personal attacks or derogatory comments
- Publishing others' private information without permission
- Dismissing someone's contribution based on their experience level

## Enforcement

Team leads are responsible for clarifying standards and are expected to take appropriate corrective action in response to unacceptable behavior.

## Scope

This code of conduct applies to all project spaces, repository, chat, meetings, and any other team forums.
```

Stage and commit:

```
git add CODE_OF_CONDUCT.md
git commit -m "Add code of conduct"
```

### Step 2, Explore the Log

Now try each of these commands and read the output carefully:

```bash
# Full log
git log

# Compact view
git log --oneline

# Show what files changed in each commit
git log --stat

# Show the actual changes (patch) for each commit
git log -p

# Show only the last 2 commits
git log -2
```

> 📖 **Stop and read** [THEORY.md](THEORY.md) **, Section 1: The Commit Graph**

### Step 3, Inspect a Specific Commit

From `git log --oneline`, pick the hash of your second commit (the "Add communication guidelines" one). Run:

```bash
git show <paste-the-hash-here>
```

This shows you exactly what that commit did, who made it, when, and every line changed.

Now try:

```bash
# See only which files were touched
git show --stat <hash>

# See the state of README.md at that specific commit
git show <hash>:README.md
```

### Step 4, Update the README Links

Now update `README.md` to link to the new file. Add this line in the "What's Inside" section:

```
- [Code of Conduct](CODE_OF_CONDUCT.md), Team behavior standards
```

Commit this change:

```
git add README.md
git commit -m "Add code of conduct link to README table of contents"
```

### Step 5, View the Full Graph

```bash
git log --oneline --graph --all
```

Right now it's just a straight line. That's about to change in the next task.

---

## Verify

```bash
# Should show 5 commits total
git log --oneline | wc -l

# Should show two files tracked
git ls-files
```

---

## What You Just Learned

- `git log` has many formats, use `--oneline` daily, `--stat` to see scope, `-p` for detail
- `git show <hash>` lets you inspect any specific commit
- `git show <hash>:<file>` lets you see any file at any point in history
- Every commit has a unique hash, this is how Git identifies everything

`git log` is not just archaeology. When something breaks, when a teammate asks "what changed last week?", when you want to understand why a file looks the way it does, this is what you reach for. Reading history fluently is what separates someone who uses Git from someone who understands it.

---

→ Next: [Task 03b: Writing Commit Messages That Actually Help](../03b-commit-messages/TASK.md)
