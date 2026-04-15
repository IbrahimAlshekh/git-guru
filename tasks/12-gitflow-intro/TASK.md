# Task 12: Gitflow Introduction

## The Scenario

Your team's handbook has grown. Other teams want to use it, but they need **stable, versioned releases**, not a `main` branch that changes daily. The manager says: "We need a proper release process. Use Gitflow."

Before jumping in, you need to understand what Gitflow is, set it up, and see how it differs from the GitHub Flow you've been using.

---

## What to Do

### Step 1, Understand the Context

> 📖 **Read** [THEORY.md](THEORY.md) **, Section 1: Why Gitflow Exists** before doing anything. This is one of the few tasks where theory comes first, because Gitflow is a convention, you need to understand the *why* before the *how* makes sense.

### Step 2, Create the Develop Branch

In Gitflow, `main` represents production, the last released version. All ongoing work happens on `develop`.

```bash
git switch main
git pull
```

Create the develop branch:

```bash
git switch -c develop
git push -u origin develop
```

### Step 3, Document the Gitflow Setup

Open `GIT_WORKFLOW.md` and replace the entire content with an expanded version:

```
# Git Workflow

This document describes how our team uses Git for day-to-day development.

## Branching Model: Gitflow

We use the Gitflow branching model. Here's how it works.

### Long-Lived Branches

| Branch | Purpose | Deploys to |
|--------|---------|------------|
| `main` | Production-ready releases only | Production |
| `develop` | Integration branch for features | Staging |

`main` always reflects what's currently in production. You never commit directly to `main`.

`develop` is where features come together. It's the base branch for all new work.

### Short-Lived Branches

| Branch Pattern | Branches from | Merges into | Purpose |
|---------------|---------------|-------------|---------|
| `feature/*` | `develop` | `develop` | New features |
| `release/*` | `develop` | `main` AND `develop` | Release preparation |
| `hotfix/*` | `main` | `main` AND `develop` | Emergency production fixes |

### Rules

1. Never commit directly to `main` or `develop`
2. All work starts as a `feature/*` branch from `develop`
3. Features merge back to `develop` via Pull Request
4. When `develop` is ready for release, create a `release/*` branch
5. Only bug fixes go into a release branch, no new features
6. Hotfixes are the only branches created from `main`
7. After merging a release or hotfix, tag `main` with a version number

## Branch Naming

- Features: `feature/short-description`
- Releases: `release/v1.0.0`
- Hotfixes: `hotfix/v1.0.1`

## Commit Messages

Write commit messages in the imperative mood:
- Good: "Add user authentication"
- Good: "Fix login redirect bug"
- Bad: "Added authentication"
- Bad: "Fixed the thing"

The first line should be under 50 characters. Add detail in the body if needed.

## Pull Request Process

1. Create a branch from `develop` (or `main` for hotfixes)
2. Make your changes in small, focused commits
3. Push the branch to GitHub
4. Open a Pull Request with a clear description of what and why
5. Request review from at least one teammate
6. Address review feedback
7. Merge after approval, delete the branch after merging
```

```bash
git add GIT_WORKFLOW.md
git commit -m "Update workflow docs with Gitflow branching model"
git push
```

### Step 4, Verify the Branch Structure

```bash
git branch -a
```

You should see:
- `develop` (local, you're on it)
- `main` (local)
- `origin/develop` (remote)
- `origin/main` (remote)

```bash
git log --oneline --graph --all
```

`develop` is one commit ahead of `main` (the workflow update).

---

## Verify

```bash
# On develop branch
git branch
# * develop

# Develop has the workflow update, main doesn't
git log develop --oneline -1
git log main --oneline -1
# Different commits

# Remote branches exist
git branch -a | grep origin
```

---

## What You Just Learned

- Gitflow uses two long-lived branches: `main` (production) and `develop` (integration)
- All new work branches from `develop`, not from `main`
- `main` is touched only by releases and hotfixes
- Gitflow is a **convention**, Git doesn't enforce it; your team does
- It trades simplicity for structure, useful when you need versioned releases

---

→ Next: [Task 13: Feature Branches](../13-feature-branches/TASK.md)
