## **AWK Command in Linux – A Detailed Guide**  

AWK is a **powerful text-processing tool** used for **pattern scanning, data extraction, and reporting** in Linux. It processes text **line by line**, splitting each line into **fields**, applying conditions, and executing commands.  

### **📌 Why Use AWK?**  
✅ **Extract and manipulate text from files**  
✅ **Process structured data like CSV, logs, etc.**  
✅ **Perform arithmetic operations on data**  
✅ **Filter and format output**  

---

## **1️⃣ Basic Syntax**
```bash
awk 'pattern { action }' filename
```
🔹 **pattern** → Defines which lines to match  
🔹 **action** → Specifies what to do with those lines  
🔹 **filename** → File to process  

If no **pattern** is provided, AWK executes the action **for every line**.

---

## **2️⃣ AWK Internal Variables**
| Variable | Description |
|----------|------------|
| `$0` | Entire line of input |
| `$1`, `$2`, `$3`... | Individual fields (columns) |
| `NF` | Number of fields in the current line |
| `NR` | Current record (line) number |
| `FS` | Field separator (default: space/tab) |
| `OFS` | Output field separator (default: space) |
| `RS` | Record separator (default: newline) |
| `ORS` | Output record separator (default: newline) |

---

## **3️⃣ Basic Examples**
### **1. Print a specific column from a file**
Extract **column 2** from `data.txt`:
```bash
awk '{ print $2 }' data.txt
```
👉 Prints the **second field** from each line.

---

### **2. Print lines matching a pattern**
Find lines containing **"error"** in `log.txt`:
```bash
awk '/error/ { print $0 }' log.txt
```
👉 Prints **entire lines** where "error" appears.

---

### **3. Print only lines where column 3 is greater than 50**
```bash
awk '$3 > 50 { print $0 }' data.txt
```
👉 Prints **entire line** where the **third column** is greater than 50.

---

### **4. Print line numbers with output**
```bash
awk '{ print NR, $0 }' file.txt
```
👉 Adds a **line number** before each line.

---

## **4️⃣ Field Separator (FS)**
By default, AWK splits fields using **spaces or tabs**. You can change it using `-F`.

### **1. Working with CSV files**
```bash
awk -F ',' '{ print $1, $3 }' data.csv
```
👉 Extracts **1st and 3rd** columns from a **comma-separated file**.

### **2. Changing Output Separator**
```bash
awk -F ':' 'BEGIN { OFS=" - " } { print $1, $2 }' users.txt
```
👉 Changes the output separator from **space** to **"-"**.

---

## **5️⃣ Advanced AWK Features**
### **1. Perform arithmetic operations**
```bash
awk '{ sum = $2 + $3; print $1, sum }' data.txt
```
👉 Adds **column 2** and **column 3**, prints result.

---

### **2. Conditional Statements**
```bash
awk '{ if ($3 > 50) print $1, "Passed"; else print $1, "Failed"; }' marks.txt
```
👉 Prints `"Passed"` or `"Failed"` based on column **3**.

---

### **3. Using AWK with Shell Variables**
```bash
threshold=100
awk -v limit=$threshold '$2 > limit { print $1, $2 }' data.txt
```
👉 Passes shell variable **$threshold** into AWK.

---

## **6️⃣ AWK vs GREP vs SED**
| Feature | AWK | GREP | SED |
|---------|-----|------|-----|
| **Pattern Matching** | ✅ | ✅ | ✅ |
| **Text Extraction** | ✅ | ❌ | ❌ |
| **Mathematical Operations** | ✅ | ❌ | ❌ |
| **Substitution (Replace Text)** | ✅ | ❌ | ✅ |
| **Column Processing** | ✅ | ❌ | ❌ |

- **Use `grep`** when you **only need to find matching lines**  
- **Use `sed`** when you need **to replace text**  
- **Use `awk`** when you need **advanced text processing** (filters, math, formatting)

---

## **7️⃣ Real-World Use Cases**
### **1. Get Disk Usage of Home Directory**
```bash
df -h | awk '$NF=="/home" { print $5 }'
```
👉 Extracts **disk usage percentage** of `/home`.

---

### **2. Extract Usernames from `/etc/passwd`**
```bash
awk -F ':' '{ print $1 }' /etc/passwd
```
👉 Prints all **usernames** in the system.

---

### **3. Find Average CPU Usage**
```bash
top -bn1 | awk '/Cpu/ { print "CPU Usage:", $2 + $4 "%"}'
```
👉 Extracts and prints **CPU usage**.

---

## **🔥 Summary**
✅ **AWK is a powerful tool for text processing**  
✅ Can **filter, extract, and manipulate structured text**  
✅ Works well with **logs, CSV, and structured data**  
✅ Supports **arithmetic operations, conditions, and formatting**  

🚀 **Want more examples or real-world problems? Let me know!** 😃
