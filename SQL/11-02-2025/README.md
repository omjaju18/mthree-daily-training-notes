# **SQL Learning Documentation - 11-02-2025**  

This document provides an overview of key SQL concepts, including bitwise operations, joins, ranking functions, and analytical queries.

---

## 📌 1. Bitwise Operations  

### 🛠️ Table Creation  
```sql
CREATE TABLE permissions (
    user_id INT PRIMARY KEY,
    username VARCHAR(50),
    permission_flags INT  -- Stores permission bits
);
```
### 🔹 Insert Sample Data  
```sql
INSERT INTO permissions (user_id, username, permission_flags) VALUES
(1, 'admin', 7),     -- Binary: 111 (Read: 1, Write: 1, Execute: 1)
(2, 'developer', 6), -- Binary: 110 (Read: 1, Write: 1, Execute: 0)
(3, 'viewer', 4),    -- Binary: 100 (Read: 1, Write: 0, Execute: 0)
(4, 'guest', 1);     -- Binary: 001 (Read: 0, Write: 0, Execute: 1)
```

### 🔹 Queries  
- **Add Write Permission (010) where missing**  
```sql
UPDATE permissions 
SET permission_flags = permission_flags | 2 
WHERE (permission_flags & 2) = 0;
```
✅ *Uses bitwise OR (|) to add write permission (2) if not already set.*

- **Toggle Execute Permission (001)**  
```sql
UPDATE permissions 
SET permission_flags = permission_flags ^ 1;
```
✅ *Uses bitwise XOR (^) to flip execute permission (1).*

- **Check if users have Read Permission (100)**  
```sql
SELECT 
    user_id, 
    username,
    CASE 
        WHEN (permission_flags & 4) > 0 THEN 'Has Read Permission'
        ELSE 'No Read Permission'
    END AS ReadPermissionStatus
FROM permissions;
```
✅ *Uses bitwise AND (&) to check if Read (4) is set.*

---

## 📌 2. Bit Shifting Operations  

Bit shifting operations allow manipulation of integer values at the **binary level**. These operations include:

- **Left Shift (`<<`)**: Multiplies the value by `2` for each shift.
- **Right Shift (`>>`)**: Divides the value by `2` for each shift.

Bit shifting is commonly used for **efficient mathematical calculations, performance optimizations, and working with binary data**.

---

## 🛠️ **Table Creation & Sample Data**

```sql
CREATE TABLE bit_shift_demo (
    id INT PRIMARY KEY,
    value INT
);
```

```sql
INSERT INTO bit_shift_demo (id, value) VALUES
(1, 8),   -- Binary: 1000
(2, 12),  -- Binary: 1100
(3, 16);  -- Binary: 10000
```

### 📋 **Sample Table Data**

| id | value | Binary Representation |
|----|-------|-----------------------|
| 1  | 8     | `1000`                |
| 2  | 12    | `1100`                |
| 3  | 16    | `10000`               |

---

## 🔹 **Left Shift (`<<`) - Multiplication by 2**

```sql
SELECT id, value, 
       (value << 1) AS left_shift_1, 
       (value << 2) AS left_shift_2 
FROM bit_shift_demo;
```

### 🔹 **Output**

| id | value | Binary | `value << 1` (Shift 1) | Binary | `value << 2` (Shift 2) | Binary  |
|----|-------|--------|----------------|--------|----------------|---------|
| 1  | 8     | `1000`  | 16             | `10000` | 32             | `100000`  |
| 2  | 12    | `1100`  | 24             | `11000` | 48             | `110000`  |
| 3  | 16    | `10000` | 32             | `100000` | 64             | `1000000`  |

### 📌 **Explanation**
- **Left shift (`<<`) shifts bits to the left**, filling the empty rightmost positions with `0`.  
- Each shift **multiplies the value by 2**.

🔹 **Example Calculation:**
- `8 << 1` → `1000` → `10000` (Decimal **16**)
- `8 << 2` → `1000` → `100000` (Decimal **32**)
- `12 << 1` → `1100` → `11000` (Decimal **24**)

✅ **Key Point**:  
Each left shift `<< 1` **doubles** the number.

---

## 🔹 **Right Shift (`>>`) - Division by 2**

```sql
SELECT id, value, 
       (value >> 1) AS right_shift_1, 
       (value >> 2) AS right_shift_2 
FROM bit_shift_demo;
```

### 🔹 **Output**

| id | value | Binary | `value >> 1` (Shift 1) | Binary | `value >> 2` (Shift 2) | Binary  |
|----|-------|--------|----------------|--------|----------------|---------|
| 1  | 8     | `1000`  | 4              | `0100`  | 2              | `0010`   |
| 2  | 12    | `1100`  | 6              | `0110`  | 3              | `0011`   |
| 3  | 16    | `10000` | 8              | `01000` | 4              | `00100`  |

### 📌 **Explanation**
- **Right shift (`>>`) moves bits to the right**, discarding the rightmost bits.
- Each shift **divides the value by 2**.

🔹 **Example Calculation:**
- `8 >> 1` → `1000` → `0100` (Decimal **4**)
- `8 >> 2` → `1000` → `0010` (Decimal **2**)
- `12 >> 1` → `1100` → `0110` (Decimal **6**)

✅ **Key Point**:  
Each right shift `>> 1` **halves** the number.

---

## 🔹 **Key Takeaways**
### ✅ **Left Shift (`<<`)**
- Moves bits to the **left**.
- Fills empty rightmost positions with `0`.
- **Multiplies** the number by `2^n` (where `n` is the number of shifts).
- Example: `8 << 2` = `32` (Multiplied by `2^2` = `4`).

### ✅ **Right Shift (`>>`)**
- Moves bits to the **right**.
- Discards the rightmost bits.
- **Divides** the number by `2^n`.
- Example: `12 >> 1` = `6` (Divided by `2^1` = `2`).

---

## 📌 3. SQL Clauses (NOT, BETWEEN, EXISTS)  

### 🛠️ Table Creation  
```sql
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    Name VARCHAR(100),
    Country VARCHAR(50),
    IsActive BIT,
    CreditLimit DECIMAL(10,2)
);

CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    OrderDate DATE,
    TotalAmount DECIMAL(10,2),
    Status VARCHAR(20)
);
```

### 🔹 Queries  
- **Find products in stock (NOT)**  
```sql
SELECT * FROM Products WHERE InStock != 0;
```
✅ *Finds all products not out of stock.*

- **Find orders with amount between 1000-2000 (BETWEEN)**  
```sql
SELECT * FROM Orders WHERE TotalAmount BETWEEN 1000 AND 2000;
```
✅ *Filters values within a given range.*

- **Find customers with at least one order (EXISTS)**  
```sql
SELECT Name 
FROM Customers C
WHERE EXISTS (SELECT 1 FROM Orders O WHERE O.CustomerID = C.CustomerID);
```
✅ *Uses EXISTS to check if a customer has orders.*

---

## 📌 4. SQL Joins (Inner Join, Left Join, Right Join)

---

## 📌 Table Structure  

```sql
CREATE TABLE Employees (
    EmpID INT PRIMARY KEY, 
    Name VARCHAR(50), 
    DeptID INT
);

CREATE TABLE Departments (
    DeptID INT PRIMARY KEY, 
    DeptName VARCHAR(50)
);
```

Here, the `Employees` table has employee details, and the `Departments` table contains department information. The `DeptID` column acts as a foreign key linking employees to departments.

---

## 📌 4. SQL Joins

### 1️⃣ **INNER JOIN**  
✅ Retrieves only the records that have matching values in both tables.  

```sql
SELECT E.Name, D.DeptName 
FROM Employees E
INNER JOIN Departments D ON E.DeptID = D.DeptID;
```
🔹 **Example Output:**  
| Name  | DeptName  |
|--------|-----------|
| John   | IT        |
| Alice  | HR        |
| Bob    | Sales     |

📌 **Explanation:**  
- If an employee has a `DeptID` that exists in the `Departments` table, they will be included.  
- Employees without a valid `DeptID` are **excluded**.  

---

### 2️⃣ **LEFT JOIN** (or **LEFT OUTER JOIN**)  
✅ Retrieves **all records** from the left table (`Employees`) and the **matching** records from the right table (`Departments`). If no match is found, `NULL` is returned for the right table's columns.  

```sql
SELECT E.Name, D.DeptName 
FROM Employees E
LEFT JOIN Departments D ON E.DeptID = D.DeptID;
```
🔹 **Example Output:**  
| Name   | DeptName  |
|--------|-----------|
| John   | IT        |
| Alice  | HR        |
| Bob    | Sales     |
| Mark   | NULL      |

📌 **Explanation:**  
- All employees appear, even those without a department (e.g., "Mark" has `NULL` under `DeptName` because no department exists for their `DeptID`).  

---

### 3️⃣ **RIGHT JOIN** (or **RIGHT OUTER JOIN**)  
✅ Retrieves **all records** from the right table (`Departments`) and the **matching** records from the left table (`Employees`). If no match is found, `NULL` is returned for the left table's columns.  

```sql
SELECT E.Name, D.DeptName 
FROM Employees E
RIGHT JOIN Departments D ON E.DeptID = D.DeptID;
```
🔹 **Example Output:**  
| Name   | DeptName  |
|--------|-----------|
| John   | IT        |
| Alice  | HR        |
| Bob    | Sales     |
| NULL   | Finance   |

📌 **Explanation:**  
- All departments appear, even those without employees (e.g., "Finance" appears with `NULL` under `Name` because no employee is assigned to this department).  

---

## 🔹 Summary of Joins  

| Join Type    | Includes Non-Matching Records? | Which Table Shows All Records? |
|-------------|----------------------------|---------------------------|
| INNER JOIN  | ❌ No                         | Only matching records     |
| LEFT JOIN   | ✅ Yes (from left table)      | Left (Employees)          |
| RIGHT JOIN  | ✅ Yes (from right table)     | Right (Departments)       |

---

Here's a detailed explanation of **RANK()** and **DENSE_RANK()** with sample outputs.  

---

## 📌 5. SQL Ranking Functions  (RANK, DENSE_RANK)

SQL provides ranking functions like **RANK()** and **DENSE_RANK()** to assign ranks to rows based on a specified order. These functions are useful in scenarios like leaderboard rankings, salary comparisons, and performance evaluations.

---

## 🛠️ Table Structure & Sample Data  

```sql
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    Name VARCHAR(100),
    Department VARCHAR(50),
    Salary DECIMAL(10,2)
);
```

```sql
INSERT INTO Employees VALUES
(1, 'John Doe', 'HR', 5000),
(2, 'Jane Smith', 'IT', 7000),
(3, 'Alice Brown', 'IT', 7000),
(4, 'Bob Johnson', 'Finance', 6000),
(5, 'Charlie Wilson', 'Finance', 4000);
```

### 📋 Sample Table Data  

| EmployeeID | Name           | Department | Salary  |
|------------|---------------|------------|---------|
| 1          | John Doe       | HR         | 5000    |
| 2          | Jane Smith     | IT         | 7000    |
| 3          | Alice Brown    | IT         | 7000    |
| 4          | Bob Johnson    | Finance    | 6000    |
| 5          | Charlie Wilson | Finance    | 4000    |

---

## 🔹 RANK() vs. DENSE_RANK()  

```sql
SELECT 
    EmployeeID, 
    Name, 
    Salary, 
    RANK() OVER (ORDER BY Salary DESC) AS RankValue,
    DENSE_RANK() OVER (ORDER BY Salary DESC) AS DenseRankValue
FROM Employees;
```

### 🔹 Output  

| EmployeeID | Name           | Salary | RankValue | DenseRankValue |
|------------|---------------|--------|-----------|---------------|
| 2          | Jane Smith     | 7000   | 1         | 1             |
| 3          | Alice Brown    | 7000   | 1         | 1             |
| 4          | Bob Johnson    | 6000   | 3         | 2             |
| 1          | John Doe       | 5000   | 4         | 3             |
| 5          | Charlie Wilson | 4000   | 5         | 4             |

### 📌 Explanation  

- **RANK()**  
  - Assigns the same rank to duplicate values.  
  - **Skips ranks** after duplicates.  
  - Example: Both `Jane Smith` and `Alice Brown` have a salary of `7000` and get rank **1**, but the next employee (`Bob Johnson`) is ranked **3** (skipping 2).  

- **DENSE_RANK()**  
  - Also assigns the same rank to duplicates.  
  - **Does not skip ranks** after duplicates.  
  - Example: `Jane Smith` and `Alice Brown` are ranked **1**, but the next employee (`Bob Johnson`) is ranked **2** instead of **3**.  

---

## 🔹 Ranking Within Departments  

```sql
SELECT 
    EmployeeID, 
    Name, 
    Department, 
    Salary, 
    RANK() OVER (PARTITION BY Department ORDER BY Salary DESC) AS RankValue
FROM Employees;
```

### 🔹 Output  

| EmployeeID | Name           | Department | Salary | RankValue |
|------------|---------------|------------|--------|-----------|
| 1          | John Doe       | HR         | 5000   | 1         |
| 2          | Jane Smith     | IT         | 7000   | 1         |
| 3          | Alice Brown    | IT         | 7000   | 1         |
| 4          | Bob Johnson    | Finance    | 6000   | 1         |
| 5          | Charlie Wilson | Finance    | 4000   | 2         |

### 📌 Explanation  

- `PARTITION BY Department` ensures that ranking is **calculated separately** for each department.  
- `IT` has **two employees with salary 7000**, both getting **rank 1**.  
- `Finance` has **two different salaries (6000 and 4000)**, so employees get **rank 1 and 2** accordingly.  

---

## 🔹 Summary  

| Function      | Behavior |
|--------------|------------------------------------------------|
| **RANK()**   | Assigns the same rank to duplicates and **skips** numbers. |
| **DENSE_RANK()** | Assigns the same rank to duplicates but **does not skip** numbers. |
| **PARTITION BY** | Groups ranking separately within a category (e.g., department). |


---

## 📌 6. LAG() Function  

- **Get Previous Salary**  
```sql
SELECT 
    EmployeeID, 
    Name, 
    Salary, 
    LAG(Salary, 1, 0) OVER (ORDER BY Salary DESC) AS PreviousSalary
FROM Employees;
```
✅ *Retrieves the previous salary of each employee in descending order.*

- **Classify Employees Based on Salary (CASE Statement)**  
```sql
SELECT 
    Name, 
    Salary, 
    CASE 
        WHEN Salary > 6000 THEN 'High Salary'
        WHEN Salary BETWEEN 4000 AND 6000 THEN 'Medium Salary'
        ELSE 'Low Salary'
    END AS SalaryCategory
FROM Employees;
```
✅ *Classifies employees based on their salary range.*

---

## 📌 7. `UNION` and `UNION ALL` in SQL**  

In SQL, `UNION` and `UNION ALL` are used to **combine results from two or more SELECT queries** into a **single result set**. However, they have key differences.

---

## 🛠️ **Table Setup & Sample Data**  

Let's create two sample tables: **EmployeesIndia** and **EmployeesUSA**.

```sql
CREATE TABLE EmployeesIndia (
    EmpID INT PRIMARY KEY,
    Name VARCHAR(50),
    Department VARCHAR(50)
);

CREATE TABLE EmployeesUSA (
    EmpID INT PRIMARY KEY,
    Name VARCHAR(50),
    Department VARCHAR(50)
);
```

### 🔹 **Insert Sample Data**  

```sql
INSERT INTO EmployeesIndia VALUES 
(1, 'Amit', 'IT'),
(2, 'Neha', 'HR'),
(3, 'Raj', 'Finance');

INSERT INTO EmployeesUSA VALUES 
(2, 'John', 'HR'),
(3, 'Mike', 'Finance'),
(4, 'Emma', 'Marketing');
```

### 📋 **Data in Both Tables**  

**`EmployeesIndia` Table**  

| EmpID | Name  | Department |
|-------|-------|------------|
| 1     | Amit  | IT         |
| 2     | Neha  | HR         |
| 3     | Raj   | Finance    |

**`EmployeesUSA` Table**  

| EmpID | Name  | Department |
|-------|-------|------------|
| 2     | John  | HR         |
| 3     | Mike  | Finance    |
| 4     | Emma  | Marketing  |

---

## 🔹 **Using `UNION`** (Removes Duplicates)

```sql
SELECT * FROM EmployeesIndia  
UNION  
SELECT * FROM EmployeesUSA;
```

### ✅ **Output (Distinct Results)**  

| EmpID | Name  | Department |
|-------|-------|------------|
| 1     | Amit  | IT         |
| 2     | Neha  | HR         |
| 2     | John  | HR         |
| 3     | Raj   | Finance    |
| 3     | Mike  | Finance    |
| 4     | Emma  | Marketing  |

### 🔍 **Explanation**
- `UNION` **removes duplicate records** (based on all selected columns).
- Even though **EmpID 2 (HR)** and **EmpID 3 (Finance)** appear in both tables, they are treated as **distinct rows** because of different names (`Neha` vs. `John` and `Raj` vs. `Mike`).

---

## 🔹 **Using `UNION ALL`** (Keeps Duplicates)

```sql
SELECT * FROM EmployeesIndia  
UNION ALL  
SELECT * FROM EmployeesUSA;
```

### ✅ **Output (All Records Including Duplicates)**  

| EmpID | Name  | Department |
|-------|-------|------------|
| 1     | Amit  | IT         |
| 2     | Neha  | HR         |
| 3     | Raj   | Finance    |
| 2     | John  | HR         |
| 3     | Mike  | Finance    |
| 4     | Emma  | Marketing  |

### 🔍 **Explanation**
- `UNION ALL` **does not remove duplicates**.
- **All records from both tables are returned**, even if they are identical.

---

## 🔹 **Key Differences: `UNION` vs. `UNION ALL`**

| Feature           | `UNION`        | `UNION ALL`    |
|------------------|--------------|--------------|
| **Removes Duplicates?** | ✅ Yes | ❌ No |
| **Performance**  | ❌ Slower (because of duplicate removal) | ✅ Faster (direct merging) |
| **Use Case**  | When you need unique values | When duplicates are acceptable |

---

## 🔹 **When to Use `UNION` vs. `UNION ALL`**
- ✅ **Use `UNION`** when you need **distinct results** and don't want duplicates.  
- ✅ **Use `UNION ALL`** when you want **all records** (including duplicates) for analysis, logs, or debugging.
- 
---

## ** Solved SQL Problems**  
After completing the morning session, we practiced SQL problems based on the topics covered. Below is the **link** to the problems and **screenshots** of the solutions.  

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
