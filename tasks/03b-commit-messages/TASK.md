# Task 03b: Writing Commit Messages That Actually Help

## The Scenario

You just ran `git log` and looked at your commit history. Some messages make sense. Some could mean almost anything. Six months from now, a message like "fix stuff" or "updates" tells you nothing about what changed, why, or what to look for if something breaks.

This task is not about learning a new Git command. It is about learning to use the one you already know, `git commit`, in a way that makes your history genuinely useful.

---

## What to Do

### Step 1, See the Problem

Inside your `handbook/` directory, run:

```bash
git log --oneline
```

Look at the messages you have written so far. Ask yourself: if you came back to this project after three months away, would each message tell you *what changed and why*?

Now look at a bad example versus a good one:

```
# Bad
fix bug
update readme
wip
changes
done

# Good
Add initial README for the Developer Handbook
Fix broken link in the contributing section
Clarify onboarding steps for Windows users
```

The bad messages describe effort. The good messages describe *what happened to the project*.

> 📖 **Stop and read** [THEORY.md](THEORY.md) **, Section 1: The Anatomy of a Good Commit Message** before continuing.

---

### Step 2, The One Rule You Must Always Follow

Write commit messages in the **imperative mood**. That means: write the message as if you are giving an instruction to the codebase.

```
# Imperative (correct)
Add contributing guidelines
Fix typo in the code of conduct
Remove outdated onboarding section

# Not imperative (avoid)
Added contributing guidelines
Fixed typo in the code of conduct
Removing outdated onboarding section
```

Why? Because Git itself uses the imperative mood in its own messages: "Merge branch 'feature/x' into main", "Revert 'Add contributing guidelines'". Your messages should blend in naturally with Git's own language.

---

### Step 3, Practice a Proper Commit

Add a new file to your handbook. Create `handbook/CONTRIBUTING.md` with this content:

```markdown
# Contributing Guidelines

We welcome contributions from all team members.

## How to Contribute

1. Create a branch from `main` for your change
2. Make your edits in that branch
3. Open a pull request and describe what you changed and why
4. Wait for at least one review before merging

## Commit Message Guidelines

- Use the imperative mood: "Add", not "Added"
- Keep the subject line under 50 characters
- If the change needs explanation, add a body after a blank line
- Explain *why* the change was made, not just *what* changed
```

Stage it:

```bash
git add CONTRIBUTING.md
```

Now commit it, but this time, write a commit with both a **subject line and a body**:

```bash
git commit
```

This opens your editor (no `-m` flag this time). Write the following, then save and close:

```
Add contributing guidelines to the handbook

Establishes the expected workflow for team contributions and documents
the commit message conventions the team will follow going forward.
```

Notice: the subject line is short and imperative. There is a blank line. The body explains *why* this file exists, not just that it was added.

> 📖 **Stop and read** [THEORY.md](THEORY.md) **, Section 2: Subject Line, Blank Line, Body**

---

### Step 4, Commit with a Bullet List Body

Sometimes one commit touches several related things. Make two small edits to `CONTRIBUTING.md`, for example, add a sentence to one section and adjust the wording in another. Stage everything, then commit using a bullet list body:

```bash
git commit
```

In your editor, write:

```
Improve wording and add detail to contributing guidelines

- Clarify the branch naming suggestion
- Add a reminder to pull latest main before opening a PR
```

Subject line first. Blank line. Then bullets starting with `-`.

> 📖 **Stop and read** [THEORY.md](THEORY.md) **, Section 3: Using Bullet Points in the Body**

---

### Step 5, Compare Bad and Good

Now make a small edit to the `CONTRIBUTING.md`, add one line, change a word, anything. Stage it and write **two different versions** of the commit message in your head before committing:

1. A vague one: something like `"update contributing"` or `"fix"`
2. A clear one: something like `"Clarify pull request review requirement in CONTRIBUTING.md"`

Commit using the clear one.

Then run:

```bash
git log --oneline
```

See the difference in your own history.

---

## Verify

```bash
# Show the full commit, including the body of your message
git show HEAD~1

# Show all commits in one line
git log --oneline
```

Your recent commit should have a clear subject line and a body that explains the reasoning. If it does, you have completed Task 03b.

---

## What You Just Learned

- A commit message is documentation, not just a label
- The imperative mood keeps your messages consistent with Git's own language
- A subject line (short, under 50 characters) and a body (explaining the *why*) are the two parts of a proper commit message
- Writing good messages is a habit, it becomes natural with practice
- Your commit history is something others (and your future self) will read

---

→ Next: [Task 04: Branching Basics](../04-branching-basics/TASK.md)
