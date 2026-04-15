# Task 13: Feature Branches

## The Scenario

Two features need to be built for the next release of the handbook: a Troubleshooting Guide and a Glossary. You'll work on both using proper Gitflow feature branches, branching from `develop` and merging back to `develop`.

---

## What to Do

### Step 1, Start the First Feature

Make sure you're on `develop` and up to date:

```bash
git switch develop
git pull
```

Create a feature branch:

```bash
git switch -c feature/troubleshooting-guide
```

Create `TROUBLESHOOTING.md`:

```
# Troubleshooting Guide

Common problems and their solutions.

## Git Issues

### "Your branch is behind 'origin/main'"
**Meaning:** The remote has commits you don't have locally.
**Fix:** Run `git pull` to sync up.

### "CONFLICT (content): Merge conflict in <file>"
**Meaning:** Two branches edited the same lines.
**Fix:** Open the file, look for `<<<<<<<` markers, choose the correct content, remove the markers, then `git add` and `git commit`.

### "fatal: not a git repository"
**Meaning:** You're not inside a Git repository.
**Fix:** Navigate to the correct directory, or run `git init` if starting a new project.

### "error: failed to push some refs"
**Meaning:** The remote has changes you don't have.
**Fix:** Run `git pull` first, resolve any conflicts, then `git push` again.

## Development Environment

### "node_modules taking too much space"
**Fix:** Add `node_modules/` to `.gitignore`. Run `git rm -r --cached node_modules/` if already tracked.

### "My changes disappeared after switching branches"
**Meaning:** You either didn't commit or didn't stash before switching.
**Fix:** If you stashed, run `git stash pop`. If you committed on another branch, switch to that branch.
```

```bash
git add TROUBLESHOOTING.md
git commit -m "Add troubleshooting guide with common Git issues"
```

Add a link in `README.md` under "What's Inside":

```
- [Troubleshooting](TROUBLESHOOTING.md), Common problems and solutions
```

```bash
git add README.md
git commit -m "Add troubleshooting link to table of contents"
```

Push the feature branch:

```bash
git push -u origin feature/troubleshooting-guide
```

### Step 2, Start the Second Feature (In Parallel)

Switch back to `develop`, not from the first feature branch:

```bash
git switch develop
git switch -c feature/glossary
```

Create `GLOSSARY.md`:

```
# Glossary

Key terms used in this handbook and in daily development work.

## Git Terms

| Term | Definition |
|------|-----------|
| **Repository (repo)** | A project tracked by Git, contains all files and their full history |
| **Commit** | A snapshot of your project at a point in time |
| **Branch** | A movable pointer to a commit, represents an independent line of work |
| **HEAD** | A pointer to the branch (or commit) you're currently on |
| **Staging area (index)** | A draft of what will go into your next commit |
| **Remote** | A copy of the repository on another server (e.g., GitHub) |
| **Clone** | Downloading a full copy of a remote repository |
| **Fork** | A personal copy of someone else's repository on GitHub |
| **Pull Request (PR)** | A request to merge a branch, includes review and discussion |
| **Merge** | Combining two branches into one |
| **Rebase** | Replaying commits from one branch onto another |
| **Conflict** | When two branches edit the same lines and Git can't auto-merge |
| **Stash** | Temporary storage for uncommitted changes |
| **Tag** | A permanent label for a specific commit (usually a release) |

## Gitflow Terms

| Term | Definition |
|------|-----------|
| **main** | The branch representing production, only released code lives here |
| **develop** | The integration branch where features are combined before release |
| **Feature branch** | A short-lived branch for developing a single feature |
| **Release branch** | A branch for stabilizing a release, no new features, only fixes |
| **Hotfix branch** | An emergency fix branch created from main |
```

```bash
git add GLOSSARY.md
git commit -m "Add glossary of Git and Gitflow terms"
git push -u origin feature/glossary
```

### Step 3, Merge Features Into Develop

In a real team, you'd do this through Pull Requests on GitHub. For this exercise, do it locally:

```bash
git switch develop
```

Merge the first feature:

```bash
git merge --no-ff feature/troubleshooting-guide -m "Merge feature/troubleshooting-guide into develop"
```

> 📖 **Stop and read** [THEORY.md](THEORY.md) **, Section 1: Why --no-ff?**

Merge the second feature:

```bash
git merge --no-ff feature/glossary -m "Merge feature/glossary into develop"
```

Add the glossary link to `README.md`:

```
- [Glossary](GLOSSARY.md), Key terms and definitions
```

```bash
git add README.md
git commit -m "Add glossary link to table of contents"
```

Push develop:

```bash
git push
```

### Step 4, Clean Up

```bash
git branch -d feature/troubleshooting-guide
git branch -d feature/glossary
git push origin --delete feature/troubleshooting-guide
git push origin --delete feature/glossary
```

---

## Verify

```bash
# On develop branch
git branch

# Both files exist
ls TROUBLESHOOTING.md GLOSSARY.md

# History shows merge commits from features
git log --oneline --graph -8

# Main is untouched, still behind develop
git log main --oneline -1
git log develop --oneline -1
```

---

## What You Just Learned

- Feature branches start from `develop` and merge back to `develop`
- `--no-ff` forces a merge commit even when fast-forward is possible, this preserves the branch record
- Multiple features can be developed in parallel on separate branches
- Features never touch `main` directly
- Clean up branches after merging, both locally and on the remote

---

→ Next: [Task 14: Release Branches](../14-release-branches/TASK.md)
