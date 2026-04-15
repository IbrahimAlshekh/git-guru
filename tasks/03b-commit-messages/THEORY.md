# Theory: Task 03b

Read each section only when the task tells you to.

---

## Section 1: The Anatomy of a Good Commit Message

A commit message is not a note to yourself about what you just did. It is a message to whoever reads this repository in the future — including you, six months from now, when you have completely forgotten the context.

The test of a good commit message is simple: can someone read it in `git log` and understand what happened and why, without opening the code?

### What makes a message bad

```
fix
update
wip
done
changes
minor fix
```

These messages describe *effort*, not *outcome*. They tell you that something happened, not what. When you are hunting down a bug that was introduced three months ago, messages like these are useless. You have to open every commit and read the diff.

### What makes a message good

```
Add code of conduct to the Developer Handbook
Fix broken internal link in the README
Remove outdated Windows setup instructions
Clarify the review process in contributing guidelines
```

These messages describe *what changed in the project*. You can read them in a list and understand the story of the project without opening a single file.

### The imperative mood

Git itself uses the imperative mood in its own generated messages:

- `Merge branch 'feature/x' into main`
- `Revert "Add initial README for the Developer Handbook"`
- `Initial commit`

Your messages should fit naturally into this pattern. Write as if you are commanding the codebase: "Add this", "Fix that", "Remove the other thing."

A simple test: your message should complete the sentence — *"If applied, this commit will..."*

- "If applied, this commit will **add contributing guidelines**." ✓
- "If applied, this commit will **added contributing guidelines**." ✗

---

## Section 2: Subject Line, Blank Line, Body

A commit message has two parts. You have only been using the first one.

### The subject line

The first line of your commit message. Keep it:

- **Under 50 characters** — most Git tools truncate at 72, but 50 is the target for clean display in `git log --oneline`
- **Capitalized** — "Add contributing guidelines", not "add contributing guidelines"
- **No period at the end** — it is a title, not a sentence
- **Imperative mood** — "Add", not "Added" or "Adding"

### The blank line

When you write a commit message in your editor (without `-m`), leave the second line completely blank. This separates the subject from the body. Git uses this blank line to distinguish the two parts. Without it, tools that read commit messages get confused.

### The body

Not every commit needs a body. A simple change — fixing a typo, renaming a file — probably does not. But when the *why* is not obvious from the subject line alone, add a body.

The body is for:
- **Why** you made the change, not *what* you changed (the diff already shows what)
- Context that will not be obvious later
- Trade-offs you considered
- References to issues, tickets, or discussions

```
Add contributing guidelines to the handbook

Establishes the expected workflow for team contributions and documents
the commit message conventions the team will follow going forward.

Without this, new contributors have no reference for how to submit
changes or what kind of commit messages the team expects.
```

Wrap body lines at 72 characters. This keeps them readable in terminals and Git tools without horizontal scrolling.

---

## Section 3: Using Bullet Points in the Body

Sometimes a commit covers more than one related change — a few fixes, a few additions that belong together. In that case, a bullet list in the body is cleaner than a paragraph.

The structure is always the same: short subject line, blank line, then the list.

```
Update handbook structure and onboarding section

- Add table of contents to README
- Rewrite the onboarding steps for clarity
- Remove outdated Windows-specific instructions
- Fix broken link to the code of conduct
```

This works well when:
- You made several small changes that are logically one "unit of work"
- A paragraph would be harder to scan than a list
- You want readers to quickly see what was touched

It does **not** mean you should bundle unrelated changes into one commit just to write a list. Each commit should still be one focused thing. The bullet points describe the parts of that one thing — not several different things.

A quick comparison:

```
# Too vague — no list, no context
Update docs

# Too much in one commit — these are three different concerns
Fix auth bug, update README, bump version number

# Just right — one concern, multiple parts clearly listed
Improve the onboarding section of the handbook

- Rewrite Step 1 with clearer terminal instructions
- Add a note about the handbook/ directory purpose
- Remove the placeholder text from the prerequisites section
```

---

## Why This Matters More Than You Think

Imagine you are debugging a production issue. You know the bug was introduced sometime in the last three months. You have 200 commits to look through.

With bad messages:
```
fix
update
minor changes
wip
done
fix again
more updates
```

You have to open every single commit and read the diff.

With good messages:
```
Add caching layer to the user profile endpoint
Increase session timeout from 30 to 60 minutes
Fix race condition in the authentication middleware
Update error handling in the payment service
```

You can read the list and immediately narrow it down to two or three candidates.

`git log` is a search tool as much as it is a history viewer. Good commit messages make that search fast. Bad ones make it painful.

---

## Key Takeaway

- Subject line: imperative, under 50 characters, no period
- Blank line between subject and body
- Body: explain *why*, not *what*; wrap at 72 characters
- Not every commit needs a body — but when context matters, add it
- You are writing for your future self and for your teammates
