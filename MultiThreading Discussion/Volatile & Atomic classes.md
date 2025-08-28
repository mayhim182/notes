**Volatile and Atomic classes**

---

### Volatile keyword

- `volatile` is a field modifier in Java.
    
- It tells JVM and threads that a variable’s value will always be read from and written to **main memory**, not from a thread’s local cache.
    
- This ensures **visibility** of changes across threads.
    
- But it doesn’t guarantee **atomicity** for compound operations.
    

**Example:**

```java
class Counter {
    volatile int count = 0;

    void increment() {
        count++;  // not atomic
    }
}
```

Steps happening in different threads:

1. read count
    
2. add 1
    
3. write back
    

→ Two threads may read the same value and updates get lost.

---

### Atomic Classes (`java.util.concurrent.atomic`)

- Provides atomic operations without using explicit synchronization (`synchronized`).
    
- Examples: `AtomicInteger`, `AtomicLong`, `AtomicBoolean`, `AtomicReference`.
    
- They ensure both **visibility** (because they use `volatile` inside) and **atomicity** (because they use CAS).
    

**Example:**

```java
import java.util.concurrent.atomic.AtomicInteger;

class AtomicCounter {
    AtomicInteger count = new AtomicInteger(0);

    void increment() {
        count.incrementAndGet();  // atomic
    }
}
```

---

### CAS (Compare-And-Swap)

- CAS is a **CPU-level atomic instruction** used for lock-free concurrency.
    
- Works like this:
    

```
CAS(memory_location, expected_value, new_value)
```

1. Check if `memory_location` still has `expected_value`.
    
2. If yes → replace it with `new_value` (success ✅).
    
3. If no → do nothing (fail ❌).
    

All of this happens **atomically**.

**Under the hood in Java (`AtomicInteger.incrementAndGet()`):**

```java
int oldValue, newValue;
do {
    oldValue = value;           // read volatile
    newValue = oldValue + 1;    // compute
} while (!CAS(value, oldValue, newValue)); // retry if CAS fails
return newValue;
```

---

### Quick Recap

- `volatile` → visibility only, no atomicity.
    
- `Atomic classes` → visibility + atomicity using CAS.
    
- Use `volatile` for simple flags (like `isRunning`).
    
- Use `AtomicInteger` (or sync) when you need compound atomic updates (like counters).
    

---
