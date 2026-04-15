# Theory: Task 01

Read each section only when the task tells you to.

---

## Section 1: The Three States

Every file in a Git repository lives in one of three states:

**Working Directory** → This is just your folder. The files you see in your file explorer. When you edit a file, the change lives here and *only* here until you do something about it.

**Staging Area** (also called "index") → This is a draft of your next commit. When you run `git add`, you're saying: "I want this specific change to be in my next snapshot." You can add some files and not others. You can even add parts of a file. The staging area gives you control over *exactly what goes into each commit*.

**Repository** (the `.git` folder) → This is where committed snapshots live permanently. Once something is committed, it's safe. You can always get it back.

The flow is always:

```
Working Directory  →  Staging Area  →  Repository
     (edit)          (git add)       (git commit)
```

This three-step process might feel annoying at first , "why can't I just save?" , but it exists for a reason. It lets you make a messy set of changes in your working directory, then *organize* them into clean, logical commits.

Think of it like cooking: your working directory is the messy kitchen, the staging area is the plated dish you're composing, and the commit is the finished plate you serve.

---

## Section 2: What Is a Commit, Really?

A commit is **a snapshot of your entire project at one moment in time**. Not a diff. Not "the changes you made." A full snapshot.

This surprises most people. When you commit, Git doesn't store "you added 3 lines to README.md." It stores the *complete state* of every tracked file. (Internally, Git is clever about not duplicating unchanged files, but conceptually , it's a snapshot.)

Every commit has:

- **A unique ID** (a long hash like `a1b2c3d4...`) , this is the commit's fingerprint
- **A pointer to its parent** , the commit that came before it
- **The snapshot** , the state of all your files
- **Metadata** , who made it, when, and the commit message

Because each commit points to its parent, commits form a **chain**:

```
[commit 1] ← [commit 2] ← [commit 3]
```

This chain is the history of your project. It's also the foundation of everything else in Git , branches, merges, rebases , they all manipulate this chain.

The commit message is your note to the future. "Fixed stuff" tells no one anything. "Add initial README for the Developer Handbook" tells you exactly what that snapshot represents, even months later.

---

## Key Takeaway

When you ran `git add` and then `git commit`, you didn't just "save your file." You:

1. Told Git which changes to include (staging)
2. Took a permanent snapshot of those changes (committing)
3. Added a link in the chain of history (parent pointer)

Everything in Git builds on this.
