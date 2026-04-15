# Task 10: Collaboration Basics

## The Scenario

A teammate (you'll simulate them) has been working on a security guidelines document. At the same time, you've been updating the Git workflow. Now you both need to share your work through GitHub. This is the everyday reality of team Git usage.

You'll also learn about **Pull Requests**, the standard way teams review and merge code on GitHub.

---

## What to Do

### Step 1, Simulate a Teammate with a Second Clone

Open a **second terminal window**. Create a "teammate's" copy of the repo:

```bash
cd /tmp
git clone https://github.com/YOUR-USERNAME/developer-handbook.git teammate-handbook
cd teammate-handbook
```

Configure this clone with a different identity (to see the difference in history):

```bash
git config user.name "Alex Teammate"
git config user.email "alex@example.com"
```

### Step 2, Teammate Creates a Branch and Pushes It

In the **teammate's terminal** (`/tmp/teammate-handbook`):

```bash
git switch -c feature/security-guidelines
```

Create `SECURITY.md`:

```
# Security Guidelines

## Password Management
- Use a password manager, no exceptions
- Enable two-factor authentication on all work accounts
- Never share credentials via chat or email, use the team vault

## Code Security
- Never commit secrets, tokens, or API keys to the repository
- Use environment variables for all sensitive configuration
- Review dependencies regularly for known vulnerabilities

## Incident Response
- If you discover a security issue, report it immediately to the security team
- Do not attempt to fix security vulnerabilities without review
- Document all incidents within 24 hours
```

```bash
git add SECURITY.md
git commit -m "Add security guidelines"
git push -u origin feature/security-guidelines
```

### Step 3, You Work on a Different Change

Switch to **your original terminal** (in the `handbook/` directory).

```bash
git switch -c feature/workflow-update
```

Open `GIT_WORKFLOW.md` and add a new section at the end:

```

## Pull Request Process

1. Create a branch from `main` with a descriptive name
2. Make your changes in small, focused commits
3. Push the branch to GitHub
4. Open a Pull Request with a clear description of what and why
5. Request review from at least one teammate
6. Address review feedback
7. Merge after approval, delete the branch after merging
```

```bash
git add GIT_WORKFLOW.md
git commit -m "Add pull request process to workflow guide"
git push -u origin feature/workflow-update
```

### Step 4, Fetch and See Both Branches

```bash
git fetch origin
git branch -a
```

You can see both remote branches: `origin/feature/security-guidelines` (from your "teammate") and `origin/feature/workflow-update` (yours).

### Step 5, Create a Pull Request on GitHub

Go to your GitHub repository in the browser. You should see a banner suggesting to create a Pull Request for your recently pushed branch.

Create a PR for `feature/workflow-update`:
- Title: "Add pull request process to workflow guide"
- Description: "Documents our team's PR review process step by step."
- Click "Create pull request"

> 📖 **Stop and read** [THEORY.md](THEORY.md) **, Section 1: GitHub Flow**

### Step 6, Review and Merge the Teammate's Work

On GitHub, switch to the `feature/security-guidelines` branch (use the branch dropdown or check the Pull Requests tab if the teammate also created one).

Create a PR for it too if needed, then merge it:
- Click "Merge pull request"
- Click "Confirm merge"
- Click "Delete branch" (clean up)

Now merge your own PR the same way.

### Step 7, Sync Locally

Back in your terminal:

```bash
git switch main
git pull
```

Check:

```bash
ls
git log --oneline -5
```

Both changes are now in `main`, yours and your teammate's.

Clean up local branches:

```bash
git branch -d feature/workflow-update
git remote prune origin
```

---

## Verify

```bash
# Security guidelines exist
cat SECURITY.md

# Workflow has the PR process section
grep "Pull Request Process" GIT_WORKFLOW.md

# Main is up to date
git log --oneline -5

# Only main branch locally
git branch
```

---

## What You Just Learned

- Multiple people can work on different branches simultaneously
- `git push -u origin <branch>` shares a branch with the team
- Pull Requests let you review code before merging, this is GitHub Flow
- `git fetch` lets you see what others have pushed
- Always `pull` before starting new work to stay current
- Delete branches after merging, they've served their purpose

---

→ Next: [Task 11: Rebasing](../11-rebasing/TASK.md)
