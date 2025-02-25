### **Git Cheat Sheet **  

```md
# 📌 Git Cheat Sheet  

## 🔹 Basic Commands  
```sh
git init                           # Initialize a new Git repository  
git clone <repo_url>               # Clone an existing repository  
git status                         # Show the status of changes  
git add <file>                     # Stage a file for commit  
git commit -m "message"            # Commit staged files  
```

## 🔹 Branching & Merging  
```sh
git branch <branch_name>           # Create a new branch  
git checkout <branch_name>         # Switch to a branch  
git merge <branch_name>            # Merge a branch into the current branch  
```

## 🔹 Working with Remote Repositories  
```sh
git remote add origin <url>        # Link local repo to a remote repo  
git push origin <branch>           # Push changes to the remote repo  
git pull origin <branch>           # Fetch and merge remote changes  
git fetch                          # Fetch changes without merging  
```

## 🔹 Undoing Changes  
```sh
git reset --soft HEAD~1            # Undo last commit (keep changes staged)  
git reset --hard HEAD~1            # Undo last commit (discard changes)  
git revert <commit_id>             # Create a new commit that undoes changes  
```

## 🔹 Stashing Changes  
```sh
git stash                          # Save uncommitted changes temporarily  
git stash list                     # View stashed changes  
git stash apply                    # Reapply last stashed changes  
git stash drop                     # Delete last stash  
```

## 💡 **Quick Tips**  
✔️ Always pull before pushing to avoid conflicts.  
✔️ Use meaningful commit messages.  
✔️ Avoid committing sensitive data like credentials.  
✔️ Use `git log --oneline --graph` to visualize commit history.  

---
