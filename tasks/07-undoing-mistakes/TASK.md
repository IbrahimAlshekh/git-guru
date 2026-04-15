# Task 07: Undoing Mistakes

## The Scenario

You just wrote something wrong, committed it, and now you need to fix it. But "fix it" can mean different things depending on the situation. Git gives you several tools, and picking the right one matters.

This task walks you through three real scenarios with three different undo strategies.

---

## What to Do

### Scenario A, Fix the Last Commit (Amend)

You need to add a changelog to the handbook. Create `CHANGELOG.md`:

```
# Changelog

## [Unreleased]

### Added
- Initial README with team overview
- Communication guidelines
- Code of conduct
- Coding standards
- Testing guidelines
```

Commit it, but "accidentally" with a typo in the message:

```bash
git add CHANGELOG.md
git commit -m "Add changlelog"
```

Oops. Fix the message without creating a new commit:

```bash
git commit --amend -m "Add changelog"
```

Check:

```bash
git log --oneline -1
```

The typo is gone. The old commit was *replaced*, same changes, corrected message, new hash.

Now open `CHANGELOG.md` and add a line you forgot:

```
- Meeting guidelines update
```

Stage it and amend again:

```bash
git add CHANGELOG.md
git commit --amend --no-edit
```

`--no-edit` keeps the same message. The commit now includes the extra line as if it was always there.

> 📖 **Stop and read** [THEORY.md](THEORY.md) **, Section 1: Amend = Rewrite**

---

### Scenario B, Unstage and Undo Working Changes (Reset)

Add something you shouldn't. Open `README.md` and add at the very end:

```
## Secret Notes
This section contains admin passwords: admin123
```

Stage it:

```bash
git add README.md
```

Wait, you don't want that committed. **Unstage** the file:

```bash
git reset HEAD README.md
```

The file is still modified (check `git status`), but it's no longer staged.

Now discard the change entirely, go back to the last committed version:

```bash
git checkout -- README.md
```

(Or in newer Git: `git restore README.md`)

Check:

```bash
git status
cat README.md
```

Clean. The secret notes are gone.

---

### Scenario C, Undo a Commit That's Already Shared (Revert)

Simulate a bad commit. Open `CODING_STANDARDS.md` and replace the "General Principles" section with:

```
## General Principles

1. Write code as fast as possible. Speed is all that matters.
2. Copy-paste is fine. DRY is overrated.
3. Comments are a waste of time.
```

Commit this terrible advice:

```bash
git add CODING_STANDARDS.md
git commit -m "Update coding principles"
```

You realize this is wrong and needs to be undone. But imagine this commit was already pushed to a shared repository, you can't just delete it. Instead, **revert** it:

```bash
git revert HEAD
```

Git opens your editor with a revert commit message. Save and close.

> 📖 **Stop and read** [THEORY.md](THEORY.md) **, Section 2: Reset vs Revert**

Check the result:

```bash
git log --oneline -3
git diff HEAD~2 HEAD
```

The revert commit *undid* the bad commit by adding a new commit. The bad commit is still in history (it happened), but its effects are reversed.

---

## Verify

```bash
# CHANGELOG.md exists with the amended content
cat CHANGELOG.md

# README.md has no "Secret Notes" section
grep "Secret" README.md
# Should find nothing

# CODING_STANDARDS.md is back to the good version
head -10 CODING_STANDARDS.md

# Log shows the revert
git log --oneline -4
```

---

## What You Just Learned

- **`git commit --amend`**, rewrites the last commit (message or content). Only for unpushed commits.
- **`git reset HEAD <file>`**, unstages a file without losing changes
- **`git checkout -- <file>`** / **`git restore <file>`**, discards working directory changes
- **`git revert <commit>`**, creates a new commit that undoes a previous one. Safe for shared history.
- **Golden rule:** If the commit has been pushed/shared, use `revert`. If it's still local, `amend` or `reset` are fine.

---

→ Next: [Task 08: Stashing Work](../08-stashing-work/TASK.md)
