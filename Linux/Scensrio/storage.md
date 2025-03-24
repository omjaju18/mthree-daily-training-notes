Here are some **scenario-based** Linux troubleshooting questions related to **processes, storage, RAM, and CPU**:  

---

### **CPU-Related Scenarios**  

1. **A server is running slow, and you suspect high CPU usage. How will you identify and resolve the issue?**  
   *Hint:* Use `top`, `htop`, `ps`, `nice`, `renice`, `kill`  

2. **How will you find the top 5 CPU-consuming processes on a Linux server?**  
   *Hint:* `ps aux --sort=-%cpu | head -5`  

3. **A process is consuming 100% CPU, and killing it is not an option. How will you reduce its CPU usage?**  
   *Hint:* Use `nice` or `renice` to lower priority  

4. **How will you check the CPU usage history of a Linux system?**  
   *Hint:* `sar -u 5 10` (from the `sysstat` package)  

---

### **Memory (RAM) Scenarios**  

5. **Your application is running out of memory. How will you check which process is consuming the most RAM?**  
   *Hint:* `ps aux --sort=-%mem | head -5`  

6. **How do you find available and total memory in Linux?**  
   *Hint:* `free -h`  

7. **How will you troubleshoot an "Out of Memory" (OOM) error in Linux?**  
   *Hint:* Check `dmesg | grep -i "oom"`, check swap usage, increase swap if needed  

8. **How will you identify if swap memory is being used heavily?**  
   *Hint:* `swapon -s`, `free -m`, `vmstat 1 5`  

---

### **Storage (Disk) Scenarios**  

9. **Your disk is full, and a critical service is down. How will you free up space?**  
   *Hint:* `df -h`, `du -sh /var/log`, `find / -size +100M`  

10. **Find the largest 10 files in a directory and delete them.**  
    *Hint:* `find /var/log -type f -exec du -h {} + | sort -rh | head -10`  

11. **Check which directories are consuming the most space.**  
    *Hint:* `du -ah / | sort -rh | head -10`  

12. **A log file is growing too fast. How will you troubleshoot and control it?**  
    *Hint:* `ls -lh /var/log`, `tail -f /var/log/syslog`, log rotation with `logrotate`  

---

### **Process Management Scenarios**  

13. **A process is stuck and unresponsive. How will you kill it forcefully?**  
    *Hint:* `kill -9 <PID>`  

14. **How will you find how long a process has been running?**  
    *Hint:* `ps -eo pid,etime,comm | grep <process_name>`  

15. **Find all running processes of a specific user.**  
    *Hint:* `ps -u username`  

16. **A process is consuming too much CPU and memory. How will you limit its resource usage?**  
    *Hint:* `ulimit`, `nice`, `cgroups`  

---

### **Network & Miscellaneous Scenarios**  

17. **A server is unreachable via SSH. How will you troubleshoot?**  
    *Hint:* `ping`, `netstat -tulnp`, `systemctl status ssh`  

18. **How will you monitor real-time system resource usage?**  
    *Hint:* `top`, `htop`, `iostat`, `vmstat`  

19. **How will you check which ports are open and listening?**  
    *Hint:* `netstat -tulnp`, `ss -tulnp`  

20. **How will you find which user ran a specific command in the past?**  
    *Hint:* `cat ~/.bash_history | grep "<command>"`  

---

Let me know if you need more! 🚀
