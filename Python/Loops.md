## **Conditional Statements, Looping Statements, and Loop Control Statements in Python**  

### **1. Conditional Statements**  
Conditional statements in Python are used to make decisions based on conditions. The common conditional statements are:  

| Conditional Statement | Description |
|----------------------|-------------|
| `if` | Executes a block of code **if** a condition is `True`. |
| `if-else` | Executes one block if the condition is `True`, otherwise executes another block. |
| `if-elif-else` | Checks multiple conditions in sequence. |
| `nested if` | An `if` statement inside another `if`. |

---

### **1.1 `if` Statement**  
Executes a block of code if the condition is `True`.  

#### **Example**:
```python
x = 10
if x > 5:  # Condition is True
    print("x is greater than 5")  
```
✅ **Output:** `x is greater than 5`

---

### **1.2 `if-else` Statement**  
Executes the `if` block if the condition is `True`, otherwise executes the `else` block.  

#### **Example**:
```python
x = 3
if x > 5:
    print("x is greater than 5")
else:
    print("x is less than or equal to 5")
```
✅ **Output:** `x is less than or equal to 5`

---

### **1.3 `if-elif-else` Statement**  
Used when multiple conditions need to be checked sequentially.  

#### **Example**:
```python
x = 20
if x < 10:
    print("x is less than 10")
elif x == 20:
    print("x is exactly 20")
else:
    print("x is greater than 10 but not 20")
```
✅ **Output:** `x is exactly 20`

---

### **1.4 `Nested if` Statement**  
An `if` statement inside another `if`.  

#### **Example**:
```python
x = 15
if x > 10:
    print("x is greater than 10")
    if x < 20:
        print("x is also less than 20")
```
✅ **Output:**  
```
x is greater than 10  
x is also less than 20  
```

---

## **2. Looping Statements**  
Loops are used to execute a block of code multiple times. Python supports three types of loops:

| Loop Type | Description |
|-----------|-------------|
| `for` loop | Iterates over a sequence (list, tuple, dictionary, set, or string). |
| `while` loop | Repeats code while a condition is `True`. |
| `nested loop` | A loop inside another loop. |

---

### **2.1 `for` Loop**  
Used to iterate over a sequence (like list, tuple, dictionary, string, or range).  

#### **Example 1: Iterating over a list**  
```python
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(fruit)
```
✅ **Output:**  
```
apple  
banana  
cherry  
```

#### **Example 2: Using `range()` function**
```python
for i in range(1, 6):  # Loops from 1 to 5
    print(i)
```
✅ **Output:**  
```
1  
2  
3  
4  
5  
```

---

### **2.2 `while` Loop**  
Executes a block of code as long as the condition is `True`.  

#### **Example**:
```python
x = 1
while x <= 5:
    print(x)
    x += 1  # Incrementing x
```
✅ **Output:**  
```
1  
2  
3  
4  
5  
```

---

### **2.3 `Nested Loops`**  
A loop inside another loop.  

#### **Example**:
```python
for i in range(1, 4):
    for j in range(1, 4):
        print(f"i={i}, j={j}")
```
✅ **Output:**  
```
i=1, j=1  
i=1, j=2  
i=1, j=3  
i=2, j=1  
i=2, j=2  
i=2, j=3  
i=3, j=1  
i=3, j=2  
i=3, j=3  
```

---

## **3. Loop Control Statements**  
Loop control statements change the execution of a loop.

| Control Statement | Description |
|------------------|-------------|
| `break` | Exits the loop completely. |
| `continue` | Skips the current iteration and moves to the next. |
| `pass` | Does nothing (used as a placeholder). |

---

### **3.1 `break` Statement**  
Used to exit the loop immediately.  

#### **Example**:
```python
for i in range(1, 10):
    if i == 5:
        break  # Stops the loop when i is 5
    print(i)
```
✅ **Output:**  
```
1  
2  
3  
4  
```

---

### **3.2 `continue` Statement**  
Skips the current iteration and continues with the next one.  

#### **Example**:
```python
for i in range(1, 6):
    if i == 3:
        continue  # Skips iteration when i is 3
    print(i)
```
✅ **Output:**  
```
1  
2  
4  
5  
```
(Note: `3` is skipped.)

---

### **3.3 `pass` Statement**  
A placeholder that does nothing. Useful when a loop or function needs to be defined but not implemented yet.  

#### **Example**:
```python
for i in range(5):
    if i == 2:
        pass  # Does nothing, just a placeholder
    print(i)
```
✅ **Output:**  
```
0  
1  
2  
3  
4  
```

---

## **Conclusion**  
✔ **Conditional Statements**: `if`, `if-else`, `if-elif-else`, `nested if`  
✔ **Looping Statements**: `for`, `while`, `nested loops`  
✔ **Loop Control Statements**: `break`, `continue`, `pass`  

These statements help in **decision making** and **iterating** over data efficiently in Python. 🚀
