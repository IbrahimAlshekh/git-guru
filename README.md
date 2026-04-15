# Git & Gitflow, Learn by Building

A hands-on, task-based learning path for Git and Gitflow. You learn by building a **Developer Handbook** from scratch, one task at a time, each introducing new Git concepts through realistic scenarios.

No slides. No lectures. You do the work, Git does its thing, and then you understand *why*.

---

## A Few Words from the Author

We are living in a strange and exciting moment. AI agents can now write code, good code, sometimes surprisingly good code. In a single afternoon, you can generate more lines than a team would have produced in a week. But here is the thing: all that code still needs to live somewhere, get versioned, get reviewed, get merged, and eventually get shipped. Without Git, none of that works. The more code AI generates, the more Git matters.

Git has always been the backbone of software projects. There are other version control systems, sure, but Git won the argument long ago. What has changed is the urgency. When a developer writes every line by hand, a shaky understanding of Git is inconvenient. When an AI is generating hundreds of files alongside you, a shaky understanding of Git is a liability. You need to know where things are, what changed, why, and how to walk it back if something goes wrong.

This handbook exists because most learning materials get it backwards. They start with the theory, the object model, the DAG, the plumbing commands, and by the time you reach anything practical, you have already lost interest or forgotten why you started. Here, you learn Git the way you learn most things worth knowing: by doing something real. Each task puts you in a situation, and the Git knowledge you need arrives exactly when you need it. Not before.

There is another thing most tutorials miss. They teach you the commands without teaching you the *thinking*. How to write a commit message that means something six months later. Why a clean history is a form of respect for your future self and your teammates. How to look at a branch and understand the story it tells. That kind of intuition does not come from memorizing flags, it comes from practice with intention.

At some point in this handbook, you will encounter Gitflow. It has its critics, and they are not wrong, it is not the right tool for every project. But understanding it is not optional. Large teams use it. Companies rely on it. And even if you end up preferring a simpler workflow, knowing Gitflow means you can navigate any project you land in.

Finally, this: Git is the one skill that never leaves your day. You might go weeks without touching a sorting algorithm. You might forget the exact syntax for a regex. But from the first command you type in the morning to the last commit before you close your laptop, Git is there. It is worth the time to get genuinely comfortable with it, not just functional, but fluent.

That is what this handbook is for.

---

## Who This Is For

This handbook is for anyone who writes code, or works alongside AI that writes code for them.

**If you have never used Git**, start at Task 01. You will not be thrown into the deep end. Each concept arrives with a reason, and the reason always comes from something you just experienced.

**If you use Git but mostly copy-paste commands from Stack Overflow**, start around Task 04. You already know the surface. This will take you underneath it, to the point where you stop guessing and start knowing.

**If you are comfortable with Git but have never used Gitflow**, jump to Task 12. At some point in your career you will work on a team that uses it. Better to meet it here, on your own terms, than under pressure on a deadline.

**If you are working with AI tools**, Copilot, Cursor, Claude, or anything that generates code alongside you, this is especially for you. The more code you generate, the more critical it is to manage it well. Git is not optional in that world. It is infrastructure.

## What You'll Build

Across all 15 tasks, you will build a **Developer Handbook**, a real documentation project written in Markdown. It starts as a blank directory and grows into something with a branching history, merged features, versioned releases, and a hotfix or two along the way.

The handbook itself is not the point. It is the vehicle. What you are really building is a working mental model of Git, one earned through doing, not through reading about it.

By the end, you will have experienced Git the way developers actually use it: messily at first, then with growing confidence, and finally with the kind of fluency that makes it feel less like a tool and more like a habit.

## What You Need

**Tools:**
- A terminal, Warp is recommended, but any terminal works (Terminal on Mac, WSL or Git Bash on Windows, any Linux shell)
- Git installed, [git-scm.com/downloads](https://git-scm.com/downloads)
- A text editor, VS Code is recommended, but anything you are comfortable with
- A GitHub account, needed from Task 09 onward

**No programming language. No framework. No build tools.**

**Mindset:**
- Willingness to do things before you fully understand them
- Tolerance for making mistakes, that is where most of the learning happens
- Patience with yourself when something breaks, breaking things in Git is almost always fixable

## How It Works

### Structure

Each task lives in `tasks/XX-task-name/` and contains:

| File | Purpose |
|------|---------|
| `TASK.md` | The scenario and what you need to do, read this first |
| `THEORY.md` | Just-in-time explanation, read *when the task tells you to* |

### Rules

1. **Do the tasks in order.** Each one builds on the previous.
2. **Read THEORY.md only when the task says to.** Not before. Do first, understand after.
3. **Don't skip the checkpoints.** Each task has a "Verify" section. Run those commands before moving on.
4. **Work in the `handbook/` directory.** That's your project. The `tasks/` folder is your guide, don't edit it.
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

**Do not edit anything in the `tasks/` directory, that's your guide.**

Start with Task 01: `../tasks/01-first-commit/TASK.md`

> Delete this file before starting Task 01, the task will have you create the real README.md from scratch.


## Start Here

→ [Task 01: First Commit](tasks/01-first-commit/TASK.md)
