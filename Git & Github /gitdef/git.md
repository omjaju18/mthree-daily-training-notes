# Git Rebase Explained

## What is Git Rebase?
Git rebase is a command used to **move or apply commits** from one branch onto another in a linear fashion. It helps maintain a **clean and structured commit history** by avoiding unnecessary merge commits.

---

## How Git Rebase Works
Instead of merging two branches (which creates an additional merge commit), `git rebase` **takes the commits from a branch and applies them on top of another branch**.  

### Example:
Assume this is your branch structure:
```
A---B---C (feature-branch)
     /
D---E---F (main)
```
If you run:
```bash
git checkout feature-branch
git rebase main
```
Git will:
1. Move `feature-branch` to `main`'s latest commit.  
2. Apply commits **B and C** on top of `F`, making it look like:
```
D---E---F---B'---C' (feature-branch rebased)
```
This removes unnecessary merge commits, keeping history linear.

---

## Types of Git Rebase

### 1️⃣ Basic Rebase
Moves a branch’s commits on top of another branch.
```bash
git checkout feature-branch
git rebase main
```

### 2️⃣ Interactive Rebase (`-i`)
Allows **modifying commit history** (reordering, squashing, editing commits).
```bash
git rebase -i HEAD~3
```
It opens an editor where you can:
- `pick` → Keep commit as is  
- `reword` → Change commit message  
- `squash` → Merge commits into one  
- `edit` → Modify commit  

### 3️⃣ Rebase Onto (`--onto`)
Useful when rebasing a branch onto a different base.
```bash
git rebase --onto new-base old-base feature-branch
```
This takes all commits **after `old-base`** and applies them onto `new-base`.

### 4️⃣ Aborting a Rebase
If conflicts occur and you want to cancel:
```bash
git rebase --abort
```

### 5️⃣ Continuing After Conflict
Resolve conflicts, then:
```bash
git add .
git rebase --continue
```

---

## Git Rebase vs Git Merge
| Feature | Git Rebase | Git Merge |
|---------|-----------|-----------|
| History | Linear | Maintains merge history |
| Merge Commit | No merge commits | Creates merge commits |
| Use Case | Clean commit history | Preserving branch history |

### When to Use Git Rebase?
✅ Keeping a clean history  
✅ Updating feature branches before merging  
✅ Avoiding unnecessary merge commits  

### When NOT to Use Git Rebase?
❌ On **shared branches** (rewriting history can cause issues)  
❌ When you need to keep track of merge points  

---

## Real-Life Scenario
You're working on a **feature branch** (`feature-branch`), and `main` has new changes. Instead of merging:
```bash
git checkout feature-branch
git rebase main
```

## Git Stash Explained

### What is Git Stash?
Git stash allows you to **save uncommitted changes** without committing them, so you can work on something else and later restore them. This is useful when you need to:
- Switch branches without committing changes.  
- Temporarily save work-in-progress changes.  
- Clean the working directory without losing progress.  

---

## Basic Git Stash Commands

### 1️⃣ Stash Changes
Saves uncommitted changes and clears the working directory.
```bash
git stash
```

### 2️⃣ List Stashed Changes
To view all stashes:
```bash
git stash list
```

### 3️⃣ Apply Stashed Changes
To restore the most recent stash:
```bash
git stash apply
```

### 4️⃣ Apply and Remove Stash
To restore and delete the stash:
```bash
git stash pop
```

### 5️⃣ Stash with a Message
To stash with a custom message:
```bash
git stash save "Work in progress: Fixing login bug"
```

### 6️⃣ Stash Only Tracked Files
To stash only tracked files, ignoring new untracked files:
```bash
git stash -u
```

### 7️⃣ Stash Only Staged Files
To stash only staged (added) changes:
```bash
git stash --keep-index
```

### 8️⃣ Drop (Delete) a Specific Stash
To delete a specific stash (e.g., `stash@{1}`):
```bash
git stash drop stash@{1}
```

### 9️⃣ Clear All Stashes
To delete all stashed changes:
```bash
git stash clear
```
---

## Forking vs Cloning

| Feature | Forking | Cloning |
|---------|---------|---------|
| Ownership | Creates a copy in your GitHub account | Creates a local copy of a repository |
| Usage | Used for contributing to open-source projects | Used for personal or team development |
| Changes | Must submit pull requests to contribute | Directly push changes if you have access |

---

## Git Branching

Git branching allows developers to work on different features independently.

### Creating a Branch
```bash
git branch feature-branch
```

### Switching to a Branch
```bash
git checkout feature-branch
```
Or, using the new syntax:
```bash
git switch feature-branch
```

### Creating and Switching to a Branch
```bash
git checkout -b new-branch
```

### Deleting a Branch
```bash
git branch -d feature-branch
```

### Listing All Branches
```bash
git branch -a
```

### Merging a Branch
```bash
git checkout main
git merge feature-branch
```

---
# Git Reset vs Git Revert

## **Git Reset** (Undo Commits & Changes)

Imagine you’re writing an essay and suddenly realize you need to remove a few paragraphs. **Git reset** allows you to go back in time and erase commits, as if they never happened.

### **Types of Git Reset**

1. **Soft Reset (`git reset --soft <commit>`)**  
   - Moves the HEAD (current branch pointer) to the specified commit.
   - Keeps all changes in the staging area (ready for commit).
   - Useful if you want to **redo a commit**.

   **Example:**  
   ```bash
   git reset --soft HEAD~1
   ```
   *Moves back one commit, but your changes remain staged.*

2. **Mixed Reset (`git reset --mixed <commit>`)** (Default)  
   - Moves HEAD to the specified commit.
   - Removes commits from history **but keeps changes in the working directory** (not staged).
   - Useful if you want to **edit your changes before recommitting**.

   **Example:**  
   ```bash
   git reset --mixed HEAD~1
   ```
   *Moves back one commit, removes it, but keeps your files untouched.*

3. **Hard Reset (`git reset --hard <commit>`)**  
   - Moves HEAD to the specified commit.
   - **Deletes all changes permanently** (cannot be recovered).
   - Useful if you want to **completely discard changes**.

   **Example:**  
   ```bash
   git reset --hard HEAD~1
   ```
   *Removes the last commit and deletes all changes.*

---

## **Git Revert** (Undo Without Losing History)

Unlike `git reset`, **git revert does NOT delete commits**. Instead, it creates a new commit that undoes the changes from a previous commit.

Imagine you made a mistake in your essay but instead of deleting the paragraph, you add a note correcting it. That’s what `git revert` does.

### **How to Revert a Commit**
```bash
git revert <commit-hash>
```
- Creates a new commit that **reverses** the specified commit.
- The history remains intact, making it safer than `git reset`.

**Example:**  
```bash
git revert HEAD~1
```
*Reverts the last commit by creating a new commit that undoes its changes.*

### **When to Use Git Reset vs Git Revert?**

| Scenario | Use `git reset` | Use `git revert` |
|----------|----------------|------------------|
| Completely remove commits | ✅ Yes | ❌ No |
| Keep commit history clean | ❌ No | ✅ Yes |
| Undo a commit on a shared branch | ❌ No (Dangerous) | ✅ Yes (Safe) |
| Recoverable changes | ❌ No (if hard reset) | ✅ Yes |

---

## **In Short:**
- `git reset` **erases commits** (like deleting a paragraph).
- `git revert` **creates a new commit that undoes changes** (like adding a correction note).  
- **Use `git revert` when working with a team** to avoid history conflicts.

---

