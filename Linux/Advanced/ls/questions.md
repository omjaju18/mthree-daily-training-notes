# **Practice Questions on `ls` Command**

Here are some sample questions to help you practice the `ls` command and its various options.

---

## **🟢 Basic Questions**
1. **How do you list all files and directories in the current directory?**  
   ```bash
   ls
   ```

2. **How do you display files in a long listing format?**  
   ```bash
   ls -l
   ```

3. **How do you include hidden files in the listing?**  
   ```bash
   ls -la
   ```

4. **How do you display file sizes in a human-readable format?**  
   ```bash
   ls -lh
   ```

5. **How do you list files in reverse order?**  
   ```bash
   ls -lr
   ```

---

## **🔵 Intermediate Questions**
6. **How do you list files sorted by modification time?**  
   ```bash
   ls -lt
   ```

7. **How do you list only directories in a given location?**  
   ```bash
   ls -ld */
   ```

8. **How do you list files sorted by their size (largest first)?**  
   ```bash
   ls -lS
   ```

9. **How do you display the inode numbers of files?**  
   ```bash
   ls -li
   ```

10. **How do you list files one per line instead of multiple columns?**  
   ```bash
   ls -1
   ```

11. **How do you show files in subdirectories recursively?**  
   ```bash
   ls -R
   ```

12. **How do you display only the filenames and hide file details?**  
   ```bash
   ls -1
   ```

---

## **🟠 Advanced Questions**
13. **How do you combine options to show hidden files in long format?**  
   ```bash
   ls -la
   ```

14. **How do you list files with a specific extension, such as `.txt`?**  
   ```bash
   ls *.txt
   ```

15. **How do you list files with color-coded output?**  
   ```bash
   ls --color=auto
   ```

16. **How do you list files in order of their extension type?**  
   ```bash
   ls -X
   ```

17. **How do you use `ls` to display directories with a trailing `/` to differentiate them from files?**  
   ```bash
   ls -p
   ```

18. **How do you exclude a specific file or pattern from the listing?**  
   ```bash
   ls --ignore="*.txt"
   ```

19. **How do you list files with a wildcard pattern, such as all `.log` files?**  
   ```bash
   ls *.log
   ```

20. **How do you list only executable files in a directory?**  
   ```bash
   ls -l | grep "^-..x"
   ```

---

## **💡 Scenario-Based Questions**
21. **You need to find the largest file in your directory. What command will you use?**  
   ```bash
   ls -lS | head -n 2
   ```

22. **You want to list files from oldest to newest. What `ls` command do you run?**  
   ```bash
   ls -ltr
   ```

23. **A system administrator asks you to list all files in a directory except hidden files. What do you use?**  
   ```bash
   ls -l
   ```

24. **You need to list all files and sort them by file type. How will you do that?**  
   ```bash
   ls -X
   ```

25. **A script you are writing requires file permissions to be displayed in the output. Which command will you use?**  
   ```bash
   ls -l
   ```

26. **You want to check how many files and directories are present in a folder. What `ls` command will help?**  
   ```bash
   ls -1 | wc -l
   ```

27. **How do you check if a particular file exists in a directory using `ls`?**  
   ```bash
   ls filename
   ```

28. **How do you list all `.conf` files in the `/etc/` directory?**  
   ```bash
   ls /etc/*.conf
   ```

29. **A folder contains thousands of files. How do you display only the first 10 files?**  
   ```bash
   ls | head -n 10
   ```

30. **You need to display a tree-like structure of directories using `ls`. Which option do you use?**  
   ```bash
   ls -R
   ```
   
   **Better alternative:**  
   ```bash
   tree
   ```
   *(Requires installation: `sudo apt install tree`)*

---

This document covers different variations and use cases of the `ls` command to help you practice effectively! 🚀

