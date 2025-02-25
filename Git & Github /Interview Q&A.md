# **Git Theoretical Questions and Answers**  

## **Introduction**  
This document provides a comprehensive list of Git theoretical questions along with detailed answers. It covers fundamental, intermediate, and advanced concepts, making it useful for beginners and experienced developers alike.  

---

## **Basic Git Questions**  

### **1. What is Git?**  
**Answer:**  
Git is a distributed version control system (VCS) that helps developers track changes in code, collaborate with teams, and manage source code efficiently. It allows multiple developers to work on a project simultaneously without overwriting each other's changes.  

### **2. What is a repository in Git?**  
**Answer:**  
A repository (repo) is a storage location that holds the project's files and complete revision history. It can be:  
- **Local Repository:** Stored on your machine.  
- **Remote Repository:** Hosted on services like GitHub, GitLab, or Bitbucket.  

To create a new local repository:  
```sh
git init
```  

To clone an existing remote repository:  
```sh
git clone https://github.com/user/repo.git
```  

### **3. What is the difference between Git and GitHub?**  
**Answer:**  
| Feature | Git | GitHub |
|---------|----|--------|
| Definition | Version Control System | Hosting service for Git repositories |
| Purpose | Tracks changes, manages source code | Enables collaboration, backup, and sharing |
| Accessibility | Works locally | Works online with remote repositories |

### **4. What is a commit in Git?**  
**Answer:**  
A commit is a snapshot of the repository at a specific point in time. Each commit has a unique identifier (SHA) and a message describing the changes.  

Example:  
```sh
git add file.txt
git commit -m "Added a new file"
```  

### **5. What is the difference between `git add` and `git commit`?**  
**Answer:**  
| Command | Purpose |
|---------|---------|
| `git add` | Stages changes for the next commit |
| `git commit` | Saves the staged changes permanently to the repository |

Example:  
```sh
git add file1.txt file2.txt
git commit -m "Added two files"
```  

### **6. What is a branch in Git?**  
**Answer:**  
A branch is an independent line of development. It allows developers to work on new features without affecting the main codebase.  

Example:  
```sh
git branch feature-branch  # Creates a new branch
git checkout feature-branch  # Switch to the new branch
```  

---

## **Intermediate Git Questions**  

### **7. What is the difference between `git pull` and `git fetch`?**  
**Answer:**  
| Command | Description |
|---------|-------------|
| `git pull` | Fetches changes from the remote repository and merges them into the current branch |
| `git fetch` | Only downloads changes from the remote repository without merging |

Example:  
```sh
git fetch origin main  # Retrieves latest changes but doesn't merge
git pull origin main   # Retrieves and merges the latest changes
```  

### **8. What is a merge conflict in Git?**  
**Answer:**  
A merge conflict occurs when Git cannot automatically merge changes due to modifications in the same file on different branches.  

**Steps to resolve:**  
1. Identify conflicts using:  
   ```sh
   git status
   ```
2. Open the conflicting file and manually resolve the differences.  
3. Stage the resolved file:  
   ```sh
   git add file.txt
   ```
4. Commit the resolution:  
   ```sh
   git commit -m "Resolved merge conflict"
   ```  

### **9. What is Git Stash?**  
**Answer:**  
Git stash temporarily saves uncommitted changes, allowing you to work on something else without losing progress.  

Example:  
```sh
git stash        # Stashes current changes
git stash list   # Lists all stashed changes
git stash apply  # Restores the latest stashed changes
```  

### **10. What is the difference between `git reset` and `git revert`?**  
**Answer:**  
| Command | Purpose |
|---------|---------|
| `git reset` | Moves the branch pointer to a previous commit, removing later commits |
| `git revert` | Creates a new commit that undoes changes of a previous commit |

Example (Undo last commit but keep changes):  
```sh
git reset --soft HEAD~1
```  

Example (Undo a specific commit by creating a new commit):  
```sh
git revert 123abc
```  

---

## **Advanced Git Questions**  

### **11. What is the difference between `git merge` and `git rebase`?**  
**Answer:**  
| Command | Description |
|---------|-------------|
| `git merge` | Combines changes from different branches and creates a new merge commit |
| `git rebase` | Moves or integrates changes from one branch onto another, rewriting commit history |

Example:  
```sh
git checkout main
git merge feature-branch
```  

Rebasing example:  
```sh
git checkout feature-branch
git rebase main
```  

### **12. What is `git cherry-pick`?**  
**Answer:**  
`git cherry-pick` applies a specific commit from one branch to another.  

Example:  
```sh
git cherry-pick abc123
```  

### **13. How do you squash commits?**  
**Answer:**  
Squashing combines multiple commits into one.  

Example:  
```sh
git rebase -i HEAD~3  # Squash last 3 commits
```  

### **14. How do you create and push a Git tag?**  
**Answer:**  
Tags mark important commits, such as version releases.  

Example:  
```sh
git tag v1.0
git push origin v1.0
```  

### **15. How do you remove a file from Git history?**  
**Answer:**  
To remove a file from Git history but keep it locally:  
```sh
git rm --cached file.txt
git commit -m "Removed file from history"
git push origin main
```  

### **16. How do you check commit history in Git?**  
**Answer:**  
Use the following command:  
```sh
git log
```  
For a compact view:  
```sh
git log --oneline --graph
```  

---

## **Conclusion**  
This document serves as a quick reference for Git theoretical questions and answers. It is useful for interviews, revision, and learning Git concepts in-depth.  
