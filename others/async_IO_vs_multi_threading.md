# Async I/O vs Multi-threading

Actually these two ideas are totally different. 

## Sync I/O vs Async I/O
Sync I/O means the thread is blocked when executing the task, async I/O means the thread start the task, and then it is freed to execute other tasks. When the first task is finished, a signal is sent to notified the thread.

## Single-threading vs Multi-threading
This is so obvious..

## Situations
* Sync I/O + Single-threading: One blocking thread
* Async I/O + Single-threading: One non-blocking thread
* Sync I/O + Multi-threading: Multiple blocking threads
* Async I/O + Multi-threading: Multiple non-blocking threads


