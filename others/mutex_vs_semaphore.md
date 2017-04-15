# Mutex vs Semaphore

Semaphore was introduce by Dijkstra (binary semaphore). He used the notation P & V, from Dutch words, Prolagen(P) means decrease, Verhogen(V) means increase.

Here is the code:

```
/* task */
...
P(S); // S is the semaphore
/* critical region */
V(S);
...
```

A semaphore with an initial value one is a **binary semaphore**. A semaphore with an initial value greater than one is called **counting semaphore**.

So what causes confusion is actually mutex vs binary semaphore. The major difference is **the principle of ownership**:

* Mutex is owned by the task that takes it. Only the task that takes the mutex can release it.
* Semaphore is not owned by any tasks, one task can take the semaphore, and another task could release that semaphore.

Mutex and binary semaphore, they do serve different purposes.

* Mutex is for exclusive access to a resource.
* Binary semaphore is used for synchronization, which means notify something just happened immediately. A task that releases the semaphore is notifying the task which takes the semaphore that the event you were waiting just happened.



