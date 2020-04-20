
Fail-Fast Vs Fail-Safe Iterator in Java https://netjs.blogspot.com/2015/05/fail-fast-vs-fail-safe-iterator-in-java.html



# Parallel Computing

并行编程模式
* 共享存储
* 消息传递
* 数据并行

并行层次
* Parallel computer system
* Parallel algorithms
* Parallel programming
* Parallel applications




并行计算机的系统结构模型(PVP、SMP、MPP、DSM和COW）
* 单指令多数据流SIMD(Single Instrunction Multiple Data)
* 并行向量处理器PVP(Parallel Vector Processor)
* 对称多处理器SMP(Symmetric Multiprocessor)
* 大规模并行处理器MPP(Massively Parallel Processor)
* 工作站集群COW(Cluster of Workstations)
* 分布共享存储DSM(Distributed Shared Memory)


可扩展并行机公用结构
* 无共享
* 共享磁盘
* 共享存储（共享内存和共享磁盘）


并行计算机的存储访问模型（ＵＭＡ、ＮＵＭＡ、ＣＯＭＡ、ＣＣ-ＮＵＭＡ 和ＮＯＲＭＡ）以及并行计算机的存储组织（层次存储技术和高速缓存一致性问题）
* 一致内存访问模型UMA(Uniform Memory Access） 
* 非一致存储访问NUMA(Nonumiform Memory Access)


* 计算密集(Compute-Intensive)型应用
* 数据密集(Data-Intensive)型应用
* 网络密集(Network-Intensive)型应用


并行计算模型(Parallel Computational Model)：三要素
* 集群参数(包括CPU性能参数、存储器参数和通信网络参数等）
* 计算行为(同步方式或异步方式）
* 成本函数(其自变量是机器参数）


* First generation Parrell computational models - shared memory (algorithm)
   * 共享存储SIMD同步模型   
   随机存取机器(Parrallel Random Access Machine:PRAM)
   * 共享存储MIMD异步模型    
   异步PRAM模型(Asynchronization PRAM: APRAM)： 分相(Phase)PRAM模式
* Second generation parallel computational models - distributed memoery (communication)
   * 固定连接的SIMB模型（SIMD-IN模型）
   * BSP (Bulk Synchronous Parallel) model：BSP模型将并行机的特性抽象为三个定量参数模型p、g、L，分别处理器数目、选路器吞吐(亦称带宽因子)、全局同步之间时间间隔
   * LogP (Latency, overhead, gap, Processor) model   
BSP=LogP+barriers-overhead
* Third generation parallel computational models - hierarchical memoery ()
   * UMH (Uniform Memory Hierarchy) Model: register, acache, memoery,disk
   * DRAM (Distributed RAM) model: local memoery, remote memory

* Numerical computation method
* Parallel algorithm
* Parallel program
* Parallel software

Classification of Parallel Algorithms
* Numerical parallel alogrithm
* Non-numerical parallel algorithm
* Misellanea: synchronous/asynchronous, parallel/distributed, deterministic/random

Programming Models
* Shared-Memory Programming
* Message-Passing Programming
* Data-Parallel Programming
* Programming Environment and Tools

Design policy of parallel algorithms
* Parallelizing a sequential algorithm
* Designing a new parallel algorithm
* Borrowing other well-known algorithm


Design mehtods of parallel algorithms
* partitioning
    * Breaking up the given problem into several nonoverlapping subproblems of almost equal sizes
    * Solving concurrently the subproblems
* Divide and conquer
    * Dividing the problem into serveral subproblems
    * Solving recursively the subproblems
    * Merging solutions of subproblems into a solution for original problem
* Pipelining
    * Breaking an algorithm into a sequence of segments in which the output of each segment is the input of its successor
    * All segments must produce results at the same rate
    
 * Iterative
    * Each iterative produces an approximation solution, measures the error between the approximation and true solution.
    * Based on the error measurement, improves on approximation solution, constructs a next iterate.
    * Repeats this process until the error is small enough
  
 Implementation principle of parallel algorithms
 * Decomposition
    * Domain decomposition (data decomposition): subdivides the data domain of problem into multiple regions, assigns defferent processors to compute the results of each region
    * Functional decomposition (task decomposition): identifies dependences among the tasks of a problem, assign defferent processor to run independent tasks in parallel.
* Scheduling
    * Definition: to assign task on proper processors and to decide their operating sequence
    * Static Scheduling (Compile time scheduling)
    * Dynamic Scheduling (Run time scheduling)
* Load balance
    * Definition: processors have roughly the same amount of workload, so that no one processor holds up the entire solution.
    * Static load balancing
    * Dynamic load balancing

Performance Evaluation of Parallel Algorithms
* Speedup
    *

计算执行时间
  * 运算操作： Computational Steps
  * 通信操作： Routing Steps

并行计算模型(Parallel Computational Model),三要素
* 机器参数，包括CPU性能参数、存储器参数和通信网络参数等
* 仔细行为，同步方式或者异步方式
* 成本函数，其自变量是机器参数

复杂性度量
* 期望复杂度(Expected Complexity)
* 最坏情况下复杂度(Worst-Case Complexity)



# Concurrency


Atul S. Khot, Concurrent Patterns and Best Practices: Build scalable apps with patterns in multithreading, synchronization, and functional programming, 2018

When things happen at the same time, we say that things are happening concurrently. As far as this book is concerned, whenever parts of an
executable program run at the same time, we are dealing with concurrent programming. We use the term parallel programming as a synonym for concurrent programming.

并发的需求：
* 任务：更小的处理时间，更大的系统吞吐
* 设备：并行处理能力
* 处理的速度的失配
* 设备复用

[The Free Lunch Is Over:A Fundamental Turn Toward Concurrency in Software](http://www.gotw.ca/publications/concurrency-ddj.htm)
 
 Instead of driving clock speeds and straight-line instruction throughput ever higher, they are instead turning en masse to hyperthreading and multicore architectures.
 
 传统的提高CPU处理能力
 * 提高系统时钟
 * 提高指令吞吐：pipelining, branch prediction, executing multiple instructions in the same clock cycle(s),instruction reordering。
 现在的方式
 * 超线程
 * 多核和众核
 
Over the past 30 years, CPU designers have achieved performance gains in three main areas, the first two of which focus on straight-line execution flow:
* clock speed
* execution optimization
* cache
借助于底层硬件的升级，上层应用和软件无须改动，就可以提高性能

动力：
* 半导体和电子技术
* 计算机系统结构
 
# Books

[Allen B. Downey. The Little Book of Semaphores. Second Edition. 2007](http://linuxinsight.com/files/downey05semaphores.pdf)
 

[1]
“synchronization” refers to relationships among events—any number of events, and any kind of relationship (before, during,
after). Computer programmers are often concerned with synchronization constraints, which are requirements pertaining to 
the order of events
* Serialization: Event A must happen before Event B.
* Mutual exclusion: Events A and B must not happen at the same time.

需要同步的原因
* 并发执行：多处理器，即使单处理器也会多线程，从而需要控制线程的同步 
* 资源共享
* 乱序执行：
* cache，数据不一致




# Web

http://www.gotw.ca/publications/index.htm

[Effective Concurrency](https://herbsutter.com/category/effective-concurrency/)

[1 The Pillars of Concurrency](http://www.drdobbs.com/parallel/the-pillars-of-concurrency/200001985)

![fundamental concurrency requirements and techniques](https://github.com/QuChunhe/study/blob/master/pics/the-pillars-of-concurrency-table1.gif)

* Pillar 1: Responsiveness and Isolation Via Asynchronous Agents
* Pillar 2: Throughput and Scalability Via Concurrent Collections
* Pillar 3: Consistency Via Safely Shared Resources

[2 How Much Scalability Do You Have or Need?](http://www.drdobbs.com/parallel/how-much-scalability-do-you-have-or-need/201202924)


|Order  |O(1): Single-Core|O(K): Fixed|O(N): Scalable
| :------------ | :------------ | :------------ | :------------| 
|Tagline |	One thing at a time |	Explicit threading |	Re-enable the free lunch|
|Summary |	Sequential applications, and bottlenecked parallel applications |	Explicitly express how much work can be done in parallel|Express lots of latent concurrency in a way that can be efficiently mapped to N cores|  
|Examples |Multithreaded code convoyed on a global lock or message queue, occasional or intermittent background work|Pipelining, hardwired division of tasks, regular or continuous background computation |Tree traversal, quicksort, compilation|  
|Applicability |	Single-core hardware, single-threaded OS, or nonCPU-bound app |	Hardware with fixed concurrency, or app whose CPU-bound parts have limited scalability |	Hardware with variable (esp. growing) concurrency, and app with CPU-bound parts that are scalably parallelizable|
|Examples |	Code targeting legacy hardware, small embedded systems, single-core game consoles; simple text processor |	Game targeting one multicore game console generation; code whose key operations are order-sensitive (e.g., can be pipelined but not fully parallelized) |	Mainstream desktop or server software with CPU-bound features and targeting commodity hardware or future upgradeable game consoles|

 exploiting natural parallelism
 * Exploit parallelism in algorithm structures: For example, recursive sorting can exploit the natural parallelism in its divide-and-conquer structure. 
 * Exploit parallelism in data structures: For example, tree traversal can often exploit the independence in each node's subtrees. Compilation can exploit independence at several levels in the structure of source code, from coarse-grained independence among source files to finer-grained independence among classes or methods within a file.


[3 Use Critical Sections (Preferably Locks) to Eliminate Races](http://www.drdobbs.com/cpp/use-critical-sections-preferably-locks-t/201804238)

A "critical section" is a region of code that shall execute in isolation with respect to some or all other code in the program, and every kind of synchronization you've ever heard of is a way to express critical sections.


# Concurrency

instruction level parallelism (ILP)

thread level parallelism (TLP)


# Reactive Design Patterns

message-driven

* It must react to its users (responsive). 能响应
* It must react to failure and stay available (resilient).可自愈
* It must react to variable load conditions (elastic).有弹性
* It must react to inputs (message-driven). 消息驱动
