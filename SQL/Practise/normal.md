## **Normalization in SQL (Up to 3NF) – Detailed Explanation with Examples**  

### **🔹 What is Normalization?**  
Normalization is the process of **organizing a database** to reduce **redundancy** and **eliminate anomalies** like **insertion, deletion, and update anomalies**. It involves **dividing large tables into smaller, related tables** while ensuring **data integrity**.  

---
## **🔹 Types of Normal Forms (NF)**
Normalization follows a step-by-step approach:  

1. **First Normal Form (1NF)**
2. **Second Normal Form (2NF)**
3. **Third Normal Form (3NF)**  

Let’s understand each with **examples**:

---

## **1️⃣ First Normal Form (1NF) – Eliminate Repeating Groups**  
**A table is in 1NF if:**
- It has a **primary key** (unique identifier for each row).
- All columns contain **atomic values** (indivisible values).
- Each column contains **values of a single type**.
- There are **no duplicate rows**.

### ❌ **Example – Before 1NF (Unnormalized Table)**  
| StudentID | StudentName | Courses          | PhoneNumbers    |  
|-----------|------------|------------------|----------------|  
| 101       | Alice      | Math, Science    | 9876543210, 8765432109 |  
| 102       | Bob        | History, English | 9123456789     |  

🔴 **Issues:**  
- **Multivalued attributes** (Courses and PhoneNumbers contain multiple values in a single column).  
- Hard to update individual course enrollments.  

### ✅ **After Applying 1NF (Atomic Values & Unique Rows)**  
| StudentID | StudentName | Course     | PhoneNumber  |  
|-----------|------------|------------|-------------|  
| 101       | Alice      | Math       | 9876543210  |  
| 101       | Alice      | Science    | 8765432109  |  
| 102       | Bob        | History    | 9123456789  |  
| 102       | Bob        | English    | 9123456789  |  

✅ Now, all columns contain **atomic values** (single, indivisible values), and each row is **unique**.  

---

## **2️⃣ Second Normal Form (2NF) – Remove Partial Dependencies**  
A table is in **2NF** if:  
- It is already in **1NF**.  
- **All non-key columns must depend on the entire primary key**, not just part of it.  

### ❌ **Example – Before 2NF (Partial Dependency Exists)**  
| StudentID | Course     | Instructor  | Department  |  
|-----------|------------|------------|-------------|  
| 101       | Math       | Dr. Smith  | Science     |  
| 101       | Science    | Dr. Adams  | Science     |  
| 102       | History    | Dr. Brown  | Humanities  |  
| 102       | English    | Dr. Taylor | Humanities  |  

🔴 **Issue:**  
- The **Instructor** and **Department** depend only on **Course**, not on **StudentID**.  
- If we delete all students taking "Math," we lose information about **Dr. Smith**.  

### ✅ **After Applying 2NF (Remove Partial Dependency)**  

**Student Table**  
| StudentID | StudentName |  
|-----------|------------|  
| 101       | Alice      |  
| 102       | Bob        |  

**Enrollment Table**  
| StudentID | Course |  
|-----------|--------|  
| 101       | Math   |  
| 101       | Science|  
| 102       | History|  
| 102       | English|  

**Course Table**  
| Course   | Instructor | Department  |  
|----------|------------|-------------|  
| Math     | Dr. Smith  | Science     |  
| Science  | Dr. Adams  | Science     |  
| History  | Dr. Brown  | Humanities  |  
| English  | Dr. Taylor | Humanities  |  

✅ Now, **Instructor and Department** are moved to the **Course Table** because they depend only on **Course**, not on **StudentID**.  

---

## **3️⃣ Third Normal Form (3NF) – Remove Transitive Dependencies**  
A table is in **3NF** if:  
- It is already in **2NF**.  
- **No non-key column depends on another non-key column** (no transitive dependencies).  

### ❌ **Example – Before 3NF (Transitive Dependency Exists)**  
| StudentID | StudentName | City      | ZipCode | State  |  
|-----------|------------|----------|--------|------|  
| 101       | Alice      | New York | 10001  | NY   |  
| 102       | Bob        | Los Angeles | 90001  | CA   |  

🔴 **Issue:**  
- **ZipCode → City, State** (ZipCode determines the city and state).  
- If a student moves to a different **city with the same ZipCode**, we must update multiple rows.  

### ✅ **After Applying 3NF (Remove Transitive Dependency)**  

**Student Table**  
| StudentID | StudentName | ZipCode |  
|-----------|------------|--------|  
| 101       | Alice      | 10001  |  
| 102       | Bob        | 90001  |  

**ZipCode Table**  
| ZipCode | City         | State  |  
|--------|-------------|------|  
| 10001  | New York    | NY   |  
| 90001  | Los Angeles | CA   |  

✅ Now, **ZipCode, City, and State** are stored separately, avoiding redundant data and **transitive dependency**.  

---

## **🔹 Summary of Normal Forms**  

| **Normal Form** | **Rule** | **Fixes** |  
|---------------|------------------------------|----------------------|  
| **1NF** | Remove **repeating groups** | Ensure atomic values |  
| **2NF** | Remove **partial dependencies** | Move dependent columns to a separate table |  
| **3NF** | Remove **transitive dependencies** | Ensure every non-key column depends only on the primary key |  

---

## **🔹 Why Normalize a Database?**  
✅ **Advantages:**  
✔ **Eliminates data redundancy**  
✔ **Reduces storage space**  
✔ **Prevents anomalies (Insert, Update, Delete anomalies)**  
✔ **Improves data consistency & integrity**  
✔ **Better query performance**  

---

You're on the right track! Let's break it down properly step by step:  

---

### **1st Normal Form (1NF) - Ensure Atomicity**  
Each column must contain atomic (indivisible) values. In the given table, the **DeliveryAddress** column is a composite value (street, city, etc.).  

So, we **split the address** into separate fields like **Street, City, and ZipCode** to make it atomic.  

**Updated Table (1NF)**  
| OrderID | CustomerName | PhoneNumber  | Product         | Quantity | Price  | Street         | City      | ZipCode  |
|---------|-------------|-------------|----------------|----------|--------|---------------|----------|--------|
| 1       | Alice       | 9876543210  | Laptop         | 1        | 60000  | Green Street  | Delhi    | 110001 |
| 1       | Alice       | 9876543210  | Mouse          | 1        | 1500   | Green Street  | Delhi    | 110001 |
| 2       | Bob         | 8765432109  | Keyboard       | 1        | 2000   | Blue Avenue   | Mumbai   | 400001 |
| 3       | Charlie     | 7654321098  | Monitor        | 2        | 15000  | Red Road      | Bangalore| 560001 |
| 3       | Charlie     | 7654321098  | Laptop Stand   | 1        | 2500   | Red Road      | Bangalore| 560001 |

---

### **2nd Normal Form (2NF) - Remove Partial Dependencies**  
**Issue:** In the current table, **CustomerName and PhoneNumber depend only on OrderID**, not on Product.  
👉 **Solution:** Separate customers and orders into different tables.  

#### **Customers Table (2NF)**
| CustomerID | CustomerName | PhoneNumber |
|------------|-------------|-------------|
| 1          | Alice       | 9876543210  |
| 2          | Bob         | 8765432109  |
| 3          | Charlie     | 7654321098  |

#### **Orders Table (2NF)**
| OrderID | CustomerID | Street        | City      | ZipCode  |
|---------|-----------|--------------|----------|--------|
| 1       | 1         | Green Street  | Delhi    | 110001 |
| 2       | 2         | Blue Avenue   | Mumbai   | 400001 |
| 3       | 3         | Red Road      | Bangalore| 560001 |

#### **OrderDetails Table (2NF)**
| OrderID | Product        | Quantity | Price  |
|---------|---------------|----------|--------|
| 1       | Laptop        | 1        | 60000  |
| 1       | Mouse         | 1        | 1500   |
| 2       | Keyboard      | 1        | 2000   |
| 3       | Monitor       | 2        | 15000  |
| 3       | Laptop Stand  | 1        | 2500   |

---

### **3rd Normal Form (3NF) - Remove Transitive Dependencies**  
Now, we check if **non-key columns depend on other non-key columns**.  
**Issue:** Product prices are dependent on ProductName, not OrderID.  
👉 **Solution:** Move product details to a **Products Table**.

#### **Products Table (3NF)**
| ProductID | ProductName    | Price  |
|-----------|--------------|--------|
| 1         | Laptop       | 60000  |
| 2         | Mouse        | 1500   |
| 3         | Keyboard     | 2000   |
| 4         | Monitor      | 15000  |
| 5         | Laptop Stand | 2500   |

#### **Final OrderDetails Table (3NF)**
| OrderID | ProductID | Quantity |
|---------|----------|----------|
| 1       | 1        | 1        |
| 1       | 2        | 1        |
| 2       | 3        | 1        |
| 3       | 4        | 2        |
| 3       | 5        | 1        |

---

### **Final Normalized Database Schema**
✅ **Customers (CustomerID, CustomerName, PhoneNumber)**  
✅ **Orders (OrderID, CustomerID, Street, City, ZipCode)**  
✅ **Products (ProductID, ProductName, Price)**  
✅ **OrderDetails (OrderID, ProductID, Quantity)**  

Now, your database follows **3rd Normal Form (3NF)**! 🚀 🎯
