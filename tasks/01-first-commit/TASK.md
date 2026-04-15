# Task 01: First Commit

## The Scenario

You've just joined a development team. Your first job: start the team's **Developer Handbook**, a shared reference that the whole team will contribute to. Right now, it's just you and a blank folder.

Your task is to create the first file of the handbook and save it into Git.

---

## What to Do

### Step 1, Set Up

Open your terminal. Navigate to the `handbook/` directory inside this project:

```
cd handbook
```

Initialize a new Git repository here:

```
git init
```

> You just created a Git repository. Everything you do in this folder is now trackable.

### Step 2, Create the First File

Create a file called `README.md` with the following content (type it yourself, don't copy-paste; the act of typing helps):

```
# Developer Handbook

Welcome to our team's Developer Handbook. This is a living document maintained by the whole team.

## What's Inside

This handbook will contain:
- Coding standards and style guides
- Team workflows and processes
- Troubleshooting guides
- Onboarding information for new team members

## Contributing

Every team member is encouraged to improve this handbook. See the contribution guidelines for how to submit changes.
```

Save the file.

### Step 3, Check What Git Sees

Run:

```
git status
```

Read the output carefully. Git is telling you something: it *sees* the file, but it's **not tracking it yet**. The file is "untracked."

> 📖 **Stop and read** [THEORY.md](THEORY.md) **, Section 1: The Three States** before continuing.

### Step 4, Stage the File

```
git add README.md
```

Now run `git status` again. Notice the difference? The file moved from "untracked" to "staged." It's now in the **staging area**, ready to be committed, but not committed yet.

### Step 5, Commit

```
git commit -m "Add initial README for the Developer Handbook"
```

Run `git status` one more time. Clean. Nothing to commit. Your snapshot is saved.

> 📖 **Stop and read** [THEORY.md](THEORY.md) **, Section 2: What Is a Commit, Really?**

---

## Verify

Run these commands and confirm the results:

```bash
# Should show one commit with your message
git log --oneline

# Should show the content of your README
git show HEAD:README.md
```

If you see your commit message and your file content, you've completed Task 01.

---

## What You Just Learned

- `git init` creates a repository
- `git status` shows you what Git sees right now
- `git add` moves changes to the staging area
- `git commit` saves a snapshot
- A commit is not just "saving", it's saving a *specific set of changes you chose*

---

→ Next: [Task 02: Tracking Changes](../02-tracking-changes/TASK.md)
