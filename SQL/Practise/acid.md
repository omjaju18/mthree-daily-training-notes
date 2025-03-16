# ACID Properties Explained with Alice & Bob's Bank Transactions

ACID properties ensure reliable and secure transactions in databases. ACID stands for:

1. **Atomicity** – All or nothing
2. **Consistency** – Valid state before and after the transaction
3. **Isolation** – Transactions execute independently
4. **Durability** – Changes persist permanently

## 1. Atomicity – "All or Nothing"
**Example:**
- Alice wants to transfer ₹5000 to Bob.
- The transaction involves two operations:
  1. Deduct ₹5000 from Alice’s account.
  2. Add ₹5000 to Bob’s account.

**Issue Without Atomicity:**
- If the system crashes after deducting money from Alice but before adding it to Bob’s account, Bob never receives the amount, causing inconsistency.

**How Atomicity Solves It:**
- If **both operations succeed**, the transaction is **committed**.
- If **either operation fails**, the transaction is **rolled back**, restoring Alice’s balance to ₹10,000.

✅ **Ensures Alice’s money doesn’t disappear.**

---

## 2. Consistency – "Valid State Before & After Transaction"
**Example:**
- The bank follows a rule: **Total money in the system must remain the same**.
- Initially:
  - Alice has ₹10,000.
  - Bob has ₹5,000.
  - **Total = ₹15,000.**
- After Alice transfers ₹5000, balances should be:
  - Alice: ₹5000
  - Bob: ₹10,000
  - **Total = ₹15,000 (unchanged).**

**Issue Without Consistency:**
- If Bob’s balance is updated incorrectly (e.g., receives ₹6000 instead of ₹5000), the total money becomes ₹16,000, violating banking rules.

✅ **Ensures no incorrect changes in data.**

---

## 3. Isolation – "Transactions Don’t Interfere"
**Example:**
- Suppose Alice and Bob both try to withdraw ₹5000 simultaneously from the same account (₹10,000 balance).

**Issue Without Isolation:**
- If both withdrawals check the balance at the same time (₹10,000), they may both proceed, leading to ₹10,000 being deducted twice, resulting in **₹0 instead of ₹5000 left**.

**How Isolation Solves It:**
- The system **processes one transaction at a time**.
- If Alice’s transaction is being processed, Bob’s transaction **must wait** until Alice’s transaction is complete.

✅ **Prevents incorrect balance calculations due to simultaneous actions.**

---

## 4. Durability – "Once Committed, It's Permanent"
**Example:**
- Alice successfully transfers ₹5000 to Bob.
- A sudden **power failure** occurs immediately after the transaction.

**Issue Without Durability:**
- If the system crashes, Bob’s updated balance might be lost, and it may appear as if he never received the money.

**How Durability Solves It:**
- The bank’s database ensures that once the transfer is **successfully completed**, it **remains saved** permanently.
- When the system restarts, Bob’s account still shows the updated balance.

✅ **Ensures transaction data isn’t lost after completion.**

---

## 🔹 Summary: How ACID Properties Help in Banking

| **ACID Property** | **Ensures in Alice & Bob's Example** |
|------------------|--------------------------------|
| **Atomicity** | If Alice’s money is deducted, Bob must receive it (or rollback). |
| **Consistency** | Total money in the system remains correct before & after. |
| **Isolation** | No two transactions interfere, preventing race conditions. |
| **Durability** | Transaction remains saved even after a system crash. |

✅ **ACID properties make banking transactions safe, reliable, and error-free.**

---

# Database Normalization (1NF, 2NF, 3NF) - README

## Introduction
Normalization is a process in **database design** that organizes data to **reduce redundancy** and **improve integrity**. It involves decomposing tables to minimize data duplication while ensuring data dependencies make sense.

---
## Normal Forms (Till 3NF)

### **1NF (First Normal Form) - Eliminate Duplicates & Ensure Atomicity**
**Rule:**  
- Each column should have **atomic** (indivisible) values.  
- Each row should have a **unique identifier** (Primary Key).  
- No **repeating groups** (i.e., no multiple values in a single column).

**Example (Before 1NF - Unnormalized Table):**  
| Student_ID | Name   | Subjects         |  
|------------|--------|-----------------|  
| 101        | Om     | Math, Science   |  
| 102        | Raj    | Science, English|  

**Problem:**  
- The **Subjects** column contains **multiple values**, violating atomicity.

**After 1NF:**  
| Student_ID | Name   | Subject  |  
|------------|--------|---------|  
| 101        | Om     | Math    |  
| 101        | Om     | Science |  
| 102        | Raj    | Science |  
| 102        | Raj    | English |  

✅ **Now, each field contains atomic values, and there are no repeating groups.**

---
### **2NF (Second Normal Form) - Eliminate Partial Dependencies**
**Rule:**  
- **Must be in 1NF**  
- **No Partial Dependency**: A column should depend on the whole primary key, not just a part of it.  
- This mainly applies to **composite keys** (keys made of multiple columns).  

**Example (Before 2NF - Partial Dependency Present):**  
Consider a scenario where a **Student_ID + Subject** together form the primary key:  

| Student_ID | Subject  | Student_Name | Teacher |  
|------------|---------|-------------|---------|  
| 101        | Math    | Om          | Mr. A   |  
| 101        | Science | Om          | Mr. B   |  
| 102        | Science | Raj         | Mr. B   |  
| 102        | English | Raj         | Mr. C   |  

**Problem:**  
- **Student_Name** depends only on **Student_ID**, not on the full composite key (**Student_ID + Subject**).  
- **Teacher** depends only on **Subject**, not on **Student_ID**.

✅ **Solution:** Split into two tables:

**Student Table:**  
| Student_ID | Student_Name |  
|------------|-------------|  
| 101        | Om          |  
| 102        | Raj         |  

**Subject Table:**  
| Subject  | Teacher |  
|---------|---------|  
| Math    | Mr. A   |  
| Science | Mr. B   |  
| English | Mr. C   |  

**Student_Subject Table (Bridge Table):**  
| Student_ID | Subject  |  
|------------|---------|  
| 101        | Math    |  
| 101        | Science |  
| 102        | Science |  
| 102        | English |  

✅ **Now, every non-key column depends on the full primary key, removing partial dependencies.**

---
### **3NF (Third Normal Form) - Eliminate Transitive Dependencies**
**Rule:**  
- **Must be in 2NF**  
- **No Transitive Dependency**: A non-key column should not depend on another non-key column.

**Example (Before 3NF - Transitive Dependency Present):**  

| Student_ID | Student_Name | City      | Pincode |  
|------------|-------------|----------|---------|  
| 101        | Om          | Hyderabad | 500001  |  
| 102        | Raj         | Mumbai    | 400001  |  

**Problem:**  
- **Pincode** depends on **City**, not directly on **Student_ID**.
- If the city name changes, multiple records will need updating.

✅ **Solution:** Split into two tables:

**Student Table:**  
| Student_ID | Student_Name | City      |  
|------------|-------------|----------|  
| 101        | Om          | Hyderabad |  
| 102        | Raj         | Mumbai    |  

**City Table:**  
| City      | Pincode |  
|----------|---------|  
| Hyderabad | 500001  |  
| Mumbai    | 400001  |  

✅ **Now, no non-key column depends on another non-key column, removing transitive dependencies.**

---
### **Summary of Normal Forms:**
| Normal Form | Key Condition | Goal |  
|------------|--------------|------|  
| **1NF**    | Atomic values, No repeating groups | Eliminates duplicate columns & ensures atomicity |  
| **2NF**    | No Partial Dependencies (Non-key columns depend on whole primary key) | Removes partial dependency |  
| **3NF**    | No Transitive Dependencies (Non-key column should not depend on another non-key column) | Removes transitive dependency |

---
## Conclusion
Normalization improves database efficiency, prevents anomalies, and ensures data integrity.



