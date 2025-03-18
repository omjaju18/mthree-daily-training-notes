### **Understanding `sort` and `uniq` Commands in Linux**
`sort` and `uniq` are powerful command-line utilities used to manipulate and analyze text files.

---

## **1️⃣ `sort` Command**
The `sort` command is used to arrange the lines in a file **in ascending or descending order**.

### **Basic Usage**
```bash
sort file.txt
```
This sorts the file alphabetically.

### **Common Options in `sort`**
| **Option**  | **Description** |
|-------------|----------------|
| `-r`        | Reverse order (descending sort) |
| `-n`        | Sort numerically (for numbers) |
| `-k COLUMN` | Sort by a specific column |
| `-t DELIM`  | Specify a delimiter (useful for CSV files) |
| `-u`        | Remove duplicate lines (same as `uniq`) |
| `-f`        | Ignore case while sorting |
| `-o FILE`   | Save the sorted output to a file |

### **Example**
#### **file.txt**
```
30 apple
10 banana
20 mango
40 orange
```
#### **Sort by the first column (numbers)**
```bash
sort -n file.txt
```
#### **Output**
```
10 banana
20 mango
30 apple
40 orange
```

---

## **2️⃣ `uniq` Command**
The `uniq` command is used to **filter out duplicate lines** in a sorted file.

### **Basic Usage**
```bash
uniq file.txt
```
⚠️ **Important:** `uniq` only works on **consecutive duplicate lines**, so the file must be sorted first.

### **Common Options in `uniq`**
| **Option**  | **Description** |
|-------------|----------------|
| `-d`        | Show only duplicate lines |
| `-u`        | Show only unique lines (no duplicates) |
| `-c`        | Show count of occurrences of each line |
| `-i`        | Ignore case when checking for duplicates |
| `--help`    | Show help information |

### **Example**
#### **file.txt**
```
apple
banana
apple
grape
banana
banana
orange
```
#### **Find duplicate lines**
```bash
sort file.txt | uniq -d
```
#### **Output**
```
apple
banana
```

#### **Count occurrences of each line**
```bash
sort file.txt | uniq -c
```
#### **Output**
```
  2 apple
  3 banana
  1 grape
  1 orange
```

---

## **Combining `sort` and `uniq`**
### **Find and Count Duplicate Lines in a File**
```bash
sort file.txt | uniq -c | sort -nr
```
This sorts, counts duplicates, and displays them in descending order.

---

Let me know if you need more details! 🚀
