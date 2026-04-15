# Task 02: Tracking Changes

## The Scenario

The team lead reviewed your initial README and said: "Good start. Now add some actual content , we need a section on our team's communication guidelines. Also, fix the 'What's Inside' section to be more specific."

You need to make *multiple changes* to an already-tracked file and commit them thoughtfully.

---

## What to Do

### Step 1 , See Where You Are

Make sure you're in the `handbook/` directory. Run:

```
git status
git log --oneline
```

You should see your one commit from Task 01 and a clean working directory.

### Step 2 , Edit the README

Open `README.md` and make these two changes:

**Change 1:** Update the "What's Inside" section to be more specific:

```
## What's Inside

- [Communication Guidelines](#communication-guidelines) , How we communicate as a team
- Coding Standards (coming soon)
- Git Workflow (coming soon)
- Troubleshooting (coming soon)
```

**Change 2:** Add a new section at the bottom of the file, before "Contributing":

```
## Communication Guidelines

### Meetings
- Daily standup: 9:15 AM, 15 minutes maximum
- All meetings must have an agenda shared at least 1 hour in advance
- No meeting Wednesdays , this is focus time

### Chat
- Use public channels by default , avoid DMs for work discussions
- Respond to messages within 4 hours during working hours
- Use threads to keep conversations organized

### Code Reviews
- Every pull request needs at least one approval
- Review within 24 hours of being assigned
- Be constructive , critique the code, not the person
```

Save the file.

### Step 3 , Examine What Changed

Run:

```
git diff
```

> 📖 **Stop and read** [THEORY.md](THEORY.md) **, Section 1: Reading a Diff** before continuing.

Look at the output carefully. Git is showing you *exactly* what changed , lines added (in green with `+`) and lines removed (in red with `-`). This is one of Git's most useful features.

### Step 4 , Stage and Check the Difference

```
git add README.md
```

Now try `git diff` again. Nothing! The changes moved to the staging area.

To see staged changes:

```
git diff --staged
```

There they are. Same changes, but now Git is comparing the staging area to the last commit, not the working directory to the staging area.

### Step 5 , Commit

```
git commit -m "Add communication guidelines and update table of contents"
```

### Step 6 , One More Small Change

The team lead sends you a quick message: "Can you add your name as the handbook maintainer at the bottom?"

Open `README.md` and add at the very end:

```
---

**Maintainer:** [Your Name]
**Last Updated:** [Today's Date]
```

Now check:

```
git status
git diff
```

Stage it and commit with a different message:

```
git add README.md
git commit -m "Add maintainer info to README"
```

---

## Verify

```bash
# Should show three commits
git log --oneline

# Should show all three messages, newest first
git log --format="%s"
```

You should see three commits, each with a clear, descriptive message.

---

## What You Just Learned

- `git diff` shows changes in your working directory (unstaged)
- `git diff --staged` shows changes ready to be committed
- You can make multiple changes and commit them separately , this keeps history clean
- Each commit should represent *one logical change*, not "everything I did today"

---

→ Next: [Task 03: Reading History](../03-reading-history/TASK.md)
