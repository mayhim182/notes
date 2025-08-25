# 📘 ACID Properties in Database Transactions

ACID stands for **Atomicity, Consistency, Isolation, Durability** — four key properties that ensure reliable, correct, and fault-tolerant database transactions.

---

## 🔹 Atomicity

**Definition**:  
All operations in a transaction must either **complete fully** or **have no effect at all**.

**Purpose**:  
Ensures *"all-or-nothing"* behavior. Prevents partial updates in case of failures.

**Example**:  
A user pays $5 to another:
- If $5 is deducted from A's wallet, it must be added to B's wallet.
- If either step fails, the entire transaction is rolled back.

---

## 🔹 Consistency

**Definition**:  
A transaction brings the database from one **valid state to another**, maintaining **all predefined rules and constraints** (e.g., foreign keys, data types, business rules).

**Purpose**:  
Guarantees that no transaction will leave the database in an invalid state.

**Example**:  
A withdrawal transaction should not allow an account balance to go negative if the system rule says balance must be ≥ 0.

> ❗ Note: Consistency is about **data validity**, not rollback. Rollback is handled by **atomicity**.

---

## 🔹 Isolation

**Definition**:  
Concurrent transactions appear to execute in **complete isolation** from one another, even if they run simultaneously.

**Purpose**:  
Prevents **race conditions**, dirty reads, non-repeatable reads, and phantom reads.

**Example**:  
Two users booking the last movie ticket simultaneously — only one should succeed, ensuring no overbooking.

> 💡 Achieved through various **isolation levels** like:
> - Read Uncommitted  
> - Read Committed  
> - Repeatable Read  
> - Serializable

---

## 🔹 Durability

**Definition**:  
Once a transaction is **committed**, its changes are **permanently saved**, even if there's a crash or power failure.

**Purpose**:  
Protects committed data against system failures.

**Example**:  
After booking a train ticket and receiving confirmation, the data is stored reliably (usually on disk), and won’t be lost in a crash.

---

## ✅ Summary Table

| Property    | Guarantees                                | Focus Area           |
|-------------|--------------------------------------------|----------------------|
| Atomicity   | All steps of a transaction succeed or none | Transaction integrity|
| Consistency | DB remains valid before and after tx       | Rule enforcement     |
| Isolation   | No interference between concurrent txs     | Concurrency control  |
| Durability  | Committed changes are never lost           | Crash recovery       |

---

> Use ACID as the foundation for building **reliable, fault-tolerant, and correct transactional systems**.
