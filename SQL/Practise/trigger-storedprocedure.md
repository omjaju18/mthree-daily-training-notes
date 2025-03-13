# Triggers & Stored Procedures in SQL

## **1. Introduction**
SQL **Stored Procedures** and **Triggers** are powerful database features that help in automating tasks, ensuring data integrity, and optimizing performance. This document explains their concepts, benefits, and provides examples.

---

## **2. Stored Procedures**

### **What is a Stored Procedure?**
A **Stored Procedure** is a collection of SQL statements that are stored in the database and can be executed multiple times. It helps in reducing redundancy and improving performance.

### **Example: Simple Employee Insertion Procedure**
#### **Step 1: Create the Table**
```sql
CREATE TABLE employees (
    emp_id INT AUTO_INCREMENT PRIMARY KEY,
    emp_name VARCHAR(100),
    salary DECIMAL(10,2)
);
```

#### **Step 2: Create the Stored Procedure**
```sql
DELIMITER //

CREATE PROCEDURE AddEmployee(
    IN name VARCHAR(100), 
    IN salary DECIMAL(10,2)
)
BEGIN
    INSERT INTO employees (emp_name, salary) VALUES (name, salary);
END //

DELIMITER ;
```

#### **Step 3: Execute the Procedure**
```sql
CALL AddEmployee('John Doe', 50000);
```

### **✅ Benefits of Stored Procedures**
- **Performance Optimization:** Reduces execution time by precompiling queries.
- **Security:** Prevents SQL injection by restricting direct table access.
- **Reusability:** Can be called multiple times without rewriting queries.
- **Consistency:** Ensures business logic is enforced at the database level.

---

## **3. SQL Triggers**

### **What is a Trigger?**
A **Trigger** is an automated SQL procedure that runs before or after an event (`INSERT`, `UPDATE`, `DELETE`) on a table.

### **Example: Logging Withdrawals from a Bank Account**
#### **Step 1: Create Tables**
```sql
CREATE TABLE accounts (
    account_id INT PRIMARY KEY,
    balance DECIMAL(10,2)
);

CREATE TABLE transaction_logs (
    log_id INT AUTO_INCREMENT PRIMARY KEY,
    account_id INT,
    transaction_type VARCHAR(50),
    amount DECIMAL(10,2),
    transaction_time TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

#### **Step 2: Create the Trigger**
```sql
CREATE TRIGGER LogTransaction
AFTER UPDATE ON accounts
FOR EACH ROW
BEGIN
    INSERT INTO transaction_logs(account_id, transaction_type, amount, transaction_time)
    VALUES (OLD.account_id, 'Withdrawal', OLD.balance - NEW.balance, NOW());
END;
```

### **✅ Benefits of Triggers**
- **Automated Auditing:** Tracks all changes automatically.
- **Enforces Business Rules:** Prevents unauthorized modifications.
- **Maintains Data Integrity:** Ensures data consistency across tables.
- **Event-Driven Execution:** Executes specific tasks when needed.

---

## **4. Key Differences Between Procedures & Triggers**

| Feature         | Stored Procedure | Trigger |
|---------------|----------------|---------|
| **Execution** | Manually executed via `CALL` | Automatically executed on `INSERT/UPDATE/DELETE` |
| **Use Case** | Complex operations, business logic | Enforcing constraints, logging, automation |
| **Performance** | Faster execution, reduces network load | Adds overhead for frequent triggers |
| **Control** | Called as needed | Fires automatically |

---

## **5. Conclusion**
Both **Stored Procedures and Triggers** enhance database efficiency, security, and consistency. While **procedures** are useful for modular operations, **triggers** ensure automated enforcement of business rules.

### **🚀 Best Practices:**
- Use **procedures** for business logic to keep application code clean.
- Use **triggers** for automation but avoid excessive use to prevent performance issues.
- Ensure proper **error handling** in procedures and triggers.
