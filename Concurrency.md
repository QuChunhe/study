

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


Let It Crash principles

[The Let It Crash Philosophy Outside Erlang](http://stratus3d.com/blog/2020/01/20/applying-the-let-it-crash-philosophy-outside-erlang/)


Future, Callback, Promise, Coroutine


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
    * Static load balancing
    * Dynamic load balancing
分解到各个线程：以数据为中心的的数据域分解和以功能为中心的功能性分解

调度：1）将线程映射到处理器，优先级；2）平衡负载

Performance Evaluation of Parallel Algorithms
* Speedup
    * Amdahl's Law: the computational workload is fixed. If f is fraction of a sequential calculation, then the maximum speedup is 1/f.
    * Gustafson's Law: the execution time is fixed. Gustafson said, the speedup is the linear function of the number of processors.

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


# Concurrency


Atul S. Khot, Concurrent Patterns and Best Practices: Build scalable apps with patterns in multithreading, synchronization, and functional programming, 2018

When things happen at the same time, we say that things are happening concurrently. As far as this book is concerned, whenever parts of an
executable program run at the same time, we are dealing with concurrent programming. We use the term parallel programming as a synonym for concurrent programming.

并发的需求：
* 任务：更小的处理时间，更大的系统吞吐
* 设备：并行处理能力
* 处理的速度的失配
* 设备复用

MapReduce pattern

Fault tolerance:redundant

Time sharing

We need to communicate and coordinate with the concurrently executing entities.

There are two prominent models for concurrent communications:
* message passing 
* shared memory

We start getting results faster, which means the system is responsive.

并发编程实际两个问题
* Coordination：协同是指协建线程的创建以及子任务的执行顺序。
* Communication：通信时指在线程间传递数据，这些数据可能时来自文件和数据库的原始输入数据，也可能时线程子任务的处理结果

We could look at the state as data in a certain stage of processing.

状态是指处理消息或者执行任务所需要的上下文数据，其往往代表处理或者执行的一个特定阶段。状态在特定线程或者node中维护，难以在线程或者node之间共享。
* 电子商务网站中的购物购物篮。
* TCP连接的状态

The shared memory and shared state model

Different concurrent processes have their own address space, while multiple threads within the same process share their address space. Each
thread also has a stack of its own.

进程之间是相互独立的，即进程具有独立的内存地址空间和资源，包括文件描述符。在一个进程内的线程共享地址空间，但是每个线程具有自己的栈。这个栈用于处理过程调用，并且在局部范围的变量也在栈中创建。线程之间可以通过进程全局内存来通信。


Threads interleaving – the need for synchronization

线程一旦开始，其何时运行完全依赖于操作系统的调度，这使得如果不添加额外机制，多个线程会以交织方式获得CPU并且执行操作，即不同线程内的操作会以不可以预料的顺序执行。访问被共享的数据需要正确的同步。

Race conditions and heisenbugs

These are heisenbugs—essentially nondeterministic and hard to reproduce.

Correct memory visibility and happens-before

incorrect memory visibility. The synchronized keyword prevents the execution of critical sections by more than one thread. The synchronized keyword also makes sure the thread's local memory syncs up correctly with the shared memory。

* write barrier
* read barrier

Java's volatile keyword guarantees correct memory visibility.

* pipes and filters design pattern
* Divide and conquer
* double-checked locking pattern


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


# Concurrency

instruction level parallelism (ILP)

thread level parallelism (TLP)


[Real-world Concurrency](https://queue.acm.org/detail.cfm?id=1454462)

[queue.acm concurrency](https://queue.acm.org/listing.cfm?item_topic=Concurrency&qc_type=theme_list&filter=Concurrency&page_title=Concurrency&order=desc)

# Reactive Design Patterns

message-driven

* It must react to its users (responsive). 能响应
* It must react to failure and stay available (resilient).可自愈
* It must react to variable load conditions (elastic).有弹性
* It must react to inputs (message-driven). 消息驱动

# Lock

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


**Be aware of false sharing.**

False sharing is a common problem in shared memory parallel processing. It occurs when two or more cores hold a copy of the same memory cache line.

If one core writes, the cache line holding the memory line is invalidated on other cores. Even though another core may not be using that data (reading or writing), it may be using another element of data on the same cache line. The second core will need to reload the line before it can access its own data again.

The cache hardware ensures data coherency, but at a potentially high performance cost if false sharing is frequent. A good technique to identify false sharing problems is to catch unexpected sharp increases in last-level cache misses using hardware counters or other performance tools.

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
 
