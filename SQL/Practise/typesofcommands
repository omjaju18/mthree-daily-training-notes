# README: SQL Commands Overview

## Introduction
Structured Query Language (SQL) commands are categorized into different types based on their functionality. This document provides an overview of SQL commands with examples.

---

## 1️⃣ DDL (Data Definition Language) – "Structure Management"
DDL commands are used to define and modify the structure of database objects like tables and schemas.

### **Common DDL Commands:**
| Command | Description | Example |
|---------|------------|---------|
| **CREATE** | Creates a new table, database, or other database objects. | `CREATE TABLE students (id INT, name VARCHAR(50), age INT);` |
| **ALTER** | Modifies an existing table structure. | `ALTER TABLE students ADD email VARCHAR(100);` |
| **DROP** | Deletes a table or database permanently. | `DROP TABLE students;` |
| **TRUNCATE** | Removes all records but keeps the table structure. | `TRUNCATE TABLE students;` |

📌 **DDL commands are auto-committed and cannot be rolled back.**

---

## 2️⃣ DML (Data Manipulation Language) – "Data Handling"
DML commands are used to manipulate data stored in the database.

### **Common DML Commands:**
| Command | Description | Example |
|---------|------------|---------|
| **INSERT** | Adds new records to a table. | `INSERT INTO students (id, name, age) VALUES (1, 'Alice', 20);` |
| **UPDATE** | Modifies existing records. | `UPDATE students SET age = 21 WHERE id = 1;` |
| **DELETE** | Removes specific records. | `DELETE FROM students WHERE id = 1;` |

📌 **DML commands can be rolled back if not committed.**

---

## 3️⃣ DCL (Data Control Language) – "Permissions Control"
DCL commands manage user access and permissions.

### **Common DCL Commands:**
| Command | Description | Example |
|---------|------------|---------|
| **GRANT** | Assigns privileges to users. | `GRANT SELECT, INSERT ON students TO user1;` |
| **REVOKE** | Removes previously assigned privileges. | `REVOKE INSERT ON students FROM user1;` |

📌 **DCL commands require administrative privileges.**

---

## 4️⃣ TCL (Transaction Control Language) – "Transaction Handling"
TCL commands control transactions and ensure data consistency.

### **Common TCL Commands:**
| Command | Description | Example |
|---------|------------|---------|
| **COMMIT** | Saves all changes made by a transaction. | `COMMIT;` |
| **ROLLBACK** | Reverts changes to the last committed state. | `ROLLBACK;` |
| **SAVEPOINT** | Creates a rollback point within a transaction. | `SAVEPOINT SP1;` |

📌 **TCL commands are useful for handling errors and maintaining data integrity.**

---

## 5️⃣ DQL (Data Query Language) – "Fetching Data"
DQL is used to retrieve data from the database.

### **Common DQL Command:**
| Command | Description | Example |
|---------|------------|---------|
| **SELECT** | Retrieves data from one or more tables. | `SELECT * FROM students;` |

📌 **DQL mainly consists of the `SELECT` statement with filters like `WHERE`, `ORDER BY`, and `GROUP BY`.**

---

## 🔹 Summary (सारांश)
| **Command Type** | **Purpose** | **Examples** |
|---------------|------------|------------|
| **DDL** (Data Definition Language) | Defines the database structure | `CREATE`, `ALTER`, `DROP`, `TRUNCATE` |
| **DML** (Data Manipulation Language) | Manipulates data in tables | `INSERT`, `UPDATE`, `DELETE` |
| **DCL** (Data Control Language) | Manages user access | `GRANT`, `REVOKE` |
| **TCL** (Transaction Control Language) | Manages transactions | `COMMIT`, `ROLLBACK`, `SAVEPOINT` |
| **DQL** (Data Query Language) | Retrieves data | `SELECT` |

✅ **SQL commands help manage and manipulate databases efficiently!** 🚀

