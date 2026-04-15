# Task 14: Release Branches

## The Scenario

The Developer Handbook has enough content for a proper release. The team wants to publish **version 1.0.0**. But development shouldn't stop, new features can keep being added to `develop` while you stabilize the release.

That's exactly what a release branch is for.

---

## What to Do

### Step 1, Cut the Release Branch

```bash
git switch develop
git pull
git switch -c release/v1.0.0
```

This snapshot of `develop` is now the release candidate. From this point, only bug fixes and version-related changes go here. No new features.

### Step 2, Version Bump

Update `CHANGELOG.md`. Replace `[Unreleased]` with the version and date:

```
# Changelog

## [1.0.0] - YYYY-MM-DD

### Added
- Initial README with team overview
- Communication guidelines
- Code of conduct
- Coding standards
- Testing guidelines
- Meeting guidelines update
- Security guidelines
- Git workflow documentation
- Pull request process
- Onboarding guide
- Troubleshooting guide
- Glossary
- Git quick reference table

### Changed
- Restructured workflow docs to use Gitflow branching model
```

(Replace `YYYY-MM-DD` with today's actual date)

```bash
git add CHANGELOG.md
git commit -m "Bump version to 1.0.0"
```

### Step 3, Release Bug Fix

During testing, you discover the troubleshooting guide is missing one common issue. This kind of fix is allowed on a release branch:

Open `TROUBLESHOOTING.md` and add at the end of the Git Issues section:

```
### "detached HEAD state"
**Meaning:** HEAD is pointing to a commit directly, not a branch.
**Fix:** If you want to keep your work, create a branch: `git switch -c my-branch`. If you ended up here by accident, switch to a branch: `git switch main`.
```

```bash
git add TROUBLESHOOTING.md
git commit -m "Add detached HEAD troubleshooting entry"
```

> 📖 **Stop and read** [THEORY.md](THEORY.md) **, Section 1: The Release Branch Lifecycle**

### Step 4, Simulate Ongoing Development

While the release stabilizes, the team keeps working. Switch to `develop` and add a new feature commit:

```bash
git switch develop
```

Open `README.md` and add to the "What's Inside" list:

```
- Deployment Guide (coming soon)
```

```bash
git add README.md
git commit -m "Add deployment guide placeholder to table of contents"
```

This commit will NOT be in release 1.0.0, it's a new feature added after the release branch was cut. This is the whole point: development continues in parallel.

### Step 5, Finish the Release: Merge to Main

```bash
git switch main
git merge --no-ff release/v1.0.0 -m "Merge release/v1.0.0 into main"
```

### Step 6, Tag the Release

```bash
git tag -a v1.0.0 -m "Release version 1.0.0, first stable release of the Developer Handbook"
```

Verify:

```bash
git tag
git show v1.0.0
```

### Step 7, Merge Back to Develop

The release branch might contain bug fixes that `develop` doesn't have yet. Merge them back:

```bash
git switch develop
git merge --no-ff release/v1.0.0 -m "Merge release/v1.0.0 back into develop"
```

If there's a conflict (because develop moved forward), resolve it and commit.

### Step 8, Clean Up

```bash
git branch -d release/v1.0.0
```

### Step 9, Push Everything

```bash
git push origin main
git push origin develop
git push origin v1.0.0
git push origin --delete release/v1.0.0
```

---

## Verify

```bash
# Tag exists on main
git switch main
git tag --list

# Main has the release
git log main --oneline -3

# Develop has the release fixes PLUS the ongoing development commit
git switch develop
git log --oneline -5

# The "Deployment Guide" placeholder is on develop but NOT on the v1.0.0 tag
git show v1.0.0:README.md | grep "Deployment"
# Should find nothing

git show develop:README.md | grep "Deployment"
# Should find it
```

---

## What You Just Learned

- Release branches stabilize a specific version while development continues
- Only bug fixes go into a release branch, no new features
- The release branch merges into BOTH `main` (deployment) and `develop` (so fixes aren't lost)
- Tags mark specific releases on `main`, they're permanent labels
- `git tag -a v1.0.0 -m "message"` creates an annotated tag with a message

The dual merge, into `main` AND back into `develop`, is the part people most often forget. If you only merge to `main`, every fix made during stabilization disappears the moment the next release is cut from `develop`. The back-merge exists to prevent exactly that.

---

→ Next: [Task 15: Hotfix Branches](../15-hotfix-branches/TASK.md)
