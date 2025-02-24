# Linux Proccess Commands

### 1. **`ps` (Process Status)**  
   - Displays information about running processes.  

   **Options:**  
   - `-e` → Show all processes.  
   - `-f` → Full-format listing.  
   - `-u user` → Show processes for a specific user.  
   - `aux` → Show detailed information of all processes.

   **Example:**  
   ```bash
   ps -ef
   ```
   Lists all running processes in a detailed format.

---

### 2. **`top` (Monitor Processes in Real-Time)**  
   - Displays system-wide tasks and resource usage.  

   **Options:**  
   - `-d seconds` → Refresh every `seconds`.  
   - `-o field` → Sort by a specific field.  
   - `-u user` → Show processes for a specific user.  
   - `-p PID` → Show details for a specific process.  

   **Example:**  
   ```bash
   top -o %MEM
   ```
   Sorts processes by memory usage.

---

### 3. **`htop` (Enhanced `top`)**  
   - A more interactive process viewer (requires installation).  

   **Options:**  
   - `-d N` → Set refresh delay to `N` seconds.  
   - `-u user` → Show processes of a specific user.  

   **Example:**  
   ```bash
   htop
   ```
   Displays an interactive process monitoring interface.

---

### 4. **`pidof` (Find Process ID)**  
   - Retrieves the PID of a running program.  

   **Options:**  
   - `-s` → Show only the first PID.  
   - `-x` → Include scripts as well.  

   **Example:**  
   ```bash
   pidof nginx
   ```
   Gets the PID of the `nginx` process.

---

### 5. **`kill` (Terminate a Process)**  
   - Sends a signal to a process.  

   **Options:**  
   - `-9` → Forcefully kill a process.  
   - `-15` → Gracefully terminate a process (default).  

   **Example:**  
   ```bash
   kill -9 1234
   ```
   Forcefully stops the process with PID `1234`.

---

### 6. **`pkill` (Kill Process by Name)**  
   - Kills a process by matching its name.  

   **Options:**  
   - `-f` → Match full command name.  
   - `-u user` → Kill processes of a specific user.  
   - `-9` → Force kill.  

   **Example:**  
   ```bash
   pkill -f python
   ```
   Kills all Python-related processes.

---

### 7. **`killall` (Kill All Instances of a Process)**  
   - Terminates all processes with a given name.  

   **Options:**  
   - `-u user` → Kill processes of a specific user.  
   - `-9` → Force kill.  

   **Example:**  
   ```bash
   killall firefox
   ```
   Stops all `firefox` processes.

---

### 8. **`nice` (Start Process with Priority)**  
   - Runs a process with a specific priority.  

   **Options:**  
   - `-n N` → Set priority `N` (-20 is highest, 19 is lowest).  

   **Example:**  
   ```bash
   nice -n 10 myscript.sh
   ```
   Starts `myscript.sh` with priority 10.

---

### 9. **`renice` (Change Priority of Running Process)**  
   - Adjusts priority of an active process.  

   **Options:**  
   - `-n N` → Change priority to `N`.  
   - `-p PID` → Change priority of process by PID.  

   **Example:**  
   ```bash
   renice -5 -p 1234
   ```
   Changes priority of process `1234` to `-5`.

---

### 10. **`bg` (Resume Process in Background)**  
   - Resumes a suspended process in the background.  

   **Options:**  
   - `%N` → Resume the `N`th background job.  

   **Example:**  
   ```bash
   bg %1
   ```
   Resumes the first background job.

---

### 11. **`fg` (Bring Background Process to Foreground)**  
   - Moves a background process to the foreground.  

   **Options:**  
   - `%N` → Bring the `N`th background job to the foreground.  

   **Example:**  
   ```bash
   fg %1
   ```
   Brings the first background job to the foreground.

---

### 12. **`jobs` (List Background Jobs)**  
   - Displays background jobs.  

   **Options:**  
   - `-l` → Show process IDs.  

   **Example:**  
   ```bash
   jobs -l
   ```
   Lists background jobs with their PIDs.

---

### 13. **`nohup` (Run Process That Ignores Hangups)**  
   - Allows a command to run even after logout.  

   **Options:**  
   - `&` → Runs command in background.  

   **Example:**  
   ```bash
   nohup myscript.sh &
   ```
   Runs `myscript.sh` in the background and prevents it from stopping after logout.

---

### 14. **`disown` (Remove Process from Job Table)**  
   - Removes a job from the shell’s job table.  

   **Options:**  
   - `-h` → Keep the job but prevent it from being terminated.  

   **Example:**  
   ```bash
   disown -h %1
   ```
   Removes job 1 from the shell's job list.

---

### 15. **`strace` (Trace System Calls)**  
   - Debugs and monitors system calls made by a process.  

   **Options:**  
   - `-p PID` → Attach to an existing process.  
   - `-c` → Count system calls.  
   - `-o file` → Output to a file.  

   **Example:**  
   ```bash
   strace -p 1234
   ```
   Traces system calls of process `1234`.
