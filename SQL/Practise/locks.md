### **Locks and Deadlocks in SQL**

#### **1️⃣ What is a Lock?**
A **lock** is a mechanism used in databases to ensure that multiple transactions can access shared resources **safely and consistently**. It prevents issues like **dirty reads, lost updates, and inconsistent data**.

#### **🔹 Types of Locks:**
- **Shared Lock (S Lock)**: Allows multiple transactions to read the same data but prevents any modifications.
- **Exclusive Lock (X Lock)**: Prevents both reading and writing by other transactions while the lock is held.
- **Row-Level Lock**: Locks a specific row in a table.
- **Table-Level Lock**: Locks an entire table, blocking all operations on it.
- **Page-Level Lock**: Locks a specific page of memory where multiple rows are stored.

---

#### **2️⃣ What is a Deadlock?**
A **deadlock** occurs when two or more transactions **hold locks on resources** and **wait for each other to release them**, leading to an infinite wait state.

#### **🔹 Example of a Deadlock:**
1. **Transaction 1** locks **Row A** and waits for **Row B** to be unlocked.
2. **Transaction 2** locks **Row B** and waits for **Row A** to be unlocked.
3. Neither transaction can proceed because they are **waiting for each other** → **Deadlock happens!** 🚨

#### **🔹 Real-World Example:**
- Imagine **Person A** and **Person B** trying to call each other at the same time. Both lines are busy, and they keep waiting indefinitely. 📞🔄

---

### **3️⃣ How to Prevent Deadlocks?**
✅ **Use proper locking strategies** (e.g., **row-level locks** instead of table-level locks).  
✅ **Ensure transactions access resources in the same order** (e.g., always lock Row A before Row B).  
✅ **Set timeout limits** so that transactions do not wait indefinitely.  
✅ **Use deadlock detection mechanisms** (e.g., SQL Server and MySQL have built-in deadlock detection and resolution).  

Would you like a SQL example of handling deadlocks? 🚀
