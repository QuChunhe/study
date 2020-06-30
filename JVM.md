
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
* Maximum Pause Time Goal: The pause time is the duration during which the garbage collector stops the application and recovers space that is no longer in use. The intent of the maximum pause time goal is to limit the longest of these pauses. The maximum pause time goal is specified with the command-line option -XX:MaxGCPauseMillis=<nnn>. 
* application throughput goal:The throughput goal is measured in terms of the time spent collecting garbage and the time spent outside of garbage collection (referred to as application time). The goal is specified by the command-line option -XX:GCTimeRatio=<nnn>. The ratio of garbage collection time to application time is 1 / (1 + <nnn>). For example, -XX:GCTimeRatio=19 sets a goal of 1/20th or 5% of the total time for garbage collection.

Choosing a maximum pause time goal may mean that your throughput goal will not be met, so choose values that are an acceptable compromise for the application.



#JMM

[Java Memory Model Pragmatics (transcript)](https://shipilev.net/blog/2014/jmm-pragmatics/)
