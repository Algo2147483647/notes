# Address Space Abstraction

[TOC]

## Context

In a multi-processes environment, the entire physical memory is shared by multiple processes.

## Problem

**Bare Physical Addressing**: Direct use of physical addresses by programs leads to severe issues.

- **Inter-process memory interference**. Errors or malicious actions cannot be contained, potentially damaging other processes or kernel memory. For example, a single program crash may corrupt the entire system; processes may erroneously assess or corrupt others processes' memory. 

- **External memory fragmentation**. External memory fragmentation refers to the wasted "gaps" scattered between allocated memory blocks, which are free memory but too fragmented to be used. Frequent allocation and of physical memory create numerous small, unusable fragments, drastically lowering memory utilization, and large blocks of memory can no longer be allocated.
- **Inefficient memory management**. Due to physical memory is divided into countless scattered blocks, the system cannot coordinate memory space holistically. In this chaotic memory space, programs cannot accurately locate their own memory regions.
- **Relocation Difficulty**. Programs bound to physical addresses cannot be dynamically moved in memory. If the operating system needs to relocate a program (e.g., to defragment memory or reallocate resources), or physical address is referenced by program become invalid, causing crashes or data corruption.

- **Program scale limited by physical memory capacity**. Both individual program size and the total memory footprint of concurrently running processes are constrained by available physical RAM. Programs cannot exceed physical memory limits, and the system cannot run workloads whose combined memory demands surpass installed RAM—even if portions of memory are idle.



一个现代内存管理系统需在以下相互制约的目标之间寻求平衡: 隔离 vs. 效率 vs. 灵活性 vs. 扩展性

**Isolation**: 确保每个进程(或虚拟机)拥有自己独立的、受保护的地址空间。一个进程的错误或恶意行为不能访问或破坏其他进程或内核的内存。

**Efficiency**: 最大化内存访问速度，最小化地址转换带来的开销(时间、空间)。目标是让虚拟内存访问的速度尽可能接近直接访问物理内存的速度。
- 内部碎片:  进程分配的内存块可能远大于其实际需求。
- 外部碎片:  进程加载/卸载后，物理内存中留下大量难以利用的小空隙。

**Flexibility**: 内存管理系统能够适应多样化的应用需求、硬件架构和内存使用模式。例如: 支持不同大小的内存区域(段、页、大页)、高效的内存共享(进程间、内核与用户态)、稀疏地址空间、动态内存分配/回收策略、与新型硬件(如NVM、异构内存)的集成等。

**Scalability**: 内存管理系统能够有效地支持不断增长的系统资源规模，包括: 物理内存容量、CPU核心数量、并发进程/线程数量、地址空间大小等。性能(吞吐量、延迟)不应随规模增长而显著劣化。

那么最简单的方式就是虚拟内存是一块连续的地址然后映射到实际内存也是一个连续的区段这些区段之间是之间的间隔, 那么我们需要考虑的内容是内存的扩展性当虚拟内存需要添加的时候怎么样在实际内存中实现这个内存的扩展这是我们需要考虑的关键之一

第二点是资源利用的效率能够更高效地利用所有的物理内存而不产生碎片和无法利用的空间

第三点则是能够保证不同进程之间内存的隔离性和安全性

## Resolution

### Address virtualization: Logic Address

**Decoupling of address space and physical storage**: In a multi-processes environment the operating system requires a mechanism that allows each program to believe it has a exclusive use of memory, while simultaneously enabling the sharing and protection a physical resources. Actual data may be scattered across physical memory and disk storage. This necessity gave rise to the concept of address space abstraction (address virtualization) which the couples address from physical storage. Address virtualization is the fundamental solution to the problem of exposing physical addresses directly, with the logical address serving as its key mechanism. 

**Logical address** provides a program with an independent, contiguous and protected virtual memory space, freeing it from concerns about the actual layout and limitations of the physical memory.

- **Isolation**: This isolation ensures that the address space of different processes do not interfere with each other, effectively preventing programmer errors or malicious actions from corrupting the memorial data of other processes or the kernel.
- **Contiguity**: The contiguity of logical addresses is an abstraction presented to the program; the actual physical memorial may be fragmented. The mapping table dynamically allocates physical page frames, mapping non-contiguous physical addresses to contiguous virtual addresses.

**The relationship between logical and physical address**: The mapping from a logical address to an actual physical memory address is a maintained by a mapping table. Various approaches implement this mapping table (such as page tables or segment tables), which lies at the core of memory virtualization system designs
$$
\text{logic address}  \xrightarrow{\text{mapping table}} \text{physical address}
$$

### History Evolution

#### Relocation + Boundary Check

**Static Relocation**: This method establishes a logical-to-physical address mapping through simple addition. The mapping occurs when the program is loaded into memory, while the loader modifies all address-related instructions and the data (absolute or relocatable addresses) to point to the actual starting physical address of the program.

- base address: the actual starting physical address of the program.

$$
\text{logic address} +\text{base address} = \text{physical address}
$$

**Base and Bounds** (Dynamic Relocation + Boundary Check): Each process owns a pair of hardware registers (base register, bounds register). CPU performs dynamic address translation.

- **Dynamic Relocation**: Converts a logical address issued by the process by adding it to the Base Register value. This implements dynamic relocation, where the actual location (base address) of a program in physical memory can be changed by simply updating the base address register, without modifying the program code itself.
- **Boundary Check**: verifies whether the logical address < Bounds Register value. If ≥ Bounds, triggers a hardware exception (memory out-of-bounds error), blocking illegal access. This provides basic process isolation, so that a process cannot access memory outside its boundaries (usually other processes or the operating system).
$$
\text{logic address} +\text{base address} = \text{physical address} < \text{bounds address}
$$

> - base address: The starting physical address of the process, stored by base register.
> - bound address: The maximum memory length of the process, stored by bounds register.
>

Limitations of Base and Bounds: Memory Fragmentation (internal and external). Inflexible Address Space, hinders independent growth/protection of segments (heap, stack, code). Demands contiguous physical memory allocation, leads to the problems such as complicated implementation of memory sharing (e.g., common code libraries).

#### Segmentation

**Segmentation** (Multiply Base-Bounds + Segment table) divides a process's address space into distinct logical segments based on its structure (e.g., code, heap, stack, data). Memory is allocated in these variable-length segments. Each segment uses a base and bounds register mechanism for protection and relocation, and its metadata (base address, limit, permissions) is stored in a segment table, indexed by a segment number. Each segment is independently allocated in physical memory, and contiguous storage within each segment, but the segments may not be adjacent. This approach overcomes the limitations of a single linear address space, aligning memory organization with program logic.

- **Segment Table**: $\text{segment number} \to (\text{base address}, \text{limit}, \text{permissions})$. Segment table stores metadata for each segment in the form of a table, with the segment number as the primary key. Segment table translates logical addresses into physical addresses at runtime via the hardware MMU (Memory Management Unit) .

$$
\begin{align*}
\text{logic address} &\overset{\mathrm{def}}{=} (\text{segment number}, \text{offset}) \xrightarrow{\text{segment table}} (\text{base address}, \text{limit}, \text{permissions})\\
\text{physical address} &= \text{base address} + \text{offset} < \text{base address} + \text{limit}
\end{align*}
$$

> - Segment number: The primary key in segment table for a segment.
> - Offset: the offset bits in a segment.
> - Limit: Maximum length of the segment
> - Permissions (Protection Bits): Read/Write/Execute flags (R/W/X)
>

Limitations of segmentation: Complex memory allocation, finding the right space for variable-length segments is a complex dynamic storage allocation problem (first fit, best fit, etc. algorithms have limited effectiveness). Relatively large address translation overhead, each access requires a segment table lookup (in memory). External fragmentation is still serious. The maximum size of a segment is limited by the size of physical memory (or the number of bits in the segment length register).

#### Segmentation with Paging

### Paging

**Paging** (Fixed-Size Paging + Scatter dynamic mapping). Paging has become the standard solution for memory address space virtualization in modern OS.

- **Fixed-Size Paging**: Physical memory is pre-divided into a equal-sized page frames. Virtual address space is logically split into equal virtual pages (same size as frames). OS allocates memory in frame units, significantly simplifying management. The memory allocator only needs to manage a simple free frame list. External fragmentation is virtually eliminated, with only internal fragmentation within the last allocated page remaining. This completely resolves the complex external fragmentation issues inherent to variable-size allocation schemes.
- **Scatter dynamic mapping (Page Table)**: Physical frame act as discrete "building blocks" assignable to any virtual page. Page table stores mapping $\text{virtual page number} \to \text{physical free number}$. Virtual page initially lack physical mapping. and frames are located on assets in demand. This allows the total virtual pages to far exceed physical frames, solving the problem of program scale limited by physical memory capacity. When physical memory is insufficient, the Swap mechanism transfers inactive pages to disk, extending effective memory capacity.

$$
\begin{align*}
\text{logic address} &\overset{\mathrm{def}}{=} (\text{virtual page number, offset}) \xrightarrow{\text{page table}} \text{page frame number}\\
\text{physical address} &= \text{page frame number} \times \text{page size} + \text{offset}
\end{align*}
$$

> - Page Directory Base Register: Stores physical starting address of current process's page table
> - Flags of Page Table Item: 
>
>   - V(Valid Bit): Is the page valid (1 = mapped to physical memory, 0 = not mapped/on disk)
>
>   - R/W(Read/Write Bit): Read/write permissions (0 = read-only, 1 = writable)
>
>   - U/S(User/Supervisor Bit): Access permissions (0 = kernel mode, 1 = user mode)
>
>   - A(Accessed Bit): Access mark (hardware set, indicating that the page has been read)
>
>   - D(Dirty Bit): Dirty page mark (hardware set, indicating that the page has been written)

![page](./assets/page.svg)

#### Page Fault Handling

当进程访问的虚拟页不在物理内存时（PTE的 Present=0），MMU触发缺页异常。操作系统接管处理流程：

Page Replacement Algorithms 当物理内存不足时，需选择牺牲页（Victim Page）换出到磁盘。目标：最小化未来缺页次数。

最优置换算法（OPT, Optimal Replacement）: 换出未来最长时间不再访问的页（预知未来）。理论最优（Belady证明），但无法实现（需预知未来访问序列）。

先进先出（FIFO, First-In First-Out）换出最早进入内存的页。Belady异常：分配的页框数增加时，缺页率可能反而上升。忽略访问频率（可能换出高频使用的老页）。

最近最久未使用（LRU, Least Recently Used）换出最长时间未被访问的页（基于局部性原理）。页表项中的 Accessed Bit：每次访问时由硬件置1。周期性清零 Accessed Bit → 软件模拟访问历史。近似实现（Clock算法）：接近OPT效果，缺页率显著低于FIFO。无Belady异常。

- **活跃链表（active_list）**：存放近期访问的页。
- **非活跃链表（inactive_list）**：候选换出页（从中选择牺牲页）。

| **算法**  | 缺页率  | 实现开销 | 是否可在线实现 | 典型应用场景   |
| :-------- | :------ | :------- | :------------- | :------------- |
| **OPT**   | 最低    | 不可能   | ❌              | 理论基准       |
| **FIFO**  | 较高    | 极低     | ✅              | 嵌入式简单系统 |
| **LRU**   | 接近OPT | 中等     | ✅              | 通用操作系统   |
| **Clock** | 近似LRU | 低       | ✅              | Linux, Windows |



#### Multilevel Page Tables

**多级页表**:  单级页表需要覆盖整个虚拟地址空间(如 64 位下巨大无比)，即使大部分区域未使用也会占用海量内存。将页表树形化(如二级、三级、四级页表)。只有实际被使用的顶级目录和中间目录需要分配内存。**稀疏地址空间下节省大量内存。**

### Translation Lookaside Buffer (TLB)

转换后备缓冲器 (TLB): 问题:  即使单级页表，每次内存访问都需查页表(在内存中)，速度太慢。解决:  在 CPU 内引入专用的高速硬件缓存 (TLB)，存储最近使用的 VPN -> PPN 映射。TLB 命中时，地址转换无需访问内存中的页表，速度极快。大幅抵消了多级页表和多级页表带来的潜在访问延迟，使分页效率极高。固定大小的页是 TLB 高效工作的前提。