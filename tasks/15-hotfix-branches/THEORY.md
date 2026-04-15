# Theory: Task 15

---

## Section 1: The Complete Picture

Here's the full Gitflow model as you've now experienced it:

```
main     ─────●────────────────────v1.0.0───v1.0.1────
               \                  /    \    /
release         \          release/   hotfix/
                 \          v1.0  \   v1.0.1
develop  ─────────●──●──●──●──●───●──●──●──●──────
                  / \    /
feature      feat/ feat/
             trbl  gloss
```

### The Flow at a Glance

1. **Features** flow into `develop` (from left to right, bottom)
2. **Releases** fork from `develop`, stabilize, then merge into both `main` and `develop`
3. **Hotfixes** fork from `main`, fix production, then merge into both `main` and `develop`
4. **Tags** mark every release on `main`

### The Dual-Merge Pattern

Both release and hotfix branches merge into TWO targets. This is the most common mistake teams make when starting Gitflow, they forget one of the merges:

| If you forget to merge into... | What happens |
|-------------------------------|-------------|
| `main` (release) | The release never reaches production |
| `develop` (release) | Bug fixes from the release are lost in the next release |
| `main` (hotfix) | The production fix never reaches production |
| `develop` (hotfix) | The fix gets overwritten by the next release |

Always merge into both. No exceptions.

### When You Don't Need Gitflow

Gitflow was designed for a world of scheduled releases. If your reality is:

- You deploy every PR to production (continuous deployment)
- You only maintain one version at a time
- Your team is small (< 5 developers)
- Your release cycle is days, not weeks or months

...then Gitflow adds overhead without proportional benefit. Consider:

**GitHub Flow**, `main` + feature branches + pull requests. Simple, fast, no ceremony.

**Trunk-Based Development**, Everyone commits to `main` (or very short-lived branches). Relies on feature flags and strong CI. The simplest model, but demands engineering discipline.

### The Real Takeaway

Gitflow is a tool, not a rule. Now that you understand it, you can choose when to use it, when to simplify, and how to adapt it for your team's needs. The underlying Git skills, branching, merging, conflict resolution, history management, are universal. The workflow is a choice.
