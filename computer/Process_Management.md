# Process Management

[TOC]

- Define
  - Narrow Sense:  Process is the execution process of a program.  
    程序是一个没有生命的实体, 只有处理器赋予程序生命时, 它才能成为一个活动的实体, 我们称其为 Process .
  - Broad Sense:  Process 是一个具有一定独立功能的程序关于某次数据集合的一次运行活动, 是操作系统分配资源的基本单元.  
    每一个 Process 都有它自己的地址空间, 包括 text region, data region, stack region

- Process states
  - Blocked: 等待某个事件的完成
  - Waiting: 等待系统分配处理器以便运行
  - Running: 占有处理器正在运行

* Scheduling Algorithm
  - Purpose
    - Process 的基本状态及状态间的转换  

  - Include
    - FCFS, first come first served
    - SJF, Shortest Job First
    - HRRN, Hight Response Ratio Next
    - RR, Round-Robin 
    - Preemptive Scheduling
      - 基于时钟中断
      - 立即抢占式

* Create Process
  * fork()
    - fork is an operation whereby a process creates a copy of itself.
    - 底层实现原理
      - fork()系统调用通过复制一个现有Process 来创建一个全新的Process . Process 被存放在一个叫做任务队列的双向循环链表当中, 链表当中的每一项都是类型为task_struct称为Process 描述符的结构, 也就是Process PCB.

* Inter Process Communication
  - Purpose
    - 数据传输: 一个 Process 发送数据给另一 Process 
    - 资源共享: 多个 Process 间共享同样资源
    - 通知事件: 一个 Process 向另一个或一组 Process 发送消息, 通知发生了某种事件
    - Process 控制: 有些 Process 希望完全控制另一 Process 的执行(如Debug Process ), 该控制 Process 希望能拦截另一 Process 的所有操作, 并及时知道其状态改变. 

  - Principle
    - 在内核中开辟一块缓冲区, 作为共享内存  

  - Include
    * Anonymous Pipe
      - Anonymous Pipe 是特殊文件, 只存在于内存, 不存在于文件系统
      - 单向通信, 若要双向通信, 需创建两个管道
      - 通信的数据是无格式的流并且大小受限
      - 只能用于存在 parent-child 关系的 Process 间通信
      - 生命周期随 Process 创建而建立, 随 Process 终止而消失

    * Name Pipe
      - 解决: Anonymous Pipe 只能在 parent-child 关系 Process 间的通信限制
      - 需在文件系统创建一个类型为 p 的设备文件, 那么毫无关系的 Process 可以通过该设备文件进行通信
      - 通信数据都遵循先进先出原则, 不支持 lseek 之类的文件定位操作

    * Message Queue
      - 解决: Pipe 数据是无格式的字节流的问题
      - Message Queue 是保存在内核的"消息链表", 消息体是可以用户自定义的数据类型
      - 发送数据时, 会被分成一个一个独立的消息体, 接收数据时, 也要与发送方发送的消息体的数据类型保持一致
      - Message Queue 通信速度不是最及时, 每次数据写入、读取都需要经过用户态与内核态之间的复制过程.

    * Shared Memory
      - 解决: Message Queue 通信中用户态与内核态之间数据复制过程带来的开销
      - 直接分配一个Shared Memory, 每个 Process 都可以直接访问, 就像访问 Process 自己的空间一样快捷方便, 不需要陷入内核态或者系统调用, 大大提高了通信的速度, 
      - 最快的 Process 间通信方式
      - 问题: 多Process 竞争同个共享资源会造成数据的错乱

    * Semaphore
      - 解决: 多Process 竞争同个共享资源会造成数据的错乱
      - 互斥访问确保任何时刻只能有一个Process 访问共享资源
      - Semaphore 不仅可以实现访问的互斥性, 还可以实现Process 间的同步
      - Semaphore 是一个计数器, 表示资源个数, 其值可以通过两个原子操作来控制, 分别是 P 操作和 V 操作

    * Signal
      - Signal 是Process 间通信机制中唯一的异步通信机制, Signal 可以在应用Process 和内核之间直接交互, 内核也可以利用 Signal 来通知用户空间的Process 发生了哪些系统事件
      - 一旦有 Signal 发生, Process 有三种方式响应 Signal: 1. 执行默认操作; 2. 捕捉 Signal; 3. 忽略 Signa; 
      - SIGKILL, SEGSTOP 两个信号, 应用Process 无法捕捉和忽略, 方便能在任何时候结束或停止某个Process. 

    * Socket Communication
      - 解决: 不同主机的Process 间通信  (还可以用于本地主机Process 间通信)
      - 三种常见的通信方式: TCP 协议, UDP 协议, 本地Process 间通信方式.

* Thread/Process Context Switch
  - Purpose
    - CPU 从一个Process 或Thread切换到另一个Process 或Thread. 
  - 分类
    - Process Context Switch
    - Thread Context Switch
    - interruption Context Switch

* Deadlock 
  - 必要条件
    - 互斥条件: 资源是独占的且排他使用, Process 互斥使用资源, 即任意时刻一个资源只能给一个Process 使用, 其他Process 若申请一个资源, 而该资源被另一Process 占有时, 则申请者等待直到资源被占有者释放资源. 
    - 不可剥夺条件: Process 所获得的资源在未使用完毕之前, 不被其他Process 强行剥夺, 而只能由获得该资源的Process 释放. 
    - 请求和保持条件: Process 每次申请它所需要的一部分资源, 在申请新的资源的同时, 继续占用已分配到的资源. 
    - 循环等待条件: 发生 Deadlock 时必然存在一个Process 等待队列, 形成一个Process 等待环路
  - Deadlock Avoidance

* Orphan Process & Zombie Process 
  * Orphan Process: 一个父Process 退出, 而它的一个或多个子Process 还在运行, 那么那些子Process 将成为Orphan Process. Orphan Process 将被 init Process (Process 号为 1)所收养, 并由 init Process 对它们完成状态收集工作. 
  * Zombie Process : 一个Process 使用 fork 创建子Process , 如果子Process 退出, 而父Process 并没有调用 wait 或 waitpid 获取子Process 的状态信息, 那么子Process 的Process 描述符仍然保存在系统中. 这种Process 称之为僵尸Process . 

## Include

- [parallel computing](./parallel computing.md)