# **Git Workflow: From Initialization to Pushing Code** 🚀  

## **1. Initialize a Git Repository (`git init`)**  
Before tracking changes, you need to create a Git repository.  

### **Command:**  
```bash
git init
```
- This initializes a new Git repository in your project folder.  
- A hidden `.git` folder is created, where Git stores all version control data.  

---

## **2. Configure Git (One-Time Setup)**
Before committing, set up your identity for Git.  

### **Commands:**  
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```
- This ensures that your commits are associated with your name and email.  

---

## **3. Check the Status of the Repository (`git status`)**  
Before making any commits, check the status of your working directory.  

### **Command:**  
```bash
git status
```
- Shows the current state of files (untracked, modified, staged).  

---

## **4. Add Files to Staging Area (`git add`)**  
Git doesn't track changes automatically. You need to stage them first.  

### **Command:**  
```bash
git add <filename>   # Adds a single file  
git add .            # Adds all modified files  
```
- Moves files from the working directory to the **staging area**.  

---

## **5. Commit Changes (`git commit`)**  
Once files are staged, commit them with a meaningful message.  

### **Command:**  
```bash
git commit -m "Initial commit"
```
- Captures the current state of the files.  

---

## **6. Connect to a Remote Repository (`git remote add origin`)**  
To push code to a remote server (e.g., GitHub, GitLab), add a remote repository.  

### **Command:**  
```bash
git remote add origin <repository-URL>
```
- Links the local repository to the remote one.  

---

## **7. Push Code to Remote Repository (`git push`)**  
Upload your commits to GitHub or another remote repository.  

### **Command:**  
```bash
git push -u origin master  # Pushes to the master branch
```
- The `-u` flag sets the upstream branch, so future pushes require only `git push`.  

---

## **8. Clone an Existing Repository (`git clone`)**  
If you're working on an existing project, clone it to your local machine.  

### **Command:**  
```bash
git clone <repository-URL>
```
- Creates a copy of the repository on your local machine.  

---

## **9. Pull Latest Changes (`git pull`)**  
Keep your local repository updated with the latest changes from the remote repository.  

### **Command:**  
```bash
git pull origin master
```
- Fetches and merges the latest changes.  

---

## **10. Create & Switch Branches (`git branch` & `git checkout`)**  
Work on a separate branch to avoid conflicts in the main branch.  

### **Commands:**  
```bash
git branch feature-branch   # Create a new branch  
git checkout feature-branch # Switch to the branch  
```
or  
```bash
git switch -c feature-branch  # Create and switch to a branch (modern approach)
```
- This allows you to work on features separately.  

---

## **11. Merge Branches (`git merge`)**  
After working on a feature branch, merge it into the main branch.  

### **Commands:**  
```bash
git checkout master  # Switch to the main branch  
git merge feature-branch  # Merge changes  
```
- This integrates changes from the feature branch into the master branch.  

---

## **12. Resolve Merge Conflicts (if any)**  
If Git cannot merge changes automatically, you must resolve conflicts manually.  

### **Steps:**  
1. Open conflicting files and manually fix the differences.  
2. Add the resolved files using:  
   ```bash
   git add <filename>
   ```
3. Complete the merge with:  
   ```bash
   git commit -m "Resolved merge conflicts"
   ```  

---

## **13. Revert a Commit (`git revert`)**  
Undo a commit without deleting history.  

### **Command:**  
```bash
git revert <commit-hash>
```
- Creates a new commit that undoes the specified commit.  

---

## **14. Reset Commits (`git reset`)**  
If you need to completely remove a commit:  

### **Commands:**  
```bash
git reset --soft HEAD~1  # Undo last commit but keep changes staged  
git reset --hard HEAD~1  # Undo last commit and remove all changes  
```
- **Caution:** Hard reset permanently deletes changes.  

---

## **15. Stash Changes (`git stash`)**  
If you need to temporarily save changes without committing:  

### **Command:**  
```bash
git stash
```
- Saves your changes and restores a clean working directory.  
- To apply the stashed changes later:  
  ```bash
  git stash pop
  ```

---

## **16. Delete a Branch (`git branch -d`)**  
After merging a feature branch, delete it to keep the repository clean.  

### **Command:**  
```bash
git branch -d feature-branch
```
- If the branch is not merged yet, force delete using:  
  ```bash
  git branch -D feature-branch
  ```

---

# **Summary of Git Workflow**
1. **Initialize:** `git init`  
2. **Track Changes:** `git add .`  
3. **Commit:** `git commit -m "Message"`  
4. **Connect to Remote:** `git remote add origin <URL>`  
5. **Push Changes:** `git push -u origin master`  
6. **Work on a Feature:** `git branch new-feature`, `git checkout new-feature`  
7. **Merge Branch:** `git merge new-feature`  
8. **Pull Latest Changes:** `git pull origin master`  
9. **Undo Mistakes:** `git reset` (removes commits) or `git revert` (safe undo)  
10. **Stash Temporary Changes:** `git stash`  

---

This covers the complete Git workflow from start to finish! 🚀

