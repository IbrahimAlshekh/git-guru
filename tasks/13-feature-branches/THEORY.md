# Theory: Task 13

---

## Section 1: Why --no-ff?

By default, if Git can do a fast-forward merge (when the target branch hasn't diverged), it will , just moving the pointer forward. No merge commit.

```
Fast-forward (default):
A ← B ← C ← D ← E  (develop, feature/glossary)
```

With `--no-ff`:

```
No-fast-forward:
A ← B ← C ← D ← M  (develop)
              ↖ ↗
                E  (feature/glossary)
```

The `--no-ff` flag forces Git to create a merge commit even when fast-forward is possible. Why bother?

**Traceability.** The merge commit records that a feature branch existed and when it was integrated. Without it, the feature commits just blend into the develop history , you can't tell where a feature started and ended.

**Reversibility.** If a feature turns out to be broken, you can revert the single merge commit to undo the entire feature. With fast-forward, you'd have to revert each individual commit.

**Convention.** Gitflow uses `--no-ff` by design. Every feature merge is a visible event in the graph. This creates the "railroad track" pattern that makes Gitflow history recognizable.

Most teams configure this as a default:

```bash
git config --global merge.ff false
```

Or enforce it through GitHub's merge button settings (select "Create a merge commit" instead of "Squash and merge" or "Rebase and merge").
