
IEEE754

javap



[JDK 14.0.1 General-Availability Release](http://jdk.java.net/java-se-ri/14)

[Java Platform, Standard Edition 8 Reference Implementations](http://jdk.java.net/java-se-ri/8-MR3)

# GC

[Do It Yourself (OpenJDK) Garbage Collector](https://shipilev.net/jvm/diy-gc/)

-XX:+UseSerialGC, -XX:+UseParallelGC, -XX:+UseConcMarkSweepGC, -XX:ParallelCMSThreads=2, -XX:ParallelCMSThreads=4, -XX:+UseG1GC


-XX:+UseParNewGC

[Java Platform, Standard Edition HotSpot Virtual Machine Garbage Collection Tuning Guide](https://docs.oracle.com/javase/8/docs/technotes/guides/vm/gctuning/index.html)

垃圾收集器(Garbage Collector: GC)是一个内存管理工具。通过如下操作，其实现了自动内存管理
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

Tenured

当某些对象经过几次年轻代垃圾收集后依然存活，则这些对象会被 提升（promoted）到老年代。典型情况下，老年代所占用的内存会比年轻代大，而且还会随时渐渐慢慢增大。这样的结果是，对老年代的垃圾收集就不能频繁进行，而且执行时间也会长很多。

新生代有一个eden区和两个survivor区组成。大多数对象初始时被分配在eden区。在任何时间总有一个survivor区是空的，用作在eden区内存活对象的目的地，另一个survivor作为下一次复制收集的目的地。对象会被从一个survivor区复制到另一个survivor区。当经过一定次数（-XX:MaxTenuringThreshold=n来指定默认值为15）的年轻代GC后依然存活的对象可以被晋升到老年代。

性能考量
* 吞吐。从一个较长的时间来看，耗费在应用运行的总时间与消耗在垃圾回收上的总时间的比值
* 暂停。暂停是由于发生了垃圾回收使得应用出现无法响应的时间。
* Footprint：一个进程的工作集合，通过页和cache　line来衡量
* Promptness:及时性 (promptness)定义为对象死去之后到对象所占用的内存可以使用之前的时间。

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
* 串行回收器，使用单一线程执行所有垃圾回收工作。由于没有线程间的通信开销，这使得串行回收器相对高效。串行回收器非常适合于没有多处理器硬件的单处理器机器，此外对于具有较小数据集的应用，串行处理器也可应用于多处理器的机器。可以通过参数-XX:+UseSerialGC指定使用串行回收器。
* 并行回收器，以并行方式执行minor回收，能够显著降低垃圾回收的开销。其针对于具有中型或者大型数据集并运行在多处理器或者多线程硬件中的应用， -XX:+UseParallelGC。平行压缩(parallel compaction）是一种能够并行回收器以并行方式执行major回收的特性。如果没有并行压缩，major回收器使用单一现场执行，其会显著地限制可伸缩性。在使用选项-XX:+UseParallelGC时，模式情况下并行压缩是使能的，通过使用-XX:-UseParallelOldGC可以关闭此选项。
* 并发回收器，并发地执行大部分工作，以保证垃圾回收暂停较短。针对于具有中型或者大型的数据集并且要求响应时间比总吞吐更为主要的应用而设计。HotSpot自带了两个并发收集器可供选择，使用-XX:+UseConcMarkSweepGC选择CMS收集器或者使用-XX:+UseG1GC选择G１收集器。

**The Parallel Collector**

并行回收器的线程数可以通过命令行参数-XX:ParallelGCThreads=\<N\>指定。

Growing and shrinking are done at different rates. By default a generation grows in increments of 20% and shrinks in increments of 5%. The percentage for growing is controlled by the command-line option -XX:YoungGenerationSizeIncrement=<Y> for the young generation and -XX:TenuredGenerationSizeIncrement=\<T\> for the tenured generation. The percentage by which a generation shrinks is adjusted by the command-line flag -XX:AdaptiveSizeDecrementScaleFactor=\<D\>. If the growth increment is X percent, then the decrement for shrinking is X/D percent.


**The Mostly Concurrent Collectors**

* Concurrent Mark Sweep (CMS) Collector: This collector is for applications that prefer shorter garbage collection pauses and can afford to share processor resources with the garbage collection.此种收集器针对于那些期望更短的垃圾回收间隔并且能够提供共享处理器资源给垃圾回收的应用
* Garbage-First Garbage Collector: This server-style collector is for multiprocessor machines with large memories. It meets garbage collection pause time goals with high probability while achieving high throughput.服务器类型的收集器针对于具有大内存的多处理器服务器，其能够满足垃圾回收暂停时间目标的前提下以较大概论实现高吞吐。

通常并发回收器以处理器资源为代价换取更短的major回收间隔时间，这些处理器资源原本是可以被应用使用的。最常见的开销是在并发回收部分使用一个或多个处理器。在一个具有N个处理器的系统上。并发回收部分可能使用K/N可用的处理器，其中1<=K<=ceiling{N/4}。除了在并发并发阶段使用处理器资源，使用并发性还会带来额外的开销。因此，使用并发回收器虽然垃圾回收暂停通常会短很多，但是与其他收集器相比，应用吞吐也会更低一些。

**Concurrent Mark Sweep (CMS) Collector**

具有相当大的数据集合并且数据存活很长时间（一个大老年代）、运行在两个或者多个处理器上的系统，更容易从使用此类收集器上获得收益。此收集器能应用于任何需要较低暂停时间的应用。可以通过命令行参数-XX:+UseConcMarkSweepGC，使得CMS生效。


However, if the CMS collector is unable to finish reclaiming the unreachable objects before the tenured generation fills up, or if an allocation cannot be satisfied with the available free space blocks in the tenured generation, then the application is paused and the collection is completed with all the application threads stopped. The inability to complete a collection concurrently is referred to as ８８**concurrent mode failure** and indicates the need to adjust the CMS collector parameters. 


The CMS collector throws an OutOfMemoryError if too much time is being spent in garbage collection: if more than 98% of the total time is spent in garbage collection and less than 2% of the heap is recovered, then an OutOfMemoryError is thrown. This feature is designed to prevent applications from running for an extended period of time while making little or no progress because the heap is too small. If necessary, this feature can be disabled by adding the option -XX:-UseGCOverheadLimit to the command line.


Because application threads and the garbage collector thread run concurrently during a major collection, objects that are traced by the garbage collector thread may subsequently become unreachable by the time collection process ends. Such unreachable objects that have not yet been reclaimed are referred to as **floating garbage**. The amount of floating garbage depends on the duration of the concurrent collection cycle and on the frequency of reference updates, also known as **mutations**, by the application. 

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
