# Git & Git Flow Cheat Sheet

## 1. Branch Model Overview (Git Flow)

| Branch | Purpose | Branched from | Merged back into |
|---|---|---|---|
| `main` | Production-ready code. Every commit = a release. | — | — |
| `develop` | Integration branch for the next release. | `main` (once) | `main` (via release) |
| `feature/*` | New features, in progress. | `develop` | `develop` |
| `release/*` | Preparing a new production release (bugfix, polish). | `develop` | `main` **and** `develop` |
| `hotfix/*` | Urgent fix on production. | `main` | `main` **and** `develop` |
| `bugfix/*` | Non-urgent bugfix. | `develop` | `develop` |

Rule of thumb: **never commit directly to `main` or `develop`** — always through a branch + merge/PR.

---

## 2. Setup & Basics

```bash
# Initialize
git init
git clone <url>
git clone <url> <folder>

# Configure identity (once per machine)
git config --global user.name  "Your Name"
git config --global user.email "you@example.com"
git config --global init.defaultBranch main
git config --global pull.rebase false   # or 'true' if you prefer rebase on pull

# Status / inspection
git status
git log --oneline --graph --decorate --all
git diff                    # unstaged changes
git diff --staged           # staged changes
git show <commit>
```

---

## 3. Staging & Committing

```bash
git add <file>              # stage one file
git add .                   # stage everything in current dir
git add -p                  # stage hunks interactively (very useful)
git restore --staged <file> # unstage
git restore <file>          # discard unstaged changes (DANGEROUS)

git commit -m "feat: short, imperative summary"
git commit --amend          # edit last commit (only if not pushed!)
```

**Conventional commit prefixes** (common convention):
`feat:`, `fix:`, `docs:`, `style:`, `refactor:`, `test:`, `chore:`, `perf:`, `build:`, `ci:`

---

## 4. Branching — Core Commands

```bash
git branch                        # list local branches
git branch -a                     # list all (incl. remote)
git branch -vv                    # show tracking info

git switch <branch>               # change branch (modern)
git switch -c <branch>            # create + switch
git checkout <branch>             # older equivalent
git checkout -b <branch>          # older "create + switch"

git branch -d <branch>            # delete (safe, refuses if unmerged)
git branch -D <branch>            # force delete
git push origin --delete <branch> # delete remote branch

git branch -m old new             # rename
```

---

## 5. Feature Branch Workflow

The 90% case — what you'll do every day.

```bash
# 1. Start from up-to-date develop
git switch develop
git pull origin develop

# 2. Create a feature branch
git switch -c feature/user-login

# 3. Work + commit in small, meaningful chunks
git add -p
git commit -m "feat(auth): add login form"

# 4. Push early, push often
git push -u origin feature/user-login     # -u sets upstream (first time only)
git push                                   # subsequent pushes

# 5. Keep your branch current while working (pick ONE strategy):
# Option A — merge develop in (safer, preserves history)
git switch feature/user-login
git fetch origin
git merge origin/develop

# Option B — rebase onto develop (cleaner history, rewrites commits)
git fetch origin
git rebase origin/develop

# 6. Open a Pull Request / Merge Request in your platform (GitHub/GitLab/etc.)

# 7. After it's merged: clean up
git switch develop
git pull origin develop
git branch -d feature/user-login
git push origin --delete feature/user-login   # if still on remote
```

**Naming:** `feature/<short-kebab-description>` or `feature/<ticket-id>-<desc>`, e.g. `feature/JIRA-123-oauth-login`.

---

## 6. Release Branch Workflow

For preparing a production release (version bump, final bugfixes, changelog).

```bash
# Cut a release branch from develop
git switch develop
git pull
git switch -c release/1.4.0

# Bump version, update CHANGELOG, last-mile fixes — commit them here.
# Do NOT add new features on a release branch.

# When ready to ship, merge to main and tag
git switch main
git pull
git merge --no-ff release/1.4.0
git tag -a v1.4.0 -m "Release 1.4.0"
git push origin main --tags

# Merge back to develop so fixes aren't lost
git switch develop
git merge --no-ff release/1.4.0
git push origin develop

# Delete the release branch
git branch -d release/1.4.0
git push origin --delete release/1.4.0
```

---

## 7. Hotfix Workflow

For urgent production bugs — bypasses `develop`.

```bash
# Branch from main (production)
git switch main
git pull
git switch -c hotfix/1.4.1

# Fix the bug, bump patch version
git commit -am "fix: null pointer in payment handler"

# Merge to main + tag
git switch main
git merge --no-ff hotfix/1.4.1
git tag -a v1.4.1 -m "Hotfix 1.4.1"
git push origin main --tags

# Merge into develop too (so the fix lives on)
git switch develop
git merge --no-ff hotfix/1.4.1
git push origin develop

# Clean up
git branch -d hotfix/1.4.1
```

---

## 8. Merge vs. Rebase — When to Use Which

| Situation | Use |
|---|---|
| Integrating a finished feature into `develop` | **Merge** (often `--no-ff` to keep a merge commit) |
| Updating your personal feature branch with latest `develop` | **Rebase** if only you work on it; **Merge** if shared |
| A shared/public branch | **Never rebase** — you rewrite history others depend on |
| Cleaning up local WIP commits before PR | **Interactive rebase** (`git rebase -i`) |

```bash
git merge <branch>               # fast-forward if possible
git merge --no-ff <branch>       # always create a merge commit
git rebase <branch>              # replay your commits on top of <branch>
git rebase -i HEAD~5             # interactively squash/edit last 5 commits
git rebase --abort               # bail out of a rebase
git merge --abort                # bail out of a merge
```

---

## 9. Resolving Merge Conflicts

```bash
# Git will mark conflicting files. Inspect them:
git status

# Open each file, look for:
# <<<<<<< HEAD
# your version
# =======
# their version
# >>>>>>> branch-name

# Edit to the final desired state, remove the markers, then:
git add <file>
git commit                  # for merge (message is pre-filled)
# OR
git rebase --continue       # for rebase
```

Useful tooling:
```bash
git mergetool               # launch configured GUI tool
git diff --name-only --diff-filter=U   # list unresolved files
```

---

## 10. Syncing with Remote

```bash
git fetch                   # get remote refs, don't touch working tree
git fetch --all --prune     # also delete stale remote-tracking branches
git pull                    # = fetch + merge (or rebase, if configured)
git pull --rebase           # explicit rebase pull
git push                    # push current branch to its upstream
git push -u origin <branch> # first push, set upstream
git push --force-with-lease # safer than --force when rewriting history
```

**Never `git push --force`** on a shared branch. Use `--force-with-lease` which refuses if someone else pushed in the meantime.

---

## 11. Undoing Things

```bash
# Change last commit message / add forgotten file
git commit --amend

# Undo last commit, keep changes staged
git reset --soft HEAD~1

# Undo last commit, keep changes unstaged
git reset --mixed HEAD~1    # (default)

# Undo last commit AND discard changes — destructive
git reset --hard HEAD~1

# Revert a commit by making a new "inverse" commit (safe on shared branches)
git revert <commit>

# Recover a "lost" commit
git reflog                  # shows everything HEAD has pointed at
git reset --hard <sha>      # jump back to it
```

Rule: **`reset` rewrites history, `revert` adds history.** Use `revert` on anything already pushed.

---

## 12. Stash — Park Changes Temporarily

```bash
git stash                       # stash tracked changes
git stash -u                    # include untracked
git stash -m "wip: refactor"    # with a label
git stash list
git stash show -p stash@{0}     # preview
git stash pop                   # apply + drop
git stash apply stash@{1}       # apply, keep in stash
git stash drop stash@{0}
git stash clear                 # nuke all stashes
```

---

## 13. Tags (for Releases)

```bash
git tag                             # list
git tag -a v1.4.0 -m "Release 1.4.0"   # annotated (preferred)
git tag v1.4.0                       # lightweight
git push origin v1.4.0               # push one tag
git push origin --tags               # push all tags
git tag -d v1.4.0                    # delete local
git push origin --delete v1.4.0      # delete remote
```

---

## 14. Cherry-Pick — Grab a Specific Commit

```bash
git cherry-pick <commit>
git cherry-pick <c1> <c2> <c3>
git cherry-pick --abort
```

Handy for backporting a fix from `develop` to a `release/*` branch.

---

## 15. Best Practices & Things to Consider

- **Small, focused commits.** One logical change per commit. Reviewers and bisects will thank you.
- **Write good commit messages.** Imperative mood ("Add X", not "Added X"), short summary line, blank line, then body explaining *why*.
- **Pull before you push.** Prevents surprise conflicts.
- **Never rewrite public history.** No `rebase` or `push --force` on shared branches.
- **Delete merged branches.** Keeps the repo tidy.
- **Protect `main` and `develop`.** Require PRs + reviews + CI in your platform settings.
- **Use `.gitignore` from day one.** Never commit secrets, `node_modules`, build artifacts.
- **Tag every production release.** Semver: `MAJOR.MINOR.PATCH`.
- **Feature flags > long-lived branches.** Branches that live for weeks are merge-conflict factories.
- **Review your own diff before pushing.** `git diff origin/develop...HEAD` catches a lot of bugs.

---

## 16. Quick Reference — Daily Loop

```bash
git switch develop && git pull              # start clean
git switch -c feature/my-thing              # new branch
# ... hack hack hack ...
git add -p && git commit -m "feat: ..."     # commit
git push -u origin feature/my-thing         # push
# Open PR → review → merge
git switch develop && git pull              # back to start
git branch -d feature/my-thing              # clean up
```

---

## 17. Optional: `git-flow` CLI Extension

There's a helper tool that automates the above workflows:

```bash
# Install (varies by OS): brew install git-flow-avh   |   apt install git-flow
git flow init                               # set up branches
git flow feature start <name>               # = branch from develop
git flow feature finish <name>              # = merge into develop, delete
git flow release start 1.4.0
git flow release finish 1.4.0               # merges + tags for you
git flow hotfix start 1.4.1
git flow hotfix finish 1.4.1
```

It's convenient, but understanding the raw git commands above matters more — the extension is just a shortcut.
