# Operating System

[TOC]

## Include

- [memory management](./memory management.md)
- [process management](./process management.md)



## File System Management

## IO

* I/O
* Blocking IO & Non-Blocking IO

## Memory Management

内存不足时:当向系统申请内存但内存不足时, 系统会把根据置换算法把暂进不用的内存置换到硬盘里,更新映射关系到硬盘上, 再更新新申请的内存映射关系, 让我们产生无限内存的错觉. (交换到硬盘后会导致性能下降, 硬盘读取速度比内存慢太多了). 例如下面这个例子, 程序0,1,2分别加载了物理地址的0,1,2. 此时程序3进来, 也需要申请内存. 然后就根据算法先把内存腾出来, 腾出来的放到磁盘上, 再把腾出来的空间给程序3. 这样就可以解决内存不足的问题而不会导致崩溃. 

程序间相同的地址:即使程序的地址相同, 但是每个程序通过自己的映射表映射到不同的物理内存而不会互相产生干扰. 但是程序间相互独立一定是好的吗？并不是, 因为有些内存是需要共享的. 例如不同的程序会共享系统文件, 系统选择框等. 让程序间实现共享内存的方法是把地址指向相同的物理内存. 

流程
- 缺页处理过程
- 缺页置换算法
  - 最久未使用
  - 先进先出
  - 最佳置换

## Device Management



## Synchronous & Asynchronous  

Thread
* Synchronization Mode
  - Purpose
    -  多线程通过特定的设置来控制线程之间的执⾏顺序
  - Include 
    - Mutex
    - SpinLock
      - 互斥锁与自旋锁的底层区别
    - Read-Write Lock
    - 条件变量

- Difference between Process and Thread
  - 不同的操作系统资源管理方式, 进程有独立的地址空间, 一个进程崩溃后, 在保护模式下不会对其它进程产生影响, 而线程只是一个进程中的不同执行路径. 线程有自己的堆栈和局部变量, 但线程之间没有单独的地址空间, 一个线程死掉就等于整个进程死掉, 所以多进程的程序要比多线程的程序健壮, 但在进程切换时, 耗费资源较大, 效率要差一些. 但对于一些要求同时进行并且又要共享某些变量的并发操作, 只能用线程, 不能用进程. 

Multi-Process & Multi-Threading


* Multi-Threading
  - 缺点
    - 使用太多Thread, 很耗系统资源, 更多Thread需要更多内存. 
    - 影响系统性能, 操作系统需要在Thread之间来回切换. 
    - 需要考虑Thread操作对程序的影响, 如Thread挂起, 中止等操作对程序的影响.
    - Thread使用不当会发生很多问题. 
* Note
  - Single   Process Single   Thread: 一个人在一个桌子上吃菜. 
    Single   Process Multiple Thread: 多个人在同一个桌子上一起吃菜. 
    Multiple Process Single   Thread: 多个人每个人在自己的桌子上吃菜.

  - Multiple Thread的问题是多个人同时吃一道菜的时候容易发生争抢, 例如两个人同时夹一个菜, 一个人刚伸出筷子, 结果伸到的时候已经被夹走菜了... 此时就必须等一个人夹一口之后, 在还给另外一个人夹菜, 也就是说资源共享就会发生冲突争抢. 
  - For Windows, "开桌子"开销很大, 因此 Windows 鼓励大家在一个桌子上吃菜. 因此 Windows 多Thread学习重点是要大量面对资源争抢与同步方面的问题. 
  - For Linux,   "开桌子"开销很小, 因此 Linux 鼓励大家尽量每个人都开自己的桌子吃菜. 这带来新的问题是: 坐在两张不同的桌子上, 说话不方便. 因此, Linux 下的学习重点大家要学习Process 间通讯的方法. 

## [xv6](.\xv6.md)

## [Linux](./Linux.md)

