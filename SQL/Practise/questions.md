Here are **multiple solutions** to retrieve the **second highest salary** from the `EMPLOYEES` table:

---

### **1️⃣ Using `LIMIT` and `OFFSET` (Recommended)**
```sql
SELECT DISTINCT SALARY 
FROM EMPLOYEES 
ORDER BY SALARY DESC 
LIMIT 1 OFFSET 1;
```
✅ **Explanation:**  
- Sorts salaries in **descending order**.  
- Uses `OFFSET 1` to **skip** the highest salary.  
- `LIMIT 1` selects the **second highest salary**.

---

### **2️⃣ Using `MAX()` with a Subquery**
```sql
SELECT MAX(SALARY) 
FROM EMPLOYEES 
WHERE SALARY < (SELECT MAX(SALARY) FROM EMPLOYEES);
```
✅ **Explanation:**  
- **First subquery**: Finds the **highest salary**.  
- **Outer query**: Finds the **highest salary below the max**, i.e., **second highest salary**.

---

### **3️⃣ Using `DENSE_RANK()` (Handles Duplicates)**
```sql
SELECT SALARY 
FROM (SELECT SALARY, DENSE_RANK() OVER (ORDER BY SALARY DESC) AS rnk 
      FROM EMPLOYEES) ranked 
WHERE rnk = 2;
```
✅ **Explanation:**  
- `DENSE_RANK()` assigns **ranking** to each distinct salary.  
- Filters the row where `rnk = 2`, meaning **second highest salary**.  
- Works even if multiple employees have the **same salary**.

---

### **4️⃣ Using `ORDER BY` with `LIMIT` (Alternative)**
```sql
SELECT SALARY 
FROM EMPLOYEES 
ORDER BY SALARY DESC 
LIMIT 1,1;
```
✅ **Explanation:**  
- `LIMIT 1,1` → First number is **offset** (`1` = skip first salary), second number is **limit** (`1` = get one row).

---

### **5️⃣ Using `ROW_NUMBER()`**
```sql
SELECT SALARY 
FROM (SELECT SALARY, ROW_NUMBER() OVER (ORDER BY SALARY DESC) AS rnk 
      FROM EMPLOYEES) ranked 
WHERE rnk = 2;
```
✅ **Explanation:**  
- `ROW_NUMBER()` assigns a **unique rank** to each row.  
- Works **only if salaries are unique** (unlike `DENSE_RANK()`).

---

### 🚀 **Next Question:**  
Find all **departments** where the **average salary** is **greater than 50,000**.
