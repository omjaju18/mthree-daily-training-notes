# Find Command Cheat Sheet

This document contains **30 `find` command questions with answers**, categorized into **Basic, Intermediate, Advanced, and Scenario-Based** types.

---

## **🔹 Basic Questions**  

1️⃣ **Find all `.txt` files inside `/home`.**  
```sh
find /home -type f -name "*.txt"
```
2️⃣ **Locate all empty files inside `/var/log`.**  
```sh
find /var/log -type f -empty
```
3️⃣ **Find all directories inside `/usr/local`.**  
```sh
find /usr/local -type d
```
4️⃣ **Search for files modified exactly 7 days ago in `/etc`.**  
```sh
find /etc -type f -mtime 7
```
5️⃣ **Find all files accessed in the last 10 days inside `/tmp`.**  
```sh
find /tmp -type f -atime -10
```
6️⃣ **Find all executable files in `/bin`.**  
```sh
find /bin -type f -perm /a=x
```
7️⃣ **Locate files owned by the user `root`.**  
```sh
find / -type f -user root
```
8️⃣ **Find all symbolic links inside `/lib`.**  
```sh
find /lib -type l
```
9️⃣ **Find files larger than 1GB in `/var`.**  
```sh
find /var -type f -size +1G
```
🔟 **Find all hidden files in your home directory (`~`).**  
```sh
find ~ -type f -name ".*"
```

---

## **🔹 Intermediate Questions**  

1️⃣1️⃣ **Find all `.log` files older than 30 days in `/var/log` and delete them.**  
```sh
find /var/log -type f -name "*.log" -mtime +30 -delete
```
1️⃣2️⃣ **Find all `.sh` files with execute permission.**  
```sh
find / -type f -name "*.sh" -perm /a=x
```
1️⃣3️⃣ **Search for files modified within the last 2 hours.**  
```sh
find / -type f -mmin -120
```
1️⃣4️⃣ **Find and change permissions of all `.sh` files in `/scripts` to `755`.**  
```sh
find /scripts -type f -name "*.sh" -exec chmod 755 {} \;
```
1️⃣5️⃣ **Find all files in `/opt` that are exactly 100MB.**  
```sh
find /opt -type f -size 100M
```
1️⃣6️⃣ **Find all files in `/etc` with read, write, and execute permissions for the owner.**  
```sh
find /etc -type f -perm 700
```
1️⃣7️⃣ **Locate files modified between 20 to 50 days ago in `/var/www`.**  
```sh
find /var/www -type f -mtime +20 -mtime -50
```
1️⃣8️⃣ **Find all `.conf` files and copy them to `/backup`.**  
```sh
find /etc -type f -name "*.conf" -exec cp {} /backup/ \;
```
1️⃣9️⃣ **Find all empty directories inside `/tmp`.**  
```sh
find /tmp -type d -empty
```
2️⃣0️⃣ **Search for files modified within the last 5 minutes.**  
```sh
find / -type f -mmin -5
```

---

## **🔹 Advanced Questions**  

2️⃣1️⃣ **Find and remove all files larger than 1GB inside `/mnt`.**  
```sh
find /mnt -type f -size +1G -delete
```
2️⃣2️⃣ **Find the top 10 largest files in `/var/log`.**  
```sh
find /var/log -type f -exec du -h {} + | sort -rh | head -n 10
```
2️⃣3️⃣ **Find and list all files modified within the last 24 hours but exclude `.log` files.**  
```sh
find / -type f -mtime -1 ! -name "*.log"
```
2️⃣4️⃣ **Find all `.jpg` or `.png` files inside `/home`.**  
```sh
find /home -type f \( -name "*.jpg" -o -name "*.png" \)
```
2️⃣5️⃣ **Find and replace "error" with "warning" in all `.log` files in `/var/log`.**  
```sh
find /var/log -type f -name "*.log" -exec sed -i 's/error/warning/g' {} \;
```
2️⃣6️⃣ **Find all files that belong to group `developers`.**  
```sh
find / -type f -group developers
```
2️⃣7️⃣ **Find files in `/home` that have been accessed in the last 15 days and are larger than 50MB.**  
```sh
find /home -type f -atime -15 -size +50M
```
2️⃣8️⃣ **Find all `.sh` scripts in `/scripts` and list them with their permissions.**  
```sh
find /scripts -type f -name "*.sh" -exec ls -l {} \;
```
2️⃣9️⃣ **Find and rename all `.txt` files in `/docs` by adding `_backup` before the extension.**  
```sh
find /docs -type f -name "*.txt" -exec bash -c 'mv "$1" "${1%.txt}_backup.txt"' _ {} \;
```
3️⃣0️⃣ **Find and delete files owned by user `testuser` inside `/tmp`.**  
```sh
find /tmp -type f -user testuser -delete
```

---

## **🔹 Final Summary**  
✅ **Basic Questions (1-10)** → Name, type, size, modification time, ownership, symbolic links.  
✅ **Intermediate Questions (11-20)** → Deleting, permission changes, modification intervals, executing commands.  
✅ **Advanced Questions (21-30)** → Large files, exclusion patterns, search & replace, renaming, user/group ownership.  

These **30 `find` command questions** cover all levels of complexity, helping you master `find`! 🚀

