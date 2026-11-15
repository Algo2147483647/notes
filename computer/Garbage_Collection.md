# Garbage Collection

[TOC]

unreachable objects

## Problem

Garbage collection (GC) is an automatic memory management mechanism that helps developers manage memory more efficiently by reclaiming memory that is no longer in use. 

## Resolution

### Marking Garbage

首先从根对象（如全局变量、调用栈中的变量等）开始，递归地标记所有可以访问到的对象，这些被标记的对象是正在使用的对象。

- Initial mark: This is a short pause phase. The garbage collector stops the world (all goroutines are paused) to mark the root objects. Root objects include global variables, local variables on the stack of running goroutines, etc.
- Concurrent mark: After the initial mark, the garbage collector runs concurrently with the application code. It traverses all reachable objects from the root objects and marks them. During this process, the application can continue to create and modify objects.
- Final mark: Another short pause phase. The garbage collector stops the world again to handle the objects that may have been missed during the concurrent mark phase due to concurrent updates.

- Reference Counting: 为每个对象维护一个引用计数器，用于记录该对象被引用的次数。当一个对象被创建时，它的引用计数器被初始化为 1。每当有一个新的引用指向该对象时，引用计数器加 1；当一个引用不再指向该对象时，引用计数器减 1。当对象的引用计数器为 0 时，说明该对象不再被任何其他对象引用，就可以将其视为垃圾对象，回收其占用的内存空间。

#### Reachability analysis

#### Stop The World



#### Tri-color marking algorithm

Three color marking algorithm 将对象按照处理前后分为三种状态, 灰色对象构成对象图中标记和未标记中间的边界线

- Unmarked (White): Initially all objects are unmarked. If at the end of the marking phase, an object remains white, it means that there are no references to it from any reachable objects, and it can be safely reclaimed.
- Ing (Gray): The object have been discovered during the marking process, but their outgoing references have not yet been fully explored.
- Marked (Black): The objects are those that have been fully explored. All of their outgoing references have been followed, and all the objects they refer to have been marked.


$$
\text{object}_{markrd} \to \text{object}_{ing} \to \text{object}_{unmarked}
$$

Process

- $W \to G$: 
- $G \to W$: 
- $B \to G$: 
- $G \to B$: 
- $W \to B$: 
- $B \to W$: 


如果出现一下情景, 算法将出现对象丢失的问题, 产生的原因源于对象图的动态性. 当且仅当一下两个操作都发生的时候, 造成黑色和白色对象直接近邻而导致问题的出现. 避免这类问题的关键是让一条或者全部的操作不会出现.

- 当 ing -> unmarked 的边被释放
- 当 marked -> unmarked 的边被建立.

$$
\text{object}_{markrd} \to \text{object}_{unmarked}
$$

![Tri-color marking algorithm](./assets/Tri-color marking algorithm.svg)

#### Write Barrier

##### Dijkstra's Write Barrier (Snapshot-at-the-Beginning)

Dijkstra's write barrier is a conservative approach. It ensures that all objects that were reachable at the start of the garbage collection cycle remain marked as reachable. When a reference is updated, if the new target object is white, the write barrier marks it gray. This way, the garbage collector will later explore this object and its outgoing references.

##### Yuasa's Write Barrier (Incremental Update)

Yuasa's write barrier focuses on updating the marking information when a reference is removed. When an object's reference is changed, the old target object (if it is black) is marked gray again. This is because the removal of a reference might make some of the objects that were previously considered fully explored (black) now have potentially unreachable descendants that need to be re - examined.

### Sweeping Garbage

- Directly Sweep: 遍历整个内存空间，清除所有未被标记的对象，这些未标记的对象就是垃圾对象，它们所占用的内存空间将被释放。
- Copying: 将内存空间划分为两个相等的区域，例如 A 区和 B 区。在分配对象时，总是在 A 区分配。当 A 区快满时，进行垃圾回收。此时，将 A 区中所有存活的对象复制到 B 区，然后将 A 区整个清空，释放 A 区的所有内存空间。接下来，下一轮分配就会在 B 区进行，当 B 区快满时，又将 B 区的存活对象复制到 A 区，如此循环。
- Compact: 将所有存活的对象向内存的一端移动，使存活对象紧密排列，然后直接清除内存另一端的垃圾对象，这样就避免了内存碎片的产生。

### Optimization Methods

Generational Collection: 基于对象的存活时间不同，将内存中的对象分为不同的代，通常分为新生代和老年代。新生代中的对象通常存活时间较短，老年代中的对象存活时间较长。在垃圾回收时，对新生代和老年代采用不同的回收算法和策略。例如，对新生代可以采用复制算法，因为新生代中垃圾对象通常较多，复制算法可以快速回收垃圾对象；对老年代可以采用标记 - 压缩算法，因为老年代中存活对象较多，标记 - 压缩算法可以避免内存碎片。
