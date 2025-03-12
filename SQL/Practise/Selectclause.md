Here’s a breakdown of when to use **WHERE**, **GROUP BY**, **ORDER BY**, **HAVING**, and **LIMIT**, with real-world examples:

---

### **1️⃣ WHERE Clause**  
- **Use Case:** Filters rows before any grouping or aggregation.  
- **Example:** Find employees in the "Finance" department who earn more than 80,000.

```sql
SELECT * FROM EMPLOYEES 
WHERE DEPARTMENT = 'Finance' 
AND SALARY > 80000;
```

---

### **2️⃣ GROUP BY Clause**  
- **Use Case:** Groups rows based on a specific column, often used with aggregate functions (`SUM`, `COUNT`, `AVG`, etc.).  
- **Example:** Count the number of employees in each department.

```sql
SELECT DEPARTMENT, COUNT(*) AS EMPLOYEE_COUNT
FROM EMPLOYEES
GROUP BY DEPARTMENT;
```

---

### **3️⃣ ORDER BY Clause**  
- **Use Case:** Sorts the result set based on one or more columns.  
- **Example:** Get employees sorted by their salary in descending order.

```sql
SELECT FIRST_NAME, SALARY 
FROM EMPLOYEES 
ORDER BY SALARY DESC;
```

---

### **4️⃣ HAVING Clause**  
- **Use Case:** Filters groups after aggregation. Similar to `WHERE`, but used with aggregate functions.  
- **Example:** Get departments where the total salary exceeds 150,000.

```sql
SELECT DEPARTMENT, SUM(SALARY) AS TOTAL_SALARY
FROM EMPLOYEES
GROUP BY DEPARTMENT
HAVING SUM(SALARY) > 150000;
```

---

### **5️⃣ LIMIT Clause**  
- **Use Case:** Limits the number of rows returned.  
- **Example:** Get the top 5 highest-paid employees.

```sql
SELECT FIRST_NAME, SALARY 
FROM EMPLOYEES 
ORDER BY SALARY DESC 
LIMIT 5;
```

---

### **Combined Example**  
Find the top 3 highest-paying departments where the total salary is more than 200,000.

```sql
SELECT DEPARTMENT, SUM(SALARY) AS TOTAL_SALARY
FROM EMPLOYEES
GROUP BY DEPARTMENT
HAVING SUM(SALARY) > 200000
ORDER BY TOTAL_SALARY DESC
LIMIT 3;
```

---

This should help clarify when to use each SQL clause. Let me know if you need more details! 🚀
