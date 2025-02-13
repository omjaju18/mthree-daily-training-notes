# Git & GitHub Guide  

## Introduction  
Git is a distributed version control system that helps track changes in source code during software development. GitHub is a cloud-based platform that provides repositories to host and collaborate on Git projects.

This guide covers essential Git commands and their explanations to help you effectively use Git and GitHub.

---

## 🔹 **Setting Up Git**  
Before using Git, configure your identity:

```sh
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```
🔹 *Sets your username and email for Git commits.*

Check your Git configuration:  
```sh
git config --list
```
🔹 *Displays the configured Git settings.*

---

## 🔹 **Initializing a Git Repository**  
```sh
git init
```
🔹 *Creates a new Git repository in the current directory.*

---

## 🔹 **Cloning an Existing Repository**  
```sh
git clone <repository_url>
```
🔹 *Copies an existing Git repository from GitHub to your local machine.*

Example:
```sh
git clone https://github.com/omjaju18/my-project.git
```

---

## 🔹 **Checking Repository Status**  
```sh
git status
```
🔹 *Shows the current state of your working directory and staged files.*

---

## 🔹 **Adding Changes to Staging Area**  
```sh
git add <file>
```
🔹 *Stages a specific file for commit.*

```sh
git add .
```
🔹 *Stages all modified and new files.*

---

## 🔹 **Committing Changes**  
```sh
git commit -m "Your commit message"
```
🔹 *Saves changes with a meaningful commit message.*

---

## 🔹 **Viewing Commit History**  
```sh
git log
```
🔹 *Displays a list of commits in the repository.*

```sh
git log --oneline
```
🔹 *Shows commit history in a compact format.*

---

## 🔹 **Checking Differences**  
```sh
git diff
```
🔹 *Shows unstaged changes between working directory and last commit.*

```sh
git diff --staged
```
🔹 *Displays staged changes ready to be committed.*

---

## 🔹 **Branching in Git**  

### Creating a New Branch  
```sh
git branch <branch_name>
```
🔹 *Creates a new branch.*

Example:
```sh
git branch feature-branch
```

### Switching to a Branch  
```sh
git checkout <branch_name>
```
🔹 *Switches to an existing branch.*

```sh
git switch <branch_name>
```
🔹 *Alternative command to switch branches (Git 2.23+).*

### Creating & Switching to a New Branch  
```sh
git checkout -b <branch_name>
```
or  
```sh
git switch -c <branch_name>
```
🔹 *Creates and switches to a new branch.*

### Listing All Branches  
```sh
git branch
```
🔹 *Displays all local branches.*

```sh
git branch -r
```
🔹 *Shows remote branches.*

```sh
git branch -a
```
🔹 *Lists all local and remote branches.*

### Deleting a Branch  
```sh
git branch -d <branch_name>
```
🔹 *Deletes a branch if merged.*

```sh
git branch -D <branch_name>
```
🔹 *Forces branch deletion, even if not merged.*

---

## 🔹 **Merging Branches**  
```sh
git merge <branch_name>
```
🔹 *Merges the specified branch into the current branch.*

Example:
```sh
git checkout main
git merge feature-branch
```

---

## 🔹 **Undoing Changes**  

### Undo Changes in a File  
```sh
git checkout -- <file>
```
🔹 *Reverts changes in a file to the last committed version.*

### Reset Staged Files  
```sh
git reset <file>
```
🔹 *Removes a file from the staging area (but keeps changes).*

### Reset to a Previous Commit  
```sh
git reset --soft <commit_hash>
```
🔹 *Moves HEAD to an older commit but keeps changes staged.*

```sh
git reset --hard <commit_hash>
```
🔹 *Resets to a specific commit and removes all changes.*

---

## 🔹 **Working with Remote Repositories**  

### Adding a Remote Repository  
```sh
git remote add origin <repository_url>
```
🔹 *Links the local repository to a remote GitHub repository.*

### Viewing Remote Repositories  
```sh
git remote -v
```
🔹 *Lists remote repositories.*

### Pushing Changes to GitHub  
```sh
git push origin <branch_name>
```
🔹 *Uploads local branch commits to GitHub.*

Example:
```sh
git push origin main
```

### Pulling Updates from GitHub  
```sh
git pull origin <branch_name>
```
🔹 *Fetches changes from GitHub and merges them into the local branch.*

Example:
```sh
git pull origin main
```

### Fetching Changes Without Merging  
```sh
git fetch origin
```
🔹 *Retrieves changes from GitHub but does not merge them.*

---

## 🔹 **Stashing Changes**  
```sh
git stash
```
🔹 *Temporarily saves uncommitted changes without committing them.*

```sh
git stash pop
```
🔹 *Applies stashed changes and removes them from stash list.*

```sh
git stash list
```
🔹 *Shows all saved stashes.*

```sh
git stash drop
```
🔹 *Deletes the most recent stash.*

---

## 🔹 **Rebasing a Branch**  
```sh
git rebase <branch_name>
```
🔹 *Reapplies commits on top of another base commit.*

Example:
```sh
git checkout feature-branch
git rebase main
```

## 🔹 **Deleting Remote Branches**  
```sh
git push origin --delete <branch_name>
```
🔹 *Removes a remote branch from GitHub.*

---

# **Git Merge Conflicts: How to Solve and Avoid Them**

## **What is a Merge Conflict in Git?**  
A **merge conflict** occurs when Git is unable to automatically merge changes from two branches due to conflicting modifications in the same file or line of code. This happens when:

- Two branches modify the same line in a file differently.
- One branch deletes a file that another branch modified.

Git tries to merge the changes, but when it detects conflicts, it stops and asks for manual resolution.

---

## **Example of a Merge Conflict**
### **Scenario:**  
1. You have two branches: `main` and `feature-branch`.
2. Both branches modify the same line in `index.html`.
3. When merging, Git detects the conflict and stops the process.

### **Conflicting File (Before Resolving)**
Git marks conflicting sections in the file like this:

```html
<<<<<<< HEAD
<h1>Welcome to My Website</h1>
=======
<h1>Welcome to Our Website</h1>
>>>>>>> feature-branch
```

**Explanation:**
- `<<<<<<< HEAD` → Code from the current branch (`main`).  
- `=======` → Separator between conflicting changes.  
- `>>>>>>> feature-branch` → Code from the other branch (`feature-branch`).  

---

## **How to Resolve a Merge Conflict?**

### **Step 1: Identify Conflicts**
Run:
```sh
git status
```
Git will show:
```
Unmerged paths:
  (use "git add <file>" to mark resolution)
	both modified:   index.html
```

### **Step 2: Open the Conflicted File**
- Open `index.html` and **manually** choose the correct version.
- Either **keep one** or **merge both**.

#### ✅ Example Resolved File:
```html
<h1>Welcome to My Awesome Website</h1>
```

---

### **Step 3: Mark Conflict as Resolved**
After editing, **add the resolved file**:
```sh
git add index.html
```

### **Step 4: Complete the Merge**
```sh
git commit -m "Resolved merge conflict in index.html"
```

---

## **Aborting a Merge (If Needed)**
If you want to cancel the merge:
```sh
git merge --abort
```
🔹 This resets the branch to its previous state.

---

## **Best Practices to Avoid Merge Conflicts**

1. **Pull before making changes:**  
   ```sh
   git pull origin main
   ```
   Always pull the latest changes before starting new work.

2. **Use feature branches:**  
   Work in separate branches and merge frequently.

3. **Communicate with teammates:**  
   Avoid working on the same file at the same time.

4. **Resolve conflicts early:**  
   Merge changes **frequently** instead of waiting too long.

---

## **Summary**

| Action | Command |
|--------|---------|
| **Check for conflicts** | `git status` |
| **Resolve conflict manually** | Edit the file |
| **Mark as resolved** | `git add <file>` |
| **Commit resolution** | `git commit -m "Resolved merge conflict"` |
| **Abort merge (if needed)** | `git merge --abort` |
| **Avoid conflicts (best practice)** | `git pull` before coding, use feature branches, commit frequently |

---

## 🚀 **Conclusion**  
This guide covers essential Git commands used in day-to-day development. With these commands, you can manage your code efficiently, collaborate with teams, and track project history effectively.

For more details, visit:  
🔗 [Git Documentation](https://git-scm.com/doc)

---
