# SQL Concepts and Queries  

## 📅 Date: 11-02-2025  

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

### 🛠️ Table Creation  
```sql
CREATE TABLE bit_shift_demo (
    id INT PRIMARY KEY,
    value INT
);
```
### 🔹 Insert Sample Data  
```sql
INSERT INTO bit_shift_demo (id, value) VALUES
(1, 8),   -- Binary: 1000
(2, 12),  -- Binary: 1100
(3, 16);  -- Binary: 10000
```

### 🔹 Queries  
- **Left Shift (Multiply by 2)**  
```sql
SELECT id, value, (value << 1) AS left_shift_1, (value << 2) AS left_shift_2 FROM bit_shift_demo;
```
✅ *Left shift (<<) doubles the value for each shift.*

- **Right Shift (Divide by 2)**  
```sql
SELECT id, value, (value >> 1) AS right_shift_1, (value >> 2) AS right_shift_2 FROM bit_shift_demo;
```
✅ *Right shift (>>) halves the value for each shift.*

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

## 📌 4. SQL Joins (INNER, LEFT, RIGHT)  

### 🛠️ Table Setup  
```sql
CREATE TABLE Employees (EmpID INT PRIMARY KEY, Name VARCHAR(50), DeptID INT);
CREATE TABLE Departments (DeptID INT PRIMARY KEY, DeptName VARCHAR(50));
```

### 🔹 Queries  
- **Inner Join (Common records only)**  
```sql
SELECT E.Name, D.DeptName 
FROM Employees E
INNER JOIN Departments D ON E.DeptID = D.DeptID;
```
✅ *Returns only matching records.*

- **Left Join (All Employees + Matching Departments)**  
```sql
SELECT E.Name, D.DeptName 
FROM Employees E
LEFT JOIN Departments D ON E.DeptID = D.DeptID;
```
✅ *All employees appear, even if they have no department.*

- **Right Join (All Departments + Matching Employees)**  
```sql
SELECT E.Name, D.DeptName 
FROM Employees E
RIGHT JOIN Departments D ON E.DeptID = D.DeptID;
```
✅ *All departments appear, even if no employees belong to them.*

---

## 📌 5. Ranking Functions (RANK(), DENSE_RANK())  

### 🛠️ Table Setup  
```sql
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    Name VARCHAR(100),
    Department VARCHAR(50),
    Salary DECIMAL(10,2)
);
```
### 🔹 Insert Sample Data  
```sql
INSERT INTO Employees VALUES
(1, 'John Doe', 'HR', 5000),
(2, 'Jane Smith', 'IT', 7000),
(3, 'Alice Brown', 'IT', 7000),
(4, 'Bob Johnson', 'Finance', 6000),
(5, 'Charlie Wilson', 'Finance', 4000);
```

### 🔹 Queries  
- **RANK() vs. DENSE_RANK()**  
```sql
SELECT 
    EmployeeID, 
    Name, 
    Salary, 
    RANK() OVER (ORDER BY Salary DESC) AS RankValue,
    DENSE_RANK() OVER (ORDER BY Salary DESC) AS DenseRankValue
FROM Employees;
```
✅ *RANK() skips ranks for duplicate salaries, while DENSE_RANK() assigns continuous ranks.*

- **Using PARTITION BY (Rank per department)**  
```sql
SELECT 
    EmployeeID, 
    Name, 
    Department, 
    Salary, 
    RANK() OVER (PARTITION BY Department ORDER BY Salary DESC) AS RankValue
FROM Employees;
```
✅ *Groups ranking separately per department.*

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
