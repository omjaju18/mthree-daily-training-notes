# Linux Commands Cheat Sheet

This document provides a categorized list of Linux commands along with their use cases and examples.

---

## **1. File and Directory Management**
| Use Case | Command | Example |
|----------|---------|---------|
| List files and directories | `ls` | `ls -l` (detailed list) |
| Change directory | `cd` | `cd /home/user` |
| Create a new directory | `mkdir` | `mkdir myfolder` |
| Remove an empty directory | `rmdir` | `rmdir myfolder` |
| Remove a directory with files | `rm -r` | `rm -r myfolder` |
| Create an empty file | `touch` | `touch file.txt` |
| Copy a file | `cp` | `cp file1.txt file2.txt` |
| Copy a directory | `cp -r` | `cp -r dir1 dir2` |
| Move or rename a file | `mv` | `mv oldname.txt newname.txt` |
| Delete a file | `rm` | `rm file.txt` |
| View file contents | `cat` | `cat file.txt` |
| View file contents page by page | `less` | `less file.txt` |
| View the first 10 lines | `head` | `head -n 10 file.txt` |
| View the last 10 lines | `tail` | `tail -n 10 file.txt` |
| Search inside a file | `grep` | `grep "error" logfile.txt` |
| Find files | `find` | `find /home -name "*.txt"` |
| Locate a command or file | `locate` | `locate myfile` |

---

## **2. File Permissions & Ownership**
| Use Case | Command | Example |
|----------|---------|---------|
| Change file permissions | `chmod` | `chmod 755 script.sh` |
| Change file ownership | `chown` | `chown user:user file.txt` |
| Change group ownership | `chgrp` | `chgrp mygroup file.txt` |
| View file permissions | `ls -l` | `ls -l file.txt` |

---

## **3. Process Management**
| Use Case | Command | Example |
|----------|---------|---------|
| View running processes | `ps` | `ps aux` |
| View real-time process usage | `top` | `top` |
| View detailed system resource usage | `htop` | `htop` |
| Kill a process | `kill` | `kill 1234` (PID) |
| Kill a process by name | `pkill` | `pkill firefox` |
| Stop a process | `Ctrl + Z` | Pauses the process |
| Resume a stopped process | `fg` | `fg` |
| Run a process in the background | `&` | `./script.sh &` |
| Bring background process to foreground | `bg` | `bg` |

---

## **4. Disk Management**
| Use Case | Command | Example |
|----------|---------|---------|
| Check disk usage | `df` | `df -h` (human-readable) |
| Check directory size | `du` | `du -sh /home/user` |
| List block devices | `lsblk` | `lsblk` |
| Mount a filesystem | `mount` | `mount /dev/sdb1 /mnt` |
| Unmount a filesystem | `umount` | `umount /mnt` |
| Check and repair filesystem | `fsck` | `fsck /dev/sda1` |
| Create a new file system | `mkfs` | `mkfs.ext4 /dev/sdb1` |

---

## **5. Networking**
| Use Case | Command | Example |
|----------|---------|---------|
| Check network interfaces | `ip a` | `ip a` |
| Display routing table | `ip r` | `ip r` |
| Ping a host | `ping` | `ping google.com` |
| Display network connections | `netstat` | `netstat -tulnp` |
| Check open ports | `ss` | `ss -tulnp` |
| Download a file | `wget` | `wget http://example.com/file.zip` |
| Download a file with curl | `curl -O` | `curl -O http://example.com/file.zip` |

---

## **6. User Management**
| Use Case | Command | Example |
|----------|---------|---------|
| Add a user | `useradd` | `useradd john` |
| Delete a user | `userdel` | `userdel john` |
| Change user password | `passwd` | `passwd john` |
| Switch user | `su` | `su - john` |
| Show current user | `whoami` | `whoami` |
| List logged-in users | `who` | `who` |
| Show system login history | `last` | `last` |

---

## **7. System Monitoring**
| Use Case | Command | Example |
|----------|---------|---------|
| Show system uptime | `uptime` | `uptime` |
| Show system load | `uptime` | `uptime` |
| Display memory usage | `free` | `free -h` |
| Show CPU usage | `mpstat` | `mpstat` |
| Display running processes | `top` | `top` |
| Show kernel version | `uname -r` | `uname -r` |

---

## **8. Package Management**
| Use Case | Command | Example |
|----------|---------|---------|
| Update package list (Debian) | `apt update` | `sudo apt update` |
| Upgrade all packages (Debian) | `apt upgrade` | `sudo apt upgrade` |
| Install a package (Debian) | `apt install` | `sudo apt install nginx` |
| Remove a package (Debian) | `apt remove` | `sudo apt remove nginx` |

---

## **9. Log Management**
| Use Case | Command | Example |
|----------|---------|---------|
| View system logs | `journalctl` | `journalctl -xe` |
| View authentication logs | `cat /var/log/auth.log` | `cat /var/log/auth.log` |
| View kernel logs | `dmesg` | `dmesg | tail` |

---

## **10. Archive and Compression**
| Use Case | Command | Example |
|----------|---------|---------|
| Create a tar archive | `tar -cvf` | `tar -cvf archive.tar myfolder` |
| Extract a tar archive | `tar -xvf` | `tar -xvf archive.tar` |
| Compress using gzip | `gzip` | `gzip file.txt` |
| Decompress using gzip | `gunzip` | `gunzip file.txt.gz` |

---

## **11. Scheduled Tasks (Cron Jobs)**
| Use Case | Command | Example |
|----------|---------|---------|
| Edit cron jobs | `crontab -e` | `crontab -e` |
| List scheduled cron jobs | `crontab -l` | `crontab -l` |

---

## **12. Shell Scripting**
```bash
#!/bin/bash
echo "Hello, World!"
```
Make the script executable: `chmod +x script.sh` and run it using `./script.sh`.

---

### **End of Document**

