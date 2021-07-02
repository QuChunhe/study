
IEEE754

javap



[JDK 14.0.1 General-Availability Release](http://jdk.java.net/java-se-ri/14)

[Java Platform, Standard Edition 8 Reference Implementations](http://jdk.java.net/java-se-ri/8-MR3)

# GC

[Do It Yourself (OpenJDK) Garbage Collector](https://shipilev.net/jvm/diy-gc/)

-XX:+UseSerialGC, -XX:+UseParallelGC, -XX:+UseConcMarkSweepGC, -XX:ParallelCMSThreads=2, -XX:ParallelCMSThreads=4, -XX:+UseG1GC


-XX:+UseParNewGC


[HotSpot Virtual Machine Garbage Collection Tuning Guide Release 11](https://docs.oracle.com/en/java/javase/11/gctuning/index.html)

### 1 Introduction to Garbage Collection Tuning

The Java HotSpot garbage collectors employ various techniques to improve the efficiency of these operations:Java HotSpot垃圾回收器采用各种技术，以提高这些操作的效率
* Use generational scavenging in conjunction with aging to concentrate their efforts on areas in the heap that most likely contain a lot of reclaimable memory areas. 分代清除与老化相结合使用，从而集中精力在堆中，堆是最可能保存大量可回收内存的区域。
* Use multiple threads to aggressively make operations parallel, or perform some long-running operations in the background concurrent to the application.使用多个线程，主动地并行操作，或者在后台相对于应用并发地执行一些长时间运行的操作。
* Try to recover larger contiguous free memory by compacting live objects. 通过压缩活跃对象来尝试恢复更大的连续可用内存。


The Java HotSpot VM provides a selection of garbage collection algorithms to choose from.Java HotSpot虚拟机提供了一个可以选择的垃圾回收算法集合。

In the Java platform, there are currently four supported garbage collection alternatives and all but one of them, the serial GC, parallelize the work to improve performance. It's very important to keep the overhead of doing garbage collection as low as possible. 
当前在Java平台中支持四种可选的垃圾回收方案，除了其中一个为串行垃圾回收之外，其他的都是并行工作，以提高性能。保持尽可能低的垃圾回收开销是非常重要的。

![Comparing Percentage of Time Spent in Garbage Collection](pics/jsgct_dt_005_gph_pc_vs_tp.png)

This figure shows that negligible throughput issues when developing on small systems may become principal bottlenecks when scaling up to large systems. However, small improvements in reducing such a bottleneck can produce large gains in performance. For a sufficiently large system, it becomes worthwhile to select the right garbage collector and to tune it if necessary.
这个图表明，在小型系统上开发时无不足道的吞吐，在扩展到大型系统时就可能变为主要的瓶颈。然而，在减小这类瓶颈中小的改进能够在性能上产生很大的收益。对于足够大的系统，如果需要，值得选择正确的垃圾回收器并且对其调优。

The serial collector is usually adequate for most small applications, in particular those requiring heaps of up to approximately 100 megabytes on modern processors. The other collectors have additional overhead or complexity, which is the price for specialized behavior. If the application does not need the specialized behavior of an alternate collector, use the serial collector. One situation where the serial collector isn't expected to be the best choice is a large, heavily threaded application that runs on a machine with a large amount of memory and two or more processors. When applications are run on such server-class machines, the Garbage-First (G1) collector is selected by default;
对于大多数小应用而言，串行回收器通常已经足够了，特别是那些在现代处理器上需要高达100M左右堆空间的应用。其他回收器有额外的开销或者复杂性，作为专门行为的代价。如果应用程序不需要专门的行为，使用串行回收器。串行回收器不是所期望的最佳选择的一个场合时大型的、重线程化应用，其运行在具有大量内存和两个或者多个处理器的机器上。当应用运行在这类服务器级别的机器上时，Garbage-First（G1）回收器是默认选择。

### 2 Ergonomics

The JVM provides platform-dependent default selections for the garbage collector, heap size, and runtime compiler. These selections match the needs of different types of applications while requiring less command-line tuning. In addition, behavior-based tuning dynamically optimizes the sizes of the heap to meet a specified behavior of the application. 
JVM为垃圾回收器、堆大小和运行时编译器提供了与平台相关的默认选项。 这些选项适合于不同类型应用程序的需求，同时需要更少的命令行调优。 此外，基于行为的调优动态地优化堆的大小，以满足应用程序的特定行为。 

These are important garbage collector, heap size, and runtime compiler default selections: 
* Garbage-First (G1) collector
* The maximum number of GC threads is limited by heap size and available CPU resources 
* Initial heap size of 1/64 of physical memory 
* Maximum heap size of 1/4 of physical memory 
* Tiered compiler, using both C1 and C2 


#### Behavior-Based Tuning

The Java HotSpot VM garbage collectors can be configured to preferentially meet one of two goals: maximum pause-time and application throughput. If the preferred goal is met, the collectors will try to maximize the other. Naturally, these goals can't always be met: Applications require a minimum heap to hold at least all of the live data, and other configuration might preclude reaching some or all of the desired goals.
Java HotSpot虚拟机的垃圾回收器能够配置来优先满足以下两个目标之一：最大暂停时间和应用程序吞吐量。 如果已经满足首选目标，那么回收器将会尝试最大化另一个目标。 自然地，这些目标不可能总是得到满足：应用程序需要一个最小堆来保存至少所有的实时数据，而其他配置可能会阻止实现部分或全部所需的目标。

**Maximum Pause-Time Goal** 最大暂停时间目标

The pause time is the duration during which the garbage collector stops the application and recovers space that's no longer in use. The intent of the maximum pause-time goal is to limit the longest of these pauses. 
暂停时间是垃圾回收器停止应用并恢复不再使用的空间这一过程所持续的时间。最大暂停时间目标的意图是限制暂停的最长时间。

The maximum pause-time goal is specified with the command-line option *-XX:MaxGCPauseMillis=<nnn>*. This is interpreted as a hint to the garbage collector that a pause-time of<nnn> milliseconds or fewer is desired. The garbage collector adjusts the Java heap size and other parameters related to garbage collection in an attempt to keep garbage collection pauses shorter than <nnn> milliseconds. 
最大暂停时间目标由命令行选项*-XX:MaxGCPauseMillis=<nnn>*指定。这被解释为对垃圾回收器的提示，即需要<nnn>毫秒或更短的暂停时间。 垃圾回收器会调整Java堆的大小和其他与垃圾回收相关的参数，以尝试使垃圾回收暂停少于<nnn>毫秒。

**Throughput Goal**

The throughput goal is measured in terms of the time spent collecting garbage, and the time spent outside of garbage collection is the application time.
吞吐量目标依据回收垃圾所消耗的时间来衡量，而在垃圾回收之外消耗的时间就是应用时间。

The goal is specified by the command-line option *-XX:GCTimeRatio=nnn*. The ratio of garbage collection time to application time is 1/(1+nnn). For example, -*XX:GCTimeRatio=19* sets a goal of 1/20th or 5% of the total time for garbage collection.
目标由命令行选项*-XX:GCTimeRatio=nnn*指定。垃圾回收与应用时间之间是1/(1+nnn)。例如，*XX:GCTimeRatio=19*针对垃圾回收设置了1/20或者5%的总时间目标。

The time spent in garbage collection is the total time for all garbage collection induced pauses. If the throughput goal isn't being met, then one possible action for the garbage collector is to increase the size of the heap so that the time spent in the application between collection pauses can be longer.
垃圾回收消耗的时间是所有垃圾回收所引起的暂停的总时间。如果没有满足吞吐量目标，那么对于垃圾回收器一个可能的操作是增加堆的大小，从而使得在回收暂停之间在应用中所消耗的时间变得更长。


**Footprint**

If the throughput and maximum pause-time goals have been met, then the garbage collector reduces the size of the heap until one of the goals (invariably the throughput goal) can't be met. The minimum and maximum heap sizes that the garbage collector can use can be set using *-Xms=<nnn>* and *-Xmx=<mmm>* for minimum and maximum heap size respectively.
如果达到了吞吐量和最大暂停时间目标，那么垃圾回收器会减小堆的大小，直到无法满足其中一个目标（始终为吞吐量目标）。垃圾回收器能够使用的最小和最大的堆大小能够分别使用*-Xms=<nnn>*和*-Xmx=<mmm>*来设置。 

[Java Platform, Standard Edition HotSpot Virtual Machine Garbage Collection Tuning Guide Release 8](https://docs.oracle.com/javase/8/docs/technotes/guides/vm/gctuning/index.html)




垃圾回收器(Garbage Collector: GC)是一个内存管理工具。通过如下操作，其实现了自动内存管理
* Allocating objects to a young generation and promoting aged objects into an old generation.
* Finding live objects in the old generation through a concurrent (parallel) marking phase. The Java HotSpot VM triggers the marking phase when the total Java heap occupancy exceeds the default threshold. 
* Recovering free memory by compacting live objects through parallel copying. 

Behavior-Based Tuning
* Maximum Pause Time Goal: The pause time is the duration during which the garbage collector stops the application and recovers space that is no longer in use. The intent of the maximum pause time goal is to limit the longest of these pauses. The maximum pause time goal is specified with the command-line option -XX:MaxGCPauseMillis=\<nnn\>. 
* application throughput goal:The throughput goal is measured in terms of the time spent collecting garbage and the time spent outside of garbage collection (referred to as application time). The goal is specified by the command-line option -XX:GCTimeRatio=\<nnn\>. The ratio of garbage collection time to application time is 1 / (1 + \<nnn\>). For example, -XX:GCTimeRatio=19 sets a goal of 1/20th or 5% of the total time for garbage collection.　

Choosing a maximum pause time goal may mean that your throughput goal will not be met, so choose values that are an acceptable compromise for the application.

如果选择最大暂停时间为目标，则意味着吞吐目标可能不会被满足，因此为应用选择一个可以被接受的折中值。

Java的一个优点就是向开发者屏蔽了内存分配和垃圾回收的复杂性。然而，当垃圾回收是主要瓶颈时，理解一些被隐藏的实现也是非常有用的。垃圾回收器假设了应用使用对象的方式，这些使用方式反映在可以调整的参数上，通过调整这些参数可以提高性能而不以牺牲抽象为代价。

如果在一个运行程序中从任何指针都无法到达一个对象，那么该对象就被认为是垃圾。

虚拟机包含了一些不同的垃圾回收算法。这些算法通过分代收集的方式组合起来。


弱分代假说（weak generational hypothesis），大部分对象仅仅生存很短的时间，即大部分对象生命期很短（die young），

强分代假说（Strong Generational Hypothesis），越老的对象越不容易死亡，即已经存活很长时间的对象很可能会继续存活很长时间（live long）

通过代来管理内存，代是持有不同生命周期对象的内存池，即将内存划分为不同的代，用于存储不同年龄的对象。对于任何一个代而言，当其被填满时，就会发生垃圾回收。

the young generation　－－ a minor collection 

Yong: Eden, Survivor, Virtual

Tenured -- Major Collection, full collection

当某些对象在经过几次年轻代的垃圾收集后依然存活，则这些对象会被提升（promoted）到老年代。典型情况下，老年代所占用的内存会比年轻代大，而且还会随时逐渐增大。这使得在老年代上垃圾回收的执行时间会比较长，因此不能频繁地对老年代进行垃圾收集。

新生代有一个eden区和两个survivor区组成。大多数对象初始时被分配在eden区。在任何时间总有一个survivor区是空的，用作在eden区内存活对象的目的地，另一个survivor作为下一次复制收集的目的地。对象会被从一个survivor区复制到另一个survivor区。当经过一定次数（-XX:MaxTenuringThreshold=n来指定默认值为15）的年轻代GC后依然存活的对象可以被晋升到老年代。

性能考量
* 吞吐。从一个较长的时间来看，耗费在应用运行的总时间与消耗在垃圾回收上的总时间的比值
* 暂停。暂停是由于发生了垃圾回收使得应用出现无法响应的时间。
* Footprint：一个进程的工作集合，通过页和cache line来衡量
* Promptness:及时性 (promptness)定义为对象死去之后到对象所占用的内存可以再次被使用之前的时间。

Some users are sensitive to other considerations. Footprint is the working set of a process, measured in pages and cache lines. On systems with limited physical memory or many processes, footprint may dictate scalability. Promptness is the time between when an object becomes dead and when the memory becomes available, an important consideration for distributed systems, including Remote Method Invocation (RMI).

**总的堆大小(Total Heap)**

存放 new MyClass() 的对象，是GC的主要区域，

-Xms/-Xmx 分别是堆的初始容量、最大可扩展容量，建议初始值等于设置为最大值，以免反复扩展或缩减的开销；

默认情况下，虚拟机在每次回收时增加或者缩减堆大小，以在每次回收中尽量维持可用空间和活跃对象的比例在一个特定访问，该范围通过如下参数设定：
-XX:MinHeapFreeRatio=<minimum> 和 -XX:MaxHeapFreeRatio=<maximum>,默认值分别为４０和７０

HeapFreeRatio =(CurrentFreeHeapSize/CurrentTotalHeapSize) * 100，值的区间为0到100，

如果该代中可用空间占比HeapFreeRatio小于MinHeapFreeRatio，则需要进行堆扩容，如果该代可用空间占比HeapFreeRatio大于MaxHeapFreeRatio，则需要进行堆缩容，使得仅仅至多MaxHeapFreeRatio的空间是可用的。

**新生代（Young Generation）**

新生代（Young Generation）：又划分为 Eden（伊甸园，新生区）, Survivor#0（幸存区S0）, Survivor#1（幸存区S1）

除了总的可用空间，第二个最能够影响垃圾回收的性能的因素是在堆中新生代所占的比例。新生代空间越大，minor回收出现的频率越小。但是，在总的对大小受限的情况下，新生代空间越大意味着老年代空间越小，其会增加major回收的频率。

-XX:NewRatio 是“老年代 / 新生代”的比例，默认值为 2；

-XX:NewSize and -XX:MaxnewSize 分别代表新生代可被分配的内存的最小下限和最大上限，默认值分别为1310M和没有限制

-XX:SurvivorRatio 用于指定Eden/Survivor#0 的比例，而Survivor#0 与 Survivor#1 容量相同。这个参数对于性能没有那么重要


**老年代（Tenured Generation）**


**类元数据(Metaspace)**

JDK8 中，永久代被完全的移除了（相关参数 -XX:PermSize / -XX：MaxPermSize 被忽略）。改用 Metaspace，相关参数如下：

-XX:MetaspaceSize

-XX:MaxMetaspaceSize： 最大容量，默认没有限制（机器内存）；

-XX:CompressedClassSpaceSize


三种不同类型的回收器
* 串行回收器，使用单一线程执行所有的垃圾回收工作。由于没有线程间的通信开销，这使得串行回收器相对高效。串行回收器非常适合于没有多处理器硬件的单处理器机器，此外对于具有较小数据集的应用，串行处理器也可应用于多处理器的机器。可以通过参数-XX:+UseSerialGC指定使用串行回收器。
* 并行回收器，以并行方式执行minor回收，能够显著降低垃圾回收的开销。其针对于具有中型或者大型数据集并运行在多处理器或者多线程硬件中的应用，可以通过参数-XX:+UseParallelGC指定并行回收器。平行压缩(parallel compaction）是一种能够并行回收器以并行方式执行major回收的特性。如果没有并行压缩，major回收器使用单一现场执行，其会显著地限制可伸缩性。在使用选项-XX:+UseParallelGC时，模式情况下并行压缩是使能的，通过使用-XX:-UseParallelOldGC可以关闭此选项。
* 并发回收器，并发地执行大部分工作，以保证垃圾回收暂停较短。针对于具有中型或者大型的数据集并且要求响应时间比总吞吐更为主要的应用而设计。HotSpot自带了两个并发回收器可供选择，使用-XX:+UseConcMarkSweepGC选择CMS回收器或者使用-XX:+UseG1GC选择G１回收器。

**The Parallel Collector**

并行回收器的线程数可以通过命令行参数-XX:ParallelGCThreads=\<N\>指定。

Growing and shrinking are done at different rates. By default a generation grows in increments of 20% and shrinks in increments of 5%. The percentage for growing is controlled by the command-line option -XX:YoungGenerationSizeIncrement=<Y> for the young generation and -XX:TenuredGenerationSizeIncrement=\<T\> for the tenured generation. The percentage by which a generation shrinks is adjusted by the command-line flag -XX:AdaptiveSizeDecrementScaleFactor=\<D\>. If the growth increment is X percent, then the decrement for shrinking is X/D percent.


**The Mostly Concurrent Collectors**

* Concurrent Mark Sweep (CMS) Collector: This collector is for applications that prefer shorter garbage collection pauses and can afford to share processor resources with the garbage collection.此种回收器针对于那些期望更短的垃圾回收停顿并且能够提供共享处理器资源给垃圾回收的应用
* Garbage-First Garbage Collector: This server-style collector is for multiprocessor machines with large memories. It meets garbage collection pause time goals with high probability while achieving high throughput.服务器类型的回收器针对于具有大内存的多处理器服务器，其在满足垃圾回收暂停时间目标的前提下以较大概率实现高吞吐。

通常并发回收器以处理器资源为代价换取更短的major回收停顿时间，这些处理器资源原本是可以被应用所使用的。最常见的开销是在并发回收部分使用一个或多个处理器。在一个具有N个处理器的系统上，并发回收部分可能使用K/N可用的处理器，其中1<=K<=ceiling{N/4}。除了在并发阶段使用处理器资源，使用并发回收器还会带来额外的开销。因此，使用并发回收器虽然垃圾回收暂停时间通常会短很多，但是与其他回收器相比，应用吞吐也会更低一些。

**Concurrent Mark Sweep (CMS) Collector**

具有相当大的数据集合并且数据存活很长时间（一个大老年代）、运行在两个或者多个处理器上的系统，更容易从使用此类回收器上获得好处。此回收器也能应用于任何需要较低暂停时间的应用。可以通过命令行参数-XX:+UseConcMarkSweepGC，使得CMS生效。


However, if the CMS collector is unable to finish reclaiming the unreachable objects before the tenured generation fills up, or if an allocation cannot be satisfied with the available free space blocks in the tenured generation, then the application is paused and the collection is completed with all the application threads stopped. The inability to complete a collection concurrently is referred to as **concurrent mode failure** and indicates the need to adjust the CMS collector parameters. 

如果CMS回收器在老年代填满之前不能回收不可达的对象，或者在老年代中可用的未分配块不能满足对象分配，那么应用将会被暂停并且。。不能并发地完成垃圾回收被成为并发模式失败，表明需要调整CMS垃圾回收参数。

The CMS collector throws an OutOfMemoryError if too much time is being spent in garbage collection: if more than 98% of the total time is spent in garbage collection and less than 2% of the heap is recovered, then an OutOfMemoryError is thrown. This feature is designed to prevent applications from running for an extended period of time while making little or no progress because the heap is too small. If necessary, this feature can be disabled by adding the option -XX:-UseGCOverheadLimit to the command line.

如果在垃圾回收上花费过多的的时间，CMS回收器抛出OutOfMemoeryError：如果超过９８％的时间都是花费在垃圾回收上并且低于２％的堆上空间被恢复。那么将会抛出OutOfMemoryError。这个特性是为了防止由于堆太小，应用长时间运行但是仅仅稍有或者没有进展。如果必要，可以通过命令行中添加选项-XX:-UseGCOverheadLimit，禁止此项功能。

Because application threads and the garbage collector thread run concurrently during a major collection, objects that are traced by the garbage collector thread may subsequently become unreachable by the time collection process ends. Such unreachable objects that have not yet been reclaimed are referred to as **floating garbage**. The amount of floating garbage depends on the duration of the concurrent collection cycle and on the frequency of reference updates, also known as **mutations**, by the application. 


在一个并发回收周期中，CMS回收器会暂停一个应用两次。第一次暂停标注所有从根（例如从应用线程栈、寄存器、静态对象等）和从其他堆（例如新生代）中可以直达的对象为存活对象。第一次暂停也被成为initial mark pause。

**JVM内存分配策略**

1.对象优先分配在 Eden

首先尝试在 Eden 分配，若 Eden 空间不足，就发起 YoungGC(简称YGC)；

如果幸存对象(被根对象直接或间接引用)在 SurvivorTo 能放下，则存活对象全部移入 SurvivorTo；

如果幸存对象在 SurvivorTo 存放不下，则存活对象全部移入老年代；

如果此时老年代空间不足，则发起一次 FullGC(简称FYC，整个系统停顿，老年代也参与回收)；

如果 FullGC 时空间仍然周转不过来，则报 OutOfMemoryError 并导致进程结束；

如果YGC/FGC能周转过来，则新对象分配在 Eden 中；

2.大对象直接分配在老年代

所谓的大对象是指，需要大量连续内存的 Java 对象，尤其是长字符串或数组，比如 byte[n] 对象；

可以指定多大才算大对象（只对 Serial/ParNew 有效）；

3.长期存活对象移入老年代

经历 n 次 YGC 仍然存活的对象，下次 YGC 时将被移入老年代；

可以设置该数值：

-XX:MaxTenuringThreshold=15(默认)

4.永久代满了也会导致 FullGC

老年代、永久代的垃圾收集是捆绑在一起的，因此无论两者谁满了，都会触发两者的FullGC。




[Java Memory Management for Java Virtual Machine (JVM)](https://betsol.com/java-memory-management-for-java-virtual-machine-jvm/)

#JMM

[Java Memory Model Pragmatics (transcript)](https://shipilev.net/blog/2014/jmm-pragmatics/)
