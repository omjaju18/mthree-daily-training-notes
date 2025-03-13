# SQL JOINS - Detailed Questions and Solutions

## Introduction
SQL JOINs are used to retrieve data from multiple tables based on a related column. This document contains **20 SQL JOIN questions** along with **solutions and explanations** to help you master different types of joins.

---

## 📌 Basic SQL JOINs

### 1️⃣ Retrieve all employees and their department names (Even if some employees don’t belong to a department)
```sql
SELECT E.EMP_NAME, D.DEPARTMENT_NAME
FROM EMPLOYEES E
LEFT JOIN DEPARTMENTS D
ON E.DEPARTMENT_ID = D.DEPARTMENT_ID;
```
📝 **Logic**: A `LEFT JOIN` ensures all employees are included, even if they don’t have a department.

### 2️⃣ List all employees and their salaries
```sql
SELECT E.EMP_NAME, S.SALARY
FROM EMPLOYEES E
INNER JOIN SALARIES S
ON E.EMP_ID = S.EMP_ID;
```
📝 **Logic**: An `INNER JOIN` ensures only employees with salary records are included.

### 3️⃣ Find all departments and the number of employees in each department, including departments with no employees.
```sql
SELECT D.DEPARTMENT_NAME, COUNT(E.EMP_ID) AS TOTAL_EMPLOYEES
FROM EMPLOYEES E
RIGHT JOIN DEPARTMENTS D
ON E.DEPARTMENT_ID = D.DEPARTMENT_ID
GROUP BY D.DEPARTMENT_NAME;
```
📝 **Logic**: A `RIGHT JOIN` ensures all departments are included, even those with zero employees.

### 4️⃣ Retrieve employees who don’t have a salary record
```sql
SELECT E.EMP_NAME
FROM EMPLOYEES E
LEFT JOIN SALARIES S
ON E.EMP_ID = S.EMP_ID
WHERE S.SALARY IS NULL;
```
📝 **Logic**: A `LEFT JOIN` with `WHERE S.SALARY IS NULL` finds employees missing salary records.

### 5️⃣ Retrieve employee names and their project names (Assuming there’s a PROJECTS table linked via EMP_ID)
```sql
SELECT E.EMP_NAME, P.PROJECT_NAME
FROM EMPLOYEES E
INNER JOIN PROJECTS P
ON E.EMP_ID = P.EMP_ID;
```
📝 **Logic**: `INNER JOIN` ensures only employees assigned to projects are listed.

---

## 📌 Intermediate SQL JOINs

### 6️⃣ Retrieve all employees, their department names, and salaries (Include those without department/salary)
```sql
SELECT E.EMP_NAME, D.DEPARTMENT_NAME, S.SALARY
FROM EMPLOYEES E
LEFT JOIN DEPARTMENTS D
ON E.DEPARTMENT_ID = D.DEPARTMENT_ID
LEFT JOIN SALARIES S
ON E.EMP_ID = S.EMP_ID;
```
📝 **Logic**: Multiple `LEFT JOIN`s ensure employees are included even if they lack a department or salary record.

### 7️⃣ Retrieve a list of employees who are not assigned to any department.
```sql
SELECT E.EMP_NAME
FROM EMPLOYEES E
LEFT JOIN DEPARTMENTS D
ON E.DEPARTMENT_ID = D.DEPARTMENT_ID
WHERE D.DEPARTMENT_NAME IS NULL;
```
📝 **Logic**: `LEFT JOIN` with `WHERE D.DEPARTMENT_NAME IS NULL` filters employees without a department.

### 8️⃣ Find departments that have no employees assigned.
```sql
SELECT D.DEPARTMENT_NAME
FROM DEPARTMENTS D
LEFT JOIN EMPLOYEES E
ON D.DEPARTMENT_ID = E.DEPARTMENT_ID
WHERE E.EMP_ID IS NULL;
```
📝 **Logic**: `LEFT JOIN` ensures departments with zero employees are included.

### 9️⃣ List the highest-paid employee in each department.
```sql
SELECT D.DEPARTMENT_NAME, MAX(S.SALARY) AS MAX_SALARY
FROM EMPLOYEES E
LEFT JOIN SALARIES S ON E.EMP_ID = S.EMP_ID
LEFT JOIN DEPARTMENTS D ON E.DEPARTMENT_ID = D.DEPARTMENT_ID
GROUP BY D.DEPARTMENT_NAME;
```
📝 **Logic**: `MAX(S.SALARY)` ensures the highest salary per department is retrieved.

### 🔟 Show employees who share the same salary as another employee.
```sql
SELECT E1.EMP_NAME AS EMPLOYEE_1, E2.EMP_NAME AS EMPLOYEE_2, E1.SALARY
FROM EMPLOYEES E1
INNER JOIN EMPLOYEES E2
ON E1.SALARY = E2.SALARY AND E1.EMP_ID <> E2.EMP_ID;
```
📝 **Logic**: A `SELF JOIN` is used to compare salaries among employees.

---

## 📌 Advanced SQL JOINs

### 1️⃣1️⃣ List all employees along with their manager’s name.
```sql
SELECT E.EMP_NAME AS EMPLOYEE, M.EMP_NAME AS MANAGER
FROM EMPLOYEES E
LEFT JOIN EMPLOYEES M
ON E.MANAGER_ID = M.EMP_ID;
```
📝 **Logic**: A `SELF JOIN` is used to link employees with their managers.

### 1️⃣2️⃣ Retrieve employees who have both a department and a project.
```sql
SELECT E.EMP_NAME, D.DEPARTMENT_NAME, P.PROJECT_NAME
FROM EMPLOYEES E
INNER JOIN DEPARTMENTS D ON E.DEPARTMENT_ID = D.DEPARTMENT_ID
INNER JOIN PROJECTS P ON E.EMP_ID = P.EMP_ID;
```
📝 **Logic**: Two `INNER JOIN`s ensure only employees assigned to both departments and projects are retrieved.

### 1️⃣3️⃣ Retrieve employees working on more than one project.
```sql
SELECT E.EMP_NAME, COUNT(P.PROJECT_ID) AS TOTAL_PROJECTS
FROM EMPLOYEES E
INNER JOIN PROJECTS P ON E.EMP_ID = P.EMP_ID
GROUP BY E.EMP_NAME
HAVING COUNT(P.PROJECT_ID) > 1;
```
📝 **Logic**: `HAVING COUNT(P.PROJECT_ID) > 1` filters employees with multiple projects.

### 1️⃣4️⃣ Show all employees with their departments, even if they don’t belong to any department.
```sql
SELECT E.EMP_NAME, COALESCE(D.DEPARTMENT_NAME, 'No Department') AS DEPARTMENT
FROM EMPLOYEES E
LEFT JOIN DEPARTMENTS D ON E.DEPARTMENT_ID = D.DEPARTMENT_ID;
```
📝 **Logic**: `COALESCE()` replaces `NULL` values with ‘No Department’.

### 1️⃣5️⃣ Show department names and the average salary in each department.
```sql
SELECT D.DEPARTMENT_NAME, AVG(S.SALARY) AS AVERAGE_SALARY
FROM EMPLOYEES E
LEFT JOIN SALARIES S ON E.EMP_ID = S.EMP_ID
LEFT JOIN DEPARTMENTS D ON E.DEPARTMENT_ID = D.DEPARTMENT_ID
GROUP BY D.DEPARTMENT_NAME;
```
📝 **Logic**: `AVG(S.SALARY)` calculates the department’s average salary.

---

## Conclusion
This README provides **20 different SQL JOIN questions** covering **basic, intermediate, and advanced** use cases. Practice these to strengthen your understanding of SQL JOINS and apply them confidently in real-world scenarios! 🚀

