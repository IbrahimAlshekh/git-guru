# Theory: Task 09

---

## Section 1: What Is a Remote?

A remote is just a URL pointing to another copy of the repository. When you run `git remote add origin <url>`, you're telling Git: "There's another version of this repo at this address. Call it `origin`."

`origin` is a convention, not a requirement. You could call it `github` or `backup` or anything. But almost everyone calls the primary remote `origin`.

Your local repo and the remote are **independent copies**. They don't automatically stay in sync. You explicitly push (send your commits) and pull (get their commits). This is deliberate , it means you can work offline, make commits, and sync up later.

The graph with a remote looks like this:

```
Local:
A ← B ← C ← D ← E  (main)
               ↑
          (origin/main)  ← "last time I checked, the remote was here"

Remote (GitHub):
A ← B ← C ← D  (main)
```

After `git push`:

```
Local:
A ← B ← C ← D ← E  (main, origin/main)

Remote:
A ← B ← C ← D ← E  (main)
```

Now they match. `origin/main` moved forward because you told the remote about your new commits.

---

## Section 2: Fetch vs Pull

This distinction confuses many people, but it's simple once you see it.

**`git fetch`** , Downloads new commits from the remote and updates your remote tracking branches (`origin/main`). Does NOT touch your local branches or working directory. It's a safe "let me see what's new" operation. You can fetch at any time without risk.

**`git pull`** , Does a `fetch` AND then merges the remote changes into your current branch. It's a convenience shortcut: `git pull` = `git fetch` + `git merge origin/main`.

Why would you ever use `fetch` instead of `pull`? Because sometimes you want to *look* before you *merge*. After fetching:

```bash
# See what's new
git log main..origin/main --oneline

# See the actual changes
git diff main origin/main
```

This lets you review before deciding to merge. In practice, most people just `pull` for simple workflows. But knowing that `fetch` exists , and that it's safe , is important when things get complicated.
