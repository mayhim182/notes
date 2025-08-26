Here’s a rewritten and structured version of your notes (without emojis):

---

# Questions

**Explain the point about scalability**

---

# Additions to the Existing Notes

## **Lambda Expressions and Variable Scope**

- Variables used inside lambda expressions must be **final** or **effectively final**.
    
- **Reason:**
    
    - A lambda may outlive the method in which it is defined (e.g., when passed to another thread).
        
    - Local variables normally exist on the stack and are destroyed when the method returns.
        
    - Lambdas capture variables **by value**, and to prevent inconsistencies in these captured values, Java enforces immutability.
        

---

## **Closure**

A closure is a function or method that **captures variables from its surrounding scope**.

---

## **1. What Does `.submit()` Do?**

- Accepts a **Runnable** or **Callable** task.
    
- Executes the task **asynchronously** in a thread from the pool.
    
- Returns a **Future**, which can be used to:
    
    - Check if the task is complete (`isDone()`)
        
    - Cancel the task (`cancel()`)
        
    - Retrieve the result (`get()`)
        

---

## **2. `submit()` vs `execute()`**

- **`execute(Runnable)`** – Fire-and-forget; no return value.
    
- **`submit(Runnable/Callable)`** – Returns a **Future**, allowing you to monitor or retrieve results.
    

---

## **Runnable vs Callable**

- **Runnable** –
    
    - No return value.
        
    - Suitable for simple background tasks.
        
- **Callable** –
    
    - Returns a result.
        
    - Can propagate exceptions.
        

---

## **Executor Framework Components**

- **Executor**
    
- **ExecutorService**
    
- **ScheduledExecutorService**
    
- **Callable**
    
- **Future**
    
- **CompletionService**
    
- **RejectedExecutionHandler**
    

---
