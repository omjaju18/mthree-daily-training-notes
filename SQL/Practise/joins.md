# SQL Joins Explained with Examples

## Overview
SQL joins are used to retrieve data from multiple tables based on a common field. They help combine related data efficiently. This document provides a comprehensive explanation of different types of SQL joins along with examples.

## Table Structure
Assume we have two tables: `Employees` and `Departments`.

### **Employees Table**
| emp_id | emp_name | dept_id |
|--------|---------|---------|
| 1      | Alice   | 101     |
| 2      | Bob     | 102     |
| 3      | Charlie | 103     |
| 4      | David   | NULL    |
| 5      | Eva     | 101     |

### **Departments Table**
| dept_id | dept_name  |
|---------|-----------|
| 101     | HR        |
| 102     | IT        |
| 104     | Finance   |

---
## **Types of SQL Joins**

### **1. INNER JOIN**
Returns only the rows that have matching values in both tables.

#### **Query:**
```sql
SELECT Employees.emp_id, Employees.emp_name, Departments.dept_name
FROM Employees
INNER JOIN Departments ON Employees.dept_id = Departments.dept_id;
```

#### **Result:**
| emp_id | emp_name | dept_name |
|--------|---------|-----------|
| 1      | Alice   | HR        |
| 2      | Bob     | IT        |
| 5      | Eva     | HR        |

---

### **2. LEFT JOIN (LEFT OUTER JOIN)**
Returns all records from the left table (`Employees`) and the matched records from the right table (`Departments`). If no match is found, NULL is returned.

#### **Query:**
```sql
SELECT Employees.emp_id, Employees.emp_name, Departments.dept_name
FROM Employees
LEFT JOIN Departments ON Employees.dept_id = Departments.dept_id;
```

#### **Result:**
| emp_id | emp_name | dept_name |
|--------|---------|-----------|
| 1      | Alice   | HR        |
| 2      | Bob     | IT        |
| 3      | Charlie | NULL      |
| 4      | David   | NULL      |
| 5      | Eva     | HR        |

---

### **3. RIGHT JOIN (RIGHT OUTER JOIN)**
Returns all records from the right table (`Departments`) and the matched records from the left table (`Employees`). If no match is found, NULL is returned.

#### **Query:**
```sql
SELECT Employees.emp_id, Employees.emp_name, Departments.dept_name
FROM Employees
RIGHT JOIN Departments ON Employees.dept_id = Departments.dept_id;
```

#### **Result:**
| emp_id | emp_name | dept_name |
|--------|---------|-----------|
| 1      | Alice   | HR        |
| 2      | Bob     | IT        |
| 5      | Eva     | HR        |
| NULL   | NULL    | Finance   |

---

### **4. FULL JOIN (FULL OUTER JOIN)**
Returns all records from both tables. NULL values are included where no match is found.

#### **Query:**
```sql
SELECT Employees.emp_id, Employees.emp_name, Departments.dept_name
FROM Employees
FULL JOIN Departments ON Employees.dept_id = Departments.dept_id;
```

#### **Result:**
| emp_id | emp_name | dept_name |
|--------|---------|-----------|
| 1      | Alice   | HR        |
| 2      | Bob     | IT        |
| 3      | Charlie | NULL      |
| 4      | David   | NULL      |
| 5      | Eva     | HR        |
| NULL   | NULL    | Finance   |

---

### **5. CROSS JOIN**
Produces a Cartesian product, meaning every row from one table is combined with every row from the other table.

#### **Query:**
```sql
SELECT Employees.emp_name, Departments.dept_name
FROM Employees
CROSS JOIN Departments;
```

#### **Result (All Possible Combinations):**
| emp_name | dept_name |
|----------|-----------|
| Alice    | HR        |
| Alice    | IT        |
| Alice    | Finance   |
| Bob      | HR        |
| Bob      | IT        |
| Bob      | Finance   |
| Charlie  | HR        |
| Charlie  | IT        |
| Charlie  | Finance   |
| David    | HR        |
| David    | IT        |
| David    | Finance   |
| Eva      | HR        |
| Eva      | IT        |
| Eva      | Finance   |

---

### **6. SELF JOIN**
Joins a table with itself. Useful for hierarchical data like employees and managers.

#### **Example Table: Employees (with Manager IDs)**
| emp_id | emp_name | manager_id |
|--------|---------|------------|
| 1      | Alice   | 3          |
| 2      | Bob     | 3          |
| 3      | Charlie | NULL       |
| 4      | David   | 1          |
| 5      | Eva     | 1          |

#### **Query:**
```sql
SELECT E1.emp_name AS Employee, E2.emp_name AS Manager
FROM Employees E1
LEFT JOIN Employees E2 ON E1.manager_id = E2.emp_id;
```

#### **Result:**
| Employee | Manager  |
|----------|---------|
| Alice    | Charlie |
| Bob      | Charlie |
| Charlie  | NULL    |
| David    | Alice   |
| Eva      | Alice   |

---

## **Summary Table**
| Join Type       | Description |
|----------------|------------|
| **INNER JOIN** | Returns only matching rows from both tables. |
| **LEFT JOIN**  | Returns all rows from the left table and matching rows from the right. NULL if no match. |
| **RIGHT JOIN** | Returns all rows from the right table and matching rows from the left. NULL if no match. |
| **FULL JOIN**  | Returns all rows from both tables. NULL if no match. |
| **CROSS JOIN** | Returns a Cartesian product of both tables (every combination). |
| **SELF JOIN**  | Joins a table with itself, useful for hierarchical relationships. |

## **Conclusion**
SQL joins are essential for retrieving meaningful data from multiple tables. Understanding when and how to use each type of join will improve your ability to work with relational databases efficiently.

---

### **Happy Learning! 🚀**

