# Triggers & Stored Procedures in SQL

## **1. Introduction**
SQL **Stored Procedures** and **Triggers** are powerful database features that help in automating tasks, ensuring data integrity, and optimizing performance. This document explains their concepts, benefits, and provides examples.

---

## **2. Stored Procedures**

### **What is a Stored Procedure?**
A **Stored Procedure** is a collection of SQL statements that are stored in the database and can be executed multiple times. It helps in reducing redundancy and improving performance.

### **Example: Simple Employee Insertion Procedure**
#### **Step 1: Create the Table**
```sql
CREATE TABLE employees (
    emp_id INT AUTO_INCREMENT PRIMARY KEY,
    emp_name VARCHAR(100),
    salary DECIMAL(10,2)
);
```

#### **Step 2: Create the Stored Procedure**
```sql
DELIMITER //

CREATE PROCEDURE AddEmployee(
    IN name VARCHAR(100), 
    IN salary DECIMAL(10,2)
)
BEGIN
    INSERT INTO employees (emp_name, salary) VALUES (name, salary);
END //

DELIMITER ;
```

#### **Step 3: Execute the Procedure**
```sql
CALL AddEmployee('John Doe', 50000);
```

### **✅ Benefits of Stored Procedures**
- **Performance Optimization:** Reduces execution time by precompiling queries.
- **Security:** Prevents SQL injection by restricting direct table access.
- **Reusability:** Can be called multiple times without rewriting queries.
- **Consistency:** Ensures business logic is enforced at the database level.

---

## **3. SQL Triggers**

### **What is a Trigger?**
A **Trigger** is an automated SQL procedure that runs before or after an event (`INSERT`, `UPDATE`, `DELETE`) on a table.

### **Example: Logging Withdrawals from a Bank Account**
#### **Step 1: Create Tables**
```sql
CREATE TABLE accounts (
    account_id INT PRIMARY KEY,
    balance DECIMAL(10,2)
);

CREATE TABLE transaction_logs (
    log_id INT AUTO_INCREMENT PRIMARY KEY,
    account_id INT,
    transaction_type VARCHAR(50),
    amount DECIMAL(10,2),
    transaction_time TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

#### **Step 2: Create the Trigger**
```sql
CREATE TRIGGER LogTransaction
AFTER UPDATE ON accounts
FOR EACH ROW
BEGIN
    INSERT INTO transaction_logs(account_id, transaction_type, amount, transaction_time)
    VALUES (OLD.account_id, 'Withdrawal', OLD.balance - NEW.balance, NOW());
END;
```

### **✅ Benefits of Triggers**
- **Automated Auditing:** Tracks all changes automatically.
- **Enforces Business Rules:** Prevents unauthorized modifications.
- **Maintains Data Integrity:** Ensures data consistency across tables.
- **Event-Driven Execution:** Executes specific tasks when needed.

---

## **4. Key Differences Between Procedures & Triggers**

| Feature         | Stored Procedure | Trigger |
|---------------|----------------|---------|
| **Execution** | Manually executed via `CALL` | Automatically executed on `INSERT/UPDATE/DELETE` |
| **Use Case** | Complex operations, business logic | Enforcing constraints, logging, automation |
| **Performance** | Faster execution, reduces network load | Adds overhead for frequent triggers |
| **Control** | Called as needed | Fires automatically |

---

## **5. Conclusion**
Both **Stored Procedures and Triggers** enhance database efficiency, security, and consistency. While **procedures** are useful for modular operations, **triggers** ensure automated enforcement of business rules.

### **🚀 Best Practices:**
- Use **procedures** for business logic to keep application code clean.
- Use **triggers** for automation but avoid excessive use to prevent performance issues.
- Ensure proper **error handling** in procedures and triggers.
  ---


  # **Indexing in SQL** 🚀  

## **Introduction**  
Indexing is a technique in databases that **speeds up data retrieval** by creating a structure (like an index in a book) that allows for **faster searching**. Instead of scanning an entire table, the database uses the index to locate data quickly.

---

## **Types of Indexing**  

### **1. Clustered Index**
- A **clustered index** determines the **physical order** of data in a table.
- There can be **only one clustered index** per table because the rows can be physically sorted in only one way.
- The **primary key** of a table **automatically creates a clustered index** (unless specified otherwise).

🔹 **Example of Clustered Index**  
Let’s say we have a `Students` table:

| Student_ID (PK) | Name  | Age |  
|-----------------|-------|----|  
| 101            | Om    | 22 |  
| 102            | Raj   | 21 |  
| 103            | Priya | 23 |  

Since `Student_ID` is the **Primary Key**, it **automatically creates a clustered index**, meaning data is **physically stored in the order of `Student_ID`**.

**Creating a Clustered Index manually:**
```sql
CREATE CLUSTERED INDEX idx_student_id  
ON Students(Student_ID);
```

✅ **Advantages of Clustered Indexing:**  
- Faster **range-based queries** (`BETWEEN`, `ORDER BY`).  
- Efficient **sorting** since data is stored in order.  

❌ **Disadvantages of Clustered Indexing:**  
- **Slower inserts/updates/deletes** because data has to be rearranged.  
- **Only one clustered index per table** (as it affects physical order).  

---

### **2. Non-Clustered Index**
- A **non-clustered index** does not affect the physical storage order of data.
- It creates a separate **lookup table** that stores pointers to the actual data.
- There can be **multiple non-clustered indexes** on a single table.

🔹 **Example of Non-Clustered Index**  
Suppose we frequently search for students by **Name**, but our primary key is `Student_ID`.

**Creating a Non-Clustered Index on Name:**
```sql
CREATE INDEX idx_student_name  
ON Students(Name);
```
Now, if we run:
```sql
SELECT * FROM Students WHERE Name = 'Om';
```
The database **quickly looks up** the index instead of scanning the whole table.

✅ **Advantages of Non-Clustered Indexing:**  
- **Faster searches** for non-primary key columns.  
- **Multiple non-clustered indexes** can exist per table.  

❌ **Disadvantages of Non-Clustered Indexing:**  
- Takes **extra storage** space.  
- **Slower writes (INSERT, UPDATE, DELETE)** because indexes must be updated.

---

### **Clustered vs. Non-Clustered Index: Key Differences**
| Feature              | Clustered Index | Non-Clustered Index |
|----------------------|----------------|---------------------|
| **Physical Storage** | Sorts & stores data in order | Stores separately, uses pointers |
| **Number per Table** | Only **one** | **Multiple** allowed |
| **Speed for Retrieval** | Faster for **range queries** | Faster for **specific searches** |
| **Speed for Updates** | Slower (needs reordering) | Faster (less reordering) |
| **Example** | Primary Key (`Student_ID`) | Searching by `Name` |

---

## **Conclusion**
- **Clustered Index** = **Physically sorts data**, faster for range queries, but only one per table.
- **Non-Clustered Index** = **Uses pointers**, multiple allowed, faster for exact lookups.

Would you like an example on **how indexing improves query performance**? 🚀

---

### **What is a Database Function?**
A **database function** is a built-in function provided by a database management system (DBMS) to perform calculations, manipulate data, or process queries within a database.

---

### **Types of Database Functions**
#### **1. Aggregate Functions (Work on Multiple Rows)**
These functions perform operations on a group of values and return a single result.

| Function  | Description | Example |
|-----------|------------|---------|
| `SUM()`   | Adds up all values in a column | `SELECT SUM(price) FROM orders;` |
| `AVG()`   | Calculates the average of values | `SELECT AVG(salary) FROM employees;` |
| `COUNT()` | Counts the number of rows | `SELECT COUNT(*) FROM customers;` |
| `MAX()`   | Returns the highest value | `SELECT MAX(salary) FROM employees;` |
| `MIN()`   | Returns the lowest value | `SELECT MIN(price) FROM products;` |

---

#### **2. String Functions (Manipulate Text)**
These functions help in handling string operations.

| Function  | Description | Example |
|-----------|------------|---------|
| `UPPER()` | Converts text to uppercase | `SELECT UPPER(name) FROM users;` |
| `LOWER()` | Converts text to lowercase | `SELECT LOWER(email) FROM users;` |
| `CONCAT()` | Joins two strings | `SELECT CONCAT(first_name, ' ', last_name) FROM employees;` |
| `LENGTH()` | Returns the length of a string | `SELECT LENGTH(name) FROM customers;` |
| `SUBSTRING()` | Extracts part of a string | `SELECT SUBSTRING(name, 1, 3) FROM employees;` |

---

#### **3. Date & Time Functions**
These functions handle date and time manipulation.

| Function  | Description | Example |
|-----------|------------|---------|
| `NOW()`   | Returns the current date and time | `SELECT NOW();` |
| `CURDATE()` | Returns the current date | `SELECT CURDATE();` |
| `CURTIME()` | Returns the current time | `SELECT CURTIME();` |
| `DATE_FORMAT()` | Formats a date | `SELECT DATE_FORMAT(NOW(), '%Y-%m-%d');` |

---

#### **4. Mathematical Functions**
These functions perform mathematical calculations.

| Function  | Description | Example |
|-----------|------------|---------|
| `ROUND()` | Rounds a number to a specified decimal place | `SELECT ROUND(23.678, 2);` |
| `CEIL()`  | Rounds up to the nearest integer | `SELECT CEIL(4.2);` |
| `FLOOR()` | Rounds down to the nearest integer | `SELECT FLOOR(4.8);` |
| `MOD()`   | Returns the remainder of division | `SELECT MOD(10, 3);` |

---

### **Why Use Database Functions?**
✔ **Optimize Queries** – Perform calculations directly in SQL instead of application code.  
✔ **Improve Performance** – Reduce the need for fetching raw data and processing it in the application.  
✔ **Data Manipulation** – Easily modify text, dates, and numbers within queries.  

Would you like an example query using these functions? 🚀

Question #17:
What is the difference between primary key, unique key and foreign key

Question Level: Expect this question for beginner and intermediate level role.

Primary key, unique key and foreign key are constraints we can create on a table. 

When you make a column in the table as primary key then this column will always have unique or distinct values. Duplicate values and NULL value will not be allowed in a primary key column. A table can only have one primary key. Primary key can be created either on one single column or a group of columns.

When you make a column in the table as unique key then this column will always have unique or distinct values. Duplicate values will not be allowed. However, NULL values are allowed in a column which has unique key constraint. This is the major difference between primary and unique key. 

Foreign key is used to create a master child kind of relationship between two tables. When we make a column in a table as foreign key, this column will then have to be referenced from another column from some other table.

Imagine we have two tables A and B. Both have just 1 column let’s call it COLUMN_1. If we create foreign key in COLUMN_1 of table A which references the COLUMN_1 from table B then the only values COLUMN_1 in table A can have is the values which are already present in COLUMN_1 of table B. 

This means table B becomes the master table and table A is the child table. COLUMN_1 of Table A can only have values which are already present in COLUMN_1 of table B. 


