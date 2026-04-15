# Theory: Task 02

---

## Section 1: Reading a Diff

When you run `git diff`, Git shows you a **unified diff**. Here's how to read it:

```
diff --git a/README.md b/README.md
index 3a4c5d6..7b8e9f0 100644
--- a/README.md
+++ b/README.md
@@ -8,10 +8,10 @@
 ## What's Inside

-This handbook will contain:
-- Coding standards and style guides
-- Team workflows and processes
+- [Communication Guidelines](#communication-guidelines), How we communicate
+- Coding Standards (coming soon)
+- Git Workflow (coming soon)
```

Line by line:

- `---` and `+++` show the "old" and "new" versions of the file
- `@@` shows *where* in the file the change is (line numbers)
- Lines starting with `-` were **removed** (old version)
- Lines starting with `+` were **added** (new version)
- Lines with no prefix are **context**, unchanged lines shown for reference

The key insight: **`git diff` compares two states**. Which two states depends on how you call it:

| Command | Compares |
|---------|----------|
| `git diff` | Working directory ↔ Staging area |
| `git diff --staged` | Staging area ↔ Last commit |
| `git diff HEAD` | Working directory ↔ Last commit |

This three-way comparison maps directly to the three states from Task 01. The staging area sits *between* your working directory and your commits, and `diff` lets you inspect each boundary.

---

## Why Separate Commits Matter

You made three commits across Tasks 01 and 02 instead of one big one. This seems like extra work, but consider: six months from now, if something breaks, you want to find *which specific change* caused the problem. A commit message that says "Add communication guidelines and update table of contents" points you right to it. A commit that says "Initial work" or "Various updates" is useless.

Good commit practice: **each commit should be one logical unit of work.** If you can't describe it in one short sentence, it's probably doing too much.
