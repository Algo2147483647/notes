# Concurrent Computing

[TOC]

## Context

并发： 多个任务在重叠的时间段内都在推进（可能在一个核心上快速切换执行，也可能在多个核心上并行执行）。并发计算最根本的是处理“同时发生的任务”。但“同时”这个词本身就有陷阱——在单核CPU上其实是快速切换，多核才是真并行。所以第一层本质是：如何虚拟化多个执行流。

并发管理，是协调多个独立的计算任务（计算流）对共享的、有限的资源（主要是 CPU 时间片、内存、I/O 带宽）进行安全、高效、可控的访问，以达成某种计算目标。所有并发模型的核心，都在于如何抽象和管理这些计算单元、资源以及它们之间的交互。

### Computational Unit

**Computational Unit**. 什么是“一个”需要被调度执行的任务？它的边界在哪里？**粒度：** 任务的大小（轻量级如协程、Future；重量级如进程）。



进程, 操作系统分配资源（内存、文件句柄、网络端口等）和调度的基本单位。拥有独立的虚拟地址空间。进程间内存空间隔离，通信需要通过IPC机制（管道、消息队列、共享内存、套接字等），开销相对较大。

线程, 进程内的一个独立执行流。共享其所属进程的内存空间和大部分资源（文件描述符等）。线程间可以直接读写同一进程的内存，这使得数据共享高效，但也引入了同步（互斥锁、信号量等）和竞态条件的复杂性。

内核线程： 由操作系统内核直接管理和调度。操作系统感知其存在。

用户线程： 在用户空间由线程库管理。内核感知不到单个用户线程，只看到其所属的内核线程（或进程）。切换开销更小，但阻塞操作会影响同一内核线程上的所有用户线程。

协程 / 纤程 / Goroutine / Erlang Process , 比线程更轻量级的用户态并发抽象。通常由语言运行时或特定库管理。

### Resource



## Problem

同步与通信



- 如何处理多个任务间的数据共享？
- 如何分配计算资源（CPU时间、线程）？
- 任务间如何交换信息？
- 如何处理任务失败？

如何高效、安全地协调多个同时（或看似同时）执行的计算任务（线程、进程、协程等）对共享资源和系统状态进行访问和修改。它旨在解决单线程顺序执行模型在面对现代计算需求时的根本性局限。

- 核心矛盾：多执行流（逻辑或物理）与共享资源之间的动态交互

约束

- 安全性（Safety）：无竞态条件、无死锁
- 活性（Liveness）：保证进展性
- 公平性（Fairness）：资源分配合理性

一致性：

- 强一致性：线性化（Linearizability）
- 弱一致性：最终一致性（Eventual Consistency）

### Resource Access & Synchronization

多个计算单元如何安全、高效地访问共享的、状态可变的关键资源（CPU时间、内存数据、文件、网络连接等）？如何防止竞态条件？

共享状态 vs. 消息传递：

共享状态： 计算单元直接读写同一块内存。需要锁、原子操作、内存屏障等机制来强制互斥访问和保证内存可见性。本质是通过约束访问时序来保证安全。

消息传递： 计算单元不直接共享内存。它们通过发送和接收不可变或深拷贝的消息进行通信。状态封装在单元内部，修改只能通过自身。本质是通过隔离状态和显式通信来避免共享。Actor 模型是此范式的代表。

协调原语： 提供高级抽象来管理单元间的执行顺序和依赖（如信号量、条件变量、通道、Promise/Future、Barrier 等）。

本质： 解决冲突和协作的问题。这是并发中最复杂、最容易出错的部分。模型的选择极大地影响了程序的安全性、可理解性和性能。

### Scheduling & Execution

有限的物理资源（CPU核心）如何分配给众多的计算单元？如何决定哪个单元何时在哪个核心上运行？

**抢占式 vs. 协作式：**

- **抢占式：** 调度器（通常是操作系统内核）在任意时刻可以中断正在运行的任务（如线程），将CPU分配给其他任务。需要处理上下文切换开销和复杂同步。
- **协作式：** 任务主动让出CPU控制权（如协程的 `yield`）。依赖任务的“合作”，但切换开销小、同步简单。

- **调度器层级：** 用户级调度器（如 Go 的 goroutine 调度器、异步运行时） vs. 操作系统级调度器。
- **公平性、优先级、亲和性：** 如何平衡不同任务的执行机会？关键任务能否优先？任务是否绑定到特定CPU核心？

**本质：** 资源的**分配策略**。决定了并发系统的吞吐量、响应延迟和资源利用率。

### Communication & Coordination

计算单元之间如何交换信息、传递数据、通知事件？如何让多个单元协同完成一个更大的目标？

共享内存（通过同步机制保护）、消息传递（点对点、发布/订阅）、事件通知、数据流管道。

同步通信： 发送方阻塞等待接收方接收（或反之），实现即时、确定的交互。

异步通信： 发送方发送后立即继续，不等待接收。消息被缓冲或由接收方主动获取。提高吞吐，但增加延迟和状态管理复杂度。

模式： RPC（远程过程调用）、数据流（如管道/过滤器）、发布/订阅、事务等。

本质： 计算单元间的信息流和控制流。是构建复杂并发系统的粘合剂。

### Error Handling & Fault Tolerance

## Resolution

### Shared memory

- 需要锁机制

- Java synchronized: 确保同一时间只有一个线程执行同步代码块，这明显是共享内存模型中解决竞争条件的方法. 共享堆内存，synchronized锁住的是对象监视器，从而保护共享数据

- C++的std::thread默认共享地址空间，显式使用互斥量来同步。Python的threading模块线程共享内存，但由于GIL，实际上在解释器级别只有一个线程执行字节码，不过对于IO操作，GIL会被释放，所以线程间还是需要同步共享数据。

#### Lock mechanism

锁模型本身是在并发单元复用共享资源时，解决竞争的一种手段。从完备性说，经典编程中实现任何锁模型只需要两个东西：互斥锁+条件变量。

- Mutex (Mutual Exclusion): A lock that ensures only one thread can access a resource at a time. 
- Spinlock: A lock where a thread repeatedly checks for a lock to become available, "spinning" in a loop.
- Read-Write Lock: A lock that allows multiple threads to read a resource concurrently, but only one thread to write at a time.
- Semaphore: A signaling mechanism that can control access to a resource by multiple threads.
- Condition Variable: A synchronization mechanism that allows threads to wait for certain conditions to be met.
- reentrant lock

#### Deadlock

Deadlock is a situation in parallel computing where two or more processes are unable to proceed because each is waiting for the other to release a resource. A deadlock situation on a resource can arise only if all of the following conditions occur simultaneously in a system.

- Mutual exclusion: multiple resources are not shareable; only one process at a time may use each resource.

- Hold and wait or resource holding: a process is currently holding at least one resource and requesting additional resources which are being held by other processes.
- No preemption: a resource can be released only voluntarily by the process holding it.
- Circular wait: each process must be waiting for a resource which is being held by another process, which in turn is waiting for the first process to release the resource.

#### Software transactional memory

STM(Software transactional memory) 一种用来代替锁模型的乐观并发同步机制。用软件的方式去实现事务内存(Transactional memory)，而事务内存中的事务(Transactional)正是关系型数据库中的概念，一个事务必须满足ACID性质. STM实现的一种方式是基于MVCC(Multiversion concurrency control)。

### Message passing

#### Actor

- 通过独立的“Actor”作为并发单元，每个 Actor 拥有私有状态，仅通过异步消息传递通信，避免共享内存。

- Actor模型通过消息传递，不共享内存

- 通信方式:  异步消息传递; 同步机制: 消息队列、邮箱

#### Communication Sequential Processes

>   Don't communicate by sharing memory; instead, share memory by communicating.

- 通过“通道”（Channel）在不同进程/协程间传递消息，发送方和接收方必须同步（类似于管道）。

- 同步机制:  通道同步（发送/接收）





### Event loop

- 单线程或少量线程通过事件循环（Event Loop）处理异步事件（如 I/O 完成、用户输入），使用回调（Callbacks）或 Promise 响应事件。
- 回调地狱（Callback Hell）





- Data Parallelism

  - 将数据分割为多个块，并行处理相同操作（如 MapReduce）