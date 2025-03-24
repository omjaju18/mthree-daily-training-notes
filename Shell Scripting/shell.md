## **Shell Scripting – Detailed Guide with Syntax & Examples**  
Shell scripting is the process of writing a sequence of commands for the shell (command-line interpreter) to execute. It is commonly used for automation, system administration, and task scheduling.

---

## **1️⃣ What is a Shell Script?**  
A shell script is a text file containing a series of UNIX commands that are executed sequentially. It typically has a **`.sh`** extension.

### **Example of a Simple Shell Script (`hello.sh`)**
```sh
#!/bin/bash
echo "Hello, Om! Welcome to Shell Scripting!"
```
🔹 `#!/bin/bash` → Shebang, specifies the shell interpreter.  
🔹 `echo "..."` → Prints output to the terminal.

#### **Run the Script**  
```sh
chmod +x hello.sh  # Make script executable
./hello.sh         # Run the script
```

---

## **2️⃣ Variables in Shell Scripting**  
### **Syntax:**
```sh
variable_name="value"
echo $variable_name
```

### **Example:**
```sh
#!/bin/bash
name="Om Jaju"
echo "My name is $name"
```
✅ **Output:**  
```
My name is Om Jaju
```

---

## **3️⃣ Taking User Input**
### **Example:**
```sh
#!/bin/bash
echo "Enter your name: "
read name
echo "Hello, $name!"
```
✅ **Output:**  
```
Enter your name:
Om
Hello, Om!
```

---

## **4️⃣ Conditional Statements**
### **Syntax:**
```sh
if [ condition ]; then
   # Code to execute if condition is true
elif [ another_condition ]; then
   # Another condition check
else
   # Code to execute if all conditions fail
fi
```

### **Example (Check Even or Odd):**
```sh
#!/bin/bash
echo "Enter a number:"
read num
if [ $((num % 2)) -eq 0 ]; then
    echo "$num is even"
else
    echo "$num is odd"
fi
```

✅ **Output:**  
```
Enter a number:
5
5 is odd
```

---

## **5️⃣ Loops in Shell Scripting**
### **A) `for` Loop**
```sh
for i in 1 2 3 4 5
do
  echo "Number: $i"
done
```

✅ **Output:**  
```
Number: 1
Number: 2
Number: 3
Number: 4
Number: 5
```

---

### **B) `while` Loop**
```sh
#!/bin/bash
counter=1
while [ $counter -le 5 ]
do
    echo "Counter: $counter"
    ((counter++))
done
```

✅ **Output:**  
```
Counter: 1
Counter: 2
Counter: 3
Counter: 4
Counter: 5
```

---

## **6️⃣ Functions in Shell Scripting**
### **Syntax:**
```sh
function_name() {
    # Commands
}
```

### **Example:**
```sh
#!/bin/bash
greet() {
    echo "Hello, $1!"
}
greet "Om"
```

✅ **Output:**  
```
Hello, Om!
```

---

## **7️⃣ Command-Line Arguments**
You can pass arguments when running a script.

### **Example (`args.sh`):**
```sh
#!/bin/bash
echo "First argument: $1"
echo "Second argument: $2"
```

#### **Run the script with arguments:**
```sh
./args.sh Om Jaju
```

✅ **Output:**  
```
First argument: Om
Second argument: Jaju
```

---

## **8️⃣ File Handling in Shell Scripting**
### **A) Reading a File**
```sh
#!/bin/bash
while read line; do
    echo "$line"
done < file.txt
```

### **B) Writing to a File**
```sh
echo "This is a test" > output.txt
```

---

## **9️⃣ Scheduling Shell Scripts (Cron Jobs)**
You can schedule scripts using **cron jobs**.

### **Edit Crontab:**
```sh
crontab -e
```

### **Example (Run script every day at 5 AM)**
```
0 5 * * * /home/user/script.sh
```

---

## **🔟 Important Shell Commands Used in Scripts**
| Command | Description |
|---------|------------|
| `echo` | Prints output |
| `read` | Reads user input |
| `ls` | Lists files/directories |
| `pwd` | Shows current directory |
| `cd` | Changes directory |
| `cp` | Copies files |
| `mv` | Moves/renames files |
| `rm` | Deletes files/directories |
| `chmod` | Changes file permissions |
| `grep` | Searches text in files |
| `find` | Finds files/directories |
| `sed` | Stream editor for modifying text |

---

## **💡 Summary**
- Shell scripting automates tasks in Linux.
- Variables store data, loops execute repeatedly, and functions structure code.
- File handling and command-line arguments make scripts more dynamic.
- Scheduling scripts using `cron` automates execution.

Would you like **real-world examples** (e.g., backup automation, log monitoring)? 🚀
