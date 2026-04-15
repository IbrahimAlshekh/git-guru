# Theory: Task 12

---

## Section 1: Why Gitflow Exists

GitHub Flow works great when you deploy continuously , every merged PR goes live. But some teams can't (or shouldn't) do that:

- A mobile app that needs App Store review
- An enterprise product with quarterly releases
- A library that maintains multiple supported versions
- A project where releases need QA testing before shipping

These teams need a way to:
1. Develop new features continuously
2. Stabilize a set of features for release without blocking new development
3. Fix production emergencies without waiting for the next release

Gitflow solves all three by giving each concern its own branch type.

## The Gitflow Model

Vincent Driessen published this model in 2010. It defines five branch types:

```
main  ─────●──────────────────●──────────●──────
            \                / \        / \
release      \        release/  \  hotfix  \
              \        v1.0 /    \   /      \
develop  ──────●──●──●─────●──●───●─●──●──●──
               /  \       /  \
feature    feat/  feat/  feat/ feat/
           auth   ui     api   dashboard
```

**`main`** , Always reflects the current production state. Every commit on main is a release (tagged with a version).

**`develop`** , The integration branch. Features merge here. When develop is "ready enough," a release branch is cut.

**`feature/*`** , Individual features. Branch from develop, merge back to develop. Short-lived , days to weeks, not months.

**`release/*`** , Created when develop has enough features for a release. Only bug fixes and version bumps happen here. When ready, it merges into both main (for deployment) and develop (so fixes aren't lost).

**`hotfix/*`** , Emergency fixes for production. Branch from main, fix the issue, merge into both main and develop.

## Gitflow vs GitHub Flow

| | GitHub Flow | Gitflow |
|--|------------|---------|
| Long-lived branches | 1 (main) | 2 (main + develop) |
| Deploy frequency | Every merge to main | Scheduled releases |
| Complexity | Low | Medium-high |
| Release prep | None , main is always deployable | Dedicated release branches |
| Emergency fixes | Fix on a branch, merge to main | Hotfix branch with dual merge |
| Best for | Web apps, SaaS, CI/CD | Versioned software, scheduled releases |

## Honest Note

Gitflow is powerful but heavy. Many teams adopted it because it was popular, not because they needed it. If your team deploys continuously and doesn't maintain versions, GitHub Flow (or trunk-based development) is simpler and faster. Use Gitflow when you genuinely need its structure , not as a default.

That said, understanding Gitflow is valuable even if you don't use it, because many established projects and companies do. The concepts of release branches and hotfix lanes transfer to other workflows.
