# Theory: Task 06

Read each section only when the task tells you to.

---

## Section 1: Anatomy of a Conflict

When Git can't automatically merge, it writes **conflict markers** directly into the file:

```
<<<<<<< HEAD
(what's currently in the branch you're merging INTO)
=======
(what's in the branch you're merging FROM)
>>>>>>> branch-name
```

Three regions:

1. **`<<<<<<< HEAD`** to **`=======`** → The current branch's version (what you had before the merge)
2. **`=======`** to **`>>>>>>> branch-name`** → The incoming branch's version (what you're trying to merge in)
3. Everything *outside* the markers → Lines where Git successfully merged automatically

Your job is to replace the entire block (including the markers) with the final version you want. You can choose one side, the other side, a combination, or something completely new. Git doesn't care, it just needs you to remove the markers and save a file that makes sense.

### Why Conflicts Happen

Git is actually very good at merging. It can handle two branches editing the same file, even the same function, as long as they don't touch the exact same lines. Conflicts only occur when:

- Two branches modify the same line(s)
- One branch modifies lines that the other branch deleted
- Both branches add content at the exact same location

In practice, conflicts happen far less often than beginners fear. And when they do, they're usually small, a few lines, not entire files.

### The Emotional Part

Conflicts feel like Git is broken or angry. It's not. It's just saying: "I can't decide this for you." That's actually respectful, Git refuses to guess because guessing could destroy someone's work. A conflict is Git asking for human judgment, and that's exactly right.
