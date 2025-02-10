# **SQL Learning Documentation - 10-02-2025**  

## **What is SQL?**  
Imagine a **wardrobe** where you store different types of clothes. SQL works similarly for databases—it helps you **store, organize, and find** information.  

Your wardrobe has **sections (tables)** like:  
- Shirts  
- Jeans  
- Jackets  

Each section has **racks (columns)** for organizing by:  
- Color (Red, Blue, Pink, Black)  
- Size (Small, Medium, Large)  
- Type (Casual, Formal)  

If you need to find **all pink shirts**, instead of searching manually, you can just ask:  
📢 *"Show me all shirts where the color is pink!"*  

SQL does the same with data—helping you **store, manage, and retrieve** information efficiently.  

### **Understanding Rows in SQL**
In this analogy, a **row** represents a specific item of clothing in a section (table).  

#### **Example: Shirts Table (SQL Table)**  
| ID | Color | Size  | Type   |  
|----|------|------|--------|  
| 1  | Red  | Small  | Casual  |  
| 2  | Blue  | Medium | Formal  |  
| 3  | Pink  | Large  | Casual  |  

Each **row** in the table represents **one shirt** with its properties (**color, size, and type**).

---

### **SQL Query Example**  
To find all **Pink shirts**, you’d use:  
```sql
SELECT * FROM Shirts WHERE Color = 'Pink';
```
👉 This retrieves the **row(s)** where the color is **Pink**!  

---

## **1. What is a Database?**  
A **database** is a structured collection of data that can be easily accessed, managed, and updated. It helps in storing large amounts of information efficiently.  

---

## **2. What is DBMS?**  
A **Database Management System (DBMS)** is software that helps users interact with databases. It allows data storage, retrieval, and management.  

---

## **3. Types of DBMS**  
- **Relational DBMS (RDBMS)** – Uses tables (e.g., MySQL, PostgreSQL).  
- **NoSQL DBMS** – Stores data in key-value pairs, documents, or graphs (e.g., MongoDB). 
---

## **4. SQL Example (Finding Pink Shirts in 400 Shirts)**  
If you have a **table named `supboard`** with different shirt types, you can find all pink shirts using SQL:  

```sql
SELECT * FROM supboard WHERE color = 'pink';
```

This selects all rows where the `color` column is `'pink'`.  

---

## **5. Table Structure Example (Creating a Supboard Table)**  
We can create a table with different types of shirts, jeans, and compartments as racks.  

```sql
CREATE TABLE supboard (
    id INT PRIMARY KEY,
    type VARCHAR(50),
    color VARCHAR(20),
    rack_number INT
);
```

Each **row** represents a clothing item, and **columns** store attributes like type, color, and rack number.  

---

## **6. Steps to Download MySQL Workbench**  
To install **MySQL Workbench**:  
1. Visit the **MySQL official website**.  
2. Download and install **MySQL Workbench**.  
3. Connect to the database and start running SQL queries.

Refer the Link for more details - https://www.geeksforgeeks.org/how-to-install-sql-workbench-for-mysql-on-windows/

---

## **7. DDL (Data Definition Language) Commands**  
These commands **modify database structure**.  

- **Create Table**  
  ```sql
  CREATE TABLE employees (id INT, name VARCHAR(50), salary INT);
  ```
- **Alter Table (Add Column)**  
  ```sql
  ALTER TABLE employees ADD COLUMN department VARCHAR(50);
  ```
- **Drop Table**  
  ```sql
  DROP TABLE employees;
  ```

---

## **8. DML (Data Manipulation Language) Commands**  
These **modify data inside tables**.  

- **Insert Values**  
  ```sql
  INSERT INTO employees (id, name, salary) VALUES (1, 'John', 50000);
  ```
- **Update Data**  
  ```sql
  UPDATE employees SET salary = 55000 WHERE id = 1;
  ```
- **Delete Data**  
  ```sql
  DELETE FROM employees WHERE id = 1;
  ```

---

## **9. Difference Between TRUNCATE and DELETE**  
- **DELETE** removes specific rows but allows rollback (undo).  
- **TRUNCATE** removes all rows permanently and is faster.  

---

## **10. Cloning a Table (Deep Copy vs. Shallow Copy)**  

### **Deep Copy**  
- Copies **both** the table structure and the data.  
- Any changes in the new table **do not** affect the original table.  
- Example:  
  ```sql
  CREATE TABLE new_table AS SELECT * FROM old_table;
  ```

### **Shallow Copy**  
- Copies **only** the table structure, but **not the data**.  
- If any changes are made in the **original table**, they **also reflect** in the new table because they share the same reference.  
- Example:  
  ```sql
  CREATE TABLE new_table LIKE old_table;
  ```

🔹 **Think of it like copying a notebook:**  
- **Deep Copy** → Makes a **duplicate** with all the notes inside. Any changes in the original notebook **will not** affect the copy.  
- **Shallow Copy** → Just copies the **empty pages (structure)** without any notes (data). If you make changes in the original notebook, they **also appear** in the copied notebook.  


---

## **11. DESC Command (Describe Table)**  
This command shows the **table structure**:  

```sql
DESC employees;
```

---

## **12. Temporary Tables**  
Temporary tables store data for a **session** and disappear after use:  

```sql
CREATE TEMPORARY TABLE temp_table AS SELECT * FROM employees;
```

---

## **13. Views (Short Explanation)**  
A **view** is a virtual table based on a query:  

```sql
CREATE VIEW high_salary AS 
SELECT * FROM employees WHERE salary > 60000;
```

---

## **14. Difference Between CHAR and VARCHAR**  

| Feature       | CHAR                         | VARCHAR                     |
|--------------|------------------------------|------------------------------|
| **Storage**  | Fixed-length storage         | Variable-length storage      |
| **Speed**    | Faster for fixed-size data   | Slower as it requires extra processing |
| **Padding**  | Adds spaces to match length  | Does not add extra spaces   |
| **Usage**    | Best for data of fixed size (e.g., **PIN codes, Country Codes**) | Best for variable-length data (e.g., **Names, Addresses**) |

#### **Example:**  
- **CHAR(10)** → Always stores **exactly** 10 characters (even if the input is smaller).  
- **VARCHAR(10)** → Stores **only** the actual characters entered (saves space).  

---

## **15. SQL Query Clauses**  

- **ORDER BY** – Sorts data in ascending (`ASC`) or descending (`DESC`) order.  
  ```sql
  SELECT * FROM employees ORDER BY salary DESC;
  ```
- **HAVING** – Filters grouped results.  
  ```sql
  SELECT department, COUNT(*) 
  FROM employees 
  GROUP BY department 
  HAVING COUNT(*) > 5;
  ```
- **WHERE** – Filters rows before grouping.  
  ```sql
  SELECT * FROM employees WHERE salary > 50000;
  ```
- **LIMIT** – Restricts the number of results.  
  ```sql
  SELECT * FROM employees LIMIT 5;
  ```
- **Finding Unique Values**  
  ```sql
  SELECT DISTINCT department FROM employees;
  ```

---

## **16. Solved SQL Problems**  
After completing the morning session, we practiced SQL problems based on the topics covered. Below is the **link** to the problems and **screenshots** of the solutions.  

🔗 Problem 1 - https://leetcode.com/problems/recyclable-and-low-fat-products/description/?envType=study-plan-v2&envId=top-sql-50

### **Screenshots of Solution**  
<img width="959" alt="image" src="https://github.com/user-attachments/assets/126aa4fc-48cf-4982-acb2-7906f4175db1" />


🔗 Problem 2 - https://leetcode.com/problems/find-customer-referee/description/?envType=study-plan-v2&envId=top-sql-50

### **Screenshots of Solution**  
<img width="959" alt="image" src="https://github.com/user-attachments/assets/9a91f297-cf57-4ca8-b7ba-66c133ace4b1" />



🔗 Problem 3 - https://leetcode.com/problems/big-countries/description/?envType=study-plan-v2&envId=top-sql-50

### **Screenshots of Solution**  
<img width="958" alt="image" src="https://github.com/user-attachments/assets/9720f12f-2e51-4264-b144-72c3f65772e3" />



🔗 Problem 4 - https://leetcode.com/problems/article-views-i/description/?envType=study-plan-v2&envId=top-sql-50

### **Screenshots of Solution**  
<img width="959" alt="image" src="https://github.com/user-attachments/assets/8cae51a5-7828-4ec8-a06b-e97de1edd118" />



🔗 Problem 5 - https://leetcode.com/problems/invalid-tweets/description/?envType=study-plan-v2&envId=top-sql-50

### **Screenshots of Solution**  
<img width="956" alt="image" src="https://github.com/user-attachments/assets/6bc56d27-4063-4d3e-b3b5-1a2477ad76ee" />



🔗 Problem 6 - https://leetcode.com/problems/not-boring-movies/description/?envType=study-plan-v2&envId=top-sql-50

### **Screenshots of Solution**  
<img width="956" alt="image" src="https://github.com/user-attachments/assets/a3e2c2ac-1050-4197-9bde-1249101e1049" />

---


## 17. **Additional Practice – SQL Joins**
We also solved a few queries related to JOINs, which were not taught in the session. Hence, we are not adding them to this document.

---

## 18. **My Experience from the Session**

Overall, the session was really good and had a great speed. I was able to understand all the topics since I already knew SQL and had practiced a lot.

I also learned a few new concepts like:

Cloning a table (Shallow Copy vs. Deep Copy)
Creating a temporary table
The most important takeaway was explaining SQL to a non-tech person with no prior knowledge.

🔹 Thank you for the informative session! Looking forward to Day 2! 🚀

