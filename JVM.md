
IEEE754

javap



[JDK 14.0.1 General-Availability Release](http://jdk.java.net/java-se-ri/14)

[Java Platform, Standard Edition 8 Reference Implementations](http://jdk.java.net/java-se-ri/8-MR3)

# GC

[JVM Tuning: How to Prepare Your Environment for Performance Tuning](https://sematext.com/blog/jvm-performance-tuning/)

Set your JVM Performance Goals
* Latency is the amount of time required to run a garbage collection event.
* Throughput is the percentage of time the VM spends executing the application versus time spent performing garbage collection.
* Footprint is the amount of memory required by the garbage collector to run smoothly.

[Do It Yourself (OpenJDK) Garbage Collector](https://shipilev.net/jvm/diy-gc/)

-XX:+UseSerialGC, -XX:+UseParallelGC, -XX:+UseConcMarkSweepGC, -XX:ParallelCMSThreads=2, -XX:ParallelCMSThreads=4, -XX:+UseG1GC


-XX:+UseParNewGC


* -XX:+PrintGCDetails 在完成每次垃圾回收之后，打印详细的GC日志消息
* -XX:+PrintGCDateStamps 打印日历时期的时间戳
* -XX:+PrintGCTimeStamps 打印相对于JVM起始时间的时间戳 
* -Xloggc:/home/admstats/admservice/logs/gc.log（对于JDK 9或者更高版本-Xlog:gc*:file=<PATH_TO_GC_LOG_FILE>） 指定GC日志消息打印到指定的目录和文件
* -XX:NumberOfGCLogFiles=10 保存多少日志文件，太老的文件将被清除
* -XX:GCLogFileSize=10M 设置GC日志文件的大小的上限。达到此值后文件会比替换。
* -XX:+UseGCLogFileRotation 满足设置条件后GC日志文件会被替换 
* -XX:+PrintHeapAtGC -XX:+PrintTenuringDistribution -XX:+PrintGCApplicationStoppedTime -XX:+PrintPromotionFailure -XX:PrintFLSStatistics=1 
* -XX:+PrintSafepointStatistics  -XX:PrintSafepointStatisticsCount=1

[Understanding Java Garbage Collection Logging: What Are GC Logs and How to Analyze Them](https://sematext.com/blog/java-garbage-collection-logs/#:~:text=What%20Are%20Garbage%20Collection%20%28GC%29%20Logs%20The%20garbage,collector%20behaves%20and%20how%20much%20resources%20it%20uses.)


The garbage collection logs will be able to answer questions like:
* When was the young generation garbage collector used? 
* When was the old generation garbage collector used?
* How many garbage collections were run?
* For how long were the garbage collectors running?
* What was the memory utilization before and after garbage collection?

垃圾回收日志将能够回答类似如下的问题
* 什么时候使用了新生代垃圾回收器
* 什么时候使用了老年代垃圾回收器
* 运行了多少次垃圾回收
* 垃圾回收器运行了多长时间
* 在垃圾回收之前和回收之后内存的使用率是多少


![GC日志文件格式]{pics/java-gc-log-format.png}
1. 垃圾回收发生的时间(timestamp of event)
2. 垃圾回收的类型(garbage collection type) 
   * Minor garbage collection：the young generation space clearing event was performed
   * Major garbage collection：the tenured generation clearing event was performed.
   * Full garbage collection： Full GC， both the young and old generation was cleared. 

3. 触发垃圾回收的原因(garbage collection cause)
   * 分配失败(Allocation Failure)：在Eden中没有足够的空间来创建对象
   * 调用垃圾回收(System.gc())
4. 279616K->146232K – The occupied heap memory before and after the GC, respectively (separated by an arrow)
5. (1013632K) – The current capacity of the heap
6. 0.3318607 secs – The duration of the GC event in seconds


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

**Throughput Goal**吞吐量目标

The throughput goal is measured in terms of the time spent collecting garbage, and the time spent outside of garbage collection is the application time.
吞吐量目标依据回收垃圾所消耗的时间来衡量，而在垃圾回收之外消耗的时间就是应用时间。

The goal is specified by the command-line option *-XX:GCTimeRatio=nnn*. The ratio of garbage collection time to application time is 1/(1+nnn). For example, -*XX:GCTimeRatio=19* sets a goal of 1/20th or 5% of the total time for garbage collection.
目标由命令行选项*-XX:GCTimeRatio=nnn*指定。垃圾回收与应用时间之间是1/(1+nnn)。例如，*XX:GCTimeRatio=19*针对垃圾回收设置了1/20或者5%的总时间目标。

The time spent in garbage collection is the total time for all garbage collection induced pauses. If the throughput goal isn't being met, then one possible action for the garbage collector is to increase the size of the heap so that the time spent in the application between collection pauses can be longer.
垃圾回收消耗的时间是所有垃圾回收所引起的暂停的总时间。如果没有满足吞吐量目标，那么对于垃圾回收器一个可能的操作是增加堆的大小，从而使得在回收暂停之间在应用中所消耗的时间变得更长。


**Footprint**

If the throughput and maximum pause-time goals have been met, then the garbage collector reduces the size of the heap until one of the goals (invariably the throughput goal) can't be met. The minimum and maximum heap sizes that the garbage collector can use can be set using *-Xms=<nnn>* and *-Xmx=<mmm>* for minimum and maximum heap size respectively.
如果达到了吞吐量和最大暂停时间目标，那么垃圾回收器会减小堆的大小，直到无法满足其中一个目标（始终为吞吐量目标）。垃圾回收器能够使用的最小和最大的堆大小能够分别使用*-Xms=<nnn>*和*-Xmx=<mmm>*来设置。 


**Tuning Strategy**调整策略

The heap grows or shrinks to a size that supports the chosen throughput goal. Learn about heap tuning strategies such as choosing a maximum heap size, and choosing maximum pause-time goal.
堆的大小会增长或缩小，以支持所选定的吞吐量目标。了解堆的调整策略，例如选择最大的堆大小和选择最大的暂停时间目标。


Don't choose a maximum value for the heap unless you know that you need a heap greater than the default maximum heap size. Choose a throughput goal that's sufficient for your application.
不要为堆选择一个最大值，除非你知道你需要一个大于默认最大堆大小的堆。选择一个足以满足你应用的吞吐量目标。

A change in the application's behavior can cause the heap to grow or shrink. For example, if the application starts allocating at a higher rate, then the heap grows to maintain the same throughput.
更改应用行为能够造成堆的增长或缩小。例如，如果应用开始以更高的速率分配，那么堆会增加，以保持相同的吞吐量。


If the heap grows to its maximum size and the throughput goal isn't being met, then the maximum heap size is too small for the throughput goal. Set the maximum heap size to a value that's close to the total physical memory on the platform, but doesn't cause swapping of the application. Execute the application again. If the throughput goal still isn't met, then the goal for the application time is too high for the available memory on the platform.
如果堆已经增加到其最大大小并且尚未满足吞吐量目标，那么这个最大堆大小对于吞吐量目标来说就太小了。将最大堆大小设置为接近平台总物理内存的值，但不会导致应用使用交换分区。再次执行应用程序。如果仍然没有达到吞吐量目标，那么应用时间的目标对于平台上的可用内存来说太高了。


If the throughput goal can be met, but pauses are too long, then select a maximum pause-time goal. Choosing a maximum pause-time goal may mean that your throughput goal won't be met, so choose values that are an acceptable compromise for the application.
如果可以达到吞吐量目标，但暂停时间太长，则选择一个最大暂停时间目标。选择最大暂停时间目标可能意味着无法满足你的吞吐量目标，因此为应用选择一个可接受的折衷值。


It's typical that the size of the heap oscillates as the garbage collector tries to satisfy competing goals. This is true even if the application has reached a steady state. The pressure to achieve a throughput goal (which may require a larger heap) competes with the goals for a maximum pause-time and a minimum footprint (which both may require a small heap).
随着垃圾回收器试图满足相互冲突的目标，堆的大小通常会上下波动。即使应用已达到稳定状态，也是如此。实现吞吐量目标（可能需要更大的堆）的压力是与最大暂停时间和最小占用空间（两者都可能需要小堆）的目标相互冲突。

#### 3 Garbage Collector Implementation 垃圾回收器的实现

One strength of the Java SE platform is that it shields the developer from the complexity of memory allocation and garbage collection.
Java SE平台的优势之一是其向开发者屏蔽了内存分配和垃圾回收的复杂性。


However, when garbage collection is the principal bottleneck, it's useful to understand some aspects of the implementation. Garbage collectors make assumptions about the way applications use objects, and these are reflected in tunable parameters that can be adjusted for improved performance without sacrificing the power of the abstraction.
然而，当垃圾回收是主要瓶颈时，了解一些实现还是很有用的。 垃圾回收器对应用使用对象的方式做出假设，这些假设反映在可调参数中，可以在不牺牲抽象能力的情况下调整这些参数来提高性能。 


**Generational Garbage Collection**分代垃圾回收

An object is considered garbage and its memory can be reused by the VM when it can no longer be reached from any reference of any other live object in the running program.
在一个正在运行的程序中当一个对象不能通过任何其他活动对象的任何应用被访问到时，这个对象就被认为是垃圾并且其内部能够被VM再次使用。


A theoretical, most straightforward garbage collection algorithm iterates over every reachable object every time it runs. Any leftover objects are considered garbage. The time this approach takes is proportional to the number of live objects, which is prohibitive for large applications maintaining lots of live data.
一个理论上最直接的垃圾回收算法在其每次运行时遍历每个可达的对象。任何剩余的对象都被看作垃圾。这个方法所花费的时间正比于活跃对象的数量，对于维护大量活跃对象的大型应用而言这个是难以承受的。

The Java HotSpot VM incorporates a number of different garbage collection algorithms that all use a technique called generational collection. While naive garbage collection examines every live object in the heap every time, generational collection exploits several empirically observed properties of most applications to minimize the work required to reclaim unused (garbage) objects. The most important of these observed properties is the weak generational hypothesis, which states that most objects survive for only a short period of time. 
Java HotSpot虚拟机吸收了很多不同的垃圾回收算法，所有算法都使用一种称为分代回收的技术。虽然原始的垃圾回收每次检测在堆中的每个活跃对象，但是分代回收利用了大多数应用的几个经验性观测属性，来最小化回收不再使用的（垃圾）对象所需要的工作。这些观察到的特性中最重要的是弱世代假设，它指出大多数对象只能存活很短的时间。 


**Generations**分代

To optimize for this scenario, memory is managed in generations (memory pools holding objects of different ages). Garbage collection occurs in each generation when the generation fills up.
为了优化这种场景，以分代（持有不同年龄的对象的内存池）方式管理内存。当每一个代被填满时，该代就会进行垃圾回收。

The vast majority of objects are allocated in a pool dedicated to young objects (the young generation), and most objects die there. When the young generation fills up, it causes a minor collection in which only the young generation is collected; garbage in other generations isn't reclaimed. The costs of such collections are, to the first order, proportional to the number of live objects being collected; a young generation full of dead objects is collected very quickly. Typically, some fraction of the surviving objects from the young generation are moved to the old generation during each minor collection. Eventually, the old generation fills up and must be collected, resulting in a major collection, in which the entire heap is collected. Major collections usually last much longer than minor collections because a significantly larger number of objects are involved. Figure 3-2 shows the default arrangement of generations in the serial garbage collector: 
绝大多数对象分配在专用于年轻对象（年轻代）的池中，并且大多数对象都会在此消亡。当新生被填满时，会导致一个在小回收，仅仅在新生代上的回收，而在其他代中的垃圾不会被回收。这种回收的成本与正在被回收的活跃对象的数量成正比；充满死对象的新生代会很快地被回收。通常，一部分存活的对象会从新生代转移到老年代。最终，老年代被填满，必须进行回收，从而导致主回收，即整个堆进行回收。因为涉及从黑茶大量的对象，所以主回收通常被小回收持续更长时间。图3-2显示了在串行垃圾回收器中代的默认布局。

The entire address space covering the Java heap is logically divided into young and old generations. 
Java堆所占用的整个地址空间被逻辑地划分为新生代和老年代。

The young generation consists of eden and two survivor spaces. Most objects are initially allocated in eden. One survivor space is empty at any time, and serves as the destination of live objects in eden and the other survivor space during garbage collection; after garbage collection, eden and the source survivor space are empty. In the next garbage collection, the purpose of the two survivor spaces are exchanged. The one space recently filled is a source of live objects that are copied into the other survivor space. Objects are copied between survivor spaces in this way until they've been copied a certain number of times or there isn't enough space left there. These objects are copied into the old region. This process is also called aging. 
新生代由eden和两个survivor空间组成。 大多数对象最初被分配在eden中。 一个survivor空间在任何时候总是空的，在垃圾回收过程中作为eden和另一个survivor空间中活跃对象的目的地；在垃圾回收之后，eden和源survivor空间是空的。 在接下来的垃圾回收中，两个survivor空间交换了用途。 最近被填充的一个空间是活跃对象的源，会被复制到另一个survivor空间。对象以这种方式在两个survivor空间之间被复制，直到它们被复制了一定次数或survivor已经没有足够的剩余空间。 这些对象被复制到老年区。 这个过程也称为老化。 

**Performance Considerations**性能考虑

The primary measures of garbage collection are throughput and latency.垃圾回收的主要衡量是吞吐量和时延
* Throughput is the percentage of total time not spent in garbage collection considered over long periods of time. Throughput includes time spent in allocation (but tuning for speed of allocation generally isn't needed).吞吐量是在经历一段较长的时期后没有消耗在垃圾回收上的总时间所占的百分百。吞吐量包括空间分配所消耗的时间（通常不需要为分配速率调优）。
* Latency is the responsiveness of an application. Garbage collection pauses affect the responsiveness of applications.时延是一个应用的响应能力。垃圾回收停顿影响了应用的响应能力。


Some users are sensitive to other considerations. Footprint is the working set of a process, measured in pages and cache lines. On systems with limited physical memory or many processes, footprint may dictate scalability. Promptness is the time between when an object becomes dead and when the memory becomes available, an important consideration for distributed systems, including Remote Method Invocation (RMI). 
一些用户对其他考虑因素很敏感。Footprint是进程的工作集合，通过页面和缓存行来衡量。在物理内存受限或有许多进程的系统上，Footprint可能决定了可扩展性。及时性是从一个对象失效到该对象所占内存变为可用之间的时间，这对于分布式系统来说是一个重要的因素，包括远程方法调用 (RMI)。 


In general, choosing the size for a particular generation is a trade-off between these considerations. For example, a very large young generation may maximize throughput, but does so at the expense of footprint, promptness, and pause times. Young generation pauses can be minimized by using a small young generation at the expense of throughput. The sizing of one generation doesn't affect the collection frequency and pause times for another generation.
通常，为特定代选择大小是在这些考虑因素之间的权衡。 例如，一个非常大的新生代可能会实现吞吐量的最大化，但是会以footprint、及时性和暂停时间为代价。 通过使用小的新生代，可以使得新生代暂停时间最小化，但是会以吞吐量为代价。一代的大小并不会影响另一代的回收频率和暂停时间。 

There is no one right way to choose the size of a generation. The best choice is determined by the way the application uses memory as well as user requirements. Thus the virtual machine's choice of a garbage collector isn't always optimal and may be overridden with command-line options;
对于选择代的大小，并没有一种正确的方式。最好的选择是由应用使用内存的方式以及用户需求来确定。虚拟机对于垃圾回收器的选择并不总是最佳的选择，可以被命令行选项所覆盖。


**Throughput and Footprint Measurement**

Throughput and footprint are best measured using metrics particular to the application.


#### 4 Factors Affecting Garbage Collection Performance 影响垃圾回收性能的因素

The two most important factors affecting garbage collection performance are total available memory and proportion of the heap dedicated to the young generation.
影响垃圾回收性能的两个最重要因素是总的可用内存和专用于新生代的堆的比例。


**Total Heap**

The most important factor affecting garbage collection performance is total available memory. Because collections occur when generations fill up, throughput is inversely proportional to the amount of memory available.
影响垃圾回收性能最重要的因素是总的可用内存。因为代填满时就会发生垃圾回收，所以吞吐量反比于可用内存数量。

**Heap Options Affecting Generation Size**影响代大小的堆选项

[Heap Option"](pics/JVMHeapOptions.png)



committed space and virtual space in the heap
* 初始分配的堆空间，committed space ，通过-Xms来设置
* 预留下来尚未分配的空间称为virtual space，一般为最大可用堆内存-最小可用堆内存

This target range is set as a percentage by the options -XX:MinHeapFreeRatio=<minimum> and -XX:MaxHeapFreeRatio=<maximum>, and the total size is bounded below by –Xms<min> and above by –Xmx<max>. 
最终的范围是由选项-XX:MinHeapFreeRatio=<minimum> 和 -XX:MaxHeapFreeRatio=<maximum>来设定百分百，并且总的大小不能低于–Xms<min>，但也不能高于–Xmx<max>。


With these options, if the percent of free space in a generation falls below 40%, then the generation expands to maintain 40% free space, up to the maximum allowed size of the generation. Similarly, if the free space exceeds 70%, then the generation contracts so that only 70% of the space is free, subject to the minimum size of the generation.
使用这些选项，如果在某一代中可用空间的百分比低于40%，则该代会扩展以保持40%的可用空间，直至该代的最大允许大小。 类似地，如果空闲空间超过70%，那么这代就收缩，直到有70%空间是空闲的，受限于代的最小大小。

The following are general guidelines regarding heap sizes for server applications:如下是关于服务器应用堆大小的一般原则
* Unless you have problems with pauses, try granting as much memory as possible to the virtual machine. The default size is often too small.除非你遇到暂停问题，否则尝试分配尽可能多的内存给虚拟机。默认大小常常太小了。
* Setting -Xms and -Xmx to the same value increases predictability by removing the most important sizing decision from the virtual machine. However, the virtual machine is then unable to compensate if you make a poor choice. 将-Xms和-Xmx设置为相同的值可以从虚拟机中取消最重要的、设置大小的决策，从而增加可预测性。然后，如果你作出错误选择，那么虚拟机将不能进行补偿。
* In general, increase the memory as you increase the number of processors, because allocation can be made parallel.通常，你要随着处理器数目的增加而增加内存，因为能够并行进行回收。

* -Xms
* -Xmx
* -XX:MinHeapFreeRatio
* -XX:MaxHeapFreeRatio
* -XX:-ShrinkHeapInSteps： In addition, you can specify -XX:-ShrinkHeapInSteps, which immediately reduces the Java heap to the target size (specified by the parameter -XX:MaxHeapFreeRatio). You may encounter performance degradation with this setting. 

**The Young Generation**

After total available memory, the second most influential factor affecting garbage collection performance is the proportion of the heap dedicated to the young generation.
在总的可用内存之后，影响垃圾回收性能的第二大因素是专用于新生代的堆的比例。


The bigger the young generation, the less often minor collections occur. However, for a bounded heap size, a larger young generation implies a smaller old generation, which will increase the frequency of major collections. The optimal choice depends on the lifetime distribution of the objects allocated by the application.
新生代越大，小回收发生的频率就越低。 然而，对于堆的大小受限的情况，较大的新生代意味着较小的老年代，从而会增加主回收的频率。最佳选择取决于应用所分配对象的生命周期分布。 

* -XX:NewRatio=3
* -XX:NewSize 
* -XX:MaxNewSize


For example, setting -XX:NewRatio=3 means that the ratio between the young and old generation is 1:3. In other words, the combined size of the eden and survivor spaces will be one-fourth of the total heap size.
例如，设置-XX:NewRatio=3意味着新生代代和老年代的比例为1:3。 换句话说，edon和survivor空间的总大小将是总堆大小的四分之一。


The options -XX:NewSize and -XX:MaxNewSize bound the young generation size from below and above. Setting these to the same value fixes the young generation, just as setting -Xms and -Xmx to the same value fixes the total heap size. This is useful for tuning the young generation at a finer granularity than the integral multiples allowed by -XX:NewRatio.
选项-XX:NewSize 和 -XX:MaxNewSize分别从下和上限制了新生代的大小。 将其设置为相同的值可以固定年轻代，就像将-Xms和-Xmx设置为相同的值可以固定堆的总大小一样。 相比于使用XX:NewRatio许可的整数倍，这对于以更细粒度调整新生代是有用的。 

**Survivor Space Sizing**

You can use the option -XX:SurvivorRatio to tune the size of the survivor spaces, but often this isn't important for performance.
你能够使用选项-XX:SurvivorRatio来调整survivor空间的大小，但这通常对性能并不重要。


For example, -XX:SurvivorRatio=6 sets the ratio between eden and a survivor space to 1:6. In other words, each survivor space will be one-sixth of the size of eden, and thus one-eighth of the size of the young generation (not one-seventh, because there are two survivor spaces). 
例如，-XX:SurvivorRatio=6 会设置eden和survivor空间之间的比率为 1:6。 换句话说，每个survivor空间将是eden空间大小的六分之一， 新生代大小的八分之一（不是七分之一，因为有两个survivor空间）。 



#### 5 Available Collectors可用的回收器

The Java HotSpot VM includes three different types of collectors, each with different performance characteristics.
Java HotSpot虚拟机包含了三种不同类型的回收器，每种回收器具有不同的性能特征。 

**Serial Collector**串行回收器

The serial collector uses a single thread to perform all garbage collection work, which makes it relatively efficient because there is no communication overhead between threads.
串行回收器使用单个线程来执行所有垃圾回收工作，这使得其相对高效，因为不存在线程之间的通信开销。


It's best-suited to single processor machines because it can't take advantage of multiprocessor hardware, although it can be useful on multiprocessors for applications with small data sets (up to approximately 100 MB). The serial collector is selected by default on certain hardware and operating system configurations, or can be explicitly enabled with the option -XX:+UseSerialGC.
串行回收器不能利用多处理器硬件，因此其最适合于单处理器的机器，但是对于运行在多处理器上的并且具有小数据集（最多约 100 MB）的应用，其是很有用的。在某些特定硬件和操作系统上将串行回收器配置为默认，或者可以通过选项 XX:+UseSerialGC 显式启用。


**Parallel Collector**并行回回收器

The parallel collector is also known as throughput collector, it's a generational collector similar to the serial collector. The primary difference between the serial and parallel collectors is that the parallel collector has multiple threads that are used to speed up garbage collection.
并行回收器也被称为吞吐量收集器。它是一种类似于串行回收器的分代回收器。串行回收器和并行回收器之间的主要区别是并行回收器采用多线程来加速垃圾回收。

The parallel collector is intended for applications with medium-sized to large-sized data sets that are run on multiprocessor or multithreaded hardware. You can enable it by using the -XX:+UseParallelGC option.
并行回收器是针对于具有中型到大型数据集的并且运行在多处理器或多线程硬件上的应用。 你能够使用-XX:+UseParallelGC选项来启用它。


Parallel compaction is a feature that enables the parallel collector to perform major collections in parallel. Without parallel compaction, major collections are performed using a single thread, which can significantly limit scalability. Parallel compaction is enabled by default if the option -XX:+UseParallelGC has been specified. You can disable it by using the -XX:-UseParallelOldGC option.
并行压缩是一个特性，其使得并行回收器可以并行地执行major回收。 如果没有并行压缩，major回收会使用单个线程来执行，这会显著地限制可伸缩性。 如果已指定选项-XX:+UseParallelGC，那么会默认启用并行压缩。 你可以使用-XX:-UseParallelOldGC选项禁用它。


**The Mostly Concurrent Collectors**通常并发回收器

Concurrent Mark Sweep (CMS) collector and Garbage-First (G1) garbage collector are the two mostly concurrent collectors. Mostly concurrent collectors perform some expensive work concurrently to the application. 并发标记清除回收器和G1垃圾回收器是两个通常并发的回收器。通常并发的回收器相对于应用以并发方式执行一些昂贵的工作。
* G1 garbage collector: This server-style collector is for multiprocessor machines with a large amount of memory. It meets garbage collection pause-time goals with high probability, while achieving high throughput. G1垃圾回收器：这种服务器风格的回收器是为了拥有大量内存的多处理器机器。其能够以很大概率满足垃圾回收的暂停时间目标，同时实现高吞吐量。

G1 is selected by default on certain hardware and operating system configurations, or can be explicitly enabled using-XX:+UseG1GC. 在特定的硬件和操作系统配置下，默认选择G1,或者使用-XX:+UseG1GC来显式地启用它。

* CMS collector: This collector is for applications that prefer shorter garbage collection pauses and can afford to share processor resources with the garbage collection.

Use the option -XX:+UseConcMarkSweepGC to enable the CMS collector

The CMS collector is deprecated as of JDK 9.CMS回收器在JDK 9中被弃用。

**The Z Garbage Collector**Z垃圾回收器

The Z Garbage Collector (ZGC) is a scalable low latency garbage collector. ZGC performs all expensive work concurrently, without stopping the execution of application threads.
Z 垃圾收集器 (ZGC) 是一种可扩展的、低延迟的垃圾回收器。ZGC并发地执行所有昂贵的工作，而不用停止应用线程的执行。

ZGC is intended for applications which require low latency (less than 10 ms pauses) and/or use a very large heap (multi-terabytes). You can enable is by using the -XX:+UseZGC option.
ZGC针对于需要低延迟（小于10毫秒的暂停）和/或使用非常大的堆（数T字节）的应用。你能够通过使用-XX:+UseZGC选项来启用它。

ZGC is available as an experimental feature, starting with JDK 11.
从JDK 11开始，ZGC被启用，作为一种实验特性。

**Selecting a Collector**

If necessary, adjust the heap size to improve performance. If the performance still doesn't meet your goals, then use the following guidelines as a starting point for selecting a collector:如有必要，就调整堆的大小以提高性能。如果性能仍然不能满足你的目标，则使用以下指南作为选择回收器的起点：
* If the application has a small data set (up to approximately 100 MB), then select the serial collector with the option -XX:+UseSerialGC. 如果应用具有很小的数据集（最多约100MB），那么使用选项-XX:+UseSerialGC来选择串行回收器。
* If the application will be run on a single processor and there are no pause-time requirements, then select the serial collector with the option -XX:+UseSerialGC. 如果应用将会运行在单处理器上并且没有暂停时间的要求，那么使用选项-XX:+UseSerialGC来选择串行回收器。
* If (a) peak application performance is the first priority and (b) there are no pause-time requirements or pauses of one second or longer are acceptable, then let the VM select the collector or select the parallel collector with -XX:+UseParallelGC. 如果 (a) 应用的峰值性能是第一优先级并且 (b) 没有暂停时间的要求或者可以接受一秒或更长的暂停，那么让VM选择回收器器或使用-XX:+UseParallelGC来选择并行回收器。
* If response time is more important than overall throughput and garbage collection pauses must be kept shorter than approximately one second, then select a mostly concurrent collector with -XX:+UseG1GC or -XX:+UseConcMarkSweepGC. 如果响应时间比整体吞吐量更重要，并且垃圾回收的暂停必须要少于一秒，那么使用-XX:+UseG1GC 或 -XX:+UseConcMarkSweepGC来选择通常并发的回收器。
* If response time is a high priority, and/or you are using a very large heap, then select a fully concurrent collector with -XX:UseZGC. 如果响应时间具有一个高优先级，和/或你正在使用一个非常大的堆，那么使用-XX:UseZGC来选择一个完全并发的回收器。 

#### 6 The Parallel Collector并行回收器 

The parallel collector is enabled with the command-line option -XX:+UseParallelGC. By default, with this option, both minor and major collections are run in parallel to further reduce garbage collection overhead. 
使用命令行选项-XX:+UseParallelGC可以启用并行回收器。这个选项在默认情况下，minor和major回收都会以并行方式运行，以进一步减小垃圾回收开销。

##Number of Parallel Collector Garbage Collector Threads##

On a machine with <N> hardware threads where <N> is greater than 8, the parallel collector uses a fixed fraction of <N> as the number of garbage collector threads. 
在有N个硬件线程的机器上，其中N大于9,并行回收器使用固定



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




[java GC进入safepoint的时间为什么会这么长](https://www.zhihu.com/question/57722838)


physical memory called the heap.


内存泄漏  OutOfMemory

extensive resource usage and slow down your application or even stop its execution.

https://sematext.com/blog/java-garbage-collection/

 Runtime.getRuntime().gc() call

If you want to force garbage collection you can use the System object from the java.lang package and its gc() method or the Runtime.getRuntime().gc() call.

In general, using the System.gc() is considered a bad practice and we should tune the work of the garbage collector instead of calling it explicitly.


It can be as simple as adjusting the heap size – the -Xmx and -Xms parameters. 

 For example, to set the heap size for our application to be of size 2GB we would add -Xms2g -Xmx2g to our application startup parameters. In most cases, I would also set them to the same value to avoid heap resizing and in addition to that I would add the -XX:+AlwaysPreTouch flag as well to load the memory pages into memory at the start of the application.

The parameters to specify minimum and maximum heap size are -Xms<heap size>[unit] and -Xmx<heap size>[unit], respectively. The unit is the unit you want to initialize the memory in. It can be ‘g’ (GB), ‘m’ (MB), or ‘k’ (KB).

https://sematext.com/blog/jvm-performance-tuning/


