
# **SQL Learning Documentation - 12-02-2025**  

THere’s a well-structured **README.md** file for your SQL Foreign Key guide:


# 📌 Foreign Key in SQL – A Complete Guide

A **Foreign Key** is a constraint in SQL that enforces **referential integrity** between two tables. It ensures that a value in the child table must exist in the parent table, preventing orphaned records and maintaining data consistency.

---

## 🔹 What is a Foreign Key?
A **Foreign Key (FK)** is a column or a combination of columns that establishes a link between two tables.

### ✅ Key Characteristics:
- A **foreign key** references a column (usually **PRIMARY KEY**) in another table.
- It ensures **referential integrity** (i.e., no orphaned records).
- The referenced column in the parent table must have **unique values** (i.e., it must be a PRIMARY KEY or UNIQUE).
- You can define actions like `CASCADE`, `SET NULL`, `RESTRICT`, and `NO ACTION` on **UPDATE** and **DELETE** events.

---

## 🔹 Creating Tables with Foreign Key
We create two tables:
1️⃣ **Departments** → **Parent Table** (Holds department details)  
2️⃣ **Employees** → **Child Table** (References `DeptID` from `Departments`)

```sql
CREATE TABLE Departments (
    DeptID INT PRIMARY KEY,
    DeptName VARCHAR(50)
);

CREATE TABLE Employees (
    EmpID INT PRIMARY KEY,
    Name VARCHAR(50),
    DeptID INT,
    FOREIGN KEY (DeptID) REFERENCES Departments(DeptID)
);
```

---

## 🔹 Inserting Data Correctly ✅
```sql
INSERT INTO Departments VALUES (1, 'IT'), (2, 'HR'), (3, 'Finance');
INSERT INTO Employees VALUES (101, 'Alice', 1), (102, 'Bob', 2), (103, 'Charlie', 3);
```
👉 Data is inserted successfully because `DeptID` values exist in `Departments`.

---

## 🔹 Violating Foreign Key Constraint ❌
```sql
INSERT INTO Employees VALUES (104, 'David', 5);
```
🔴 **Error**:  
```
ERROR: Cannot add or update a child row: a foreign key constraint fails.
```
🔍 **Why?**  
1. `DeptID = 5` does **not exist** in `Departments`.  
2. The **foreign key prevents invalid references**.

---

## 🛠️ Foreign Key with ON DELETE and ON UPDATE Actions
### Example:
```sql
CREATE TABLE Employees (
    EmpID INT PRIMARY KEY,
    Name VARCHAR(50),
    DeptID INT,
    FOREIGN KEY (DeptID) REFERENCES Departments(DeptID)
    ON DELETE CASCADE
    ON UPDATE CASCADE;
);
```

### ✅ How It Works:
- **`ON DELETE CASCADE`** → If a department is deleted, all employees in that department are **also deleted**.
- **`ON UPDATE CASCADE`** → If a department ID is updated, the update is **reflected** in `Employees`.

---

## 🔹 ON DELETE Actions
| Action | Effect |
|--------|--------|
| **CASCADE** | Deletes child records when the parent record is deleted. |
| **SET NULL** | Sets the foreign key column in the child table to `NULL`. |
| **RESTRICT** | Prevents deletion if references exist. |
| **NO ACTION** | Similar to `RESTRICT` but enforced at the end of a transaction. |

---

## 🔹 ON UPDATE Actions
| Action | Effect |
|--------|--------|
| **CASCADE** | Updates foreign key values in child table if parent key changes. |
| **SET NULL** | Sets foreign key in the child table to `NULL` when parent key updates. |
| **RESTRICT** | Prevents update if foreign key references exist. |
| **NO ACTION** | Similar to `RESTRICT` but enforced at the end of a transaction. |

---

## 🔹 Why Use Foreign Keys?
✔ **Data Integrity** → Prevents orphaned records.  
✔ **Cascading Actions** → Automates changes for consistency.  
✔ **Data Relationships** → Enforces logical links between tables.  
✔ **Prevents Inconsistent Updates** → Ensures that dependent data stays correct.  

---

## 📌 Entity-Relationship Diagram (ER Diagram)  
An **ER Diagram (ERD)** is a **visual representation** of a database structure, showing how different entities (**tables**) relate to each other.

### 🔹 Components of an ER Diagram:
- **Entities** → Represent objects in the database (e.g., Employees, Departments).
- **Attributes** → Properties of entities (e.g., Employee Name, Salary).
- **Primary Key (PK)** → Uniquely identifies an entity (e.g., `EmpID` in Employee).
- **Foreign Key (FK)** → Links two entities (e.g., `DeptID` in Employee referring to Department).
- **Relationships** → Connects entities (e.g., "Works In" relationship between Employee and Department).

### 🔹 Example ER Diagram:
```
+-------------+        +--------------+
|  Employee   |        |  Department  |
|-------------|        |--------------|
| EmpID (PK)  | -----> | DeptID (PK)  |
| Name        |        | DeptName      |
| Salary      |        +--------------+
| DeptID (FK) |
+-------------+
```
✔ `DeptID` in **Employee** is a **foreign key** referring to `DeptID` in **Department**.  
✔ **One Department** can have **many Employees** (**1:M relationship**).  

---
# 📌 Database Normalization Explained

**Normalization** is the process of **organizing data** in a database to **reduce redundancy** and **improve data integrity**. It involves breaking a large table into **smaller, related tables** and defining relationships between them.

---

## 🔹 Why Normalize a Database?
✅ **Reduces Data Redundancy** → Avoids storing the same data multiple times.  
✅ **Improves Data Integrity** → Ensures accuracy and consistency.  
✅ **Eliminates Anomalies** → Prevents insert, update, and delete issues.  
✅ **Enhances Query Performance** → Reduces unnecessary data storage.

---

## 📌 Types of Normal Forms (NF)
Normalization is done in stages, called **normal forms (NF)**. The most common forms are **1NF, 2NF, 3NF, and BCNF**.

| **Normal Form** | **Key Rule** |
|---------------|------------|
| **1NF** | Atomic values (**No multi-valued columns**) |
| **2NF** | No **partial dependency** (**Non-key attributes depend on the full primary key**) |
| **3NF** | No **transitive dependency** (**Non-key attributes do not depend on another non-key attribute**) |
| **BCNF** | Every determinant must be a **candidate key** |

---

## 🔹 1NF (First Normal Form) – Atomicity ✅
A table is in **1NF** if:
- **Each column contains atomic (indivisible) values**.
- **No repeating groups or arrays**.

### ❌ Example (Before 1NF):
| StudentID | Name  | Courses       |
|-----------|------|--------------|
| 101       | Alice | Math, Science |
| 102       | Bob   | English       |

🔴 **Problem**: The "Courses" column contains **multiple values** → **violates 1NF**.

### ✅ Solution (Convert to 1NF):
| StudentID | Name  | Course  |
|-----------|------|--------|
| 101       | Alice | Math   |
| 101       | Alice | Science |
| 102       | Bob   | English |

✔ **Each field has atomic values**.  
✔ **No multi-valued columns** → **Now in 1NF**.

---

## 🔹 2NF (Second Normal Form) – No Partial Dependency ✅
A table is in **2NF** if:
- **It is already in 1NF**.
- **All non-key attributes depend on the full primary key** (not just a part of it).

### ❌ Example (Before 2NF):
| StudentID | CourseID | StudentName | CourseName |
|-----------|---------|------------|------------|
| 101       | C1      | Alice      | Math       |
| 101       | C2      | Alice      | Science    |

🔴 **Problem**:  
- `StudentName` depends **only on StudentID** (not CourseID).  
- `CourseName` depends **only on CourseID** (not StudentID).  
- **Partial dependency exists** → **violates 2NF**.

### ✅ Solution (Convert to 2NF):
**Student Table**  
| StudentID | StudentName |
|-----------|------------|
| 101       | Alice      |

**Course Table**  
| CourseID | CourseName |
|---------|-----------|
| C1      | Math      |
| C2      | Science   |

**Enrollment Table** (Bridge Table)  
| StudentID | CourseID |
|-----------|---------|
| 101       | C1      |
| 101       | C2      |

✔ **Now, each column depends on the full primary key** → **Now in 2NF**.

---

## 🔹 3NF (Third Normal Form) – No Transitive Dependency ✅
A table is in **3NF** if:
- **It is already in 2NF**.
- **No transitive dependencies exist** (i.e., non-key attributes do not depend on another non-key attribute).

### ❌ Example (Before 3NF):
| StudentID | StudentName | CourseID | InstructorID | InstructorName |
|-----------|------------|---------|--------------|---------------|
| 101       | Alice      | C1      | I101        | Prof. John    |
| 102       | Bob        | C2      | I102        | Prof. Smith   |

🔴 **Problem**:  
- `InstructorName` depends on `InstructorID`, **not StudentID or CourseID**.  
- **Transitive dependency exists** → **violates 3NF**.

### ✅ Solution (Convert to 3NF):
**Student Table**  
| StudentID | StudentName |
|-----------|------------|
| 101       | Alice      |
| 102       | Bob        |

**Course Table**  
| CourseID | CourseName |
|---------|-----------|
| C1      | Math      |
| C2      | Science   |

**Instructor Table**  
| InstructorID | InstructorName |
|--------------|---------------|
| I101        | Prof. John     |
| I102        | Prof. Smith    |

**Enrollment Table** (Bridge Table)  
| StudentID | CourseID | InstructorID |
|-----------|---------|--------------|
| 101       | C1      | I101         |
| 102       | C2      | I102         |

✔ **Now, all attributes depend only on the primary key** → **Now in 3NF**.

---

## 📌 Summary: Normalization Steps
| **Normal Form** | **Key Rule** | **Fix** |
|---------------|------------|-------|
| **1NF** | No multi-valued columns | Create separate rows for each value |
| **2NF** | No partial dependency | Split tables based on full primary key |
| **3NF** | No transitive dependency | Remove attributes that depend on non-key attributes |

---

## 📌 Stored Procedure in SQL: A Complete Guide  

A **stored procedure** is a precompiled set of **SQL statements** stored in the database. It allows for reusability, better performance, and enhanced security by grouping multiple SQL operations into a single callable unit.

---

## 🔹 Why Use Stored Procedures?
| Feature           | Benefit                                              |
|------------------|------------------------------------------------------|
| ✅ **Reusability** | Write once, use multiple times.                     |
| ✅ **Performance Boost** | Reduces parsing and compilation overhead.       |
| ✅ **Security** | Can restrict access and prevent SQL injection.        |
| ✅ **Encapsulation** | Groups logic inside a single unit.                |
| ✅ **Reduced Network Traffic** | Running one procedure is faster than multiple queries. |

---

## 📌 Creating a Stored Procedure

### 🛠️ Example Table
```sql
CREATE TABLE Employees (
    EmpID INT PRIMARY KEY,
    Name VARCHAR(50),
    Salary DECIMAL(10,2),
    Department VARCHAR(50)
);
```

---

## 🔹 Basic Stored Procedure (No Parameters)
This procedure **fetches all records** from the `Employees` table.

```sql
DELIMITER //

CREATE PROCEDURE GetAllEmployees()
BEGIN
    SELECT * FROM Employees;
END //

DELIMITER ;
```
✅ **Usage:**  
```sql
CALL GetAllEmployees();
```

---

## 🔹 Stored Procedure with Parameters

### 1️⃣ **Input Parameter**
We can pass values as parameters.

```sql
DELIMITER //

CREATE PROCEDURE GetEmployeeByDept(IN dept_name VARCHAR(50))
BEGIN
    SELECT * FROM Employees WHERE Department = dept_name;
END //

DELIMITER ;
```
✅ **Usage:**  
```sql
CALL GetEmployeeByDept('IT');
```
✔ **Returns** → All employees from the given department.

---

### 2️⃣ **Output Parameter**
We can return a value using an `OUT` parameter.

```sql
DELIMITER //

CREATE PROCEDURE GetMaxSalary(OUT max_salary DECIMAL(10,2))
BEGIN
    SELECT MAX(Salary) INTO max_salary FROM Employees;
END //

DELIMITER ;
```
✅ **Usage:**  
```sql
CALL GetMaxSalary(@salary);
SELECT @salary;
```
✔ **Stores** the **maximum salary** in `@salary`.

---

### 3️⃣ **Input & Output Parameters Combined**
This procedure **calculates the total salary** of a department.

```sql
DELIMITER //

CREATE PROCEDURE GetTotalSalary(IN dept_name VARCHAR(50), OUT total_salary DECIMAL(10,2))
BEGIN
    SELECT SUM(Salary) INTO total_salary FROM Employees WHERE Department = dept_name;
END //

DELIMITER ;
```
✅ **Usage:**  
```sql
CALL GetTotalSalary('HR', @total);
SELECT @total;
```
✔ **Returns** → Total salary of the specified department.

---

## 📌 Stored Procedure with **IF-ELSE** Logic
This procedure **categorizes** an employee’s salary as **High** or **Low**.

```sql
DELIMITER //

CREATE PROCEDURE GetSalaryStatus(IN emp_id INT, OUT status VARCHAR(20))
BEGIN
    DECLARE emp_salary DECIMAL(10,2);
    
    SELECT Salary INTO emp_salary FROM Employees WHERE EmpID = emp_id;
    
    IF emp_salary >= 7000 THEN
        SET status = 'High Salary';
    ELSE
        SET status = 'Low Salary';
    END IF;
END //

DELIMITER ;
```
✅ **Usage:**  
```sql
CALL GetSalaryStatus(2, @status);
SELECT @status;
```
✔ **Returns** → `"High Salary"` or `"Low Salary"`.

---
---

## 📌 Dropping a Stored Procedure
If you want to delete a stored procedure:

```sql
DROP PROCEDURE IF EXISTS GetAllEmployees;
```
✅ **Effect:** → Deletes the `GetAllEmployees` procedure.

---

## 🔹 Advantages of Stored Procedures
| Feature        | Benefit                                          |
|---------------|--------------------------------------------------|
| 🚀 **Performance** | Precompiled and optimized execution.         |
| 🔒 **Security** | Prevents SQL injection and controls access.    |
| 🔄 **Reusability** | Reduces code duplication.                    |
| 🛠️ **Consistency** | Centralizes business logic.                 |

---

# 📌 ACID Properties in DBMS (with a Bank Example)

ACID stands for **Atomicity, Consistency, Isolation, and Durability**, ensuring reliable database transactions. Let's understand each property with a **bank transaction example**.

---

## 🔹 1. Atomicity (All or Nothing)
- Ensures that a transaction is **either fully completed or completely rolled back** if any part fails.
- **Example**: Suppose Alice transfers **₹5000** to Bob’s account.
  - ✅ **Step 1**: Deduct ₹5000 from Alice’s account.
  - ✅ **Step 2**: Add ₹5000 to Bob’s account.
  - ❌ If Step 2 fails (**e.g., database crash**), Step 1 must be **rolled back** to prevent money loss.
  - **Outcome**: Either both steps succeed, or **none happen**.

---

## 🔹 2. Consistency (Valid State Before & After Transaction)
- Ensures that the **database remains in a valid state** before and after a transaction.
- **Example**: The bank ensures that the **total money remains unchanged**.
  - **Before Transaction**:  
    - Alice: ₹10,000, Bob: ₹5,000 (**Total: ₹15,000**)
  - **After Transaction (Alice sends ₹5000 to Bob)**:  
    - Alice: ₹5,000, Bob: ₹10,000 (**Total: ₹15,000**) ✅
  - ❌ If a failure occurs, the database **must not enter an invalid state** (e.g., missing ₹5000).

---

## 🔹 3. Isolation (No Interference Between Transactions)
- Ensures that **multiple transactions do not interfere** with each other.
- **Example**:
  - Alice is **transferring ₹5000 to Bob**.
  - At the same time, **Bob is withdrawing ₹2000** from his account.
  - ❌ If transactions are not properly isolated, Bob’s balance might show **inconsistent values**.
  - ✅ **Solution**: Transactions should be executed **one after another** or managed using **locking mechanisms**.

---

## 🔹 4. Durability (Changes are Permanent)
- Ensures that **once a transaction is committed, it is permanently stored**, even if the system crashes.
- **Example**:
  - Alice transfers **₹5000 to Bob**.
  - The **transaction is successfully committed**.
  - ❌ Even if the **bank server crashes**, the transfer **must not be lost**.
  - ✅ **Solution**: The database writes the transaction to **non-volatile storage** (logs, backups).

---

# **Indexes in SQL: A Complete Guide**  

## 🔹 **What is an Index in SQL?**  
An **index** in SQL is a database object that improves the speed of data retrieval operations. It works like an index in a book, helping the database locate rows quickly without scanning the entire table.  

---

## 🔹 **Why Use Indexes?**  
✅ **Faster Queries** → Speeds up `SELECT` queries by reducing search time.  
✅ **Efficient Sorting** → Optimizes `ORDER BY` and `GROUP BY` operations.  
✅ **Quick Lookups** → Enhances `WHERE`, `JOIN`, and `LIKE` conditions.  
✅ **Improved Performance** → Reduces I/O operations and CPU usage.  
💡 **Note:** While indexes speed up **read** operations, they **slow down write** operations (`INSERT`, `UPDATE`, `DELETE`) due to index maintenance.  

---

## 📌 **Types of Indexes in SQL**  

| **Index Type**      | **Description**                                        |
|--------------------|------------------------------------------------|
| **Primary Index**   | Automatically created for the **primary key**. |
| **Unique Index**    | Ensures all values in a column are **unique**. |
| **Non-Unique Index**| Speeds up searches but **allows duplicates**. |
| **Composite Index** | Index on **multiple columns** for better performance. |
| **Clustered Index** | **Physically sorts** table rows. Only **one per table**. |
| **Non-Clustered Index** | **Logical ordering** without affecting physical data. Multiple per table. |

---

## 📌 **Creating Indexes in SQL**  

### 🔹 **1. Primary Index (Automatically Created)**  
A **primary index** is created automatically when defining a `PRIMARY KEY`.  

```sql
CREATE TABLE Employees (
    EmpID INT PRIMARY KEY,
    Name VARCHAR(50),
    Salary DECIMAL(10,2),
    Department VARCHAR(50)
);
```
✔ **Effect** → A **clustered index** is automatically created on `EmpID` since it’s the primary key.  

---

### 🔹 **2. Unique Index (Prevents Duplicates)**  
A **unique index** ensures that a column does **not** contain duplicate values.  

```sql
CREATE UNIQUE INDEX idx_unique_email ON Employees (Email);
```
✔ **Effect** → Prevents duplicate emails from being inserted.  

---

### 🔹 **3. Clustered Index (Sorts Data Physically)**  
A **clustered index** sorts and stores the data **physically** based on the column.  

```sql
CREATE CLUSTERED INDEX idx_salary ON Employees (Salary);
```
✔ **Effect** → The table will be **physically sorted** based on `Salary`.  
✔ **Only one clustered index** can exist per table.  

---

### 🔹 **4. Non-Clustered Index (Separate Structure)**  
A **non-clustered index** speeds up searches **without changing the physical order** of data.  

```sql
CREATE INDEX idx_name ON Employees (Name);
```
✔ **Effect** → Optimizes searches on `Name` **without affecting the table’s physical order**.  
✔ **Multiple non-clustered indexes** can exist per table.  

---

## 📌 **Dropping an Index**  
If an index is **no longer needed**, drop it to free up space.  

```sql
DROP INDEX idx_name ON Employees;
```
✔ **Effect** → Removes the `idx_name` index.  

---

## 📌 **When to Use Indexes?**  

### ✅ **Use indexes when:**  
✔ Columns are **frequently used** in `WHERE`, `ORDER BY`, or `JOIN` clauses.  
✔ Queries **return a small subset** of rows (not the entire table).  
✔ You need **fast searching** in large tables.  

### ❌ **Avoid indexes when:**  
✘ Tables are **small** (indexing adds unnecessary overhead).  
✘ Columns have **frequent updates** (index maintenance slows writes).  
✘ The column has **low uniqueness** (e.g., `Gender`, `Yes/No` values).  

---
