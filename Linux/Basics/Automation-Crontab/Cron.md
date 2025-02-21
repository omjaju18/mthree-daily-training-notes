# **Scheduled & Automated Tasks in Linux**

Linux provides several ways to **schedule and automate tasks**, mainly using **cron**, **at**, and **systemd timers**.

---

## **1. Cron Jobs (Recurring Tasks)**
`cron` is a built-in job scheduler in Linux that runs tasks at specified intervals.

### **Basic Commands**
```bash
crontab -e   # Edit cron jobs
crontab -l   # List cron jobs
crontab -r   # Remove all cron jobs
```

### **Cron Job Format**
```
MIN HOUR DAY MONTH DAY-OF-WEEK COMMAND
```
| Field       | Values        |
|------------|--------------|
| `MIN`      | 0 - 59       |
| `HOUR`     | 0 - 23       |
| `DAY`      | 1 - 31       |
| `MONTH`    | 1 - 12       |
| `DAY-OF-WEEK` | 0 - 6 (0 = Sunday) |
| `COMMAND`  | The script/command to execute |

### **Example Cron Jobs**
```bash
30 2 * * * /home/user/backup.sh   # Run script daily at 2:30 AM
0 17 * * 1 /home/user/script.sh   # Run script every Monday at 5:00 PM
*/10 * * * * /home/user/script.sh  # Run script every 10 minutes
0 0 * * * find /var/log -name "*.log" -type f -mtime +7 -delete  # Delete old logs daily at midnight
0 8 * * * python3 /home/user/script.py  # Run Python script daily at 8 AM
```

---

## **How to Create a Cron Job in Linux**

A **cron job** is a scheduled task in Linux that runs automatically at specified times. Here’s a step-by-step guide to setting up a cron job.

### **Step 1: Open the Crontab Editor**
To create a cron job, use the following command:
```bash
crontab -e
```
- If running for the **first time**, it may ask you to choose an editor (select `nano` if unsure).
- This opens the **crontab file** where you can define your scheduled tasks.

### **Step 2: Add a New Cron Job**
Inside the crontab editor, add a new line in the following format:

```
MIN HOUR DAY MONTH DAY-OF-WEEK COMMAND
```
| Field       | Values        | Example |
|------------|--------------|---------|
| `MIN`      | 0 - 59       | `30` (30th minute) |
| `HOUR`     | 0 - 23       | `14` (2 PM) |
| `DAY`      | 1 - 31       | `*` (Any day) |
| `MONTH`    | 1 - 12       | `*` (Any month) |
| `DAY-OF-WEEK` | 0 - 6 (0 = Sunday) | `5` (Friday) |
| `COMMAND`  | The script/command to execute | `/home/user/script.sh` |

#### **Example Cron Jobs**
1️⃣ **Run a script every day at 2:30 AM**  
```bash
30 2 * * * /home/user/backup.sh
```
2️⃣ **Run a script every Friday at 6:00 PM**  
```bash
0 18 * * 5 /home/user/fixGenerator.sh
```
3️⃣ **Run a Python script every day at 8 AM**  
```bash
0 8 * * * python3 /home/user/script.py
```

### **Step 3: Save and Exit**
- **If using nano:** Press `CTRL + X`, then `Y`, and hit `Enter`.  
- **If using vim:** Press `ESC`, then type `:wq`, and hit `Enter`.  

### **Step 4: Verify the Cron Job**
Check if the cron job was added successfully:
```bash
crontab -l
```

### **Step 5: Ensure the Script is Executable**
Before the cron job runs, make sure the script has **execute permissions**:
```bash
chmod +x /home/user/fixGenerator.sh
```

### **Step 6: Restart the Cron Service (if needed)**
To ensure the cron service is running:
```bash
sudo systemctl restart cron
```

### **Step 7: Check Cron Logs (If Debugging Issues)**
If the cron job doesn't seem to run, check the logs:
```bash
grep CRON /var/log/syslog | tail -20
```

✅ **Now your cron job is successfully set up and will run at the scheduled time!** 🚀

---

## **2. `at` Command (One-Time Scheduled Task)**
The `at` command allows scheduling a one-time job for a later time.

### **Install `at` (if not installed)**
```bash
sudo apt install at  # Debian-based (Ubuntu)
sudo yum install at  # RHEL-based (CentOS)
```

### **Start the `at` Service**
```bash
sudo systemctl enable atd
sudo systemctl start atd
```

### **Scheduling a Task with `at`**
```bash
echo "/home/user/script.sh" | at 18:00   # Run script at 6:00 PM today
echo "/home/user/script.sh" | at 9:30 AM tomorrow   # Run script tomorrow at 9:30 AM
echo "echo 'Hello, World!'" | at now + 15 minutes   # Run task in 15 minutes
```

### **Manage `at` Jobs**
```bash
atq  # List scheduled `at` jobs
atrm <job_number>  # Remove a scheduled job
```

---

## **3. Systemd Timers (Advanced Scheduling)**
Linux `systemd` timers provide more flexibility than `cron` and `at`.

### **Create a systemd service file**
```bash
sudo nano /etc/systemd/system/myscript.service
```
```ini
[Unit]
Description=Run My Script

[Service]
ExecStart=/home/user/myscript.sh
```

### **Create a timer file**
```bash
sudo nano /etc/systemd/system/myscript.timer
```
```ini
[Unit]
Description=Run My Script Every Hour

[Timer]
OnCalendar=hourly
Persistent=true

[Install]
WantedBy=timers.target
```

### **Enable and Start the Timer**
```bash
sudo systemctl enable myscript.timer
sudo systemctl start myscript.timer
```

### **Check Timer Status**
```bash
systemctl list-timers
```

---

## **Comparison of Task Schedulers**
| Scheduler  | Best For |
|------------|---------|
| `cron` | Recurring tasks (e.g., backups, monitoring) |
| `at` | One-time tasks (e.g., shutdown, reminders) |
| `systemd timers` | Advanced scheduling with logs & dependencies |
