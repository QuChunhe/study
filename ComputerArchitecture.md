
translation lookaside buffer TLB 旁路转换缓冲，或称为页表缓冲

一切都是围绕着PPA（Power、Performace、Area）而行动

CPU：Central Processing Unit

cycles per instruction * seconds per cycle

(PCIe)
Peripheral Component Interconnect Express)

现代CPU的架构和性能优化
* 流水线 Pipelining
* 旁路 Bypassing
* 分支预测 Branch Prediction
* 超标量 Superscalar
* 寄存器重命名 Register Renaming
* 乱序执行 Out-of-Order (OoO) Execution
* 存储器层次 Memory Hierarchy
* 矢量操作 Vector Operations
* 多核处理 Multi-Core


cycles/seconds * instruction/cycle

* CPI (每条指令的时钟数)
* 时钟周期

superScalar
* IPC为N,N路超标量


 
CPU内部的并行性
* 指令级并行 Instruction-Level Parallelism(ILP) 
  * 超标量 superscalar
  * 乱序执行 Out-of-order
* 数据级并行 Data-Level Parallelism (DLP)
  * 矢量计算 Vectors
* 线程级并行 Thread-Level Parallelism (TLP)
   * 同步多线程 Simutaneous Multithreading (SMT)
   * 多核 Multicore


* 问题: 多线程读写同一块数据
* 解决方法: 加锁

* 问题: 谁的数据是正确的？
* 解决方法: 缓存一致性协议 Coherence

* 问题: 什么样的数据是正确的 Consistency
* 解决方法: 存储器同一性模型


“Power Wall + Memory Wall + ILP Wall = Brick Wall”


[45-year CPU evolution: one law and two equations](https://arxiv.org/ftp/arxiv/papers/1803/1803.00254.pdf)

John L. Hennessy, David A. Patterson, A New Golden Age for Computer Architecture, Communications of the ACM, February 2019, Vol. 62 No. 2, Pages 48-6

key insights
* Software advances can inspire architecture innovation.
* Elevating the hardware/software interface creates opportunities for architecture innovation.
* The marketplace ultimately settles architecture debates.

Software talks to hardware through a vocabulary called an instruction set architecture (ISA).


“Power Wall + Memory Wall + ILP Wall = Brick Wall”
* The Power Wall means faster computers get really hot.
* The Memory Wall means 1000 pins on a CPU package is way too many.
* ILP Wall means a deeper instruction pipeline really means digging a deeper power hole. (ILP stands for instruction level parallelism.)



四十年来CPU发展的推动力
* 半导体工艺：更高的频率、更多的晶体管
* 体系结构

摩尔定律
* 集成电路芯片上所集成的电路的数目，每隔18个月就翻一番；
* 微处理器的性能每隔18个月提高一倍，而价格下降一半

摩尔定律说的是半导体工艺的发展，其本质上是在技术可能性的前提下实现商业利益的最大化
* 技术的可能性
* 商业利益的最大化

* 周期间隔太小，厂家收不回成本
* 周期间隔太大，面对更多竞争以及更少的需求，也会造成利润下降

相对固定的周期，有利于上下游厂商的协同
* 为更快的CPU，设计开发操作系统和系统软件
* 根据摩尔周期清理库存，避免压货

[什么是CPU Die](https://zhuanlan.zhihu.com/p/51354994)   

Die或者CPU Die指的是处理器在生产过程中，从晶圆/硅片/硅圆片（Silicon Wafer）上切割下来的一个个小方块，也被称之为裸片，在切割下来之前，每个小方块（Die）都需要经过各种加工，将电路逻辑刻到该Die上面.

对于主流的CPU厂商Intel和AMD而言，他们会将1个或者N个CPU Die封装起来形成一个CPU Package，有时候也叫作CPU Socket.

而对于AMD的EYPC CPU而言，它的每个CPU Socket由4个CPU Die组成，每个CPU Die中包含有4个CPU内核

CPU Die之间通过片外总线（Infinity Fabric）互联，并且不同CPU Die上的CPU内核不能共享CPU缓存，而单个Die的Xeon处理器内和所有CPU内核其实是可以共享CPU的第三级缓存（L3 Cache）的。

CPU Socket(NUMA Node)--> CPU Die --> CPU Core (Physic CPU)--> HyperThread (logic CPU)

* socket <-> node

socket是一个物理上的概念，指的是主板上的cpu插槽。node是一个逻辑上的概念，对应于socket。

* core <-> 物理cpu

core就是一个物理cpu,一个独立的硬件执行单元

* thread <-> 逻辑cpu

socket就是主板上的CPU插槽; Core就是socket里独立的一组程序执行的硬件单元，比如寄存器，计算单元等; Thread：就是超线程hyperthread的概念，逻辑的执行单元，独立的执行上下文，但是共享core内的寄存器和计算单元。

# Memory


[What Every Programmer Should Know About Memory](https://people.freebsd.org/~lstewart/articles/cpumemory.pdf)



[Modern Microprocessors:A 90-Minute Guide!](http://www.lighterra.com/papers/modernmicroprocessors/)

关键技术
* pipelining (superscalar, OOO, VLIW, branch prediction, predication)
* multi-core and simultaneous multi-threading (SMT, hyper-threading)
* SIMD vector instructions (MMX/SSE/AVX, AltiVec, NEON)
* caches and the memory hierarchy

**Pipelining & Instruction-Level Parallelism**
* Fetch
* Decode
* Execute
* Writeback   
Modern processors overlap these stages in a pipeline, like an assembly line. 

**Deeper Pipelines – Superpipelining**

Since the clock speed is limited by (among other things) the length of the longest, slowest stage in the pipeline, the logic gates that make up each stage can be subdivided, especially the longer ones, converting the pipeline into a deeper super-pipeline with a larger number of shorter stages. Then the whole processor can be run at a higher clock speed! Of course, each instruction will now take more cycles to complete (latency), but the processor will still be completing 1 instruction per cycle (throughput), and there will be more cycles per second, so the processor will complete more instructions per second (actual performance).




**Multiple Issue – Superscalar(超标量)**

Since the execute stage of the pipeline is really a bunch of different functional units, each doing its own task, it seems tempting to try to execute multiple instructions in parallel, each in its own functional unit. To do this, the fetch and decode/dispatch stages must be enhanced so they can decode multiple instructions in parallel and send them out to the "execution resources".

The number of instructions able to be issued, executed or completed per cycle is called a processor's width.

**Explicit Parallelism – VLIW(very long instruction word)**


**Instruction Dependencies & Latencies**


**Branches & Branch Prediction**

**Eliminating Branches with Predication**

**Instruction Scheduling, Register Renaming & OOO(out-of-order execution)**

The instructions in the program must be reordered so that while one instruction is waiting, other instructions can execute. Not surprisingly, this is called out-of-order execution, or just OOO for short (sometimes written OoO or OOE).


Another approach to the whole problem is to have the compiler optimize the code by rearranging the instructions. This is called static, or compile-time, instruction scheduling. The rearranged instruction stream can then be fed to a processor with simpler in-order multiple-issue logic, relying on the compiler to "spoon feed" the processor with the best instruction stream. 

A question that must be asked is whether the costly out-of-order logic is really warranted, or whether compilers can do the task of instruction scheduling well enough without it. This is historically called the brainiac vs speed-demon debate. 

**The Power Wall & The ILP Wall**

功耗和散热问题(power and heat issures)限制了时钟频率。And while power increases linearly with clock frequency, it increases as the square of voltage, making for a kind of "triple whammy" at very high clock speeds (f*V*V).

It gets even worse, because in addition to the normal switching power, there is also a small amount of leakage power, since even when a transistor is off, the current flowing through it isn't completely reduced to zero. And just like the good, useful current, this leakage current also goes up as the voltage is increased. If that wasn't bad enough, leakage generally goes up as the temperature increases as well, due to the increased movement of the hotter, more energetic electrons within the silicon.


The power and heat problems become unmanageable, because it's simply not possible to provide that much power and cooling to a silicon chip in any practical fashion, even if the circuits could, in fact, operate at higher clock speeds. This is called the power wall.

Pursuing more and more ILP also has definite limits, because unfortunately, normal programs just don't have a lot of fine-grained parallelism in them, due to a combination of load latencies, cache misses, branches and dependencies between instructions. This limit of available instruction-level parallelism is called the ILP wall.
* 通常的程序没有很多细粒度的并行性
* 读取（内存）的时延。CPU和内存的速度失配。
* ache未命中
* 指令的分支和依赖


**Threads – SMT(Simultaneous multi-threading), Hyper-Threading & Multi-Core**

Simultaneous multi-threading (SMT) is a processor design technique which exploits exactly this type of thread-level parallelism.

在Intel　CPU中被成为超线程(hyper-threading)

**More Cores or Wider Cores?**

 One key problem is that the complex multiple-issue dispatch logic scales up as roughly the square of the issue width, because all n candidate instructions need to be compared against every other candidate.8-issue more than 4 times larger than 4-issue (for only 2 times the width).In addition, a very wide superscalar design requires highly multi-ported register files and caches, to service all those simultaneous accesses. Both of these factors conspire to not only increase size, but also to massively increase the amount of longer-distance wiring at the circuit-design level, placing serious limits on the clock speed. 


**Data Parallelism – SIMD Vector Instructions**

In addition to instruction-level parallelism and thread-level parallelism, there is yet another source of parallelism in many programs – data parallelism. Rather than looking for ways to execute groups of instructions in parallel, the idea is to look for ways to make one instruction apply to a group of data values in parallel.

This is sometimes called SIMD parallelism (single instruction, multiple data). More often, it's called vector processing. Supercomputers used to use vector processing a lot, with very long vectors, because the types of scientific programs which are run on supercomputers are quite amenable to vector processing.

[Gallery of Processor Cache Effects](http://igoro.com/archive/gallery-of-processor-cache-effects/)
## Memory Barriers

[LINUX KERNEL MEMORY BARRIERS](https://www.mjmwired.net/kernel/Documentation/memory-barriers.txt)

weakly ordered CPU 

There are some minimal guarantees that may be expected of a CPU:
* On any given CPU, dependent memory accesses will be issued in order, with respect to itself. 
* Overlapping loads and stores within a particular CPU will appear to be ordered within that CPU.

# Intel
The processor uses three interdependent mechanisms for carrying out locked atomic operations:
* Guaranteed atomic operations
* Bus locking, using the LOCK# signal and the LOCK instruction prefix
* Cache coherency protocols that ensure that atomic operations can be carried out
on cached data structures (cache lock)


These mechanisms are interdependent in the following ways. Certain basic memory transactions (such as reading or writing a byte in system memory) are always guaranteed to be handled atomically. That is, once started, the processor guarantees that the operation will be completed before another processor or bus agent is allowed access to the memory location. The processor also supports bus locking for performing selected memory operations (such as a read-modify-write operation in a shared area of memory) that typically need to be handled atomically, but are not automatically handled this way. Because frequently used memory locations are often cached in a processor’s L1 or L2 caches, atomic operations can often be carried out inside a processor’s caches without asserting the bus lock. Here the processor’s cache coherency protocols ensure that other processors that are caching the same memory locations are managed properly while atomic operations are performed on cached memory locations.

处理器使用三种相互依赖额机制执行锁定的原子操作
* 确保的原子操作
* 总线锁定，即使用LOCK＃线号和LOCK前缀
* cache一致性协议，其确保原子操作能够在缓存的数据结构上被执行（chache锁）




<<Intel 64 and IA-32 Architectures Software Developer’s Manual Volume 3 (3A, 3B & 3C): System Programming Guide>> Chater 8 Mutiple-Processor Managment


[Intel® 64 Architecture Memory Ordering White Paper](http://www.cs.cmu.edu/~410-f10/doc/Intel_Reordering_318147.pdf)


LOCK is not an instruction itself: it is an instruction prefix, which applies to the following instruction. That instruction must be something that does a read-modify-write on memory (INC, XCHG, CMPXCHG etc.) --- in this case it is the incl (%ecx) instruction which increments the long word at the address held in the ecx register.

The LOCK prefix ensures that the CPU has exclusive ownership of the appropriate cache line for the duration of the operation, and provides certain additional ordering guarantees. This may be achieved by asserting a bus lock, but the CPU will avoid this where possible. If the bus is locked then it is only for the duration of the locked instruction.

Causes the processor’s LOCK# signal to be asserted during execution of the accompanying instruction (turns the instruction into an atomic instruction). In a multiprocessor environment, the LOCK# signal ensures that the processor has exclusive use of any shared memory while the signal is asserted.

[Intel® 64 and IA-32 ArchitecturesSoftware Developer’s Manual](https://software.intel.com/sites/default/files/managed/39/c5/325462-sdm-vol-1-2abcd-3abcd.pdf)

[x86 and amd64 instruction reference](https://www.felixcloutier.com/x86/index.html)

alignment：对于alignment为A的任意类型的变量，他的地址必须是A的倍数．字节对齐主要是为了提高内存的访问效率
起始地址对齐，CPU从内存中获取数据时起始地址必须是地址总线宽度的倍数

内存对齐的3大规则:
1. 对于结构体的各个成员，第一个成员的偏移量是0，排列在后面的成员其当前偏移量必须是当前成员类型的整数倍
2. 结构体内所有数据成员各自内存对齐后，结构体本身还要进行一次内存对齐，保证整个结构体占用内存大小是结构体内最大数据成员的最小整数倍
3. 如程序中有#pragma pack(n)预编译指令，则所有成员对齐以n字节为准(即偏移量是n的整数倍)，不再考虑当前类型以及最大结构体内类型



Memory Barriers: a Hardware View for Software Hackers

# Cache

[CPU cache](https://en.wikipedia.org/wiki/CPU_cache)

Most modern desktop and server CPUs have at least three independent caches: an **instruction cache** to speed up executable *instruction fetch, a **data cache** to speed up data fetch and store, and a **translation lookaside buffer (TLB)** used to speed up virtual-to-physical address translation for both executable instructions and data. A single TLB can be provided for access to both instructions and data, or a separate Instruction TLB (ITLB) and data TLB (DTLB) can be provided.[2] The data cache is usually organized as a hierarchy of more cache levels (L1, L2, etc.; see also multi-level caches below). However, the TLB cache is part of the memory management unit (MMU) and not directly related to the CPU caches. 


Data is transferred between memory and cache in blocks of fixed size, called **cache lines** or cache blocks. When a cache line is copied from memory into the cache, a cache entry is created. The cache entry will include the copied data as well as the requested memory location (called a tag).

If the processor finds that the memory location is in the cache, a cache hit has occurred. However, if the processor does not find the memory location in the cache, a cache miss has occurred. In the case of a cache hit, the processor immediately reads or writes the data in the cache line. For a cache miss, the cache allocates a new entry and copies data from main memory, then the request is fulfilled from the contents of the cache. 

* Replacement policies.  One popular replacement policy, **least-recently used (LRU)**, replaces the least recently accessed entry.
* Write policies. In a **write-through** cache, every write to the cache causes a write to main memory. Alternatively, in a **write-back or copy-back cache**, writes are not immediately mirrored to the main memory, and the cache instead tracks which locations have been written over, marking them as dirty. The data in these locations is written back to the main memory only when that data is evicted from the cache.


Cached data from the main memory may be changed by other entities (e.g., peripherals using direct memory access (DMA) or another core in a multi-core processor), in which case the copy in the cache may become out-of-date or stale. Alternatively, when a CPU in a multiprocessor system updates data in the cache, copies of data in caches associated with other CPUs become stale. Communication protocols between the cache managers that keep the data consistent are known as **cache coherence protocols**. 

**CPU stalls**.
The time taken to fetch one cache line from memory (read latency due to a cache miss) matters because the CPU will run out of things to do while waiting for the cache line. When a CPU reaches this state, it is called a stall.

If the placement policy is free to choose any entry in the cache to hold the copy, the cache is called fully associative. At the other extreme, if each entry in main memory can go in just one place in the cache, the cache is direct mapped. Many caches implement a compromise in which each entry in main memory can go to any one of N places in the cache, and are described as N-way set associative.

* 全关联(fully-associative)
* 直接映射(direct map)
* 组关联(set associative):

the main differences between dynamic RAM (DRAM) and static RAM (SRAM).
|Feature          |Dynamic RAM (DRAM) | Static RAM (SRAM) |
|:--------------- |:------------------|:------------------|
|Storage circuit存储电路 | Capacitor电容器       |Flip-flop |
|Transfer speed传送速率  |Slower than CPU慢于CPU |Same as CPU与CPU一样快|
|Latency 时延            |High高                |Low低         |
|Density密度             |High高                | Low低|
|Power Consumption能耗   |Low低                 |High高     |
|Cost价格                |Cheap便宜             |Expensive昂贵|

#ARM

[ARM Manul](http://infocenter.arm.com/help/index.jsp?topic=/com.arm.doc.ddi0198e/Cacghbij.html)


# Books

