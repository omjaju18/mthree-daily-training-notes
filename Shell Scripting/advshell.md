# **Advanced Shell Scripting: Debugging, Monitoring, and Automation**

Now, let's dive deeper into **debugging, monitoring, and automation** in shell scripting.

---

## **1️⃣ Debugging in Shell Scripting**
Debugging is crucial to find and fix issues in your shell scripts.

### **A) Enable Debugging Mode (`-x` option)**
You can use the `-x` option to see each command executed.
```sh
#!/bin/bash
set -x  # Enable debugging
echo "Debugging mode enabled"
name="Om Jaju"
echo "My name is $name"
set +x  # Disable debugging
```
✅ **Output:**  
```
+ echo 'Debugging mode enabled'
Debugging mode enabled
+ name='Om Jaju'
+ echo 'My name is Om Jaju'
My name is Om Jaju
```

---

### **B) Debugging Using `trap`**
The `trap` command captures errors and executes a specific action.

#### **Example: Catching Errors**
```sh
#!/bin/bash
trap 'echo "Error at line $LINENO"' ERR
echo "Starting script"
ls /non_existent_directory  # This will cause an error
echo "Script completed"
```
✅ **Output:**  
```
Starting script
Error at line 4
```

---

### **C) Logging Debug Information**
Redirect output to a log file.
```sh
#!/bin/bash
exec > >(tee debug.log) 2>&1  # Save output to debug.log
echo "This is a test script"
ls /wrongpath
```
✅ **The log file (`debug.log`) contains:**
```
This is a test script
ls: cannot access '/wrongpath': No such file or directory
```

---

## **2️⃣ System Monitoring with Shell Scripts**
### **A) CPU and Memory Usage Monitoring**
```sh
#!/bin/bash
echo "CPU Usage:"
top -bn1 | grep "Cpu(s)"

echo "Memory Usage:"
free -h
```
✅ **Output:**
```
CPU Usage:
%Cpu(s): 3.5 us, 1.2 sy, 0.0 ni, 95.3 id, 0.0 wa, 0.0 hi, 0.0 si, 0.0 st
Memory Usage:
              total        used        free      shared  buff/cache   available
Mem:          8.0Gi       2.1Gi       4.2Gi       110Mi       1.7Gi       5.5Gi
```

---

### **B) Disk Usage Monitoring**
```sh
#!/bin/bash
df -h | grep "/dev/sda"
```
✅ **Output:**
```
/dev/sda1       100G  45G   55G   45% /
```

---

### **C) Network Monitoring**
```sh
#!/bin/bash
ping -c 4 google.com
```
✅ **Output:**
```
PING google.com (142.250.186.46): 56 data bytes
64 bytes from 142.250.186.46: icmp_seq=1 ttl=118 time=18.1 ms
64 bytes from 142.250.186.46: icmp_seq=2 ttl=118 time=17.9 ms
```

---

### **D) Check If a Process is Running**
```sh
#!/bin/bash
process="nginx"
if pgrep -x "$process" > /dev/null
then
    echo "$process is running"
else
    echo "$process is not running"
fi
```
✅ **Output:**
```
nginx is running
```

---

## **3️⃣ Automation with Shell Scripts**
Automation helps reduce manual work.

### **A) Automating Backups**
This script backs up a directory daily.
```sh
#!/bin/bash
backup_dir="/home/user/backup"
mkdir -p $backup_dir
tar -czf $backup_dir/backup_$(date +%F).tar.gz /home/user/documents
echo "Backup completed!"
```
✅ **Output:**
```
Backup completed!
```
🔹 **Cron Job (Schedule Daily Backup at 1 AM):**
```sh
0 1 * * * /home/user/backup_script.sh
```

---

### **B) Auto Restart Service if Down**
This script restarts **Nginx** if it is not running.
```sh
#!/bin/bash
if ! pgrep nginx > /dev/null
then
    echo "Nginx is down! Restarting..."
    systemctl start nginx
fi
```
✅ **Automate with Cron:**
```sh
*/5 * * * * /home/user/restart_nginx.sh
```
🔹 Runs **every 5 minutes** to check and restart Nginx.

---

### **C) Auto Cleanup of Logs**
This script **deletes logs** older than **7 days**.
```sh
#!/bin/bash
find /var/log -name "*.log" -type f -mtime +7 -delete
echo "Old logs deleted!"
```
✅ **Automate with Cron (Runs Daily at Midnight)**
```sh
0 0 * * * /home/user/cleanup_logs.sh
```

---

## **4️⃣ Sending Email Alerts**
You can send email alerts when something goes wrong.

### **A) Send Alert When CPU Usage is High**
```sh
#!/bin/bash
cpu_usage=$(top -bn1 | grep "Cpu(s)" | awk '{print $2 + $4}')
threshold=80.0

if (( $(echo "$cpu_usage > $threshold" | bc -l) )); then
    echo "High CPU Usage: $cpu_usage%" | mail -s "Alert: High CPU Usage" omjaju03@gmail.com
fi
```
✅ **Cron Job (Runs Every 5 Minutes)**
```sh
*/5 * * * * /home/user/cpu_monitor.sh
```

---

## **🔟 Summary**
✅ **Debugging Techniques**
- `set -x`: Enable debugging.
- `trap`: Catch errors.
- Logging (`tee`): Save script output.

✅ **Monitoring Scripts**
- `top`, `free`, `df -h`: Monitor CPU, Memory, and Disk.
- `ping`, `pgrep`: Check network and process status.

✅ **Automation**
- **Backups**: Automate file backups.
- **Service Restarts**: Ensure critical services stay up.
- **Log Cleanup**: Delete old logs.

✅ **Alerts**
- Send **email alerts** when CPU usage is high.

Would you like a **real-time alerting system** (e.g., monitoring server logs)? 🚀
