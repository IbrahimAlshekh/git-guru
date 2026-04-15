# Task 04: Branching Basics

## The Scenario

The team wants a Coding Standards section in the handbook. But the README is also being updated by another team member (you'll simulate this). You shouldn't work on coding standards directly in `main`, if it takes a few days and something urgent comes up, you'd have half-finished work blocking the main branch.

Solution: work on a **separate branch**.

---

## What to Do

### Step 1, See Your Current Branch

```bash
git branch
```

You'll see `* main` (or `* master`). The `*` means "this is where HEAD is."

### Step 2, Create a New Branch

```bash
git branch coding-standards
```

Now run `git branch` again. You see two branches, but the `*` is still on `main`. Creating a branch doesn't switch to it.

> 📖 **Stop and read** [THEORY.md](THEORY.md) **, Section 1: What Is a Branch?**

### Step 3, Switch to the New Branch

```bash
git switch coding-standards
```

(If `git switch` doesn't work on your Git version, use `git checkout coding-standards`)

Run `git branch` again. The `*` moved. Run `git log --oneline`. Same commits, because the branch started at the same point as `main`.

### Step 4, Work on the Branch

Create a new file called `CODING_STANDARDS.md`:

```
# Coding Standards

This document defines our team's coding standards and best practices.

## General Principles

1. **Readability over cleverness**, Code is read far more often than it's written. Prefer clear, obvious code over clever one-liners.
2. **Consistency matters more than preference**, Follow the existing style even if you'd personally do it differently.
3. **Small functions**, If a function doesn't fit on one screen, it's probably doing too much.

## Naming Conventions

- Variables: `camelCase`, descriptive names, no abbreviations
- Functions: `camelCase`, start with a verb (`getUserName`, not `userName`)
- Constants: `UPPER_SNAKE_CASE`
- Files: `kebab-case.js`

## Comments

- Don't comment *what* the code does, the code should be readable enough
- Do comment *why*, the reasoning behind non-obvious decisions
- TODO comments must include a name: `// TODO(alex): refactor this after migration`

## Formatting

- Indent with 2 spaces (not tabs)
- Maximum line length: 100 characters
- Always use trailing commas in multiline structures
- Opening braces on the same line
```

Stage and commit:

```bash
git add CODING_STANDARDS.md
git commit -m "Add coding standards document"
```

### Step 5, Add More Content to the Branch

Add a new section at the end of `CODING_STANDARDS.md`:

```

## Error Handling

- Never swallow errors silently, at minimum, log them
- Use custom error types for domain-specific failures
- Always include context in error messages: what failed, why, and what the user can do
- Handle errors at the appropriate level, don't catch what you can't fix
```

Commit:

```bash
git add CODING_STANDARDS.md
git commit -m "Add error handling section to coding standards"
```

### Step 6, Look at the Graph

```bash
git log --oneline --graph --all
```

Now you can see the branches diverging. `coding-standards` is ahead of `main` by two commits.

### Step 7, Switch Back to Main

```bash
git switch main
```

Now list the files:

```bash
ls
```

Where did `CODING_STANDARDS.md` go? It's not here. Switch back:

```bash
git switch coding-standards
ls
```

It's back. **The files on disk change when you switch branches.** Git swaps the working directory to match the branch you're on.

> 📖 **Stop and read** [THEORY.md](THEORY.md) **, Section 2: The Graph with Branches**

---

## Verify

```bash
# On coding-standards branch
git log --oneline
# Should show 7 commits (5 from before + 2 new)

git switch main
git log --oneline
# Should show 5 commits (the original ones)

# The graph should show a fork
git log --oneline --graph --all
```

---

## What You Just Learned

- `git branch <name>` creates a branch (but doesn't switch)
- `git switch <name>` moves HEAD to that branch
- Branches are cheap, they're just pointers, not copies
- Switching branches changes the files on disk
- Commits on one branch don't appear on another (yet)

---

→ Next: [Task 05: Merging](../05-merging/TASK.md)
