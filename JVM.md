
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
* Finding live objects in the old generation through a concurrent (parallel) marking phase. The Java HotSpot VM triggers the marking phase when the total Java heap occupancy exceeds the default threshold. See the sections Concurrent Mark Sweep (CMS) Collector and Garbage-First Garbage Collector.
* Recovering free memory by compacting live objects through parallel copying. See the sections The Parallel Collector and Garbage-First Garbage Collector

Behavior-Based Tuning
* Maximum Pause Time Goal: The pause time is the duration during which the garbage collector stops the application and recovers space that is no longer in use. The intent of the maximum pause time goal is to limit the longest of these pauses. The maximum pause time goal is specified with the command-line option -XX:MaxGCPauseMillis=\<nnn\>. 
* application throughput goal:The throughput goal is measured in terms of the time spent collecting garbage and the time spent outside of garbage collection (referred to as application time). The goal is specified by the command-line option -XX:GCTimeRatio=\<nnn\>. The ratio of garbage collection time to application time is 1 / (1 + \<nnn\>). For example, -XX:GCTimeRatio=19 sets a goal of 1/20th or 5% of the total time for garbage collection.

Choosing a maximum pause time goal may mean that your throughput goal will not be met, so choose values that are an acceptable compromise for the application.

Java的一个优点就是向开发者屏蔽了内存分配和垃圾回收的复杂性。然而，当垃圾回收是主要瓶颈时，理解一些被隐藏的实现也是非常有用的。垃圾回收器假设了应用使用对象的方式，这些使用方式反映在可以调整的参数上，通过调整这些参数可以提高性能而不以牺牲抽象为代价。

如果在一个运行程序中从任何指针都无法到达一个对象，那么该对象就被认为是垃圾。

虚拟机包含了一些不同的垃圾回收算法。这些算法通过分代收集组合起来。


弱分代假说（weak generational hypothesis），大部分对象仅仅生存很短的时间，即大部分对象生命期很短（die young），

强分代假说（Strong Generational Hypothesis） 越老的对象越不容易死亡，而没有die young的对象则很可能会存活很长时间（live long）

通过代来管理内存，代是持有不同生命周期对象的内存池。任何一个代，当其被填满时，就会发生垃圾回收。

the young generation　－－ a minor collection 

Yong: Eden, Survivor, Virtual

Tenured



#JMM

[Java Memory Model Pragmatics (transcript)](https://shipilev.net/blog/2014/jmm-pragmatics/)
