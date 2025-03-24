Here is a **list of scenario-based Linux interview questions** with **detailed answers** for your preparation:

---

### **1️⃣ The server is running slow. How will you troubleshoot?**  
#### **Solution:**  
1. **Check CPU usage:**  
   ```bash
   top  
   htop  # If installed  
   ps aux --sort=-%cpu | head -5  
   ```
   - If a process is consuming too much CPU, kill it:  
     ```bash
     kill -9 <PID>  
     ```

2. **Check memory usage:**  
   ```bash
   free -m  
   ps aux --sort=-%mem | head -5  
   ```
   - If RAM is full, consider increasing **swap space** or **killing processes**.  
   ```bash
   swapon --show  
   ```

3. **Check disk usage:**  
   ```bash
   df -h  
   du -ah / | sort -rh | head -10  
   ```
   - Delete old logs & backups:  
     ```bash
     rm -rf /var/log/*.log  
     ```

4. **Check running services:**  
   ```bash
   systemctl list-units --type=service  
   ```
   - Restart high resource-consuming services:  
     ```bash
     systemctl restart <service-name>  
     ```

5. **Check network issues:**  
   ```bash
   ping -c 4 google.com  
   netstat -tulnp  
   iftop  # To monitor bandwidth usage  
   ```

6. **Check system logs for errors:**  
   ```bash
   journalctl -xe  
   dmesg | tail -20  
   ```

7. **Check load average:**  
   ```bash
   uptime  
   ```

---

### **2️⃣ A user is unable to log in to the Linux server via SSH. How will you troubleshoot?**  
#### **Solution:**  
1. **Check if SSH service is running:**  
   ```bash
   systemctl status sshd  
   ```
   - If not running, restart it:  
     ```bash
     systemctl restart sshd  
     ```

2. **Check if the SSH port (default 22) is open:**  
   ```bash
   netstat -tulnp | grep 22  
   ```

3. **Check firewall rules:**  
   ```bash
   iptables -L  
   sudo ufw status  
   ```

4. **Check user authentication logs:**  
   ```bash
   cat /var/log/auth.log | grep ssh  
   ```

5. **Verify SSH key authentication (if used):**  
   - Ensure correct **public key** is in `~/.ssh/authorized_keys`  
   - Check key permissions:  
     ```bash
     chmod 600 ~/.ssh/authorized_keys  
     ```

---

### **3️⃣ A cron job is not running. How will you debug?**  
#### **Solution:**  
1. **Check if the cron service is running:**  
   ```bash
   systemctl status cron  
   ```

2. **List all scheduled cron jobs:**  
   ```bash
   crontab -l  
   ```

3. **Check the cron job syntax:**  
   ```bash
   crontab -e  
   ```
   - Ensure correct time format: `* * * * * command`

4. **Check cron logs for errors:**  
   ```bash
   cat /var/log/syslog | grep cron  
   ```

5. **Test the cron job manually:**  
   ```bash
   /bin/bash -x /path/to/script.sh  
   ```

---

### **4️⃣ A process is consuming too much CPU/RAM. How will you handle it?**  
#### **Solution:**  
1. **Find high CPU-consuming processes:**  
   ```bash
   top  
   ps aux --sort=-%cpu | head -5  
   ```

2. **Find high memory-consuming processes:**  
   ```bash
   ps aux --sort=-%mem | head -5  
   ```

3. **Kill the process if necessary:**  
   ```bash
   kill -9 <PID>  
   ```

4. **Monitor in real-time:**  
   ```bash
   htop  
   ```

---

### **5️⃣ A server is running out of disk space. How will you troubleshoot?**  
#### **Solution:**  
1. **Check disk usage:**  
   ```bash
   df -h  
   ```

2. **Find large files:**  
   ```bash
   du -ah / | sort -rh | head -10  
   ```

3. **Delete unnecessary logs & backups:**  
   ```bash
   rm -rf /var/log/*.log  
   ```

4. **Check and clean temporary files:**  
   ```bash
   rm -rf /tmp/*  
   ```

5. **Move large files to another disk/storage.**  

---

### **6️⃣ A website is down. How will you troubleshoot?**  
#### **Solution:**  
1. **Check if the web server is running:**  
   ```bash
   systemctl status nginx  # For Nginx  
   systemctl status apache2  # For Apache  
   ```

2. **Check if the website’s port is open (default 80/443):**  
   ```bash
   netstat -tulnp | grep 80  
   ```

3. **Check server logs for errors:**  
   ```bash
   tail -f /var/log/nginx/access.log  
   tail -f /var/log/nginx/error.log  
   ```

4. **Check DNS resolution:**  
   ```bash
   nslookup mywebsite.com  
   ```

5. **Check SSL certificate (for HTTPS websites):**  
   ```bash
   openssl s_client -connect mywebsite.com:443  
   ```

---

### **7️⃣ A file is missing from the system. How will you recover it?**  
#### **Solution:**  
1. **Check if the file exists in backups:**  
   ```bash
   ls -l /path/to/backup  
   ```

2. **Find recently modified files:**  
   ```bash
   find / -mtime -1  
   ```

3. **Check logs for deletion events (if auditd is enabled):**  
   ```bash
   ausearch -f /path/to/file  
   ```

4. **Recover from Trash (GUI-based systems):**  
   ```bash
   ls ~/.local/share/Trash/files  
   ```

5. **If on a mounted filesystem, check for previous versions:**  
   ```bash
   cd /path/to/directory && ls -lah  
   ```

---

### **8️⃣ How will you check if a network port is open or blocked?**  
#### **Solution:**  
1. **Check active ports:**  
   ```bash
   netstat -tulnp  
   ```

2. **Check if a specific port is open:**  
   ```bash
   nc -zv 192.168.1.1 22  
   ```

3. **Check firewall rules:**  
   ```bash
   iptables -L  
   ```

4. **Use telnet to test connectivity:**  
   ```bash
   telnet google.com 80  
   ```

---

### **9️⃣ A user accidentally deleted a critical file. How will you recover it?**  
#### **Solution:**  
1. **Check Trash folder:**  
   ```bash
   ls ~/.local/share/Trash/files  
   ```

2. **Search for backup copies:**  
   ```bash
   find / -name "file.txt"  
   ```

3. **Check the disk for undeleted inodes (ext4 systems):**  
   ```bash
   extundelete /dev/sda --restore-all  
   ```

4. **Restore from snapshots (if enabled in LVM or backup system).**  

---
Good approach! Here's a **detailed step-by-step** method to troubleshoot a **slow server**:  

---

### **1️⃣ Check CPU Usage**  
Find out which process is consuming the most CPU:  
```bash
top  
```
OR  
```bash
htop  # If installed (more user-friendly)
```
- Look for **high CPU-consuming processes** and note their **PID (Process ID)**.  
- If a process is consuming **too much CPU**, **kill it**:  
  ```bash
  kill -9 <PID>  
  ```

---

### **2️⃣ Check Memory Usage**  
Find out if the server is running out of RAM:  
```bash
free -m  
```
- **If RAM usage is high**, find memory-heavy processes:  
  ```bash
  ps aux --sort=-%mem | head -5  
  ```
- **Solution:**  
  - **Kill unnecessary processes**  
  - **Increase swap space** if needed  
  ```bash
  swapon --show  
  ```

---

### **3️⃣ Check Disk Space**  
If the disk is full, the server can slow down:  
```bash
df -h  
```
- If a partition is **full**, find large files:  
  ```bash
  du -ah / | sort -rh | head -10  
  ```
- **Solution:**  
  - **Delete old logs & backups**:  
    ```bash
    rm -rf /var/log/*.log  
    ```
  - **Move large files to another disk/storage**  

---

### **4️⃣ Check Running Services**  
See which services are running and their resource usage:  
```bash
systemctl list-units --type=service  
```
- Restart **high CPU/memory consuming services** if needed:  
  ```bash
  systemctl restart <service-name>  
  ```

---

### **5️⃣ Check Network Issues**  
Find out if the issue is network-related:  
```bash
ping -c 4 google.com  
```
- **High latency?** Might be an **internet issue**.  

Check active network connections:  
```bash
netstat -tulnp  
```
- Look for **unwanted open connections** consuming bandwidth.  

Check bandwidth usage:  
```bash
iftop  
```
OR  
```bash
nload  
```

---

### **6️⃣ Check System Logs for Errors**  
```bash
journalctl -xe  
```
OR  
```bash
dmesg | tail -20  
```
- Look for any **hardware errors, kernel issues, or failed services**.  

---

### **7️⃣ Check Load Average**  
```bash
uptime  
```
- If load average is **too high (above CPU cores)**, it indicates excessive workload.  

---
Good approach! But let's **refine and structure** it better for an interview:  

---

### **1️⃣ Analyze the System Performance**  
Since the application is slow but not down, start by identifying resource bottlenecks.  

#### ✅ **Check CPU and Memory Usage**  
- Look for high CPU or memory usage processes:  
  ```bash
  top  
  ps aux --sort=-%cpu | head -5   # Find top CPU-consuming processes  
  ps aux --sort=-%mem | head -5   # Find top memory-consuming processes  
  ```
- If a process is consuming too many resources, restart it:  
  ```bash
  kill -9 <PID>  
  systemctl restart <service_name>  
  ```

#### ✅ **Check Disk Usage**  
- If the disk is full, it can slow down read/write operations:  
  ```bash
  df -h       # Check disk space  
  du -sh /var/log/*  # Check large log files  
  ```
- If needed, clear space:  
  ```bash
  find /var/log -type f -name "*.log" -mtime +10 -delete  
  ```

#### ✅ **Check Running Processes**  
- Find **stuck or zombie processes** (processes that aren't completing):  
  ```bash
  ps aux | grep defunct  
  ```

---

### **2️⃣ Check Network Performance**  
If system resources are fine, the issue might be network-related.  

#### ✅ **Check Latency & Connectivity**  
- Ping the application server to check if there's **high latency**:  
  ```bash
  ping -c 5 <server_ip>  
  ```
- Use **traceroute** to detect delays:  
  ```bash
  traceroute <server_ip>  
  ```

#### ✅ **Check Network Traffic & Open Connections**  
- Find network bottlenecks:  
  ```bash
  netstat -tulnp  
  ss -tulwn  # Alternative to netstat  
  ```

---

### **3️⃣ Check Application Logs for Errors**  
- Application-specific logs can help identify timeouts or errors:  
  ```bash
  journalctl -u <service_name> --since "10 minutes ago"  
  tail -f /var/log/<application>.log  
  ```

---

### **4️⃣ Fix & Optimize Performance**  
- If a process is **consuming too many resources**, restart it.  
- If **logs are too large**, delete old ones.  
- If **network is slow**, investigate external dependencies.  
- If **database queries are slow**, optimize indexes.  

---

Good answer! But let's **improve** it with a more structured approach:  

---

### **1️⃣ Identify the High CPU Process**  
First, check which process is consuming high CPU:  
```bash
ps aux --sort=-%cpu | head -5   # Top 5 CPU-consuming processes  
top                            # Live CPU usage monitoring  
htop                           # Interactive process viewer  
```

---

### **2️⃣ Analyze the Process Behavior**  
Once you find the process **using high CPU**, check if:  
✅ It's a critical system process (like MySQL, Apache, or Jenkins).  
✅ It's an unnecessary or zombie process.  

- Find the **owner of the process**:  
  ```bash
  ps -u <username>  
  ```
- Check if it's a **stuck process**:  
  ```bash
  ps aux | grep defunct  
  ```

---

### **3️⃣ Take Action**  
✅ **If it's an unnecessary process, kill it**  
```bash
kill -9 <PID>  
```
✅ **If it's a system service, restart it safely**  
```bash
systemctl restart <service_name>  
```
✅ **If it's a background job consuming CPU, reduce priority**  
```bash
renice +10 -p <PID>   # Lower priority  
```
✅ **If it’s a scheduled job (cron), disable it**  
```bash
crontab -l  
crontab -e  # Edit and disable unnecessary jobs  
```

---

### **4️⃣ Prevent Future High CPU Issues**  
✅ **Check CPU load over time**  
```bash
uptime       # Shows load average  
sar -u 5 5   # Monitors CPU usage every 5 seconds  
```
✅ **Limit CPU usage for processes**  
Use `cpulimit` to restrict CPU usage for a process.  
```bash
cpulimit -p <PID> -l 30  # Limits the process to 30% CPU  
```
✅ **Check logs for recurring issues**  
```bash
journalctl -u <service_name> --since "10 minutes ago"  
```

---

Your approach is good, but here’s how you can **structure it better** for clarity and impact in an interview:  

---

### **1️⃣ Immediate Action: Rollback to the Previous Version**  
- If the application is critical, first **rollback** to a stable version (if available) to minimize downtime.  
- Example: If using a package manager like `rpm`, `dpkg`, or `yum`:  
  ```bash
  yum history rollback <ID>   # For RHEL/CentOS  
  apt-get install --reinstall <package>  # For Ubuntu/Debian  
  ```

### **2️⃣ Identify the Root Cause**  
Check **why** the application crashed before attempting a restart.  

#### ✅ **Check System Health**
- **Check memory usage** (Is the system out of RAM?)  
  ```bash
  free -m  
  vmstat 1 5  
  ```
- **Check CPU usage** (Any high CPU-consuming process?)  
  ```bash
  top  
  ps aux --sort=-%cpu | head -5  
  ```
- **Check Disk space** (Out of storage?)  
  ```bash
  df -h  
  du -sh /var/log/*  # Check log sizes  
  ```

#### ✅ **Check Running Processes**
- If the process stopped, find out why.  
  ```bash
  ps -ef | grep <application_name>  
  systemctl status <service_name>  
  ```
- Restart the service if needed:  
  ```bash
  sudo systemctl restart <service_name>  
  ```

#### ✅ **Check Application Logs**
- View recent logs to see **why** it crashed:  
  ```bash
  journalctl -u <service_name> --since "10 minutes ago"  
  tail -f /var/log/<application>.log  
  ```

#### ✅ **Check Network Issues**
- If the application relies on external APIs or DBs, verify network connectivity:  
  ```bash
  ping <external_server>  
  netstat -tulnp  
  ```

---

### **3️⃣ Fix the Issue and Prevent Future Crashes**
- If storage was full, **clean up space**:  
  ```bash
  find /var/log -type f -name "*.log" -mtime +10 -delete  
  ```
- If memory is exhausted, **restart heavy processes** or allocate more swap:  
  ```bash
  swapon --show  
  ```

---

### **Final Step: Monitor and Document the Fix**
- Set up **monitoring tools** (e.g., Prometheus, Grafana, Nagios) to **prevent** future crashes.  
- Document the issue and resolution for future reference.  

---

