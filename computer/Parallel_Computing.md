# Parallel Computing

[TOC]

CAP定理是分布式系统中的一个重要理论，指出在一个分布式数据存储中，最多只能同时满足以下三项中的两项：
一致性（Consistency）：所有节点在同一时间看到的数据是一致的。
可用性（Availability）：每个请求都会在合理的时间内得到响应，无论响应的结果是否最新。
分区容忍性（Partition Tolerance）：系统在网络分区的情况下仍然能够继续操作。

## Synchronous &  Asynchronous

Synchronous: Tasks are performed one after the other, in a sequence. Each task must be completed before the next one starts.

Asynchronous: Tasks are performed independently of each other. A task can start before the previous one is completed.

Synchronous

- 必须一件一件事做, 等前一件做完了才能做下一件事.  

Asynchronous

- 一个异步过程调用发出后, 调用者在没有得到结果之前, 就可以继续执行后续操作. 当这个调用完成后, 一般通过状态、通知和回调来通知调用者. 对于异步调用, 调用的返回并不受调用者控制. 
  - 状态  
    监听被调用者的状态（轮询）, 调用者需要每隔一定时间检查一次, 效率会很低. 
  - 通知  
    当被调用者执行完成后, 发出通知告知调用者, 无需消耗太多性能. 
  - 回调  
    与通知类似, 当被调用者执行完成后, 会调用调用者提供的回调函数. 

## Communication between processes

- Information channel between processes
  - Pipes: Unidirectional data channels used for communication between processes on the same machine.
  - Channel
- Communication based on a shared storage between processes
  - Shared Memory: Multiple processes can access a common memory space. Efficient but requires synchronization.
  - Redis
  - Database
- Communication based on Computer Network
  - Sockets: Enable communication between processes over a network, supporting both TCP (reliable) and UDP (unreliable) protocols.
  - Remote Procedure Calls (RPC): Allow a program to execute a procedure on another address space (commonly on a remote server).
  - HTTP
- Third-party communication services
  - Message Queues: Allow processes to exchange messages in a queue format, supporting both asynchronous and synchronous communication.

## Shared resources

### Lock mechanism

- Mutex (Mutual Exclusion): A lock that ensures only one thread can access a resource at a time. 
- Spinlock: A lock where a thread repeatedly checks for a lock to become available, "spinning" in a loop.
- Read-Write Lock: A lock that allows multiple threads to read a resource concurrently, but only one thread to write at a time.
- Semaphore: A signaling mechanism that can control access to a resource by multiple threads.
- Condition Variable: A synchronization mechanism that allows threads to wait for certain conditions to be met.
- reentrant lock

### Deadlock

Deadlock is a situation in parallel computing where two or more processes are unable to proceed because each is waiting for the other to release a resource. A deadlock situation on a resource can arise only if all of the following conditions occur simultaneously in a system.

- Mutual exclusion: multiple resources are not shareable; only one process at a time may use each resource.

- Hold and wait or resource holding: a process is currently holding at least one resource and requesting additional resources which are being held by other processes.
- No preemption: a resource can be released only voluntarily by the process holding it.
- Circular wait: each process must be waiting for a resource which is being held by another process, which in turn is waiting for the first process to release the resource.



## Task Assignment: Load Balancing

### Amdahl’s Law & Gustafson’s Law
