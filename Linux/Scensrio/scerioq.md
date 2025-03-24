
Here are some **important Linux commands** categorized based on your mentioned topics:  

### **🔹 CPU & Memory Utilization**  
1. `top` – View CPU & memory usage dynamically.  
2. `htop` – Interactive version of `top` (if installed).  
3. `free -m` – Check available and used memory in MB.  
4. `vmstat 1 5` – Monitor CPU, memory, and I/O stats.  

### **🔹 Disk Space & Storage Management**  
5. `df -h` – Show disk space usage in human-readable format.  
6. `du -ah / | sort -rh | head -10` – Find largest files & directories.  
7. `lsblk` – Display information about block devices.  
8. `fdisk -l` – Show partitions of all disks.  

### **🔹 Process Management**  
9. `ps aux` – List all running processes.  
10. `ps aux --sort=-%cpu | head -5` – Find top CPU-consuming processes.  
11. `ps aux --sort=-%mem | head -5` – Find top memory-consuming processes.  
12. `kill -9 <PID>` – Force kill a process by its PID.  

### **🔹 Network Troubleshooting**  
13. `ping google.com` – Check network connectivity.  
14. `traceroute google.com` – Trace the route packets take to the destination.  
15. `netstat -tulnp` – List open ports and active connections.  
16. `ss -tulnp` – Alternative to `netstat`, faster and more detailed.  
17. `iftop` – Monitor real-time network bandwidth usage (if installed).  

### **🔹 Service & System Management**  
18. `systemctl status <service-name>` – Check service status.  
19. `systemctl restart <service-name>` – Restart a service.  
20. `systemctl enable <service-name>` – Enable service to start on boot.  
21. `journalctl -xe` – Check system logs for errors.  
22. `uptime` – Show system load and uptime.  

---

### **Linux Interview Questions Based on These Commands**  
1️⃣ **How do you check CPU and memory utilization in Linux?**  
   **Answer:** Use `top`, `htop`, or `free -m` to check CPU and memory usage.  

2️⃣ **How do you check disk space and find large files?**  
   **Answer:** Use `df -h` for disk usage and `du -ah / | sort -rh | head -10` to find large files.  

3️⃣ **How do you identify high CPU-consuming processes?**  
   **Answer:** Use `ps aux --sort=-%cpu | head -5` or `top`.  

4️⃣ **How do you troubleshoot network issues?**  
   **Answer:** Use `ping` to check connectivity, `traceroute` to check routing, and `netstat -tulnp` to see open ports.  

5️⃣ **How do you check if a service is running and restart it?**  
   **Answer:** Use `systemctl status <service-name>` to check status and `systemctl restart <service-name>` to restart it.  

---

Let me know if you need more questions or explanations! 🚀
