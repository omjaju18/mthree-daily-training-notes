# **GREP Command - Detailed README**

## **Introduction**
`grep` (Global Regular Expression Print) is a powerful command-line tool in Linux used for searching text patterns within files. It is commonly used for filtering log files, configuration files, and other text-based documents.

---

## **Basic Syntax**
```bash
grep [OPTIONS] PATTERN [FILE...]
```
- `OPTIONS`: Various flags to modify search behavior.
- `PATTERN`: The string or pattern to search.
- `FILE`: The file(s) in which to search.

---

## **Commonly Used Options & Examples**

### **1️⃣ Basic Search**
```bash
grep "error" syslog.log
```
Searches for the word "error" in `syslog.log`.

### **2️⃣ Case-Insensitive Search (`-i`)**
```bash
grep -i "warning" messages.log
```
Finds both "warning" and "WARNING".

### **3️⃣ Display Line Numbers (`-n`)**
```bash
grep -n "failed login" auth.log
```
Shows matching lines with line numbers.

### **4️⃣ Count Matches (`-c`)**
```bash
grep -c "timeout" server.log
```
Displays the number of occurrences.

### **5️⃣ Search Recursively (`-r`)**
```bash
grep -r "critical error" /var/logs/
```
Searches in all files inside `/var/logs/`.

### **6️⃣ Show Only Filenames (`-l`)**
```bash
grep -l "database connection lost" logs/*
```
Lists files containing the phrase.

### **7️⃣ Invert Match (`-v`)**
```bash
grep -v "success" output.log
```
Displays lines **not** containing "success".

### **8️⃣ Show Matching Words Only (`-o`)**
```bash
grep -o "404" access.log
```
Prints only the matching word instead of the full line.

### **9️⃣ Match Whole Line (`-x`)**
```bash
grep -x "System OK" status.log
```
Finds lines that exactly match "System OK".

### **🔟 Search for Multiple Patterns (`-E`)**
```bash
grep -E "error|failed|timeout" syslog.log
```
Finds lines containing **any** of the provided words.

### **🔟 Highlight Matches (`--color`)**
```bash
grep --color=auto "disk failure" system.log
```
Highlights matching words in the output.

### **🔟 Show Lines Before Match (`-B`)**
```bash
grep -B 3 "segmentation fault" app.log
```
Shows 3 lines **before** each match.

### **🔟 Show Lines After Match (`-A`)**
```bash
grep -A 2 "shutdown" system.log
```
Displays 2 lines **after** each match.

### **🔟 Show Context Before & After (`-C`)**
```bash
grep -C 2 "kernel panic" sys.log
```
Shows 2 lines **before and after** each match.

### **🔟 Exclude Specific Files (`--exclude`)**
```bash
grep "memory leak" /var/logs/* --exclude=debug.log
```
Searches all files **except** `debug.log`.

### **🔟 Include Only Certain Files (`--include`)**
```bash
grep "crash" /var/logs/* --include=*.log
```
Searches only `.log` files.

### **🔟 Suppress Errors (`-s`)**
```bash
grep -s "not found" missingfile.log
```
Prevents error messages if a file does not exist.

---

## **30 Sample Questions with Answers**

### **Basic Search**
1️⃣ Find all lines in `server.log` that contain "error".
```bash
grep "error" server.log
```

2️⃣ Search for "timeout" in `network.log`, ignoring case.
```bash
grep -i "timeout" network.log
```

3️⃣ Show line numbers where "disk full" appears in `storage.log`.
```bash
grep -n "disk full" storage.log
```

### **Pattern Matching & Counting**
4️⃣ Count occurrences of "login failed" in `auth.log`.
```bash
grep -c "login failed" auth.log
```

5️⃣ Show only filenames where "service started" appears in `/var/logs/`.
```bash
grep -l "service started" /var/logs/*
```

### **Advanced Searches**
6️⃣ Display 4 lines after "kernel panic" in `sys.log`.
```bash
grep -A 4 "kernel panic" sys.log
```

7️⃣ Show lines not containing "success" in `results.log`.
```bash
grep -v "success" results.log
```

8️⃣ Search for "error" in `/var/logs/` but exclude `.bak` files.
```bash
grep -r "error" /var/logs/ --exclude=*.bak
```

9️⃣ Find occurrences of "connection reset" and highlight them.
```bash
grep --color=auto "connection reset" network.log
```

🔟 Search for "access denied" in `auth.log` and show filenames only.
```bash
grep -l "access denied" auth.log
```

---

## **GREP Cheat Sheet**
| Option | Description |
|--------|-------------|
| `-i` | Case-insensitive search |
| `-n` | Show line numbers |
| `-c` | Count occurrences |
| `-r` | Recursive search in directories |
| `-l` | Show filenames with matches |
| `-v` | Invert match (show lines that do not match) |
| `-o` | Show only matching words |
| `-x` | Match whole line |
| `-E` | Extended search (multiple patterns) |
| `--color=auto` | Highlight matches |
| `-A [N]` | Show N lines **after** match |
| `-B [N]` | Show N lines **before** match |
| `-C [N]` | Show N lines **before and after** match |
| `--exclude=[file]` | Exclude specific files from search |
| `--include=[pattern]` | Search only specific file types |

---

## **Conclusion**
`grep` is a crucial tool for searching text efficiently in Linux. By mastering different options, you can extract valuable information from large log files and automate text processing tasks effectively.

Happy Grepping! 🚀

