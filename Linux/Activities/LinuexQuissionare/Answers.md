1. **Creating a new user account in Linux**  
   Use the `useradd` command followed by the username:  
   ```bash
   sudo useradd -m newuser
   ```  
   Then, set a password for the new user:  
   ```bash
   sudo passwd newuser
   ```

2. **Difference between relative and absolute paths**  
   - **Absolute Path**: Starts from the root (`/`) and specifies the full path to a file or directory (e.g., `/home/user/documents`).  
   - **Relative Path**: Starts from the current directory (e.g., `./documents` or `../parent_folder`).

3. **Changing file ownership**  
   Use the `chown` command:  
   ```bash
   sudo chown newowner:newgroup filename
   ```

4. **Scheduling a task to run automatically**  
   Use `cron` for repeated tasks:  
   ```bash
   crontab -e
   ```  
   Example: Run a script at 2 AM daily:  
   ```bash
   0 2 * * * /path/to/script.sh
   ```  
   Use `at` for a one-time task:  
   ```bash
   echo "command_to_run" | at 14:30
   ```

5. **Compressing and decompressing files**  
   - **Compress**: `tar -czvf archive.tar.gz folder/`  
   - **Decompress**: `tar -xzvf archive.tar.gz`

6. **Purpose of the 'grep' command**  
   The `grep` command is used to search for text in files. Example:  
   ```bash
   grep "error" /var/log/syslog
   ```

7. **Checking and managing running processes**  
   - `ps aux` – List processes  
   - `top` or `htop` – Real-time process monitoring  
   - `kill PID` – Kill a process  


9. **Checking system resource usage**  
   - CPU & RAM: `top` or `htop`  
   - Disk usage: `df -h`  
   - Memory usage: `free -m`

12. **Difference between 'sudo' and 'su'**  
   - `sudo`: Runs a single command as root  
   - `su`: Switches to the root user (requires root password)

13. **Searching for files larger than a specific size**  
   ```bash
   find /path -type f -size +100M
   ```

14. **Redirecting output to a file**  
   - Overwrite: `command > file.txt`  
   - Append: `command >> file.txt`

15. **Viewing real-time log entries**  
   ```bash
   tail -f /var/log/syslog
   ```

16. **Checking and modifying file permissions recursively**  
   ```bash
   chmod -R 755 /path/to/directory
   ```

17. **Using 'find' to locate files**  
   ```bash
   find / -name "filename.txt"
   ```


20. **Using 'tar' for backup and restore**  
   - Backup: `tar -cvf backup.tar /path/to/directory`  
   - Restore: `tar -xvf backup.tar`
