# Theory: Task 14

Read each section only when the task tells you to.

---

## Section 1: The Release Branch Lifecycle

A release branch exists in three phases:

### Phase 1: Creation
Cut from `develop` when you decide "we have enough features for a release." At this moment, develop is forked:

```
develop  ──●──●──●──●──
                       \
release/v1.0.0          ●
```

Development continues on `develop`. The release branch only accepts bug fixes and version bumps.

### Phase 2: Stabilization
QA tests the release branch. Bugs found during testing get fixed here:

```
develop  ──●──●──●──●──●──●──  (new features continue)
                       \
release/v1.0.0          ●──●──●  (only bug fixes)
```

This is the key benefit: **new features don't destabilize the release.** If a teammate merges a big feature into develop tomorrow, it doesn't affect v1.0.0.

### Phase 3: Completion
The release branch merges into two places:

```
main     ────────────────────M ← tag: v1.0.0
                            /
develop  ──●──●──●──●──●──M──  (gets the bug fixes)
                       \  /
release/v1.0.0          ●──●──●
```

1. **Into `main`**, because main represents production
2. **Back into `develop`**, so bug fixes from the release aren't lost

Then the release branch is deleted. Its purpose is served.

### Why Two Merges?

Imagine a release branch fixes a typo. If you only merge to `main`, develop still has the typo. Every future release cut from develop would carry that bug. The back-merge to develop prevents this.

### Tags

Tags are like branches that never move. `v1.0.0` will always point to the exact commit that was released. Unlike branches, tags don't advance when new commits are made. They're permanent bookmarks in history.

Use annotated tags (`-a` flag) for releases, they store the tagger's name, date, and a message. Lightweight tags (no `-a`) are just pointers, fine for personal bookmarks but not for releases.
