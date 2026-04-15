# Task 15: Hotfix Branches

## The Scenario

Disaster. The published handbook (v1.0.0, now live on `main`) has a **critical error** in the Security Guidelines: it recommends an insecure practice. This needs to be fixed immediately , you can't wait for the next release.

This is what **hotfix branches** are for: emergency fixes to production that bypass the normal develop → release flow.

---

## What to Do

### Step 1 , Create the Hotfix Branch from Main

This is the critical difference: hotfixes branch from `main`, not `develop`.

```bash
git switch main
git pull
git switch -c hotfix/v1.0.1
```

### Step 2 , Fix the Critical Issue

Open `SECURITY.md` and find the "Password Management" section. Add a critical line that was "missing" (simulating the error fix):

Change the section to:

```
## Password Management
- Use a password manager , no exceptions
- Minimum password length: 16 characters for all service accounts
- Enable two-factor authentication on all work accounts
- Never share credentials via chat or email , use the team vault
- Rotate service account credentials every 90 days
```

(You added the minimum length and rotation requirements , critical security practices that were missing)

```bash
git add SECURITY.md
git commit -m "Fix missing password requirements in security guidelines"
```

### Step 3 , Bump the Patch Version

Open `CHANGELOG.md` and add a new section above the 1.0.0 entry:

```
## [1.0.1] - YYYY-MM-DD

### Fixed
- Added missing password length and rotation requirements to security guidelines

```

(Replace `YYYY-MM-DD` with today's date)

```bash
git add CHANGELOG.md
git commit -m "Bump version to 1.0.1"
```

### Step 4 , Merge Hotfix to Main

```bash
git switch main
git merge --no-ff hotfix/v1.0.1 -m "Merge hotfix/v1.0.1 into main"
```

### Step 5 , Tag the Hotfix Release

```bash
git tag -a v1.0.1 -m "Hotfix: add missing password security requirements"
```

### Step 6 , Merge Hotfix Back to Develop

Just like release branches, hotfixes must merge into `develop` too , otherwise the fix would be lost in the next release.

```bash
git switch develop
git merge --no-ff hotfix/v1.0.1 -m "Merge hotfix/v1.0.1 into develop"
```

Resolve any conflicts if they appear (develop may have diverged from main).

### Step 7 , Clean Up

```bash
git branch -d hotfix/v1.0.1
```

### Step 8 , Push Everything

```bash
git push origin main
git push origin develop
git push origin v1.0.1
```

### Step 9 , View the Full Picture

```bash
git log --oneline --graph --all
```

Take a moment to look at this graph. You can see the entire story of the project:
- Feature branches merging into develop
- A release branch merging into both main and develop
- A hotfix branching from main and merging into both main and develop
- Tags marking each release

> 📖 **Stop and read** [THEORY.md](THEORY.md) **, Section 1: The Complete Picture**

---

## Verify

```bash
# Two tags exist
git tag --list
# v1.0.0
# v1.0.1

# Main has the hotfix
git log main --oneline -3

# Develop also has the hotfix
git switch develop
git log --oneline | grep "hotfix"

# The security fix is in both branches
git show main:SECURITY.md | grep "16 characters"
git show develop:SECURITY.md | grep "16 characters"
```

---

## What You Just Learned

- Hotfixes branch from `main` (not develop) , they fix production
- Like releases, hotfixes merge into BOTH `main` and `develop`
- Hotfixes get their own version tag (patch increment: 1.0.0 → 1.0.1)
- This is the "emergency lane" of Gitflow , fast, targeted, bypasses the normal pipeline

---

## Congratulations , You've Completed the Entire Course!

### What You Can Now Do

**Solo (Tier 1):**
- Initialize repos, track changes, read diffs and history
- Branch, merge, and resolve conflicts
- Undo mistakes safely
- Stash work temporarily

**Collaboration (Tier 2):**
- Push/pull with remotes
- Work with Pull Requests and team workflows
- Rebase for clean history

**Gitflow (Tier 3):**
- Maintain `main` and `develop` branches
- Use feature branches for parallel development
- Cut release branches for stabilization
- Deploy hotfixes to production

### What's Next

- **Practice:** Use what you learned in a real project , there's no substitute
- **Explore further:** `git bisect` (find which commit introduced a bug), `git cherry-pick` (move specific commits), `git hooks` (automation)
- **Read:** [Pro Git book](https://git-scm.com/book) , free, comprehensive, excellent
- **Decide:** Does your team actually need Gitflow? Or would GitHub Flow or trunk-based development be simpler? Now you have the knowledge to make that call.

### The Developer Handbook

Look at what you built: a complete team handbook with real content, meaningful commit history, proper branching, tagged releases, and a hotfix. This isn't a toy project , it's a real artifact of your learning.

Keep it. Use it. Improve it.
