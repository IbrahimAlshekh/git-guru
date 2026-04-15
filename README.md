# Git & Gitflow , Learn by Building

A hands-on, task-based learning path for Git and Gitflow. You learn by building a **Developer Handbook** from scratch , one task at a time, each introducing new Git concepts through realistic scenarios.

No slides. No lectures. You do the work, Git does its thing, and then you understand *why*.

---

## Who This Is For

- **Newcomers** who have never used Git (start at Task 01)
- **Mid-level learners** who use Git but don't really understand it (start at Task 04 or wherever your knowledge gets shaky)
- **Anyone** who memorized commands but panics when something goes wrong

## What You'll Build

A team Developer Handbook , a collection of Markdown files that grows across all 15 tasks. By the end, you'll have a real documentation project with branching history, merged features, releases, and hotfixes. The handbook is the vehicle; Git mastery is the destination.

## Prerequisites

- A terminal (Warp terminal is recommended,but Terminal on Mac, WSL or Git Bash on Windows, any Linux terminal)
- Git installed ([git-scm.com/downloads](https://git-scm.com/downloads))
- A text editor (VS Code recommended, but anything works)
- A GitHub account (needed from Task 09 onward)

**That's it.** No programming language, no framework, no build tools.

## How It Works

### Structure

Each task lives in `tasks/XX-task-name/` and contains:

| File | Purpose |
|------|---------|
| `TASK.md` | The scenario and what you need to do , read this first |
| `THEORY.md` | Just-in-time explanation , read *when the task tells you to* |

### Rules

1. **Do the tasks in order.** Each one builds on the previous.
2. **Read THEORY.md only when the task says to.** Not before. Do first, understand after.
3. **Don't skip the checkpoints.** Each task has a "Verify" section. Run those commands before moving on.
4. **Work in the `handbook/` directory.** That's your project. The `tasks/` folder is your guide , don't edit it.
5. **If you get stuck**, the `solutions/` directory has expected outputs for each task. Use it to get unstuck, not to skip ahead.

### The Three Tiers

| Tier | Tasks | What You Learn |
|------|-------|----------------|
| **Solo Git** | 01–08 | Everything you need to work alone with Git |
| **Collaboration** | 09–11 | Remotes, pushing, pulling, working with others |
| **Gitflow** | 12–15 | The Gitflow branching model for structured teams |

You can stop after any tier and be better than when you started.

---

## Quick Start

```bash
# Clone this project
git clone <repository-url> git-guru
cd git-guru

# Open the first task
cat tasks/01-first-commit/TASK.md
# Or open it in your editor

# Start working in the handbook/ directory
cd handbook
```

> **Important:** The `handbook/` directory is where you do all your work. You'll initialize a *separate* Git repository inside it. This outer project is just the learning material.

---

# Handbook Directory

This is your workspace. You'll initialize a Git repository here and build the Developer Handbook step by step.

**Do not edit anything in the `tasks/` directory , that's your guide.**

Start with Task 01: `../tasks/01-first-commit/TASK.md`

> Delete this file before starting Task 01 , the task will have you create the real README.md from scratch.


## Start Here

→ [Task 01: First Commit](tasks/01-first-commit/TASK.md)
