# SQL Queries with Explanations

## 1️⃣ Retrieve employees from the 'Finance' department who earn more than 80,000 and were hired before January 1, 2020.
### **Query:**
```sql
SELECT * FROM EMPLOYEES
WHERE DEPARTMENT = 'FINANCE'
AND SALARY > 80000
AND HIRE_DATE < '2020-01-01';
```
### **Explanation:**
- **WHERE DEPARTMENT = 'FINANCE'** filters only Finance department employees.
- **AND SALARY > 80000** ensures they earn more than 80,000.
- **AND HIRE_DATE < '2020-01-01'** checks employees hired before January 1, 2020.

---

## 2️⃣ Find employees whose first name starts with 'J' and whose last name contains exactly six letters.
### **Query:**
```sql
SELECT * FROM EMPLOYEES
WHERE FIRST_NAME LIKE 'J%'
AND LAST_NAME LIKE '______';
```
### **Explanation:**
- **LIKE 'J%'** selects names starting with 'J'.
- **LIKE '______'** ensures the last name has exactly 6 characters (each underscore represents one character).

---

## 3️⃣ Get a list of employees who do not belong to 'HR' or 'IT' but have a salary greater than 65,000.
### **Query:**
```sql
SELECT * FROM EMPLOYEES
WHERE DEPARTMENT NOT IN ('HR', 'IT')
AND SALARY > 65000;
```
### **Explanation:**
- **NOT IN ('HR', 'IT')** excludes employees from HR and IT.
- **AND SALARY > 65000** ensures they earn more than 65,000.

---

## 4️⃣ Find all employees who work in the same city as 'Alice Johnson'.
### **Query:**
```sql
SELECT * FROM EMPLOYEES
WHERE CITY = (SELECT CITY FROM EMPLOYEES WHERE FIRST_NAME = 'ALICE' AND LAST_NAME = 'JOHNSON');
```
### **Explanation:**
- Subquery fetches Alice Johnson's city.
- The outer query retrieves all employees in that city.

---

## 5️⃣ Retrieve the sum of all salaries grouped by department and only display those departments where the total salary exceeds 200,000.
### **Query:**
```sql
SELECT DEPARTMENT, SUM(SALARY) AS TOTAL_SALARY
FROM EMPLOYEES
GROUP BY DEPARTMENT
HAVING SUM(SALARY) > 200000;
```
### **Explanation:**
- **SUM(SALARY)** calculates total salary per department.
- **HAVING SUM(SALARY) > 200000** filters departments where total salary is above 200,000.

---

## 6️⃣ Count the number of employees in each department and sort by department name in descending order.
### **Query:**
```sql
SELECT DEPARTMENT, COUNT(*) AS EMP_COUNT
FROM EMPLOYEES
GROUP BY DEPARTMENT
ORDER BY DEPARTMENT DESC;
```
### **Explanation:**
- **COUNT(*)** counts employees per department.
- **ORDER BY DEPARTMENT DESC** sorts departments alphabetically in descending order.

---

## 7️⃣ Find the top 5 highest-paid employees who work in 'New York'.
### **Query:**
```sql
SELECT * FROM EMPLOYEES
WHERE CITY = 'NEW YORK'
ORDER BY SALARY DESC
LIMIT 5;
```
### **Explanation:**
- **WHERE CITY = 'NEW YORK'** filters employees in New York.
- **ORDER BY SALARY DESC** sorts salaries in descending order.
- **LIMIT 5** selects the top 5 highest-paid employees.

---

## 8️⃣ Get the average salary of employees who have been working for more than 4 years (hired before March 1, 2021).
### **Query:**
```sql
SELECT AVG(SALARY) AS AVERAGE_SALARY
FROM EMPLOYEES
WHERE HIRE_DATE < '2021-03-01';
```
### **Explanation:**
- **WHERE HIRE_DATE < '2021-03-01'** filters employees hired before March 1, 2021.
- **AVG(SALARY)** calculates the average salary.

---

## 9️⃣ Retrieve employees whose salary is greater than the average salary of all employees in the company.
### **Query:**
```sql
SELECT * FROM EMPLOYEES
WHERE SALARY > (SELECT AVG(SALARY) FROM EMPLOYEES);
```
### **Explanation:**
- **Subquery** calculates the average salary.
- **Outer query** retrieves employees earning more than the average.

---

## 🔟 Find employees who joined in the same year as 'Grace Lee'.
### **Query:**
```sql
SELECT * FROM EMPLOYEES
WHERE YEAR(HIRE_DATE) = (SELECT YEAR(HIRE_DATE) FROM EMPLOYEES WHERE FIRST_NAME = 'GRACE' AND LAST_NAME = 'LEE');
```
### **Explanation:**
- **Subquery** fetches the year Grace Lee was hired.
- **Outer query** retrieves employees hired in the same year.

---

## 1️⃣1️⃣ Get the department with the highest total salary and display the department name along with the total salary.
### **Query:**
```sql
SELECT DEPARTMENT, SUM(SALARY) AS TOTAL_SALARY
FROM EMPLOYEES
GROUP BY DEPARTMENT
ORDER BY TOTAL_SALARY DESC
LIMIT 1;
```
### **Explanation:**
- **SUM(SALARY)** calculates total salary per department.
- **ORDER BY TOTAL_SALARY DESC** sorts in descending order.
- **LIMIT 1** selects the highest-paid department.

---

## 1️⃣2️⃣ Find employees in 'Marketing' whose salary is higher than at least one employee in 'IT'.
### **Query:**
```sql
SELECT * FROM EMPLOYEES
WHERE DEPARTMENT = 'MARKETING'
AND SALARY > (SELECT MIN(SALARY) FROM EMPLOYEES WHERE DEPARTMENT = 'IT');
```
### **Explanation:**
- **Subquery** fetches the lowest salary in IT.
- **Outer query** selects Marketing employees earning more than that.

---

## 1️⃣3️⃣ Retrieve employees who have the same salary as 'Frank Wilson'.
### **Query:**
```sql
SELECT * FROM EMPLOYEES
WHERE SALARY = (SELECT SALARY FROM EMPLOYEES WHERE FIRST_NAME = 'FRANK' AND LAST_NAME = 'WILSON');
```
### **Explanation:**
- **Subquery** fetches Frank Wilson's salary.
- **Outer query** selects employees with the same salary.

---

## 1️⃣4️⃣ Find employees who are the oldest in their respective department.
### **Query:**
```sql
SELECT * FROM EMPLOYEES E1
WHERE AGE = (SELECT MAX(AGE) FROM EMPLOYEES E2 WHERE E1.DEPARTMENT = E2.DEPARTMENT);
```
### **Explanation:**
- **Subquery** finds the oldest employee in each department.
- **Outer query** selects employees matching that age.

---

## 1️⃣5️⃣ Get the total number of employees in each city and display only those cities with more than 3 employees.
### **Query:**
```sql
SELECT CITY, COUNT(*) AS EMP_COUNT
FROM EMPLOYEES
GROUP BY CITY
HAVING COUNT(*) > 3;
```
### **Explanation:**
- **COUNT(*)** counts employees per city.
- **HAVING COUNT(*) > 3** filters cities with more than 3 employees.

