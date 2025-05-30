
硬件组织
* cluster
* ...
* Processing Element (UE)：例如ALU

软件
* Task
* Unit of Execution: 例如Thread

阻塞/非阻塞
* 阻塞：调用者caller，停止运行，放弃cpu
* 非阻塞：调用者caller继续执行

同步/异步
* 同步：调用者caller来处理调用结果
* 异步：非调用者处理返回的结果


Concurrency vs Parallelism


顾名思义，并发就是同时发生，并行就是同时执行。因此，并发指的是同时开始执行这个事件，也就是说后续的执行是串行，还是并行，不确定，依赖于底层的硬件条件和操作系统的调度，而并行指的是同时执行这个过程。

multiprogramming　--> multithread (Concurrency) --> multiprocessor (parallelism).

传统单核和单CPU时代的并发
* 分时复用CPU
* 线程交织执行   

微观上交替执行，宏观上并发执行。现在已经是多CPU(SMP)和多核时代，主流的商用服务器装备多个CPU，每个CPU拥有多个内核。从软件角度，并发和并行没有本质的区别。

并发和并行都需要挖掘问题或者任务的并行性。三个维度挖掘并行性
* 数据(data)，需要处理很多的输入数据或者中间结果。
* 功能(function)，需要更加复杂的计算
* 请求(request), 更多的服务请求

在当前，并发和并行区别
1）硬件不同：并行需要底层硬件支撑，需要更多的处理单元（包括CPU和GPU）和专门的通信硬件
2）软件不同：并行需要更加复杂的并行化软件支持和专门的并行算法
3）问题不同：并行往往针对更大规模的数据或/和更复杂的计算，必须依赖于强大的计算能力，并发往往针对更大规模的数据或者更多数量的请求。
4) 目标不同，并行往往以减小处理时间为目标，而并发可能以增加系统吞吐、减小处理时延和实现资源复用为目标。

无法充分利用多个CPU和多个内核的原因
* 硬件资源的竞争，包括Cache，内存带宽(memory bandwidth)和I/O等。硬件资源竞争使得线程无法继续运行，比如内存墙问题限制了多核和多CPU的并发运行能力，采取：
   * 放弃指令级并行：中断CPU流水线
   * 忙等待(busy waiting)：继续霸占CPU，执行检查操作，直到满足条件，执行后续操作。
   * 放弃CPU运行：置于阻塞或者等待状态，放弃CPU使用。为此，需要进行上线文切换，引入额外的性能开销。何时恢复可运行状态，存在两个机制：1）主动轮询；2）被动拥有锁（原来拥有锁的线程释放锁）或者收到信号（其他线程发送信号）。
* 软件问题
   * 问题/任务固有的串行化，即没有办法并发处理。核心问题是依赖性问题，其各个子子问题／子任务相互依赖，包括数据依赖和功能依赖
   * 没有充分挖掘问题/任务所蕴含的并行性
   * 分割的子问题/子任务的粒度不均匀，使得并发执行的线程处理时间相差太大
   * 线程间的任务协调和数据通信占用太多的时间
   * CPU的负载不均匀
 


充分利用计算资源，通过多线程提高代码的性能
* 吞吐量
* 处理时间，加速比


 
 [The Memory Wall Is Ending Multicore Scaling](https://www.electronicdesign.com/technologies/analog/article/21794572/the-memory-wall-is-ending-multicore-scaling)
 
 
线程协调的主要机制
* 共享内存
   * atomic operations，例如CAS指令
   * lock，依赖于底层指令支持
   * 线程安全的数据结构，其往往依赖于lock。
   * lock-free data structures/Algorithms,其依赖于底层的原子操作指令 
* 消息传递
   




Thread Pool 线程池的好处
* 复用线程，通过线程复用，避免重复创建和消耗线程，从而大大减小创建/消耗线程的代价。
* 避免过载，通过设置线程池中最大可用线程数，避免过渡使用线程资源，而拖垮系统性能
实现线程池需要考虑的几个问题
* 线程的生命周期管理，包括何时创建和何时线程；
* 任务队列，主要难点：1）线程安全的数据结构；2）高效的支持多线程的插入和读取
* 策略：1）任务队列为空时，线程如何操作，是等待，还是销毁；2）如果任务队列已满，如何处理任务




busy waiting is a technique in which a process repeatedly checks to see if a condition is true, such as whether keyboard input or a lock is available


[Fail-Fast Vs Fail-Safe Iterator in Java](https://netjs.blogspot.com/2015/05/fail-fast-vs-fail-safe-iterator-in-java.html)

fail-fast 机制是Java集合(Collection)中的一种错误机制。 在用迭代器遍历一个集合对象时，如果遍历过程中对集合对象的结构进行了修改（增加、删除），则会抛出Concurrent Modification Exception（并发修改异常）。

Fail-Safe iterators favor lack of failures over the inconvenience of exception handling.

Those iterators create a clone of the actual Collection and iterate over it. If any modification happens after the iterator is created, the copy still remains untouched. Hence, these Iterators continue looping over the Collection even if it’s modified.

However, it’s important to remember that there’s no such thing as a truly Fail-Safe iterator. The correct term is Weakly Consistent.

That means, if a Collection is modified while being iterated over, what the Iterator sees is weakly guaranteed. This behavior may be different for different Collections and is documented in Javadocs of each such Collection.



Let It Crash principles

[The Let It Crash Philosophy Outside Erlang](http://stratus3d.com/blog/2020/01/20/applying-the-let-it-crash-philosophy-outside-erlang/)


Future, Callback, Promise, Coroutine

并发设计的层次
* patterns 
* paradigms
* Architecture
* Style


# Actor & CSP
Akka/Erlang的actor模型与Go语言的协程Goroutine与通道Channel代表的CSP(Communicating Sequential Processes)

[The actor model in 10 minutes](https://www.brianstorti.com/the-actor-model/)

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


并行计算机的存储访问模型（UMA, NUMA, COMA, CC_NUMA和NORMA）以及并行计算机的存储组织（层次存储技术和高速缓存一致性问题）
* 一致内存访问模型UMA(Uniform Memory Access） 
* 非一致存储访问NUMA(Nonumiform Memory Access)

应用类型
* 计算密集(Compute-Intensive)型应用
* 数据密集(Data-Intensive)型应用
* 网络密集(Network-Intensive)型应用


并行计算模型(Parallel Computational Model)：三要素
* 集群参数(包括CPU性能参数、存储器参数和通信网络参数等）
* 计算行为(同步方式或异步方式）
* 成本函数(其自变量是机器参数）

并行计算模型的演进
* First generation Parallel computational models - shared memory (algorithm)
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

并行的层次
* Numerical computation method
* Parallel algorithm
* Parallel program
* Parallel software

Classification of Parallel Algorithms
* Numerical parallel alogrithm,数值计算，包括矩阵运算、多项式求值、解线性方程组等
* Non-numerical parallel algorithm，非数值计算，例如排序、查找、搜索和匹配等
* Misellanea: synchronous/asynchronous, parallel/distributed, deterministic/random


* 同步算法(Synchronized Algorithm)
* 异步算法(Asynchronized Algorithm)


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
 
 partitioning在开始的时候将数据划分为更小的数据规模，然后处理．分而治之采用递归，持续地将大问题分解为小问题
 
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
    * Static load balancing: to divide the task and communications evently before the execution of the algorithm.
    * Dynamic load balancing: if the task size is unknown until run time, we have to use dynamic load balancing.


分解到各个线程：以数据为中心的的数据域分解和以功能为中心的功能性分解

调度：1）将线程映射到处理器，优先级；2）平衡负载

Performance Evaluation of Parallel Algorithms
* Speedup
    * Amdahl's Law: the computational workload is fixed as the number of processors increases, the computational time decreased. Amdahl said, if f is fraction of a sequential calculation, then the maximum speedup is 1/f. It is a negative argument against massively parallel processing.
    * Gustafson's Law: the execution time is fixed, as the number of processors increases, correspondingly computational workload increases. Gustafson said, the speedup is the linear function of the number of processors.
* Efficiency
    * Definition: it is defined as the ratio of speed up to the number of processors which is between zero and one.
    * Meaning: it describes the fraction of the time that is usefully employed by the processors.
* Scalability
    * Definition:  the algorithm is thought to be scalable if larger parallel system can solve proportionally larger problem in the same running time as smaller problem on smaller parallel system. In fact, the scalability of parallel algorithm is a measure of its capacity to increase speed up in proportion to the number of processors.
    * Metrics: iso-efficiency, iso-speed and average latency are three popular scalability metrics of parallel algorithms.  


Paralle Programming Models
* shared variable model
  * Originality: it is the native model for shared memory machines.
  * Characters: in this model, tasks share a common address space (implicit data distribution), tasks exchange data through reading/writing the shared variables (impplict communication), tasks access to shared variable controlled by locks/semaphores etc. (explicit synchronization).
  * Comments: it is easy to develop programs, but the portability of programs is problematic.
* message passing model
  * Originality: it is the native model for distribute memory machines
  * Characters: In this model, tasks reside in different address space (explicit data allocation), tasks exchange data through sending/receiving message (explicit communication), task asynchronously operate need to use barrier/event etc. (explicit synchronization).
  * Comments: the portablity of programs is enhanced, but it is rather difficult to develop the programs.
* Data parallel model
  * Originality: this programming model originates from vector programming.
  * Characters: in this model, each task performs similar operations on different data. Data parallel programming emphasis local computation and data routing to minimize interaction overheads.
  * Implementation: data parallel model can be implemented in both shared address space (shared memory machines) and multiple address space (distributed memory machines). The former can easy programming, the latter may offer a bettery locality.
* Unified programming model
  * High abstraction level: suitable for various distributed and shared memory paralle architectures; hiding implementation details of message passing or synchronization; supporting height abstraction level parallel algorithm design and description.
  * Height productivity: support fast and intuitive mapping from parallel algorithm to parallel programs; support high-performance implementation of paralleled programs; highly readable parallel programs.
  * High extensibility: can be customized or extended conveniently; can accommodate the needs of various application areas.  

Parallel Programming Languages and Parallelization Methodologies
* Auto-parallelization compilers
   * Fully automatic: the compiler analyzes the source code and identifies opportunities for parallelism. Loops (do, for) statements are the most frequenct target for automatic parallelization.
   * Programmer directed: using compiler directives or possibly compiler flags, the programmer explicity tells the compiler how to parallelize the code and distribute the data.
   * Comments: researchesrs finally found out that the automatic parallelization is not always effective.
* Library extension of sequential Programming language
   * Callable parallel programming library: in a sequential programming languages, a callable parallel programming library is embedded, such that the users can easily realize parallel programming.
   * MPI is a message passing library standard. It is now the "de facto" industry standard.MPICH and LAM/MPI are two popular and freely available MPI packages.
   * OpenMP is an Application Program Interface (API) that my be used to explicitly direct multi-threaded, shared memory parallelism. It consist of thress primary API components: compiler directives, runtime library routines, enviroment variables.   



|  前缀 | 缩写 | 基幂 | 含意    | 数值  |
|:-----|-----:|:----:|--------:|-----:|
| Kilo | K    | 10^3 | Thousand | 千  |
| Mega | M    | 10^6 | Million  | 百万，兆  |
| Giga | G    | 10^9 | Billion  | 十亿，千兆  |
| Tera | T    | 10^12 | Trillion | 万亿  |
| Peta | K    | 10^15 | Quadrillion | 千万亿  |
| Exa| E    | 10^18 | Quitillion | 百亿亿  |


并行计算的应用需求
* 计算密集型（Computing-insensive）
* 数据密集型（Data-intensive）
* 通信密集型（Network-intensive）


系统互联


网络性能指标
* 节点度（Node Degree）
* 网络之间（Network Diameter）
* 对剖宽带（Bisection Width）：对分网络各半所必须移去的最少边数
* 对剖带宽（Bisection Bandwidth）：每秒钟内，在最小的对剖平面上通过所有连线的最大信息为（或字节）书。
* 如果从任意节点观看网络都一样，则称网络为对称的 （Symmetry）

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


并行算法描述

par-do, do in parallel
```
 for i=1 to n par-do
 
 end for
```

https://www.cs.rice.edu/~vs3/comp422/lecture-notes/comp422-lec20-s08-v1.pdf

并行计算模型
* Provides a way to think about computers. Influences design of:
  * Architectures
  * Languages
  * Algorithms
* Provides a way of estimating how well a program will perform.Cost in model should be roughly same as cost of executing program



1. The Random Access Machine Model
  * Memory is a sequence of words, each  capable of containing an integer.
  * Each memory access takes one unit of time


PRAM [Parallel Random Access Machine] 
* EREW - exclusive read, exclusive write
A program isn’t allowed to have two processors access the same memory location at the same time.
* CREW - concurrent read, exclusive write
* CRCW - concurrent read, concurrent write 
Needs protocol for arbitrating write conflicts
* CROW – concurrent read, owner write
Each memory location has an official “owner”


Parallel Memory Hierarchy (PMH) model

BSP (Bulk Synchronous Parallel) Model
* BSP programs composed of supersteps.
* In each superstep, processors execute up to L computational steps using locally stored data, and also can send and receive messages 
* Processors synchronize at end of superstep (at which time all messages have been received)

LogP Model


[Is Parallel Programming Hard, And, If So, What Can You Do About It?](https://mirrors.edge.kernel.org/pub/linux/kernel/people/paulmck/perfbook/perfbook.html)




[Designing Parallel Algorithms: Part 1](https://www.drdobbs.com/parallel/designing-parallel-algorithms-part-1/223100878)


[Parallel Programming: Beyond the Critical Section](https://www.slideshare.net/Tony.Albrecht/parallel-programming-beyond-the-critical-section-presentation?qid=beb3d4ff-d8bb-44b8-bd00-c72ce37dd580&v=&b=&from_search=1)

The problems of Parallel Programming
* Race conditions
* deadlocks
* Read/Write tearing
* Priority Inversion
* ABA Problem
* Thread scheduling problems
  * convoy: Multiple threads restricted by a bottleneck
  * stampede: 
  
 
Higher level Locking primitime
* SpinLock
* Mutex
* Barrier
* RWlock
* Semaphore

Problem decomposition
* organise by tasks
  * linear: Task Parallelism
  * Recursive: Divide and Conquer
* organise by data decomposition
  * linear: geometric decomposition
  * recursive: Recursive data
* organise by data flow
  * linear: pipeline
  * recursive: event-based coordination
  
Program Structures
* Program Structrues
  * SPMD: Single Progam, Multiple data
  * Master/Worker. Task are highly variable. Program Structure does't map onto loops. Master sets up tasks and waits for completion. Workers grab task from queue, execute and then grap the next one.
  * Loop Parallelism. Split iterations of the loop out to threads. Be careful of memory use and process granularity.
  * Fork/Join
* Data Structures
  * Shared Data
  * Distributed Array. break array into thread specific parts. Be aware of cache line overlap, Keep data distribution coarse.
  * Shared Queue. Fundamental part of Master/Worker.



Flynn矩阵
* SISD
* SIMD
* MISD
* MIMD

概念
* Task 任务
* Parallel Task 并行任务
* Serial Execution 串行执行
* Parallel Execution 并行执行
* Shared Memory 共享存储
* Distributed Memory 分布式存储 
* Communication 通信
* Synchronization 同步
* Granulariy 粒度
* Observed Speedup 加速比
* Parallel Overhead 并行开销
* Scalability 可扩展性

通信指的是在并行任务之间的数据交互

同步指的是并行任务之间的等待

并行编程模型
* 共享存储模型 Shared Memory Model: OpenMP
* 线程模型 Threads Model
* 消息传递模型 Message Passing Model:MPI
* 数据并行模型 Data Parallel Model


设计并行处理
* 自动和手工并行
* 理解问题和程序
* 分块分割:数据分块,任务分割
* 通信
* 同步
* 数据依赖
* 负载均衡
* 粒度
* I/O
* 成本
* 性能分析和优化

# Concurrency

CAS(Compare-and-Swap),Mamory Barriers, Cache Line, False Sharing, Cache line padding





并发模型
* Lock-base Concurrency
* Actor-based Concurrency
* Transactional Memory

[The Free Lunch Is Over:A Fundamental Turn Toward Concurrency in Software](http://www.gotw.ca/publications/concurrency-ddj.htm)
 
 Instead of driving clock speeds and straight-line instruction throughput ever higher, they are instead turning en masse to hyperthreading and multicore architectures.
 
 传统的提高CPU处理能力
 * 提高系统时钟
 * 提高指令吞吐：pipelining, branch prediction, executing multiple instructions in the same clock cycle(s),instruction reordering。
 现在的方式
 * 超线程:一个内核同时运行多个线程，从而实现一个物理内核实现多个逻辑内核的效果
 * 多核和众核
 
Over the past 30 years, CPU designers have achieved performance gains in three main areas, the first two of which focus on straight-line execution flow:
* clock speed
* execution optimization
* cache
借助于底层硬件的升级，上层应用和软件无须改动，就可以提高性能

动力：
* 半导体和电子技术
* 计算机系统结构

It has become harder and harder to exploit higher clock speeds due to not just one but several physical issues, notably heat (too much of it and too hard to dissipate), power consumption (too high), and current leakage problems.
 
The performance gains are going to be accomplished in fundamentally different ways for at least the next couple of processor generations. And most current applications will no longer benefit from the free ride without significant redesign.
 
The near-term future performance growth drivers are:
* hyperthreading
* multicore
* cache 
 
Applications will increasingly need to be concurrent if they want to fully exploit continuing exponential CPU throughput gains

Efficiency and performance optimization will get more, not less, importan


 
# Books

[Programming on Parallel Machines](http://heather.cs.ucdavis.edu/matloff/public_html/158/PLN/ParProcBook.pdf)

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

Venkat Subramaniam, Programming Concurrency on the JVM : Mastering Synchronization, STM, and Actors

We’re interested in concurrency for two reasons: to make an application responsive/improve the user experience and to make it faster.
* Making Apps More Responsive
* Making Apps Faster

任务或者问题极少能够被划分为能够完全相互独立运行的部分。经常性的，我们能够执行独立的操作，但是却不得合并部分结果，以获得最总的结果。这就需要线程通信部分结果，有时需要等等这些结果准备好。

* 数据交换：交换需要处理的数据和已经处理的结果
* 任务协同：需要等待前一步的处理完成以及触发下一步的处理

并发程序的三个问题
* starvation(饥饿).Starvation occurs when a thread waits for an event that may take a very long time or forever to happen. 比如调用异常，一直无法返回。针对这种情况，一般需要添加timeout。
* deadlock(死锁).Two or more threads are waiting on each other for some action or resource.需要线程主动放弃资源。
* race conditions(条件竞争).If two threads compete to use the same resource or data, we have a race condition.Two forces can lead to race conditions—the Just-in-Time (JIT) compiler optimization and the Java Memory Model.

Visibility: Understand the Memory Barrier。

[Is Parallel Programming Hard, And, If So, What Can You Do About It?](https://mirrors.edge.kernel.org/pub/linux/kernel/people/paulmck/perfbook/perfbook.html)



[Designing and Building Parallel Programs](https://www.mcs.anl.gov/~itf/dbpp/text/book.html)

# Web

http://www.gotw.ca/publications/index.htm

[Effective Concurrency](https://herbsutter.com/category/effective-concurrency/)

[1 The Pillars of Concurrency](http://www.drdobbs.com/parallel/the-pillars-of-concurrency/200001985)

![fundamental concurrency requirements and techniques](https://github.com/QuChunhe/study/blob/master/pics/the-pillars-of-concurrency-table1.gif)

* Pillar 1: Responsiveness and Isolation Via Asynchronous Agents。通过异步代理，提高响应性和隔离性。换言之，能够快速响应服务请求，避免或减小服务的相互干扰或者阻塞。互扰在本质上是来因为任务之间的相互等待，即一个任务即使独立于其他其他任务，也需要被迫处于阻塞状态，以等待其他任务处理结束，才能运行。互扰来自于两个方面：1）硬件资源的复用，包括计算资源、存储资源和内存资源等；2）软件串行处理。软件串行处理意味着如果有多个任务，那么仅仅有一个任务在运行，而其他任务则必须等待。在复用的资源没有达到门限的前提下，采用多线程并发处理任务，可以减小任务的等待时间，避免相互干扰。独立的任务之间通过异步消息相互通信。

Finally, how should the independent tasks communicate? A key is to have the communication itself be asynchronous, preferably using asynchronous messages where possible because messages are nearly always preferable to sharing objects in memory (which is Pillar 3's territory). In the case of a GUI thread, this is an easy fit because GUIs already use message-based event-driven models.
 
* Pillar 2: Throughput and Scalability Via Concurrent Collections。通过并发聚集(Collection)，提高吞吐能力和可扩展性。使得众多内核处于繁忙状态，以更快的计算出结果。我们特别期望目标操作在聚集（collection）上执行，在数据和算法结构上挖掘并行性。

* Pillar 3: Consistency Via Safely Shared Resources。通过安全的共享资源，实现一致性。

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

通过开发固有的并发性，寻找可扩展的并发机会
* 开发算法结构的并发性
* 开发数据结构的并发性

[3 Use Critical Sections (Preferably Locks) to Eliminate Races](http://www.drdobbs.com/cpp/use-critical-sections-preferably-locks-t/201804238)

A "critical section" is a region of code that shall execute in isolation with respect to some or all other code in the program, and every kind of synchronization you've ever heard of is a way to express critical sections.

# Caching

[Intro to Caching,Caching algorithms and caching frameworks part 1](https://javalandscape.blogspot.com/2009/01/cachingcaching-algorithms-and-caching.html)
[Intro to Caching,Caching algorithms and caching frameworks part 2](https://javalandscape.blogspot.com/2009/01/intro-to-cachingcaching-algorithms-and.html)
[Intro to Caching,Caching algorithms and caching frameworks part 3](https://javalandscape.blogspot.com/2009/02/intro-to-cachingcaching-algorithms-and.html)
[Intro to Caching,Caching algorithms and caching frameworks part 4](https://javalandscape.blogspot.com/2009/03/intro-to-cachingcaching-algorithms-and.html)
[Intro to Caching,Caching algorithms and caching frameworks part 5](https://javalandscape.blogspot.com/2009/05/intro-to-cachingcaching-algorithms-and.html)

为什么要使用缓存
* 暂时性地保存临时数据
* 保持数据的一个副本，使得应用能够以更快的速度访问数据。

# Concurrency

instruction level parallelism (ILP)

thread level parallelism (TLP)


[Real-world Concurrency](https://queue.acm.org/detail.cfm?id=1454462)

[queue.acm concurrency](https://queue.acm.org/listing.cfm?item_topic=Concurrency&qc_type=theme_list&filter=Concurrency&page_title=Concurrency&order=desc)

## CPU Cache

cache位于CPU和主存之间，用于适配CPU和内存之间的速度差距。从上个世纪80年代开始，主存与CPU之间的速度差距持续增大，例如从1986年到2000年，CPU速度以每年55%的速度提高，而内存速度每年仅仅提高了10%。长期累积下来，内存像墙一样阻止了CPU性能的发挥，因此也被称之为内存墙(Memory wall)。为此，cache的大小和级数也在不断增加。目前主流的CPU一般有三级cache，三级cache和主存的访问速度如下表所示
。
|         |CPU周期   |1级cache(L1 cache)|2级cache(L2 cache)|3级cache(L3 cache)| 主存(Main Memory)|
|:------- |:---------|:----------------|:-----------------|:----------------|:------------------|
|绝对时间  | 0.3ns    | 0.9ns           |  3ns             | 10ns            | 100ns             |
|相对时间  |1个CPU周期 | 3个CPU周期       |  10个CPU周期      | 33个CPU周期      | 333个CPU周期       |

与主存相比，cache之所以具有更快的访问速度，是因为如下两个根本性原因
* cache采用静态随机存储器（SRAM），而主存采用动态随机存储器（DRAM）。静态随机存储器虽然存取速度更快，但是其电路更加复杂、能耗更高、价格更贵、晶体管密度更低。
* cache位于CPU内部，具有更短的传输距离。L1、L2和L3三级cache随着与内核距离的逐渐增加，访问时延逐渐增大。
显然，上述两个原因也使得受限于CPU芯片的大小和成本，cache容量不能随意增加。

近十几年来随着多核/众核的发展，内存墙问题还变得越来越严重。内核的流水线经常需要停顿下来，以等待从内存获取数据。这使得对多核处理器性能提升形成的严重阻碍和制约

优化使用cache，能够充分发挥多核CPU的潜力，幅度提升CPU的处理性能

可以通过分别通过lscpu或者cat /proc/cpuinfo命令查看CPU和cache的信息，通过lstopo查看cpu和cache的拓扑连接关系。


dmidecode -t cache

L1 cache一般会细分位数据cache（L1d cache）和指令cache（L1i cache）。

读取（内存）的时延。CPU和内存的速度失配。内存的存取速度严重滞后

在内存和不同的cache中存在多个副本或者拷贝，需要实现数据的寻址和影射，并确保数据的一致性，不仅仅大大增加了硬件的复杂度，而且给软件的开发和编写带来了条件。一方面，需要充分利用CPU cache提高CPU的处理性能，另一方面要避免由于cache而引起问题。
三个问题
* cache友好性Cache-Friendl
* 伪共享 False Sharing
* 可见性
Cache-Friendly Code & False Sharing 缓存友好的代码和缓存的伪共享


在cache中的数据被划分为不同块，每一个块被称为一个缓存行（cache line），一个cache line通常为64或128字节的宽度。cache line是从内存读取或写入到内存的最小单元。在内存中相互邻近的数据通常被一个特定的线程在相近的时间访问，这在大多数程序中都是正确的。然而，这种局部性是虚假分享问题的根源。

Modern processors use the MESI protocol to implement cache coherence. This basically means each cache line can be in one of four states:
* **M**odified
* **E**xclusive
* **S**hared
* **I**nvalid

When a core modifies any data in a cache line, it transitions to "Modified", and any other caches that hold a copy of the same cache line are forced to "Invalid". The other cores must then read the data from main memory next time they need it. 

embarrassingly parallel（(also called pleasingly parallel or perfectly parallel) ），完美并行，这个术语字面难以理解，意指任务之间没有依赖或者依赖很少，可以完美并行。尽管这意味着你可能会对代码能如此简单的并行而感到尴尬，但这是好事。

设想一下，两个不同的变量被两个运行在不同内核上的线程使用。不同线程使用相互独立的数据，这显然是一个完美并行。但是，如果两个变量位于同一个cache line中并且至少有一个便利被更改，那么就会出现cache line的竞争。这就是伪共享。之所以被称为伪共享，是因为虽然不同的线程没有共享数据，但是它们无意中共享了一个cache line。


* Padding 填充
* spacing 间距

cache友好代码的两个例子
* 矩阵的处理
   * 按照行
   * 按照列
* Hash
   * 数组+指针
   * 数组

引用的局部性
如果存在如下情况，就可能造成伪共享
* 在一个数据结构中具有多个元素存储在相邻的位置
* 多线程以方法方式访问（读和写）不同的元素

```
perf stat ./yourapp
```


内存屏障(Memory Barrier)

Memory Model由Instruction Reordering和Store Atomicity来定义。总是就是每种模型对于乱序的定义不太一样。

memory fence instruction

[Memory Barriers: a Hardware View for Software Hackers](http://www.rdrop.com/users/paulmck/scalability/paper/whymb.2010.07.23a.pdf)

[membarrier(2) — Linux manual page](https://man7.org/linux/man-pages/man2/membarrier.2.html)

[The design of memory barrier in Linux kernel (I)](https://developpaper.com/the-design-of-memory-barrier-in-linux-kernel-i/)

[ Memory barriers in C](https://mariadb.org/wp-content/uploads/2017/11/2017-11-Memory-barriers.pdf)

[Concurrency Hazards: False Sharing](https://www.codeproject.com/articles/51553/concurrency-hazards-false-sharing)




# Reactive Design Patterns

message-driven

* It must react to its users (responsive). 能响应
* It must react to failure and stay available (resilient).可自愈
* It must react to variable load conditions (elastic).有弹性
* It must react to inputs (message-driven). 消息驱动

# Lock

[Mutual Exclusion: Classical Algorithms for Locks](https://www.cs.rice.edu/~vs3/comp422/lecture-notes/comp422-lec19-s08-v1.pdf)

[Modern High-Performance Locking](https://neerc.ifmo.ru/sptcc/slides/slides-shavit.pdf)

[Effective Synchronization on Linux/NUMA Systems](http://www.lameter.com/gelato2005.pdf)



[Lecture Locking](https://www.ics.uci.edu/~aburtsev/cs5460/lectures/lecture11-locking/lecture11-locking.pdf)

* Lock ordering: Locks need to be acquired in the same order
* Locks and interrupts: Never hold a lock with interrupts enabled

Problems with locks
* Deadlock: Locks break modularity of interfaces, easy to get wrong

Priority inversion
* Low-priority task holds a lock required by a higher priority task
* Priority inheritance can be a solution, but can also result in errors (see What really happened on Mars)
* Convoying
   1. Several tasks need the locks in roughly the same order
   2. One slow task acquires the lock first
   3. Everyone slows to the speed of this slow task
* Signal safety: Similar to interrupts, but for user processes
* Kill safety: What if a task is killed or crashed while holding a lock? 
* Preemption safety: What happens if a task is preempted while holding a lock

[The Trouble With Locks](http://gotw.ca/publications/mill36.htm)

A lock convoy occurs when multiple threads of equal priority contend repeatedly for the same lock. http://t.cn/RG0RQDH     Lock Convoys Explained  http://t.cn/zW4t7eS

使用锁引起性能的下降主要是如下两个原因：1)并发/并行多个进程中，只有成功获得锁的进程能够继续执行，而其他进程则进入阻塞队列等待被唤醒，在极端条件下并发/并行程序会退化为串行执行；2)进程从运行状态到阻塞状态或者从阻塞状态被唤醒，OS需要切换上下文执行环境，代价高昂。

无锁操作使得进程不会被阻塞，从而免去了进程切换导致的性能消耗，但是：1)并发/并行进程在竞争互斥资源时或者采用spin方式，或者polling方式，不可避免地引入进程空转；2)很多情况下还无法替换锁，虽然恨它，却无法离开它。

尽量避免使用锁。检索操作（put方法）无需加锁，并不阻塞索引线程，而更新操作（put和remove方法）则要加锁。如果检索线程和更新线程相互重叠，则检索操作返回最近修改的结果，但不会受到更新操作的影响。对于put方法，或者更新值，或者在链表末尾增加节点。上述两种情况，都不会引起put方法异常

* Lock-based programming
* Lock-free programming

Unforeseen races (i.e., program corruption), deadlocks (i.e., program lockup), and performance cliffs (e.g., priority inversion, convoying, and sometimes complete loss of parallelism and/or worse performance than a single-threaded program)

it works (avoids data corruption) and doesn’t hang (avoids deadlock and livelock). 


乐观并发控制/乐观锁基于出现写竞争的情况是一个小概率事件，即使出现写竞争，操作者也可通过检查状态发现并容忍操作失败时回滚操作。操作步骤：1）Begin；2）Modify；3）Validate；4）Commit/Rollback。『Optimistic concurrency control - Wikipedia, the free encyclopedia』http://t.cn/R5j2lUV




Problems with Locks
* Conceptual
  * coarse-grained: poor scalability 降低并发度
  * fine-grained: hard to write 增加锁开销
* Semantic 
  * deadlock
  * riority inversion
* Performance 
  * convoying
  * intolerance of page faults and preemption

[Linux中常见同步机制设计原理](http://www.wowotech.net/kernel_synchronization/445.html)


[Linux同步机制 - 基本概念(死锁,活锁,饿死,优先级反转,护航现象)](https://cloud.tencent.com/developer/article/1021123)

* 死锁（deadlock）是指两个或两个以上的进程在执行过程中，因争夺资源而造成的一种互相等待的现象，若无外力作用，它们都将无法推进下去。此时称系统处于死锁状态或系统产生了死锁，这些永远在互相等待的进程称为死锁进程。虽然进程在运行过程中，可能发生死锁，但死锁的发生也必须具备一定的条件，死锁的发生必须具备以下四个必要条件。
  * 互斥条件。
  * 请求和保持条件
  * 不剥夺条件
  * 环路等待条件
* 活锁（livelock）：指事物1可以使用资源，但它让其他事物先使用资源；事物2可以使用资源，但它也让其他事物先使用资源，于是两者一直谦让，都无法使用资源。
* 饥饿（hungry）:所谓饥饿，是指如果事务T1封锁了数据R，事务T2又请求封锁R，于是T2等待。T3也请求封锁R，当T1释放了R上的封锁后，系统首先批准了T3的请求，T2仍然等待。然后T4又请求封锁R，当T3释放了R上的封锁之后，系统又批准了T4的请求......T2可能永远等待，这就是饥饿。
* 优先级反转（Priority inversion）.优先级反转是指一个低优先级的任务持有一个被高优先级任务所需要的共享资源。高优先任务由于因资源缺乏而处于受阻状态，一直等到低优先级任务释放资源为止。解决方案：
  * 设置优先级上限。
  * 优先级继承。
* 锁伴随（Lock Convoys） 
 
 
Priority Inversion is a problem while Priority Inheritance is a solution. Literally, Priority Inversion means that priority of tasks get inverted and Priority Inheritance means that priority of tasks get inherited
 
 优先级反转(Priority Inversion) 
 *  优先级继承(priority inheritance) 
 *  优先级天花板(priority ceilings)
 
 
 
几个问题

Starvation and Fairness
　
 饥饿(Starvation)问题
 
 公平(Fairness)问题
 
 Deadlock, Starvation, and Livelock
 
 [Unreliable Guide To Locking](https://www.kernel.org/doc/htmldocs/kernel-locking/index.html)
 
 Race Conditions and Critical Regions
 
 竞争条件和临界区
 
 This overlap, where the result depends on the relative timing of multiple tasks, is called a race condition. The piece of code containing the concurrency issue is called a critical region.
 
 强占
 
Preemption can have the same effect, even if there is only one CPU: by preempting one task during the critical region, we have exactly the same race condition. In this case the thread which preempts might run the critical region itself. 
 
Two Main Types of Kernel Locks: Spinlocks and Mutexes
 
RCU（read copy update）
[The RCU API, 2010 Edition](https://lwn.net/Articles/418853/)

[What is RCU, Fundamentally?](https://lwn.net/Articles/262464/)


[volatile vs. volatile](https://www.drdobbs.com/parallel/volatile-vs-volatile/212701484)


[Intel Guide for Developing Multithreaded Applications ](https://software.intel.com/content/www/us/en/develop/articles/intel-guide-for-developing-multithreaded-applications.html)



## 网络编程


两个模型
* 线程池模型，逻辑简单，实现简单；一个线程在一个时间点仅仅服务一个请求
* 事件驱动模型，并发度高，能够支持更多的服务请求；逻辑复杂，实现复杂

* 海量的TCP连接
* 保证公平性对用户体验非常重要

问题1： select()/epoll()返回的socket fd从小到大排序，导致socket fd小的TCP连接总是优先得到服务，而socket fd大的总是最后得到服务

问题2：通常socket的触发模式为水平触发(level triggered),当socket有数据达到时，必须把所有的数据一次性接收完毕

解决办法：
* epoll使用edge triggered模式
* 将待处理的socket放入FIFO队列中
* 

## 杂项

[Real-world Concurrency](https://queue.acm.org/detail.cfm?id=1454462)

Concurrent execution can improve performance in three fundamental ways: it can reduce latency (that is, make a unit of work execute faster); it can hide latency (that is, allow the system to continue doing work during a long-latency operation); or it can increase throughput (that is, make the system able to perform more work).
* 减小服务时延，能够更快的得到服务的响应或者输出
* 提高系统吞吐，能够处理更多的输入，例如更多的服务请求以及更大的数据规模等
* 降低系统负载，充分利用系统硬件资源，能够在相同的硬件条件下服务更多的服务请求和输入数据


Using concurrency to reduce latency is highly problem-specific in that it requires a parallel algorithm for
the task at hand.In short, the degree to which one can use concurrency to reduce latency depends much more on the problem than on those endeavoring to solve it—and many important problems are simply not amenable to it.

减小服务时延依赖于问题或者任务本身:挖掘问题/任务的并行性，将问题/任务分解为子问题/子任务，并通过并行处理这些子问题/子任务，以减小处理时间
* 并发处理过程中需要引入额外的开销，因此只有问题规模足够大时，并发处理所减小的时延才能补偿所带来的额外开销
* 问题或者任务固有的顺序性，使得难以并行化。

For long-running operations that cannot be parallelized, concurrent execution can instead be used to perform
useful work while the operation is pending; in this model,the latency of the operation is not reduced, but it is hidden by the progression of the system.

以时分复用方式占用资源，
* 充分利用资源
* 避免资源空闲   

当不需要硬件资源时，则放弃对于硬件资源的独占，使得其他应用以分时复用的方式共享该硬件资源。

Further, concurrent execution is not the　only way to hide system-induced latencies: one can often
achieve the same effect by employing nonblocking operations (e.g., asynchronous I/O) and an event loop (e.g.,
the poll()/select() calls found in Unix) in an otherwise　sequential program. Programmers who wish to hide
latency should therefore consider concurrent execution as　an option, not as a foregone conclusion.


Instead of using parallel logic to make a single operation faster, one can employ multiple concurrent executions of sequential logic to　accommodate more simultaneous work. Importantly, a system using concurrency to increase throughput need
not consist exclusively (or even largely) of multithreaded code. Rather, those components of the system that
share no state can be left entirely sequential, with the system executing multiple instances of these components concurrently.

it is concurrency by architecture instead of by implementation.

**Know your cold paths from your hot paths.** it is to know which paths through your code you want to be able to execute in
parallel (the hot paths) versus which paths can execute sequentially without affecting performance (the cold paths).

In cold paths, keep the locking as coarse-grained as possible. Don’t hesitate to have one lock that covers a wide range of rare activity in your subsystem. Conversely, in hot paths—those that must execute concurrently to deliver highest throughput—you must be much more careful: locking strategies must be simple and fine-grained, and you must be careful to avoid activity that
can become a bottleneck.

热点路径
* 执行耗时过长的功能或模块
* 经常调用执行的功能或模块

功能(模块)的平均执行次数＊功能(模块)的平均运行时间/总的平均运行时间＝功能(模块)的运行时间占比

热点路径是指运行时间占比高的那些模块或功能。二八定律，即经常被执行的功能/模块不多，大部分功能/模块很少被执行。优化时间占比大的功能或者模块，效果会更加明显，实现更优的产出／投入比更高。

冷僻路径
* 执行耗时不长
* 执行次数不多


**Intuition is frequently wrong—be data intensive.** Today, dynamic instrumentation continues to provide　us with the data we need not only to find those parts of the system that are inhibiting scalability, but also to gather sufficient data to understand which techniques will be best suited for reducing that contention.

在优化之前需要通过性能分析工具，收集足够的数据，用于标示出哪些子系统或者模块是热的路径，哪些子系统缺乏并行性或者需要可伸缩性。

设计和开发阶段：人工分析和估计热点路径

系统上线之后需要性能采样和诊断工具(Profiling Tool)
* Linux perf, Java async-profiler
* 火焰图（flame graph）

**Know when—and when not—to break up a lock.**

Global locks can naturally become scalability inhibitors, and when gathered data indicates a single hot lock, it
is reasonable to want to break up the lock into per-CPU locks, a hash table of locks, per-structure locks, etc.

Breaking up a lock is not the only way to reduce contention, and contention can be (and often is) more easily reduced by
decreasing the hold time of the lock. This can be done by algorithmic improvements (many scalability improvements have been achieved by reducing execution under the lock from quadratic time to linear time!) or by finding　activity that is needlessly protected by the lock.


全局锁天然地成为可伸缩性的障碍物。将全局锁分解为更细粒度的锁。

* 减小临界区(Critical Section)的执行时间或者范围，比如将无需锁保护的数据或者功能，移出临界区。
* 减小锁的粒度，即将锁分解为若干小锁，从而实现更好的并发性。可以从两个纬度进行分解
   * 功能维度，将一个大的临界区的功能分割为多个相互独立的小临界区，并采用不同锁进行保护
   * 数据维度，采用具有并发能力的数据结构，比如ConcurrentHashMap采用了"分段锁"策略，以支持多线程并发操作。
  
  
  
**Be wary of readers/writer locks.**

If there is a novice error when trying to break up a lock, it is this: seeing that a data structure is frequently accessed for reads and infrequently accessed for writes, one may be tempted to replace a mutex guarding the structure with a readers/writer lock to allow for concurrent readers.

对于满足如下两种情况的
* 操作读多写少
* 数据数量较少
可以采用如下两个方式提高数据读操作的并发性
* Readers/Writer Locks　读写锁
* Copy-On-Write　复制读

**Consider per-CPU locking.**

Per-CPU locking (that is,acquiring a lock based on the current CPU identifier) can be a convenient technique for diffracting contention, as a per-CPU lock is not likely to be contended (a CPU can run only one thread at a time).

Two notes on this technique: first, it should be employed only when the data indicates that it’s necessary, as it clearly introduces substantial complexity into the implementation; second, be sure to have a single order for acquiring all locks in the cold path: if one case acquires the per-CPU locks from lowest to highest and another acquires them from highest to lowest, deadlock will (naturally) result.


per-cpu variables are widely used in Linux kernel such as per-cpu counters, per-cpu cache. The advantages of per-cpu variables are obvious: for a per-cpu data, we do not need locks to synchronize with other cpus. Without locks, we can gain more performance. There are two kinds of type of per-cpu variables: static and dynamic. 

**Know when to broadcast—and when to signal.**

A broadcast will awaken all waiting threads, it should generally be used to indicate state change rather than resource availability. If a condition broadcast is used when a condition signal would have been more appropriate, the result will be a
thundering herd: all waiting threads will wake up, fight over the lock protecting the condition variable, and (assuming that the first thread to acquire the lock also consumes the available resource) sleep once again when they discover that the resource has been consumed. This needless scheduling and locking activity can have a serious effect on performance.


* signal --> resource availability
* broadcast --> state change

不正确的使用广播方式会造成lock convoys(锁陪绑)问题,即大量被同一个锁阻塞的线程，频繁地被唤醒和被阻塞，引起大量不必要的CPU调度和上下文切换，导致性能问题。


**Learn to debug postmortem.**

排查死锁问题需要打印各个线程的快照，即每个线程的调用栈，根据调用关系确定哪些线程和哪些锁出现死锁，并进一步确定死锁条件。

This information is contained in a snapshot of state so essential to software develop ment that its very name reflects its origins at the dawn of computing: it is a core dump.

Debugging from a core dump—postmortem debugging—is an essential skill




**Design your systems to be composable.**

There are two ways to make lock-based systems completely composable, and each has its own place. First (and
most obviously), one can make locking entirely internal to the subsystem.

Second (and perhaps counterintuitively), one can achieve concurrency and composability by having no locks whatsoever.

尽量把锁隐藏到子系统内部，比如Java采用内置锁时采用内部对象作为锁。

**Don’t use a semaphore where a mutex would suffice.**

Unlike a semaphore, a mutex has a notion of ownership—the lock is either owned or not, and if it is
owned, it has a known owner. By contrast, a semaphore (and its kin, the condition variable) has no notion of ownership.


First, there is no way of propagating the blocking thread’s scheduling priority to the thread that is in the critical section. This ability to propagate scheduling priority—priority inheritance—is critical in a realtime system, and in the absence of other
protocols, semaphore-based systems will always be vulnerable to priority inversions. A second problem with the lack of ownership is that it deprives the system of the ability to make assertions about itself. For example, when ownership is tracked, the machinery that implements thread blocking can detect pathologies such as deadlocks and recursive lock acquisitions, inducing fatal failure (and that all-important core dump) upon detection. Finally, the lack of ownership makes debugging much more
onerous.

获得锁的所有者，能够带来很多灵活性
* 所有者关系能够转递调度优先级，实现优先级继承，这在实时系统中非常关键
* 缺少所有者关系剥夺了系统诊断自己的能力
* 缺少所有者关系使得调试更加复杂


**Consider memory retiring to implement per-chain hash-table locks.**


**Be aware of false sharing.**注意伪共享


False sharing is a common problem in shared memory parallel processing. It occurs when two or more cores hold a copy of the same memory cache line.
伪共享是在共享内存并行处理中的一个常见问题。当两个或者更多内核持有同一个内存cache line的副本时，就会发生伪共享。

If one core writes, the cache line holding the memory line is invalidated on other cores. Even though another core may not be using that data (reading or writing), it may be using another element of data on the same cache line. The second core will need to reload the line before it can access its own data again. 
如果一个内核写入数据，那么在其他内核中持有该内存线的cache line将会失效。即使另一个内核可能不会使用这个数据（读取或者写入），而是可能使用在同一个cache line上的另一个数据元素。其他内核还是需要在访问其自己的数据之前，重新向这个cache line加载数据。

The cache hardware ensures data coherency, but at a potentially high performance cost if false sharing is frequent. A good technique to identify false sharing problems is to catch unexpected sharp increases in last-level cache misses using hardware counters or other performance tools.
缓存硬件确保了数据的一致性，但如果频繁地发生伪共享，还是会付出很高的性能代价。识别伪共享问题的一个好方法是使用硬件计数器或其他性能工具捕捉在最后一级缓存中意外急剧增加的缓存未命中。

**Consider using nonblocking synchronization routines to monitor contention.**

**When reacquiring locks, consider using generation counts to detect state change.**

```java
    /**
     * The number of times this HashMap has been structurally modified
     * Structural modifications are those that change the number of mappings in
     * the HashMap or otherwise modify its internal structure (e.g.,
     * rehash).  This field is used to make iterators on Collection-views of
     * the HashMap fail-fast.  (See ConcurrentModificationException).
     */
    transient int modCount;

```

**Use wait- and lock-free structures only if you absolutely must.**

in normal contexts, wait- and lock-free data structures are to be avoided as their failure
modes are brutal (livelock is much nastier to debug than deadlock), their effect on complexity and the mainte-
nance burden is significant, and their benefit in terms of performance is usually nil.


[Concepts in Multicore Computing](https://www.cse.wustl.edu/~angelee/archive/cse539/spr15/)

[Algorithms for Scalable Synchronization on Shared-Memory Multiprocessors](https://www.cs.rice.edu/~johnmc/scalable_synch/tocs91.pdff)

同步方式可以划分为两类
* 阻塞方式(blocking construncts)：线程释放资源，等待被重新调度。
* 忙等待方式(busy-wait constructs)：线程持有资源，并且重复测试共享的变量，以确定其十分可以继续执行

如果重新调度的时间消耗超过所期望的等待时间，则选择阻塞方式

两种最常用的忙等待方式是
* spin lock. spin lock提供一种实现排他执行的方式，即确保在一个时间仅仅有一个处理器能够访问特定的共享数据结构
* barriers.　屏障提供了一种方式，以确保在计算过程中，直到所有线程都执行到特定的点之前，没有线程可以超过这个点执行。


[Managing Lock Contention: Large and Small Critical Sections](https://software.intel.com/content/www/us/en/develop/articles/managing-lock-contention-large-and-small-critical-sections.html)

在多线程应用中，锁用于同步进入临界区。临界区是一段访问共享资源的代码。当一个线程位于临界区内时，其他线程不能进入。因此，临界区被顺序执行。

当多线程试图访问共享资源时，临界区能够确保数据的完整性。但是以顺序执行临界区的代码为代价。线程应该在临界区内消耗尽可能少额时间，以减小其他线程等待获取锁的时间。锁竞争。尽可能地减小临界区的执行时间。最好保持较小额临界区。每个临界区都需要获取或者释放锁，因此使用多个较小的、相互分开的临界区会引入额外开销。
```
Begin Thread Function ()

    Initialize ()	

    BEGIN CRITICAL SECTION 1

    UpdateSharedData1 ()

    END CRITICAL SECTION 1
    
    DoFunc1 ()	

    BEGIN CRITICAL SECTION 2

    UpdateSharedData2 ()

    END CRITICAL SECTION 2	

    DoFunc2 ()

End Thread Function ()
```
如果临界区被一个名为doFunc1的调用分隔，如果doFunc1仅仅消耗非常少的时间，那么就不能忽略锁引入的同步开销。在这种情况下，一个更好的方案是合并这两个小临界区成为一个较大的临界区。

如果doFunc1消耗的时间远高于合并临界区锁锁减小的耗时，那么合并临界区就不是一个可行方案。随着临界区的增大，增加了锁竞争的可能性，增加了线程等待额时间。

如果线程在功能UpdateSharedData2花费大量大量的时间，使用包含UpdateSharedData1和UpdateSharedData2的单一临界区将不在是一个好的解决方案，因为锁竞争额可能性非常高。

使用不同的锁保护不同的共享变量。为一个数据结构中的不同元素分别创建独立的锁，或者创建一个锁用于保护访问整个数据结构。依赖于更新元素的代价，大粒度或小粒度的极端情况并不是一个可行的方案，最佳的锁粒度往往是在中间。例如给定一个共享的数组，采用一对锁：一个用于保护偶数元素，另一个用于保护奇数元素。

对于功能UpdateSharedData2需要耗费大量的时间才能完成的情况,可以分解此功能的工作并采用新的临界区可能是一个更好的选择，以减小锁竞争

平衡临界区的大小以减小获取和释放锁的开销。考虑合并小临界区以分摊锁的开销。将具有严重锁竞争的大临界区分割为小临界区。将锁关联到特定共享数据，以减小锁竞争。最佳的方案位于针对共享的每个数据元素使用不同的锁与针对所有共享数据使用一个锁这两个方案之间。

获取锁和释放锁需要引入额外的代价，这个代价主要是因为增加lock指令，或在普通的操作上增加锁总线。

总的线程数为n，临界区的评价执行时间为t，那么总的等待时间可达n*t_cache+n*(t_lock)+n*(n-1)*t/2。由于需要锁住总线，使得内存访问传行化，增加了线程之间和应用之间的互扰。显然，随着线程数的增加，执行时间会增加。
+
[Bus Lock](https://software.intel.com/en-us/forums/intel-performance-bottleneck-analyzer/topic/308523)

[Intel® 64 and IA-32 Architectures Developer's Manual: Vol. 3A](https://www.intel.com/content/www/us/en/architecture-and-technology/64-ia-32-architectures-software-developer-vol-3a-part-1-manual.html)

The Intel-64 memory ordering model guarantees that, for each of the following 
memory-access instructions, the constituent memory operation appears to execute 
as a single memory access:

* Instructions that read or write a single byte.
* Instructions that read or write a word (2 bytes) whose address is aligned on a 2
byte boundary.
* Instructions that read or write a doubleword (4 bytes) whose address is aligned
on a 4 byte boundary.
* Instructions that read or write a quadword (8 bytes) whose address is aligned on
an 8 byte boundary.

Any locked instruction (either the XCHG instruction or another read-modify-write
 instruction with a LOCK prefix) appears to execute as an indivisible and 
uninterruptible sequence of load(s) followed by store(s) regardless of alignment.

[LOCK — Assert LOCK# Signal Prefix](https://www.felixcloutier.com/x86/lock)

Intel提供了Lock前缀，可以应用在如下指令之前ADD, ADC, AND, BTC, BTR, BTS, CMPXCHG, CMPXCH8B, CMPXCHG16B, DEC, INC, NEG, NOT, OR, SBB, SUB, XOR, XADD, and XCHG。处理器会使用LOCK＃信号，在关键的内存操作期间自动生效，锁定系统总线。一旦信号生效，其他处理器或者总线代理的总线控制请求将会被阻塞。

总线锁具有诶出高的性能损失，需要尽可能地避免锁住内存访问，以提高内存访问的并发性。

从P6处理器家族开始，如果使用了LOCK指令前缀的指令要访问的目的地址的内容已经缓存在了cache中，那么LOCK#信号一般就不会被设置，但是当前处理器的cache会被锁定，然后缓存一致性（cache coherency ）机制会自动确保操作的原子性。

[MFENCE — Memory Fence](https://www.felixcloutier.com/x86/mfence)

https://www.cnblogs.com/-9-8/p/4654294.html

[读写一气呵成 - Linux中的原子操作](https://zhuanlan.zhihu.com/p/89299392)

[Atomic explosion: evolution of relaxed concurrency primitives — Will Deacon](https://kernel-recipes.org/en/2018/live-blog-day-2-1/)

https://kernel-recipes.org/en/2018/talks/atomic-explosion-evolution-and-use-of-relaxed-concurrency-primitives/

https://web.mit.edu/6.005/www/fa15/classes/23-locks/


[Operating Systems: Three Easy Pieces](http://pages.cs.wisc.edu/~remzi/OSTEP/)

[Classical Problems of Synchronization](https://www.studytonight.com/operating-system/classical-synchronization-problems)

[Syllabus for CS 598, Concurrent Programming](http://bluehawk.monmouth.edu/~rclayton/web-pages/u03-598/syl.html#part2)

Lock Scaling Analysis on Intel® Xeon® Processors

[Mutex vs Semaphore](https://www.geeksforgeeks.org/mutex-vs-semaphore/)

Modeling Critical Sections in Amdahl’s Law and its Implications for Multicore Design

book Semaphores, Locks, and Conditional Critical Regions

[Solving 11 Likely Problems In Your Multithreaded Code](https://docs.microsoft.com/en-us/archive/msdn-magazine/2008/october/concurrency-hazards-solving-problems-in-your-multithreaded-code)

* Incorrect Granularity. Even if access to shared state occurs with proper synchronization, the resulting behavior may still be incorrect. The granularity must be sufficiently large that the operations that must be seen as atomic are encapsulated within the region. There is a tension between correctness and making the region smaller, because smaller regions reduce the time that other threads will have to wait to concurrently enter.

* Read and Write Tearing. Tearing occurs because reading or writing such locations actually involves multiple physical memory operations. Concurrent updates can happen in between these, potentially causing the resultant value to be some blend of the before and after values.

* Lock-Free Reordering.

* Lock Convoys

* Two-Step Dance

* Priority Inversion

[Parallel Computing](https://docs.microsoft.com/en-us/previous-versions/bb964701(v=msdn.10)?redirectedfrom=MSDN)

[Quantitative System Performance: Computer System Analysis Using Queueing Network Models](https://homes.cs.washington.edu/~lazowska/qsp/)


two parameters:
* workload intensity
* service demand

performance measure: 
* utilization: the proportion of time the server is busy
* residence time: the average time spande at the service center by a customer, both queuing and receiving service
* queue length: the average number of customers at the service center, both waiting and receiving service
* throughput

http://www.johngustafson.net/pubs/pub13/amdahl.htm


[Scalability, basics, application to systems, teams and processes](https://www.slideshare.net/AvishaiIshShalom/resilient-design-101?qid=b7d32533-3be1-45fb-bdf5-c5461d6c9362&v=&b=&from_search=16)

[Resilient Design 101 (JeeConf 2017)](https://www.slideshare.net/AvishaiIshShalom/resilient-design-101?qid=b7d32533-3be1-45fb-bdf5-c5461d6c9362&v=&b=&from_search=16)

[Resilient design 101 (BuildStuff LT 2017)](https://www.slideshare.net/AvishaiIshShalom/resilient-design-101-82223160)

# Concurrency Patterns 并发模式

[Category Concurrency Patterns](http://wiki.c2.com/?CategoryConcurrencyPatterns)


# Asynchrony

[Async fun ](https://www.slideshare.net/TomaszKogut/async-fun?qid=13cbb241-6304-44be-a0a0-ed9e05782a3d&v=&b=&from_search=65)
* express computation that will run outside the main flow
* handle errors if they occur during processing
* tell our computation how to return the result to us
* use type-safte constructs.

# Performance

https://www.infoq.com/performance/

https://www.infoq.com/apm/

https://www.infoq.com/performance-scalability/

https://www.infoq.com/performance_tuning/

https://www.infoq.com/performance_evaluation/

[Understanding CPU Microarchitecture to Increase Performance](https://www.slideshare.net/InfoQ/understanding-cpu-microarchitecture-to-increase-performance)

memory and cache, cache line, memory prefetching (CPU), false sharing, Branch Prediction, linux perf

[Applied Performance Theory](https://www.slideshare.net/InfoQ/applied-performance-theory?qid=b7d32533-3be1-45fb-bdf5-c5461d6c9362&v=&b=&from_search=12) 
 
 performance 
 * 在不降低响应世界的情况下，系统还能支持多少额外负载
 * 系统的使用瓶颈是什么
 * 当改变响应时间和最大吞吐时会产生什么影响
 
 Capacity
 * 为了支持10倍的负载，需要添加多少服务器
 * 系统是否过渡供给
 
 性能评估的方法
 * 负载模拟
 * 性能建模
 
 性能评估指标
 * 最大系统吞吐，即系统的容量
 * 平均响应时间，
 
 在满足给定的响应时间目标的情况下，此台服务器的最大吞吐量

queueing delay + service time = response time 

等待时间 + 服务时间 = 响应时间

utilization = arrival rate * service time

利用率 = 到达速率 * 服务时间

Pollaczek-Khinchine (P-K) formula

meaning queuing dela = U/(1-U）* linear fn(mean service time) * quadratic fn(service time variability)

meaning queuing delay time 正比于 U/(1-U）


How can we improve the mean response time>
* respone time 正比于 queuing delay, prevent requests from queuing to long
  * Controlled delay。key insight: queues are typically empty allows short bursts, prevents standing queues
  * Adaptive or always LIFO. helps when system is overloaded,makes no difference when it’s not. newest requests ﬁrst, not old requests that are likely to expire.  
  * set a max queue length
  * client-side concurrency control
* decrease sevice time by optimizing application code
* decrease request/service size variability for example, by bathing requests.

两类系统
* open system:
* close system：throughput depends on response time
   * 请求是同步的
   * 同时服务的客户端数目是固定的
 
 系统吞吐不是随着资源增加而线性增长的，即不是线性可扩展的
 * 竞争代价(contention penalty), 共享资源所固有的串行性，比如数据库竞争和锁竞争,αN
 * 串扰影响(crosstalk penalty),βN^2
 
 Universal Scalability law: throughput of N thread = N/(αN+βN^2+C)
 
 How can we improve the system scales: avoid contention (serialization) and crosstalk (synchronization)
 
 [Quantifying Scalability with the USL](https://www.xaprb.com/slides/dataengconf-2018-quantifying-scalability-universal-scalability-law/1)
 
 Gunther, N.  Guerrilla Capacity Planning. Springer, Berlin Heidelberg 2007.



Thread Saftey线程安全性：无需额外的协同机制，就许可多个线程以并发方式访问（读和写）一个数据结构，并能够正确地执行和得到所期望的结果。



* 无共享状态，仅仅是局部变量而无全局变量
* 线程私有数据，即Thread-local storage线程本地存储
* 不可变对象
* 互斥执行：利用锁机制以串行方式访问共享数据
* 原子型操作

There are basically below approaches to make an object thread safe in java :
* Using Synchronized keyword
* Make it immutable
* Use a thread safe wrapper
* Using Concurrency Locks
* Using volatile keyword
* copy on write
* 原子对象
 
线程安全的数据结构的指标
* 并发能力：许可多少线程同时访问数据。在不是并发访问
* 可扩展性：随内核增加而提高并发能力

[A Short Guide to Mastering Thread-Safety](http://www.thinkingparallel.com/2006/10/15/a-short-guide-to-mastering-thread-safety/)

We have multiple ways to deal with it, some of which are highlighted in the following list:
* Put a big, fat lock right at the start of the function and unlock it at the end of the function.对于访问数据的方法或者过程上锁
* Put one or many smaller locks in the function around the data that actually need protection. 采用多个更小的锁在数据访问的过程中以更细的粒度保护数据，从而提高并发能力。
* Protect the data instead of the code. Instead of protecting a small region of code with a lock where critical data is accessed, associate a lock with the critical data in question. This may allow you to use two different locks for the same region of code but when working on different data, allowing concurrent execution by multiple threads. An example: When you have written a function that multiplies each element of an array by two, you can associate a different lock to different arrays, allowing two threads to carry out the function concurrently when working on two different arrays. 保护数据而不是保护代码。使用锁不是保护一小段访问关键数据的代码，而是将锁与正在被并发访问的关键数据相关联。这可能会使你针对工作在不同数据上的相同代码段使用不同的锁，从而许可多个线程并发执行。一个例子：当你编写一个功能将一个数组中的每个元素乘以2的过程时，可以将不同的锁关联到不同的数组，从而在处理两个不同数组时，允许两个线程并发执行。
* Use atomic operations to change the data that need protection. 在更改需要保护的数据时采用原子操作。
* Change your functions to only work on thread-private data. This may sound harder than it actually is, but many times shared data are not really necessary. Even if they may seem necessary, there is little trick that can change this quite often: delegate the shared data to the caller of the function, which passes it in as a parameter (most likely a pointer or a reference in C++) and document that the caller is responsible for protecting that data before the function is called. This may sound not like a solution, but rather like a delegation of the whole problem. But considering that the caller may have more knowledge about the present state of the program and its data, it makes a whole lot of sense. As an example, the caller may know, that no other thread presently calls that function with the same data and therefore no protection from concurrent access is necessary. Of course, the moment you employ this last technique, the function is not thread-safe anymore, so make really sure to document this properly! It also changes the interface of the function, which may not be doable for your particular case.更改你的过程，从而仅仅工作于线程私有的数据。这听起来比实际上要困难，很多时候共享数据并不是真正必须的。即使共享数据可能看起来时必须的，但是只要很少的技巧就能够改变这种情况：

[Reading 20: Thread Safety](http://web.mit.edu/6.031/www/fa17/classes/20-thread-safety/)


There are basically four ways to make variable access safe in shared-memory concurrency:
* Confinement. Don’t share the variable between threads. This idea is called confinement, and we’ll explore it today.
* Immutability. Make the shared data immutable. We’ve talked a lot about immutability already, but there are some additional constraints for concurrent programming that we’ll talk about in this reading.
* Threadsafe data type. Encapsulate the shared data in an existing threadsafe data type that does the coordination for you. We’ll talk about that today.
* Synchronization. Use synchronization to keep the threads from accessing the variable at the same time. Synchronization is what you need to build your own threadsafe data type.

[What is Thread-Safety and How to Achieve it?](https://www.baeldung.com/java-thread-safety)


[Accelerators at Virginia Tech](https://accel.cs.vt.edu/courses.php)

chip multiprocessors (CMPs), e.g., traditional & massively parallel multicore

parallelism models, communication models


A multicore chip is a single silicon die containing multiple fully functional sequential processor cores tied together to form a small parallel computer.

How to Improve Performance
* Increase instructions per clock cycle.
* Increase throughput or work completed per unit time.
* Lower latencies intrinsic in the system that limit the above metrics.


Pipelining：Breakdown complex instructions into a set of smaller steps that are executed in order like a factory assembly line.
* 充分利用硬件
* 实现并行处理

Power and cooling are design constraints of equal importance to performance now.

Power Density： Watts/cm2

Power is really a function of ...
* Die size：More transistors and wires to feed
* Frequency f -> How often do you need to feed them
* Voltage V -> At what level do you need to feed them



Pipelining: A double-edged sword，Better Performance (Maybe) and Higher Power Consumption
* Increase # of small steps to realize an instruction.   
More small steps = deeper pipeline = higher f and V, thus enabling better performance but
* Better performance only if pipeline can be kept full. Difficult to do as pipelines get deeper.


Smaller steps = deeper pipeline = more ILP = higher f but
* Hardware much more complex.
* Hardware runs hotter.
* Deeper pipelines and better ILP identification is getting harder and more costly -> diminishing returns


Hyperthreading： “virtual cores”


Multicore Classes
* Homogenous Multicore：Replication of the same processor type on the die as a shared memory multiprocessor.
* Heterogeneous/Hybrid Multicore： Different processor types on a die

Homogeneous Multicore：This will work for now, but it likely will not scale to high core counts. Why?

CPU cache是一个关键的性能特性，充分利用CPU cache，尤其是很对于计算密集型的应用，可以大大提高CPU的处理速度。

引入cache用于解决内存墙问题

Utilization = (t total – t idle ) / t total

Decreased utilization = less work per unit time.

Caches: 预先读取内存数据；代表CPU将数据写入内存。一方面使得CPU在读取/写入数据时无需等待内存，另一方面CPU cache能够与CPU并行工作，即在CPU处理指令时执行内存读写。
* Access a location in memory.
* Copy the location and its neighbors into the faster memories closer to the CPU.

Locality：Spatial and Temporal。局部性：空间局部性和时间局部性。
Locations near each other in space (address) are highly likely to be accessed near each other in time.

Burden?
* The machine makes sure that memory is kept consistent. If a part of cache must be reused, the cache system writes the data back to main memory before overwriting it with new data.
* Hardware cache design deals with managing mappings between the different levels and deciding when to write back down the hierarchy.

Burden?
* The machine makes sure that memory is kept consistent. If a part of cache must be reused, the cache system writes the data back to main memory before overwriting it with new data.
* Hardware cache design deals with managing mappings between the different levels and deciding when to write back down the hierarchy.

Common Memory Models
* Shared Memory Architecture
 * UMA
 * NUMA 
* Distributed Memory Architecture



Memory Consistency


Memory Coherence


* Write-Back：On a write miss, the CPU reads the entire block from memory where the write address is, updates the value in cache, and marks the block as modified (aka dirty).
* Write-Through： When the processor writes, even to a block in cache, a bus write is generated.


在一个DistributedSystem中，最容易想到的是使用一个Global Time Scale决定存储器访问次序，从而判断Most Recent，这种Memory Consistency Model即为Strict Consistency，也被称为Atomic Consistency。Global Time Scale不容易以较小的代价实现，退而求其次采用每一个处理器的Local Time Scale确定Most Recent的方法被称为Sequential Consistency[56]。

与SequentialConsistency要求不同处理器的写操作对于所有处理器具有一致的Order不同，Causal Consistency要求具有Inter-Process Order的写操作具有一致的Order，是Sequential Consistency的一种弱化形式。Processor Consistency进一步弱化，要求来自同一个处理器的写操作具有一致的Order即可。Slow Memory是最弱化的模型，仅要求同一个处理器对同一地址的写操作具有一致的Order[56]。


![Different kinds of cache](pics/cach-kinds.png)


* Look-aside / demand-fill cache: 
For look-aside cache, client will query cache first before querying the data store. If it's a HIT, it will return the value in cache. If it's a MISS, it will return the value from data store. That's it. It says nothing about how the cache should be filled. It just specifies how it would be queried. But usually, it's demand-fill. Demand-fill means in the case of MISS, client will not only uses the value from data store, but also puts that value into cache. 

[Quantitative System Performance: Computer System Analysis Using Queueing Network Models](https://homes.cs.washington.edu/~lazowska/qsp/)

# CS149 2023并行计算

[主页](https://gfxcourses.stanford.edu/cs149/fall23/)

https://www.bilibili.com/video/BV1du17YfE5G/

# 网络编程

三种多路复用模型
* select 有限制，最多1024个，poll、epoll没有这个限制。此外，对socket扫描时是线性扫描，采用轮询的方法
* poll 对数据结构有优化，没有 1024 个的限制。  每次调用poll，都需要把fd集合从用户态拷贝到内核态，这个开销在fd很多时会很大。对socket扫描时是线性扫描，采用轮询的方法，效率较低（高并发时）。
* epoll 对遍历有优化，不会遍历所有socket，只会遍历那些可读的socket，所以效率有所提升。


epoll 有 EPOLLLT 和 EPOLLET 两种触发模式，LT是默认的模式，ET是“高速”模式。
* LT（水平触发）模式下，只要这个文件描述符还有数据可读，每次 epoll_wait都会返回它的事件，提醒用户程序去操作；
* ET（边缘触发）模式下，在它检测到有 I/O 事件时，通过 epoll_wait 调用会得到有事件通知的文件描述符，对于每一个被通知的文件描述符，如可读，则必须将该文件描述符一直读到空，让 errno 返回 EAGAIN 为止，否则下次的 epoll_wait 不会返回余下的数据，会丢掉事件。如果ET模式不是非阻塞的，那这个一直读或一直写势必会在最后一次阻塞。

https://mp.weixin.qq.com/s/PzOF9lFYVacPIRx0JakTjA