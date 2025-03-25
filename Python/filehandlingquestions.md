For a **Production Support Engineer** role, file handling is crucial in troubleshooting, monitoring logs, automating fixes, and managing system files. Here are some **scenario-based questions** tailored for a **Production Support Job**:  

---

## **1. Identifying Errors in Log Files**  
🔹 **Scenario:**  
A production server has a log file (`application.log`) where errors are logged with the keyword `"ERROR"`. You need to extract all error messages from the last **30 minutes**.  

💡 **How would you do this?**  

✅ **Solution:**  
```python
from datetime import datetime, timedelta

log_file = "application.log"
time_threshold = datetime.now() - timedelta(minutes=30)

with open(log_file, "r") as file:
    for line in file:
        if "ERROR" in line:
            timestamp_str = line.split()[0]  # Assuming first part is the timestamp
            log_time = datetime.strptime(timestamp_str, "%Y-%m-%d %H:%M:%S")
            if log_time >= time_threshold:
                print(line.strip())
```
🛠 **Follow-up:** What if the log format changes? How can you make it dynamic?

---

## **2. Disk Space Monitoring (Large Log Files)**  
🔹 **Scenario:**  
A server is running out of disk space due to **large log files** (`.log` files). You need to find all log files larger than **500MB** in a directory (`/var/logs`) and move them to an archive folder (`/archive`).  

💡 **How would you automate this?**  

✅ **Solution (Using Python & OS module)**  
```python
import os
import shutil

log_dir = "/var/logs"
archive_dir = "/archive"

for file in os.listdir(log_dir):
    file_path = os.path.join(log_dir, file)
    if file.endswith(".log") and os.path.isfile(file_path):
        if os.path.getsize(file_path) > 500 * 1024 * 1024:  # 500MB
            shutil.move(file_path, archive_dir)
            print(f"Moved {file} to archive.")
```
🛠 **Follow-up:** How would you implement automatic log rotation?

---

## **3. Detecting Failed Transactions from Log Files**  
🔹 **Scenario:**  
A transaction processing system logs each transaction in `transactions.log`. Failed transactions contain the word **"FAILED"** and the transaction ID. You need to extract all failed transaction IDs and save them to `failed_transactions.txt`.  

💡 **How would you extract and store them?**  

✅ **Solution:**  
```python
with open("transactions.log", "r") as log, open("failed_transactions.txt", "w") as output:
    for line in log:
        if "FAILED" in line:
            txn_id = line.split()[1]  # Assuming second field is Transaction ID
            output.write(txn_id + "\n")

print("Failed transactions saved.")
```
🛠 **Follow-up:** How would you automate retrying these failed transactions?

---

## **4. Checking File Integrity**  
🔹 **Scenario:**  
A critical file (`config.cfg`) is used in production. If it gets corrupted (size is **0 bytes**), the application fails. You need to create a Python script that **checks its size** and **restores a backup** if it’s empty.  

💡 **How would you handle this?**  

✅ **Solution:**  
```python
import os
import shutil

config_file = "/etc/app/config.cfg"
backup_file = "/backup/config.cfg"

if os.path.exists(config_file) and os.path.getsize(config_file) == 0:
    shutil.copy(backup_file, config_file)
    print("Corrupted file restored from backup.")
```
🛠 **Follow-up:** How can you detect **partial corruption** beyond just file size?

---

## **5. Automating File Cleanup (Old Files Deletion)**  
🔹 **Scenario:**  
Your team wants to **delete all files older than 7 days** in the `/tmp` directory to free up space.  

💡 **How would you automate this?**  

✅ **Solution:**  
```python
import os
import time

dir_path = "/tmp"
now = time.time()

for file in os.listdir(dir_path):
    file_path = os.path.join(dir_path, file)
    if os.path.isfile(file_path) and now - os.path.getmtime(file_path) > 7 * 86400:
        os.remove(file_path)
        print(f"Deleted: {file}")
```
🛠 **Follow-up:** How would you ensure critical files are not deleted by mistake?

---

## **6. Monitoring File Changes in Real-Time**  
🔹 **Scenario:**  
A production file (`server_status.log`) contains **live application status**. You need to continuously monitor it and print new changes **as they are added**.  

💡 **How would you implement this?**  

✅ **Solution (Using `tail -f` equivalent in Python)**  
```python
import time

log_file = "server_status.log"

with open(log_file, "r") as file:
    file.seek(0, 2)  # Move to the end of file
    while True:
        line = file.readline()
        if line:
            print(line.strip())  # Print new log lines
        time.sleep(1)  # Avoid high CPU usage
```
🛠 **Follow-up:** How would you handle **log rotation** (when the file gets replaced)?

---

## **7. Checking If a Process is Running by Reading a PID File**  
🔹 **Scenario:**  
A critical process writes its Process ID (PID) to `/var/run/app.pid`. You need to check if the process is running by reading the PID file and verifying it against running processes.  

💡 **How would you implement this?**  

✅ **Solution:**  
```python
import os

pid_file = "/var/run/app.pid"

if os.path.exists(pid_file):
    with open(pid_file, "r") as file:
        pid = file.read().strip()
        if os.path.exists(f"/proc/{pid}"):
            print(f"Process {pid} is running.")
        else:
            print(f"Process {pid} is NOT running.")
else:
    print("PID file not found.")
```
🛠 **Follow-up:** How would you restart the process if it’s not running?

---

## **8. Handling File Permission Issues**  
🔹 **Scenario:**  
A script fails to write logs due to a **Permission Denied** error. You need to check if the file is writable before writing.  

💡 **How would you troubleshoot and fix it?**  

✅ **Solution:**  
```python
import os

log_file = "/var/log/app.log"

if os.access(log_file, os.W_OK):
    with open(log_file, "a") as file:
        file.write("New log entry\n")
else:
    print(f"Permission issue: Cannot write to {log_file}")
```
🛠 **Follow-up:** How would you **automatically adjust permissions** if needed?

---

### **Final Thoughts**  
These **Production Support File Handling Scenarios** test:  
✅ **Log Analysis & Monitoring**  
✅ **Automation & Housekeeping**  
✅ **Error Handling & Recovery**  
✅ **Process Management**  

Would you like **more scenario-based questions** related to **incident management or real-time alerting**? 🚀
