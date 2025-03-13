## **🔹 ACID Properties in SQL – Detailed Explanation with Examples**  

### **What are ACID Properties?**  
ACID properties ensure **data reliability, consistency, and integrity** in databases, especially in transactions. ACID stands for:  

1. **Atomicity** – All or nothing  
2. **Consistency** – Valid state before and after the transaction  
3. **Isolation** – Transactions execute independently  
4. **Durability** – Changes persist permanently  

---

## **1️⃣ Atomicity (All or Nothing)**
**Definition:**  
- A transaction is **atomic**, meaning it is either **fully completed** or **fully rolled back** if an error occurs.  
- If any part of the transaction fails, **none** of the operations are executed.  

### **Example – Atomicity in Banking**  
Imagine transferring **₹5000 from Account A to Account B**:  

```sql
START TRANSACTION;

UPDATE accounts 
SET balance = balance - 5000 
WHERE account_id = 1;  -- Deduct ₹5000 from Account A

UPDATE accounts 
SET balance = balance + 5000 
WHERE account_id = 2;  -- Add ₹5000 to Account B

COMMIT;
```
**Scenario:**  
✔ **If both updates succeed**, the transaction is committed.  
❌ **If one update fails (e.g., due to insufficient balance in Account A),** the transaction is rolled back.  

```sql
ROLLBACK;
```
✅ **Ensures no partial transaction occurs.**  

---

## **2️⃣ Consistency (Data Validity Before & After Transaction)**
**Definition:**  
- A transaction must bring the database from **one valid state to another**.  
- No transaction should leave the database in an **invalid or corrupt state**.  

### **Example – Consistency in E-commerce Orders**  
A customer purchases an item from an online store. The **order is placed only if stock is available**:  

```sql
START TRANSACTION;

-- Check stock availability
SELECT stock FROM products WHERE product_id = 101;

-- Reduce stock count if available
UPDATE products 
SET stock = stock - 1 
WHERE product_id = 101;

-- Insert order details
INSERT INTO orders (order_id, product_id, customer_id) 
VALUES (5001, 101, 202);

COMMIT;
```
✔ If the stock is **sufficient**, the transaction completes.  
❌ If stock is **zero**, the transaction is rolled back, ensuring data remains **consistent**.  

✅ **Prevents incorrect data entry or inconsistent states.**  

---

## **3️⃣ Isolation (Transactions Should Not Interfere)**
**Definition:**  
- Transactions execute **independently** and **do not interfere** with each other.  
- Isolation **prevents race conditions** where two transactions **read or modify the same data simultaneously**.  

### **Example – Isolation in Concurrent Transactions**  
Imagine two users withdrawing **₹10,000 from the same bank account** at the same time.  

#### **Without Isolation (Dirty Read Issue)**
Transaction 1:  
```sql
START TRANSACTION;
SELECT balance FROM accounts WHERE account_id = 1;  -- Reads ₹50,000
```
Transaction 2 (Runs simultaneously):  
```sql
START TRANSACTION;
UPDATE accounts SET balance = balance - 10000 WHERE account_id = 1;  -- Deduct ₹10,000
COMMIT;
```
Transaction 1 continues:  
```sql
UPDATE accounts SET balance = balance - 10000 WHERE account_id = 1;  -- Deduct ₹10,000 again based on old balance
COMMIT;
```
🔴 **Issue:** The final balance becomes **₹30,000 instead of ₹40,000**, leading to a **race condition**.  

#### **With Isolation (Serializable Mode)**
```sql
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
```
✔ Ensures **transactions execute one after the other, not simultaneously.**  

✅ **Prevents incorrect data updates due to concurrent transactions.**  

---

## **4️⃣ Durability (Changes Are Permanent)**
**Definition:**  
- Once a transaction is committed, the changes are **permanent**, even if the system crashes.  
- Data remains **safe** after a successful transaction.  

### **Example – Durability in Flight Booking**  
A user books a flight ticket online:  

```sql
START TRANSACTION;

INSERT INTO bookings (user_id, flight_id, seat_number) 
VALUES (301, 'AI-202', '12A');

COMMIT;
```
**Scenario:**  
✔ If the system crashes **after COMMIT**, the booking is still saved when the database restarts.  
✔ Even if the power goes out, the **data remains intact**.  

✅ **Ensures that once a transaction is completed, it cannot be undone due to system failures.**  

---

## **🔹 Summary of ACID Properties**  

| **ACID Property** | **Definition** | **Ensures** |  
|------------------|---------------|-------------|  
| **Atomicity** | All or nothing | No partial transactions |  
| **Consistency** | Database remains valid | No invalid states |  
| **Isolation** | Transactions do not interfere | Prevents race conditions |  
| **Durability** | Data is saved permanently | Survives crashes |  
