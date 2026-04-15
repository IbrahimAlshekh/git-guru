# Task 06: Merge Conflicts

## The Scenario

Two team members edited the **same section** of the handbook at the same time. One updated the standup meeting time. The other rewrote the meeting guidelines entirely. When you try to merge, Git can't decide which version wins. That's a **conflict**, and it's your job to resolve it.

This is the task most beginners fear. By the end of it, you won't.

---

## What to Do

### Step 1, Create the First Branch

```bash
git switch main
git switch -c update-meeting-time
```

Open `README.md` and find the Meetings section under Communication Guidelines. Change the standup time:

```
### Meetings
- Daily standup: 9:30 AM, 15 minutes maximum
- All meetings must have an agenda shared at least 1 hour in advance
- No meeting Wednesdays, this is focus time
```

(You changed 9:15 to 9:30)

Commit:

```bash
git add README.md
git commit -m "Update standup time to 9:30 AM"
```

### Step 2, Create the Second Branch (From Main)

Switch back to `main`, **not** from `update-meeting-time`:

```bash
git switch main
git switch -c rewrite-meetings
```

Now edit the *same* Meetings section with a completely different rewrite:

```
### Meetings
- Daily sync: 10:00 AM (async standup on Slack before 9 AM)
- Weekly team retro: Fridays 3:00 PM
- All meetings require a shared agenda, no agenda, no meeting
- Focus blocks: No meetings Tuesday and Thursday mornings
```

Commit:

```bash
git add README.md
git commit -m "Rewrite meeting guidelines with new format"
```

### Step 3, Merge the First Branch Into Main

```bash
git switch main
git merge update-meeting-time
```

This works fine, fast-forward, no conflict.

### Step 4, Now Merge the Second Branch

```bash
git merge rewrite-meetings
```

**This fails.** Git says: `CONFLICT (content): Merge conflict in README.md`

Don't panic. Run:

```bash
git status
```

It tells you which files have conflicts.

### Step 5, Look at the Conflict

Open `README.md` in your editor. Find the conflict markers:

```
<<<<<<< HEAD
- Daily standup: 9:30 AM, 15 minutes maximum
- All meetings must have an agenda shared at least 1 hour in advance
- No meeting Wednesdays, this is focus time
=======
- Daily sync: 10:00 AM (async standup on Slack before 9 AM)
- Weekly team retro: Fridays 3:00 PM
- All meetings require a shared agenda, no agenda, no meeting
- Focus blocks: No meetings Tuesday and Thursday mornings
>>>>>>> rewrite-meetings
```

> 📖 **Stop and read** [THEORY.md](THEORY.md) **, Section 1: Anatomy of a Conflict**

### Step 6, Resolve the Conflict

You need to **manually edit the file** to contain what you actually want. Remove the conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`) and write the final version.

For this exercise, combine the best of both, use the new format but keep the updated time:

```
### Meetings
- Daily sync: 9:30 AM (async standup on Slack before 9 AM)
- Weekly team retro: Fridays 3:00 PM
- All meetings require a shared agenda, no agenda, no meeting
- Focus blocks: No meetings Tuesday and Thursday mornings
```

Save the file.

### Step 7, Complete the Merge

```bash
# Mark the file as resolved
git add README.md

# Finish the merge
git commit
```

Git will provide a default merge commit message. Accept it.

### Step 8, Clean Up

```bash
git branch -d update-meeting-time
git branch -d rewrite-meetings
```

These branches are merged and no longer needed.

---

## Verify

```bash
# Should show a clean working directory
git status

# Should show the merge commit and the branch diamond
git log --oneline --graph -6

# Verify the file has no conflict markers
grep "<<<" README.md
# Should return nothing
```

---

## What You Just Learned

- Conflicts happen when two branches edit the same lines, this is **normal**
- Git marks conflicts with `<<<<<<<`, `=======`, `>>>>>>>`, you choose what stays
- After resolving, `git add` marks the file resolved, `git commit` finishes the merge
- Conflicts are not errors, they're Git asking for your judgment
- `git branch -d` deletes branches that have been merged

---

→ Next: [Task 07: Undoing Mistakes](../07-undoing-mistakes/TASK.md)
