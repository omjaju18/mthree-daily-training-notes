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

Here are more **scenario-based questions** for **file handling in Python**, specifically for a **Production Support** role:

---

## **9. Parsing a Configuration File and Validating Settings**
🔹 **Scenario:**  
Your application reads configurations from a `config.ini` file. Sometimes, due to human error, certain required fields are missing, leading to production failures. You need to write a script that **validates if all required keys are present** in the file.  

💡 **How would you ensure the configuration file is valid before the application starts?**  

✅ **Solution:**  
```python
import configparser

required_keys = {"database", "host", "port", "username", "password"}
config = configparser.ConfigParser()
config.read("config.ini")

if "DEFAULT" in config:
    missing_keys = required_keys - set(config["DEFAULT"].keys())
    if missing_keys:
        print(f"Missing keys: {missing_keys}")
    else:
        print("Configuration file is valid.")
else:
    print("Configuration section missing.")
```
🛠 **Follow-up:** How would you handle missing or incorrect data types (e.g., `port` should be an integer)?

---

## **10. Detecting and Handling Corrupt Log Files**  
🔹 **Scenario:**  
Your production system generates log files every hour. Sometimes, logs become corrupted (e.g., **truncated lines, missing timestamps, or binary characters**). You need to scan logs and **flag corrupt entries**.  

💡 **How would you detect corruption in log files?**  

✅ **Solution:**  
```python
import re

log_file = "server.log"
pattern = re.compile(r"^\d{4}-\d{2}-\d{2} \d{2}:\d{2}:\d{2} - (INFO|ERROR|WARNING) - .+$")

with open(log_file, "r", encoding="utf-8", errors="replace") as file:
    for line in file:
        if not pattern.match(line):
            print(f"Corrupt entry detected: {line.strip()}")
```
🛠 **Follow-up:** How would you automate a **self-healing mechanism** to fix corrupted logs?

---

## **11. Recovering Missing Log Entries from Backups**  
🔹 **Scenario:**  
A production outage caused logs between **1 PM and 2 PM** to be lost. However, backups are stored in `/backup/logs/`. You need to **restore missing logs** from backups into the main log file.  

💡 **How would you do this?**  

✅ **Solution:**  
```python
import shutil

backup_dir = "/backup/logs/"
main_log_file = "/var/logs/app.log"

# Copy backup logs for the missing time range
shutil.copy(backup_dir + "app-2025-03-25-13.log", main_log_file)
shutil.copy(backup_dir + "app-2025-03-25-14.log", main_log_file)
print("Logs restored successfully.")
```
🛠 **Follow-up:** How would you **automate this process** to check missing logs dynamically?

---

## **12. Identifying Unauthorized File Modifications**
🔹 **Scenario:**  
Critical files in `/etc/app/` should **not** be modified manually. However, unauthorized changes have been detected. You need a Python script to **compare file checksums** and alert if changes occur.  

💡 **How would you detect unauthorized modifications?**  

✅ **Solution:**  
```python
import hashlib

def get_checksum(file_path):
    with open(file_path, "rb") as f:
        return hashlib.sha256(f.read()).hexdigest()

file_path = "/etc/app/config.cfg"
expected_checksum = "abcd1234xyz..."  # Store this from a trusted state

if get_checksum(file_path) != expected_checksum:
    print("ALERT: Unauthorized modification detected!")
```
🛠 **Follow-up:** How can you **automatically restore** the file if tampered with?

---

## **13. Merging Multiple Log Files Chronologically**
🔹 **Scenario:**  
Your application generates **hourly logs**, but an analysis tool requires **all logs merged in order**. The logs are stored as:  
```
app-2025-03-25-00.log
app-2025-03-25-01.log
...
app-2025-03-25-23.log
```
You need to **merge them into a single log file in chronological order**.  

💡 **How would you handle this?**  

✅ **Solution:**  
```python
import glob

log_files = sorted(glob.glob("app-2025-03-25-*.log"))  # Sort to ensure order
with open("merged_logs.log", "w") as output:
    for file in log_files:
        with open(file, "r") as log:
            output.write(log.read() + "\n")

print("Logs merged successfully.")
```
🛠 **Follow-up:** How would you handle duplicate entries in logs?

---

## **14. Finding Files with Specific Content (Search within Files)**  
🔹 **Scenario:**  
A production bug occurred where certain log files contain `"Segmentation Fault"`. You need to search all logs in `/var/logs/` and **list files containing this keyword**.  

💡 **How would you efficiently find these files?**  

✅ **Solution:**  
```python
import os

log_dir = "/var/logs/"
search_term = "Segmentation Fault"

for file in os.listdir(log_dir):
    file_path = os.path.join(log_dir, file)
    if os.path.isfile(file_path):
        with open(file_path, "r", errors="ignore") as f:
            if search_term in f.read():
                print(f"Found in: {file_path}")
```
🛠 **Follow-up:** How would you optimize this for **large log files**?

---

## **15. Tracking File Growth in Real-Time**  
🔹 **Scenario:**  
A production log file **should not exceed 1GB**. If it does, a new log file should be created (`logfile_1.log`, `logfile_2.log`, etc.).  

💡 **How would you track file growth and rotate logs?**  

✅ **Solution:**  
```python
import os

log_file = "app.log"
max_size = 1 * 1024 * 1024 * 1024  # 1GB

if os.path.exists(log_file) and os.path.getsize(log_file) > max_size:
    os.rename(log_file, f"{log_file}.1")
    open(log_file, "w").close()  # Create a new empty log file
    print("Log rotated.")
```
🛠 **Follow-up:** How would you integrate this with **log rotation policies** like `logrotate`?

---

## **16. Sending Alerts When a Critical File is Deleted**
🔹 **Scenario:**  
Your application depends on `/var/data/important.csv`. If this file gets deleted, an alert should be **immediately triggered**.  

💡 **How would you monitor and alert if the file is missing?**  

✅ **Solution:**  
```python
import os
import time

file_path = "/var/data/important.csv"

while True:
    if not os.path.exists(file_path):
        print(f"ALERT: {file_path} has been deleted!")
        break
    time.sleep(10)  # Check every 10 seconds
```
🛠 **Follow-up:** How can you integrate this with **email or Slack alerts**?

---

### **Final Thoughts**  
These **scenario-based questions** test your ability to:  
✅ **Troubleshoot production issues**  
✅ **Automate log & file management**  
✅ **Detect & recover from failures**  
✅ **Enhance system observability**  

