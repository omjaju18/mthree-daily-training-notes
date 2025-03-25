File handling in Python allows you to work with files—reading from and writing to them. Python provides built-in functions to manipulate files efficiently.

## **Opening a File**
Python uses the `open()` function to open files. The syntax is:

```python
file = open("filename", "mode")
```

### **File Modes**
| Mode | Description |
|------|------------|
| `'r'`  | Read mode (default) - Opens a file for reading, raises an error if file doesn't exist |
| `'w'`  | Write mode - Creates a file if it doesn’t exist, overwrites content if it does |
| `'a'`  | Append mode - Adds data at the end of the file, creates the file if it doesn't exist |
| `'x'`  | Exclusive creation - Creates a file, fails if it already exists |
| `'b'`  | Binary mode - Used with `rb`, `wb`, etc., for non-text files (e.g., images) |
| `'t'`  | Text mode (default) - Used for text files |

---

## **Reading a File**
### **1. Reading the whole file**
```python
file = open("sample.txt", "r")  # Open in read mode
content = file.read()  # Read entire file
print(content)
file.close()  # Close the file
```

### **2. Reading line by line**
```python
file = open("sample.txt", "r")
for line in file:
    print(line.strip())  # Removes newline characters
file.close()
```

### **3. Using `readlines()`**
```python
file = open("sample.txt", "r")
lines = file.readlines()  # Returns a list of lines
print(lines)
file.close()
```

---

## **Writing to a File**
### **1. Writing a new file (`w` mode)**
```python
file = open("sample.txt", "w")
file.write("Hello, Python!\nThis is file handling.")
file.close()
```

### **2. Appending to a file (`a` mode)**
```python
file = open("sample.txt", "a")
file.write("\nAppending a new line.")
file.close()
```

---

## **Using `with` Statement (Best Practice)**
Using `with` ensures that the file is properly closed after the block execution.

```python
with open("sample.txt", "r") as file:
    content = file.read()
    print(content)  # File automatically closes after this block
```

---

## **Checking if a File Exists**
```python
import os

if os.path.exists("sample.txt"):
    print("File exists")
else:
    print("File not found")
```

---

## **File Handling in Binary Mode**
### **Reading a binary file**
```python
with open("image.jpg", "rb") as file:
    binary_data = file.read()
```

### **Writing a binary file**
```python
with open("copy.jpg", "wb") as file:
    file.write(binary_data)
```

---

## **Deleting a File**
```python
import os

if os.path.exists("sample.txt"):
    os.remove("sample.txt")
    print("File deleted")
else:
    print("File does not exist")
```

---

### **Summary**
- Use `open("filename", "mode")` to open files.
- Always close files (`file.close()`) or use `with open(...)` for auto-closing.
- Read using `.read()`, `.readline()`, or `.readlines()`.
- Write using `.write()` or `.writelines()`.
- Use `os.remove("filename")` to delete a file.

Would you like an example of handling CSV or JSON files? 🚀
