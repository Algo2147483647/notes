# $Synchronization$

[TOC]

# Purpose

## Define

> Process synchronization refers to the idea that multiple processes are to join up or handshake at a certain point, in order to reach an agreement or commit to a certain sequence of action.



## Problems

- **Race Condition**: This occurs when two or more threads can access shared data and they try to change it at the same time.
- **Deadlock**: This is a state where two or more processes are unable to proceed because each is waiting for the other to release a resource.
- **Livelock**: Similar to deadlock, a livelock is a situation where two or more processes continuously change their state in response to the change in state of the other processes, without making any progress.
- **Starvation**: Starvation occurs when one or more threads are unable to gain access to resources or the CPU because other "greedy" threads are monopolizing these resources. 
- **Priority Inversion**: This problem occurs when a high priority task is forced to wait because a lower priority task has a lock on a resource the high priority task needs.
- **Convoy effect**: Convoy effect happens when one slow process blocks or significantly hampers the performance of other faster processes, similar to how a slow vehicle can slow down all vehicles behind it in a single-lane road.
- **Complexity & Overhead**

# Concepts

## Atomic operation

```cpp
std::atomic<int> atomicInt = 0;
```



## Mutex (*Mutually exclusive flag*)

The primary purpose of a mutex is to enforce mutually exclusive access to the shared resource, allowing only one thread or process to execute a critical section of code at a time. When a thread or process acquires the mutex, it gains the right to access the protected resource while other threads or processes that try to acquire the mutex will be blocked until the current owner releases it.

- Lock (Acquire)
- Unlock (Release)

```cpp
std::mutex mtx; // Define a global mutex

{
    mtx.lock();
    // works
    mtx.unlock(); // Release the mutex
}
```

## Semaphore

A semaphore maintains a counter (usually an integer) that represents the number of available resources.

- Wait
- Signal

```cpp
const int N = 3; // Maximum number of concurrent threads allowed

std::semaphore sem(N); // Initialize semaphore with N resources

{
    sem.acquire(); // Wait (P) on the semaphore
    // works
    sem.release(); // Signal (V) the semaphore, releasing the resource
}
```



## Condition Variable
The primary purpose of a condition variable is to enable threads to block and wait for a specific condition to be met, rather than busy-waiting (actively checking repeatedly) for the condition. This leads to more efficient CPU utilization and avoids unnecessary consumption of system resources.
- Wait 
- Notify 
  - `notify_one`
  - `notify_all`

```cpp
std::mutex mtx;
std::condition_variable cv;
bool condition = false;

{
    // wait for condition
    std::unique_lock<std::mutex> lock(mtx);
    cv.wait(lock, []{ return condition; });
}

{
    // works
    {
        std::lock_guard<std::mutex> lock(mtx);
        condition = true;
    }
    cv.notify_all();
}
```



## Critical Section

## Read-Write Lock

## Spinlock



