# Curriculum Overview

This document maps every task to its learning objectives and the Git concepts introduced.
Use it as a reference, not as a starting point. Start with Task 01.

---

## Tier 1: Solo Git (Tasks 01–08)

After this tier, you can manage your own projects with Git confidently.

### Task 01, First Commit
- **Scenario:** Start the Developer Handbook with a README
- **Git concepts:** `init`, `add`, `commit`, staging area vs working directory
- **Mental model:** What a commit actually is (a snapshot, not a diff)

### Task 02, Tracking Changes
- **Scenario:** Expand the README with team guidelines
- **Git concepts:** `diff`, `status`, the three states of a file (modified, staged, committed)
- **Mental model:** The staging area as a "draft" of your next commit

### Task 03, Reading History
- **Scenario:** Add a Code of Conduct file, review what you've done so far
- **Git concepts:** `log`, `show`, `log --oneline`, `log --graph`
- **Mental model:** The commit graph, linear history as a chain of snapshots

### Task 04, Branching Basics
- **Scenario:** Create a "coding standards" section on a separate branch
- **Git concepts:** `branch`, `switch`/`checkout`, HEAD
- **Mental model:** Branches are just pointers. HEAD is "where you are now."

### Task 05, Merging
- **Scenario:** Your coding standards are ready, bring them into the main branch
- **Git concepts:** `merge`, fast-forward vs three-way merge
- **Mental model:** Merging = combining two lines of history

### Task 06, Merge Conflicts
- **Scenario:** Two branches edited the same section of the README, resolve the conflict
- **Git concepts:** Conflict markers, manual resolution, `add` to mark resolved
- **Mental model:** Why conflicts happen and why they're normal, not scary

### Task 07, Undoing Mistakes
- **Scenario:** You committed something wrong. Fix it, three different ways.
- **Git concepts:** `amend`, `reset` (soft/mixed/hard), `revert`
- **Mental model:** The difference between rewriting history and adding corrective history

### Task 08, Stashing Work
- **Scenario:** You're mid-edit but need to switch branches urgently
- **Git concepts:** `stash`, `stash pop`, `stash list`
- **Mental model:** The stash as a temporary shelf

---

## Tier 2: Collaboration (Tasks 09–11)

After this tier, you can work with others using Git and GitHub.

### Task 09, Working with Remotes
- **Scenario:** Push your handbook to GitHub so your "team" can access it
- **Git concepts:** `remote add`, `push`, `clone`, `fetch`, remote tracking branches
- **Mental model:** Local vs remote, two copies of the same graph

### Task 10, Collaboration Basics
- **Scenario:** A teammate made changes. Pull them in. Then push your own.
- **Git concepts:** `pull`, `push` rejection, pull before push, pull requests (GitHub)
- **Mental model:** GitHub Flow, the simplest collaborative workflow

### Task 11, Rebasing
- **Scenario:** Your branch is behind main. Rebase it to get a clean history.
- **Git concepts:** `rebase`, `rebase -i`, rebase vs merge tradeoffs
- **Mental model:** Rebase = replay your commits on top of a new base

---

## Tier 3: Gitflow (Tasks 12–15)

After this tier, you understand structured branching workflows and can work in Gitflow teams.

### Task 12, Gitflow Introduction
- **Scenario:** Set up the Gitflow branch structure for the handbook
- **Git concepts:** `develop` branch, long-lived vs short-lived branches
- **Mental model:** Why Gitflow exists, when to use it, when not to

### Task 13, Feature Branches
- **Scenario:** Add a troubleshooting guide using a proper Gitflow feature branch
- **Git concepts:** `feature/*` branches, branching from and merging back to `develop`
- **Mental model:** Feature isolation and parallel development

### Task 14, Release Branches
- **Scenario:** Prepare version 1.0 of the handbook for release
- **Git concepts:** `release/*` branches, version bumps, merging to both `main` and `develop`
- **Mental model:** The release as a stabilization phase

### Task 15, Hotfix Branches
- **Scenario:** A critical error in the published handbook needs an emergency fix
- **Git concepts:** `hotfix/*` branches, branching from `main`, merging to both `main` and `develop`
- **Mental model:** Hotfixes as the "emergency lane" of Gitflow

---

## After You Finish

You will have:
- A Git repository with real, meaningful history
- Experience with every common Git operation
- A clear mental model of how Git works internally
- Practical knowledge of Gitflow and when to use it (or not)

Suggested next steps:
- Explore trunk-based development and compare it to Gitflow
- Learn Git hooks for automation
- Try `git bisect` for debugging
- Read the Pro Git book (free at git-scm.com/book)
