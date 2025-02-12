
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

## 📌 Summary
- A **foreign key** establishes a relationship between two tables.
- `ON DELETE` & `ON UPDATE` control behavior when referenced records change.
- **CASCADE** propagates changes (**deletion or update**).
- **SET NULL** ensures data remains but removes the reference.
- **RESTRICT/NO ACTION** prevent changes if dependencies exist.

🚀 **Foreign keys maintain consistency and integrity in relational databases!**

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

## 📌 Database Normalization Explained  
**Normalization** organizes data to reduce redundancy and improve integrity.

| **Normal Form** | **Key Rule** |
|---------------|------------|
| **1NF** | Atomic values (no multi-valued columns) |
| **2NF** | No partial dependency (non-key attributes depend on full primary key) |
| **3NF** | No transitive dependency (non-key attributes do not depend on another non-key attribute) |
| **BCNF** | Every determinant must be a candidate key |

---

## 📌 Stored Procedure in SQL: A Complete Guide  
A **stored procedure** is a precompiled set of SQL statements stored in a database.

### 🔹 Why Use Stored Procedures?
✔ **Reusability** → Write once, use multiple times.  
✔ **Performance Boost** → Reduces parsing and compilation overhead.  
✔ **Security** → Can restrict access and prevent SQL injection.  
✔ **Encapsulation** → Groups logic inside a single unit.  
✔ **Reduces Network Traffic** → One execution is faster than multiple queries.  

### 🔹 Example:
```sql
DELIMITER //

CREATE PROCEDURE GetAllEmployees()
BEGIN
    SELECT * FROM Employees;
END //

DELIMITER ;
```
✅ **Usage**: `CALL GetAllEmployees();`  
👉 Fetches all records from the `Employees` table.

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

## 📌 Conclusion
ACID properties ensure that **banking transactions are reliable**, preventing **data loss, inconsistency, and corruption**.

| Property  | Without ACID (Issues) | With ACID (Solution) |
|-----------|----------------------|----------------------|
| **Atomicity** | Money deducted but not credited. | Transaction fully succeeds or rolls back. |
| **Consistency** | System loses money. | Database remains valid before and after transactions. |
| **Isolation** | Transactions mix up, showing wrong balances. | Transactions do not interfere with each other. |
| **Durability** | Crashes erase transactions. | Committed changes are **permanently stored**. |

🚀 **ACID properties are the foundation of secure and reliable database management systems!**  

---


🔗 Problem 1 - https://leetcode.com/problems/replace-employee-id-with-the-unique-identifier/description/?envType=study-plan-v2&envId=top-sql-50

```sql
SELECT euni.unique_id, e.name 
FROM Employees  e
LEFT JOIN EmployeeUNI  euni
ON e.id = euni.id;
```

### **Screenshots of Solution**  
<img width="959" alt="image" src="https://github.com/user-attachments/assets/c7911ccd-6013-425f-b68b-4b259d382093" />




🔗 Problem 2 - https://leetcode.com/problems/product-sales-analysis-i/?envType=study-plan-v2&envId=top-sql-50

```sql
select p.product_name, s.year, s.price
from sales s
left join Product p
on s.product_id=p.product_id
```

### **Screenshots of Solution**  
<img width="952" alt="image" src="https://github.com/user-attachments/assets/0ef24fdc-196d-4334-aa36-4f07d5e603e9" />



🔗 Problem 3 - https://leetcode.com/problems/rising-temperature/description/?envType=study-plan-v2&envId=top-sql-50

```sql
SELECT w1.id
FROM Weather w1
JOIN Weather w2
ON DATEDIFF(w1.recordDate, w2.recordDate) = 1
WHERE w1.temperature > w2.temperature;
```

### **Screenshots of Solution**  
<img width="959" alt="image" src="https://github.com/user-attachments/assets/bea08393-2468-4a51-8975-0ff44a1aeed9" />



🔗 Problem 4 - https://leetcode.com/problems/customer-who-visited-but-did-not-make-any-transactions/?envType=study-plan-v2&envId=top-sql-50

```sql
SELECT V.customer_id , COUNT(*) AS count_no_trans
FROM VISITS V
LEFT JOIN Transactions T
ON V.visit_id = T.visit_id
WHERE T.amount is null
group by V.customer_id;
```

### **Screenshots of Solution**  
<img width="959" alt="image" src="https://github.com/user-attachments/assets/ad1f75a6-52e7-43a5-af4c-bdfa23e44181" />



🔗 Problem 5 - https://leetcode.com/problems/employee-bonus/description/?envType=study-plan-v2&envId=top-sql-50

```sql
SELECT e.name, b.bonus 
FROM Employee e
LEFT JOIN Bonus b ON e.empId = b.empId
WHERE b.bonus < 1000 OR b.bonus IS NULL;
```

### **Screenshots of Solution**  
<img width="953" alt="image" src="https://github.com/user-attachments/assets/0477096d-0aad-46fa-9487-00ad995ea739" />



🔗 Problem 6 - https://leetcode.com/problems/managers-with-at-least-5-direct-reports/description/?envType=study-plan-v2&envId=top-sql-50

```sql
SELECT m.name
FROM employee e
JOIN employee m ON e.managerId = m.id 
GROUP BY e.managerId
HAVING COUNT(*) >= 5;
```

### **Screenshots of Solution**  
<img width="959" alt="image" src="https://github.com/user-attachments/assets/d62f80ac-e688-460d-8133-bbe501a9440f" />



🔗 Problem 7 - https://leetcode.com/problems/not-boring-movies/description/?envType=study-plan-v2&envId=top-sql-50

```sql
select * from cinema 
where description != "boring" and id % 2 !=0
order by rating desc;
```

### **Screenshots of Solution**  
<img width="943" alt="image" src="https://github.com/user-attachments/assets/04fc2808-9535-4d11-9dec-c392b938ebeb" />


🔗 Problem 8 - https://leetcode.com/problems/number-of-unique-subjects-taught-by-each-teacher/description/?envType=study-plan-v2&envId=top-sql-50

```sql
select teacher_id, count(distinct subject_id) as cnt from Teacher group by teacher_id;
```

### Screenshots of Solution
<img width="959" alt="image" src="https://github.com/user-attachments/assets/a99fa1c3-125c-4aab-9444-51e7404bdf62" />


🔗 Problem 9 - https://leetcode.com/problems/biggest-single-number/description/?envType=study-plan-v2&envId=top-sql-50

```sql
SELECT MAX(num) AS num 
FROM (
    SELECT num 
    FROM MyNumbers
    GROUP BY num
    HAVING COUNT(num) = 1
) AS unique_numbers;
```

### **Screenshots of Solution**  
<img width="959" alt="image" src="https://github.com/user-attachments/assets/63379c8e-643b-4067-a259-d8cfa37f6d39" />



---
