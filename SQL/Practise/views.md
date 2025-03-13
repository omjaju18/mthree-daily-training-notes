# **Views in SQL - Complete Guide**

## **1️⃣ What is a View in SQL?**
A **view** in SQL is a **virtual table** based on the result of a SELECT query. It does not store data itself but fetches data dynamically from the base table.

### **Key Features of Views:**
- Acts as a **virtual table**
- Stores only the **query definition**, not actual data
- Can be used for **security, simplification, and abstraction**
- Helps **restrict access** to specific columns or rows
- Always fetches the **latest data** from the base table

---

## **2️⃣ Creating a View**
### **Syntax:**
```sql
CREATE VIEW view_name AS
SELECT column1, column2 FROM table_name
WHERE condition;
```

### **Example:**
```sql
CREATE VIEW IT_Employees AS
SELECT EmployeeID, Name, Salary
FROM Employees
WHERE Department = 'IT';
```
This view will display only employees from the IT department.

---

## **3️⃣ Why Use Views? (Use Cases)**
| Use Case            | Benefit |
|---------------------|---------|
| **Security**        | Restrict access to sensitive columns |
| **Simplification**  | Make complex queries easier to manage |
| **Data Abstraction** | Hide unnecessary details from users |
| **Consistency**     | Provide a consistent view of data |
| **Logical Data Independence** | Changes in base tables don’t require changes in dependent queries |

---

## **4️⃣ Types of Views in SQL**
### **1. Regular Views**
- Fetches real-time data from the table
- Does NOT store data physically
- **Auto-updates** when the base table changes

### **2. Read-Only Views**
- Prevents `INSERT`, `UPDATE`, and `DELETE`
- Created using `WITH CHECK OPTION`

**Example:**
```sql
CREATE VIEW ReadOnly_Employees AS
SELECT EmployeeID, Name FROM Employees
WITH CHECK OPTION;
```

### **3. Materialized Views**
- **Stores data physically** (unlike regular views)
- Improves performance by precomputing results
- **Requires manual refresh**

**Example:**
```sql
CREATE MATERIALIZED VIEW EmployeeSummary AS
SELECT Department, COUNT(*) AS EmployeeCount, AVG(Salary) AS AvgSalary
FROM Employees
GROUP BY Department;
```
To refresh the materialized view manually:
```sql
REFRESH MATERIALIZED VIEW EmployeeSummary;
```

---

## **5️⃣ Does a View Automatically Update When the Table Data Changes?**
| View Type           | Auto Update? |
|---------------------|-------------|
| **Regular View**    | ✅ Yes |
| **Materialized View** | ❌ No (needs manual refresh) |

---

## **6️⃣ Deleting Data in Views – Effect on Base Table**
| Action | Regular View | Read-Only View | Materialized View |
|--------|-------------|---------------|------------------|
| **Delete from View** | ✅ Deletes in base table | ❌ Not allowed | ❌ Only deletes in the materialized view |
| **Delete from Base Table** | ✅ Reflects in view | ✅ Reflects in view | ❌ No change until refreshed |

**Example:**
Deleting from a regular view:
```sql
DELETE FROM IT_Employees WHERE EmployeeID = 105;
```
🚀 **This will delete from `Employees` too!**

---

## **8️⃣ Making a View Read-Only (Preventing Deletes and Updates)**
Use `WITH CHECK OPTION` to prevent unauthorized updates:
```sql
CREATE VIEW SecureView AS
SELECT EmployeeID, Name FROM Employees
WITH CHECK OPTION;
```
Now, **INSERT/UPDATE/DELETE will fail** for this view!

---

## **9️⃣ Advantages and Disadvantages of Views**
### ✅ **Advantages:**
- Improves **security** by restricting access
- Simplifies **complex queries**
- Ensures **data consistency**
- Provides **logical abstraction**

### ❌ **Disadvantages:**
- Cannot always be updated (depends on complexity)
- Performance overhead for complex views
- Materialized views require manual refreshing

---

## **🔟 Conclusion**
- **Regular Views** auto-update but do not store data.
- **Materialized Views** improve performance but need manual refresh.
- **Read-Only Views** restrict modifications.
- **Deleting from a view deletes from the base table (except materialized views).**
- **Use `WITH CHECK OPTION` to make a view read-only.**

### **Would you like to see how to automate materialized view refresh using a scheduler? 🚀**

