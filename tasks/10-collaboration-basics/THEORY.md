# Theory: Task 10

---

## Section 1: GitHub Flow

GitHub Flow is the simplest collaborative workflow. It has one rule: **anything on `main` is deployable**. Everything else happens on branches.

The cycle:

```
1. Pull latest main
2. Create a branch
3. Do your work (commits)
4. Push the branch
5. Open a Pull Request
6. Get reviewed
7. Merge to main
8. Delete the branch
```

That's it. No `develop` branch, no release branches, no version numbers. Just `main` + feature branches + pull requests.

### Why Pull Requests?

A Pull Request (PR) is not a Git feature , it's a GitHub feature (other platforms call them Merge Requests). It's a way to say: "I'd like to merge this branch into main. Can someone review it first?"

PRs provide:
- **Code review** , someone else reads your changes before they go live
- **Discussion** , a place to ask questions and suggest improvements
- **CI/CD integration** , automated tests can run on every PR
- **History** , a record of *why* a change was made, not just *what*

### When GitHub Flow Works

GitHub Flow is great for teams that deploy continuously , web apps, SaaS products, anything where you ship often. It's simple, fast, and has low ceremony.

It's less ideal for projects that need to maintain multiple versions simultaneously (e.g., a library that supports v1 and v2) or projects with complex release schedules. That's where Gitflow comes in , Tier 3.

---

## The Push Rejection Problem

If you and a teammate both push to `main` at the same time, one of you will get rejected:

```
! [rejected] main -> main (non-fast-forward)
```

This means the remote has commits you don't have. Fix it by pulling first:

```bash
git pull
# (resolve any conflicts if needed)
git push
```

This is normal. It's not an error , it's Git preventing you from overwriting someone else's work.
