# Task 09: Working with Remotes

## The Scenario

So far, your handbook lives only on your machine. The team can't see it, can't contribute, and if your laptop dies, it's gone. Time to put it on **GitHub** so the team can access it, and so you have a backup.

This is where Git becomes a collaboration tool.

---

## Prerequisites

- A GitHub account (sign up at github.com if you don't have one)
- Git configured with your name and email:
  ```bash
  git config --global user.name "Your Name"
  git config --global user.email "you@example.com"
  ```

---

## What to Do

### Step 1, Create a GitHub Repository

Go to [github.com/new](https://github.com/new) and create a new repository:

- Name: `developer-handbook`
- Description: "Team developer handbook, a learning project"
- **Do NOT** initialize with a README, .gitignore, or license (you already have content)
- Click "Create repository"

GitHub will show you setup instructions. You need the commands under **"…or push an existing repository from the command line."**

### Step 2, Connect Your Local Repo to GitHub

In your `handbook/` directory:

```bash
git remote add origin https://github.com/YOUR-USERNAME/developer-handbook.git
```

(Replace `YOUR-USERNAME` with your actual GitHub username)

Verify:

```bash
git remote -v
```

You should see `origin` listed with your GitHub URL for both fetch and push.

> 📖 **Stop and read** [THEORY.md](THEORY.md) **, Section 1: What Is a Remote?**

### Step 3, Push

```bash
git push -u origin main
```

(`-u` sets the upstream tracking, you only need it the first time)

Go to your GitHub repository page in the browser. Refresh. Your files are there, README, coding standards, everything.

### Step 4, Understand What Happened

```bash
git log --oneline --all
```

You'll see a new reference: `origin/main`. This is a **remote tracking branch**, it's Git's local memory of where `main` is on GitHub.

```bash
git branch -a
```

This shows all branches: local and remote.

### Step 5, Simulate a Teammate's Change

Go to the GitHub web interface. Click on `CODE_OF_CONDUCT.md`. Click the pencil icon (edit). Add a new section at the bottom:

```
## Attribution

This Code of Conduct is adapted from the Contributor Covenant, version 2.1.
```

Click "Commit changes" on GitHub. Write a commit message like "Add attribution to code of conduct."

Now your GitHub repo has a commit that your local repo doesn't.

### Step 6, Fetch and Pull

Back in your terminal:

```bash
git fetch origin
```

This downloads the new commit but doesn't change your working directory. Check:

```bash
git log --oneline --all
```

You can see `origin/main` is *ahead* of your local `main`. Now pull:

```bash
git pull
```

Check the file:

```bash
cat CODE_OF_CONDUCT.md
```

The attribution section is there. Your local repo is now in sync with GitHub.

> 📖 **Stop and read** [THEORY.md](THEORY.md) **, Section 2: Fetch vs Pull**

### Step 7, Make a Local Change and Push

Add a new file `GIT_WORKFLOW.md`:

```
# Git Workflow

This document describes how our team uses Git for day-to-day development.

## Branch Naming

- Features: `feature/short-description`
- Bug fixes: `fix/short-description`
- Documentation: `docs/short-description`

## Commit Messages

Write commit messages in the imperative mood:
- Good: "Add user authentication"
- Good: "Fix login redirect bug"
- Bad: "Added authentication"
- Bad: "Fixed the thing"

The first line should be under 50 characters. Add detail in the body if needed.
```

```bash
git add GIT_WORKFLOW.md
git commit -m "Add Git workflow guidelines"
git push
```

Check GitHub, your new file appears.

---

## Verify

```bash
# Local and remote should be in sync
git log --oneline -3
git log --oneline origin/main -3
# Should show the same commits

# All files present
ls
# Should include: CHANGELOG.md, CODE_OF_CONDUCT.md, CODING_STANDARDS.md,
# GIT_WORKFLOW.md, ONBOARDING.md, README.md, TESTING.md
```

---

## What You Just Learned

- `git remote add` connects a local repo to a remote (like GitHub)
- `git push` sends your commits to the remote
- `git fetch` downloads remote changes without applying them
- `git pull` = `fetch` + `merge`, downloads and applies
- `origin/main` is a remote tracking branch, Git's bookmark for "where main is on the remote"
- Push and pull keep local and remote in sync

---

→ Next: [Task 10: Collaboration Basics](../10-collaboration-basics/TASK.md)
