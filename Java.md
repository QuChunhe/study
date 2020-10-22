

＃ Parallelism

[Java多线程及并行编程基础 莱斯大学](https://www.bilibili.com/video/BV1St411i7oa?from=search&seid=7184861422555047434)

[Sophomoric Parallelism and Concurrency](https://homes.cs.washington.edu/~djg/teachingMaterials/spac/)

[A Sophomoric∗Introduction toShared-Memory Parallelism and Concurrenc](https://cs.pomona.edu/classes/cs062-2018sp/handouts/CS62sophomoricParallelismAndConcurrency.pdf)

Task Parallelism（任务并行）  Functional Parallelism（功能并行）loop parallelism（循环并行） dataflow parallelism（数据流并行性）

determine which of these steps can run in parallel with each other. How their parallelism should be coordinate.



# Concurrency

## 协同模型
Phaser

 CyclicBarrier 
 
 CountDownLatch

* thread-saft Collections
* concurrent Collections



Semaphore

限流，限制并发执行的调用数量

资源共享：多个资源，每个线程排他地 占用资源

协同：

CyclicBarrier

协同：在一个出来内部需协同，即在一个线程处理中，发放多个 阶段，每个阶段需要协同，同时 进入下一个阶段

[Close Encounters of The Java Memory Model Kind](https://shipilev.net/blog/2016/close-encounters-of-jmm-kind/)

[The JSR-133 Cookbook for Compiler Writers](http://gee.cs.oswego.edu/dl/jmm/cookbook.html)


[A Java Fork/Join Framework](http://gee.cs.oswego.edu/dl/papers/fj.pdf)

fork/join框架是熟知分而治之方法的并行版本
```
Result solve(Problem problem) {
    if (problem is small)
        directly solve problem
    else {
        split problem into independent parts
        fork new subtasks to solve each part
        join all subtasks
        compose result from subresults
    }
}
```
迭代地、重复地分解子任务，直到这些子任务足够小，能够被简单的和短小的顺序方法解决。

确定任务的粒度。分解任务和合并结果以及管理和调度线程都需要额外的性能开销，任务的粒度的过小，上述的开销要超过任务的计算时间。反之，如果任务的粒度太大，限制了开发任务的并行能力

分而治之是一种思想，迭代是一种方法，fork/join是一种工具

forkjoin framwork

ForkJoinPool.commonPool()

java.util.concurrent.ForkJoinPool.common.parallelism

fork/join框架的一些局限
* 所分解的任务规模不能太小，也不能太大，根据JDK Doc的建议在100到10000之间比较适合
* 不能使用阻塞式I/O操作，例如读取用户输入或者从网络socket读取数据，这些操作会一直等待直到数据可用时为止。因此，这类操作将会导致CPU内核处于空闲，从而降低并行能力。
* 不能在一个任务内抛出非检测型异常。

* ForkJoinPool
* ForkJoinTask
* RecursiveTask
* RecursiveAction
* CountedCompleter

## Lock

JDK中的所机制
* 内置锁 synchronized
* 锁对象 Lock接口的的实现，包括ReentrantLock, ReentrantReadWriteLock.ReadLock, ReentrantReadWriteLock.WriteLock，本质上依赖于Unsafe.unpark()和Unsafe.park(LockSupport类调用Unsafte)。

ReentrantLock, ReentrantReadWriteLock.ReadLock, ReentrantReadWriteLock.WriteLock --> AbstractOwnableSynchronizer --> LockSupport --> Unsafe

```java
class X {
   private final ReentrantLock lock = new ReentrantLock();
   // ...

   public void m() {
     lock.lock();  // block until condition holds
     try {
       // ... method body
     } finally {
       lock.unlock()
     }
   }
   
   public void n() {
       if (lock.tryLock()) {
           try {
              
           } finally {
              lock. unlock();
            }
       }
   }
 }
```

在JAVA中ReentrantLock相对于内置锁有如下优势:
1. 可中断锁，
2. 可超时锁；
3. 能够获得运行线程和阻塞线程,可以通过发起中断，唤醒阻塞的线程
4. 多个条件。
5. 设置不同的加锁策略，fair和unfair 

1)和2)能够使线程优雅地退出加锁阻塞状态，而3)适用于需要等待多个Condition的复杂场景，例如读写锁。


如下三个原因造成了在java中的线程饥饿
* 高优先级的线程会具有低优先级的线程那里抢占所有的CPU时间，造成低优先级线程无法执行
* 由于其他线程总能够获得锁，造成线程被无限期的阻塞，一直等待进入临界区
* 由于其他线程总能够获得信号，从而被唤醒，导致执行wait方法的线程无限期地等待被信号唤醒

```java
public class Lock{
  private boolean isLocked      = false;
  private Thread  lockingThread = null;

  public synchronized void lock() throws InterruptedException{
    while(isLocked){
      wait();
    }
    isLocked      = true;
    lockingThread = Thread.currentThread();
  }

  public synchronized void unlock(){
    if(this.lockingThread != Thread.currentThread()){
      throw new IllegalMonitorStateException(
        "Calling thread has not locked this lock");
    }
    isLocked      = false;
    lockingThread = null;
    notify();
  }
}
```
 
 ```java
 public class FairLock {
    private boolean           isLocked       = false;
    private Thread            lockingThread  = null;
    private List<QueueObject> waitingThreads =
            new ArrayList<QueueObject>();

  public void lock() throws InterruptedException{
    QueueObject queueObject           = new QueueObject();
    boolean     isLockedForThisThread = true;
    synchronized(this){
        waitingThreads.add(queueObject);
    }

    while(isLockedForThisThread){
      synchronized(this){
        isLockedForThisThread =
            isLocked || waitingThreads.get(0) != queueObject;
        if(!isLockedForThisThread){
          isLocked = true;
           waitingThreads.remove(queueObject);
           lockingThread = Thread.currentThread();
           return;
         }
      }
      try{
        queueObject.doWait();
      }catch(InterruptedException e){
        synchronized(this) { waitingThreads.remove(queueObject); }
        throw e;
      }
    }
  }

  public synchronized void unlock(){
    if(this.lockingThread != Thread.currentThread()){
      throw new IllegalMonitorStateException(
        "Calling thread has not locked this lock");
    }
    isLocked      = false;
    lockingThread = null;
    if(waitingThreads.size() > 0){
      waitingThreads.get(0).doNotify();
    }
  }
}
 
 ```
 
 ```java
 public class QueueObject {

  private boolean isNotified = false;

  public synchronized void doWait() throws InterruptedException {
    while(!isNotified){
        this.wait();
    }
    this.isNotified = false;
  }

  public synchronized void doNotify() {
    this.isNotified = true;
    this.notify();
  }

  public boolean equals(Object o) {
    return this == o;
  }
}
 ```
 [Starvation and Fairness](http://tutorials.jenkov.com/java-concurrency/starvation-and-fairness.html)
 
 
 Nested Monitor Lockout(嵌套监视器锁定)是一个类似于死锁的问题，其来如下情况下会发生
 ```
Thread 1 synchronizes on A
Thread 1 synchronizes on B (while synchronized on A)
Thread 1 decides to wait for a signal from another thread before continuing
Thread 1 calls B.wait() thereby releasing the lock on B, but not A.

Thread 2 needs to lock both A and B (in that sequence)
         to send Thread 1 the signal.
Thread 2 cannot lock A, since Thread 1 still holds the lock on A.
Thread 2 remain blocked indefinately waiting for Thread1
         to release the lock on A

Thread 1 remain blocked indefinately waiting for the signal from
        Thread 2, thereby never releasing the lock on A, that must be released to make
        it possible for Thread 2 to send the signal to Thread 1, etc.
 ```
 
 
 [Nested Monitor Lockout](http://tutorials.jenkov.com/java-concurrency/nested-monitor-lockout.html)

所谓Slipped conditions，就是说， 从一个线程检查某一特定条件到该线程操作此条件期间，这个条件已经被其它线程改变，导致第一个线程在该条件上执行了错误的操作。

[Slipped Conditions](http://tutorials.jenkov.com/java-concurrency/slipped-conditions.html)

https://www.cnblogs.com/aishangJava/p/6555291.html


[Thread Signaling](http://tutorials.jenkov.com/java-concurrency/thread-signaling.html#missedsignals)

线程发送信号的目的是使得线程之间能够相互发送信号。

方法notify()和notifyAll()在调用时，如果没有线程正在等待该信号，那么这个信号将会被丢弃。 因此，如果在接受信号的线程调用wait()方法之前，线程已经调用notify()方法，则这个信号将会被等待的线程丢失。 这可能是一个问题，也可能不是一个问题。在某些情况下，错过了唤醒信号可能会导致等待的线程永远处于等待状态，永远不会被唤醒。

为了避免信号丢失，需要在临界区内设置和检查标志或者状态。设置标志或者改变状态后，发出信号。在调用wait和进入等待信号之前以及被信号唤醒之后，都需要检查标志和状态。

虚假唤醒（spurious wakeup）

由于无法解释的原因，即使在没有调用notify()和notifyAll()的情况下，线程也可能被唤醒。这就是所谓的虚假唤醒。在这种情况下，如果被异常唤醒的线程继续执行，就可能造成严重的问题。为了防止上述情况额发生，被唤醒的线程需要检测状态或者标志，以确定开始执行后续代码，还是继续调用wait等待信号 

对于多线程等待的情况，在while中检查状态或者标志是一个不错的解决方案。通过notifyAll()方法唤醒所有线程，但仅仅有一个线程许可继续执行。在同一个时间，仅仅有一个线程能够获得锁，即仅仅有一个对象能够离开wait调用并清除wasSignalled的标志。一旦这个线程离开wait所在的同步块，其他线程可以离开wait调用并检测wasSignalled标志

[Understanding Deadlock, Livelock and Starvation with Code Examples in Java](https://www.codejava.net/java-core/concurrency/understanding-deadlock-livelock-and-starvation-with-code-examples-in-java)

[多核系统上的 Java 并发缺陷模式（bug patterns）](https://www.ibm.com/developerworks/cn/java/j-concurrencybugpatterns/)

1)一定要谨记 volatile 关键字在 Java 代码中仅仅保证这个变量是可见的：它不保证原子性。

i++,
read-modify-write
```java
    private volatile int p;
    
    public void m() {
        ...
        p++;
	...
    }
```

2)在 Java 语言中，我们使用了同步语句来获取互斥锁，这可以保护多线程系统的共享资源访问。然而，易变域的同步中会有一个漏洞，它可能破坏互斥。解决的方法是一定要将同步的域声明为 private final

```java
   private Parameter parameter = new Parameter();
   
   public void m() {
       synchronized (parameter) {
           ...
           parameter = new Parameter();
	   ...
       }
   }
```
争取的用法
```java
   private Parameter parameter = new Parameter();
   private final Ojbect lock = new Object();
   public void m() {
   
       synchronized (lock) {
           ...
           parameter = new Parameter();
	   ...
       }
   }
```

3) 锁泄漏. 要保证锁得到释放，我们只需要在每一个 lock 之后对应执行一个 unlock 方法，而且它们应该置于 try-finally 复杂语句中.
```java
private final Lock lock = new ReentrantLock();
 
public void lockLeak() {
   lock.lock();
   try {
      // access the shared resource
      accessResource();
   } catch (Exception e) {}
   finally {
      lock.unlock();
   }
 
public void accessResource() throws InterruptedException {...}
```

4)同步语句的性能优化：分解锁，减小临界区的大小

```java
public class Operator {
   private int generation = 0; //shared variable
   private float totalAmount = 0; //shared variable
   private final Object lock = new Object();
 
   public void workOn(List<Operand> operands) {
      synchronized (lock) {
         int curGeneration = generation; //requires synch
         float amountForThisWork = 0;
         for (Operand o : operands) {
            o.setGeneration(curGeneration);
            amountForThisWork += o.amount;
         }
         totalAmount += amountForThisWork; //requires synch
         generation++; //requires synch
      }
   }
}
```
分解之后,在保证线程安全的前提下要尽可能地简化同步语句。
```java
public void workOn(List<Operand> operands) {
   int curGeneration;
   float amountForThisWork = 0;
   synchronized (lock) {
      int curGeneration = generation++;
   }
   for (Operand o : operands) {
      o.setGeneration(curGeneration);
      amountForThisWork += o.amount;
   }
   synchronized (lock)
      totalAmount += amountForThisWork;
   }
}
```

5)多阶段访问

6) 对称锁死锁



## Concurrent Collections

copy-on-write collections

“写时复制”——要写的时候复制一份副本，往副本里面写，然后引用到这个副本，在引用到这个副本之前有读操作的话，读的还是之前的老版本，读写分离，写不影响读可以并发读读，读写，但是写写的时候还是冲突的，如果拷贝了N个副本，最后到底引用谁呢，引用某个副本，写到其他副本上的数据就丢失了，所以写要加锁，也就是一个一个来，串行写。
* CopyOnWriteArrayList
* CopyOnWriteArraySet

The way it does this is to make a brand new copy of the list every time it is altered.
* Reads do not block, and effectively pay only the cost of a volatile read;
* Writes do not block reads (or vice versa), but only one write can occur at once; 

Copy-on-write collections are designed for cases where:
* reads hugely outnumber writes;
* the size of collections array is small (or writes are very infrequent); 

ConcurrentLinkedQueue


## 原子操作




# Performance

提高性能的三个方面
* 减小服务时延，能够更快的得到服务的响应或者输出
* 提高系统吞吐，能够处理更多的输入，例如更多的服务请求以及更大的数据规模等
* 降低系统负载，充分利用系统硬件资源，能够在相同的硬件条件下服务更多的服务请求和输入数据

减小服务时延的方法
* 更快的硬件，比如采用固态硬盘(Solid Stat Drive)，以取代机械硬盘(Hard Disk Drive)
* 并行化，挖掘问题/任务的并行性，将问题/任务分解为子问题/任务，并通过并行处理这些子问题/子任务，以减小处理时间
* cache(缓存)，通过缓存数据，避免重复处理 
* 更快的子系统或子任务，比如优化MySQL查询或者采用Redis替换MySQL
* 功能优化，包括算法优化、数据结构优化和编程语言优化

throughtput=concurrency/latency

提高系统吞入的方法
* 提高并发度，即采用更多的线程提供服务，但是随着线程数量的增加，线程之间的互扰会逐渐增加，从而不断增加服务响应时间
* 减小服务时延，即减小服务响应时间
* 采用非阻塞式调用或异步调用
* 避免或减小共享资源，包括共享硬件和共享的数据，例如避免使用锁或者减小所额粒度

降低系统负载的方法


[http://tutorials.jenkov.com/java-performance/index.html](Java Performance)


[JAVA 线上故障排查完整套路，从 CPU、磁盘、内存、网络、GC 一条龙！](https://zhuanlan.zhihu.com/p/145180618)


[高性能 性能优化和测试](https://www.jdon.com/performance.html)

[可伸缩性/可扩展性(Scalable/scalability)](https://www.jdon.com/scalable.html)

[分布式系统](https://www.jdon.com/DistributedSystems.html)




# Tools


[async-profiler](https://github.com/jvm-profiling-tools/async-profiler)


[JVM CPU Profiler技术原理及源码深度解析 ](https://mp.weixin.qq.com/s?__biz=MjM5NjQ5MTI5OA==&mid=2651750821&idx=1&sn=3876eb1ea3963d568a35235a72550e62&chksm=bd1258e88a65d1fed4fc4248398af17537281ca11f90a5808bcb9e2079d0272f3d59cd659c94&mpshare=1&scene=1&srcid=0523O7Lto7wKrJQsEAlQ6v5l&sharer_sharetime=1590241994068&sharer_shareid=fc937fe50a97e6c10553c542abe0a39b&exportkey=AcIcetLP1FaoVWANh0K%2B%2BOk%3D&pass_ticket=aPCoYgXoBsTz6ID87xukGuKUB%2F0jC3shEYI%2BzFX4WzBHZJtlLnSwSzjsGCI93oyx#rd)

## jstack
[How to Read a Thread Dump ](https://dzone.com/articles/how-to-read-a-thread-dump)

A thread dump is a snapshot of the state of all the threads of a Java process. The state of each thread is presented with a stack trace, showing the content of a thread's stack. A thread dump is useful for diagnosing problems as it displays the thread's activity.

jstack prints Java stack traces of Java threads for a given Java process or core file or a remote debug server. For each Java frame, the full class name, method name, 'bci' (byte code index) and line number, if available, are printed. With the -m option, jstack prints both Java and native frames of all threads along with the 'pc' (program counter). 
```
jstack [ option ] pid
jstack [ option ] executable core
jstack [ option ] [server-id@]remote-hostname-or-IP

```
Option
* -F:  Force a stack dump when 'jstack [-l] pid' does not respond.
* -l:  Long listing. Prints additional information about locks such as list of owned java.util.concurrent ownable synchronizers.
* -m:  prints mixed mode (both Java and native C/C++ frames) stack trace.
* -h:  prints a help message.
* -help: prints a help message

The second line represents the current state of the thread. The possible states for a thread are captured in the Thread.State enumeration:
* NEW
* RUNNABLE
* BLOCKED
* WAITING
* TIMED_WAITING
* TERMINATED

线程的状态
* waiting on condition: TIMED_WAITING (sleeping), WAITING (parking)
* runnable: RUNNABLE
* in Object.wait(): TIMED_WAITING (on object monitor)
* sleeping: TIMED_WAITING (sleeping)


Within this stack trace, we can see that locking information has been added, which tells us that this thread is waiting for a lock on an object with an address of 0x00000006c861e938 (and a type of java.lang.Object) and, at this point in the stack trace, holds a lock on an object with an address of x00000006cad83ca8 (also of type java.lang.Object). This supplemental lock information is important when diagnosing deadlocks, as we will see in the following sections
```
- parking to wait for  <0x00000006c861e938>

  Locked ownable synchronizers:
        - <0x00000006cad83ca8> 
```
[Class LockInfo](https://docs.oracle.com/javase/8/docs/api/java/lang/management/LockInfo.html)   
An ownable synchronizer is a synchronizer that may be exclusively owned by a thread and uses AbstractOwnableSynchronizer (or its subclass) to implement its synchronization property. ReentrantLock and ReentrantReadWriteLock are two examples of ownable synchronizers provided by the platform.


```
"Reference Handler" #2 daemon prio=10 os_prio=0 tid=0x00007f06001ae800 nid=0x4f03 in Object.wait() [0x00007f05e39f8000]
   java.lang.Thread.State: WAITING (on object monitor)
	at java.lang.Object.wait(Native Method)
	- waiting on <0x0000000782c06c08> (a java.lang.ref.Reference$Lock)
	at java.lang.Object.wait(Object.java:502)
	at java.lang.ref.Reference.tryHandlePending(Reference.java:191)
	- locked <0x0000000782c06c08> (a java.lang.ref.Reference$Lock)
	at java.lang.ref.Reference$ReferenceHandler.run(Reference.java:153)

   Locked ownable synchronizers:
	- None

```
|  Section   |   Example  |   Description  |
| :------------ | :------------ | :------------ |
Name | "Reference Handler"  |Human-readable name of the thread. This name can be set by calling the setName method on a Threadobject and be obtained by calling getName on the object.|
ID   | #2  | A unique ID associated with each Thread object. This number is generated, starting at 1, for all threads in the system. Each time a Thread object is created, the sequence number is incremented and then assigned to the newly created Thread. This ID is read-only and can be obtained by calling getId on a Thread object.|
Daemon status | daemon |A tag denoting if the thread is a daemon thread. If the thread is a daemon, this tag will be present; if the thread is a non-daemon thread, no tag will be present. For example, Thread-0 is not a daemon thread and therefore has no associated daemon tag in its summary: Thread-0" #12 prio=5....|
Priority | prio=10 | The numeric priority of the Java thread. Note that this does not necessarily correspond to the priority of the OS thread to with the Java thread is dispatched. The priority of a Thread object can be set using the setPriority method and obtained using the getPriority method.|
OS Thread Priority | os_prio=2 |The OS thread priority. This priority can differ from the Java thread priority and corresponds to the OS thread on which the Java thread is dispatched.|
Address | tid=0x00000250e4979000 |The address of the Java thread. This address represents the pointer address of the Java Native Interface (JNI) native Thread object (the C++ Thread object that backs the Java thread through the JNI). This value is obtained by converting the pointer to this (of the C++ object that backs the Java Thread object) to an integer on line 879 of **hotspot/share/runtime/thread.cpp:** ```st->print("tid=" INTPTR_FORMAT " ", p2i(this));``` Although the key for this item (tid) may appear to be the thread ID, it is actually the address of the underlying JNI C++ Thread object and thus is not the ID returned when calling getId on a Java Thread object.|
OS Thread ID | nid=0x3c28 | The unique ID of the OS thread to which the Java Thread is mapped. This value is printed on line 42 of **hotspot/share/runtime/osThread.cpp:**  ```st->print("nid=0x%x ", thread_id()); ```|
Status | waiting on condition| A human-readable string depicting the current status of the thread. This string provides supplementary information beyond the basic thread state (see below) and can be useful in discovering the intended actions of a thread (i.e. was the thread trying to acquire a lock or waiting on a condition when it blocked).|
Last Known Java Stack Pointer | [0x000000b82a9ff000] | The last known Stack Pointer (SP) for the stack associated with the thread. This value is supplied using native C++ code and is interlaced with the Java Thread class using the JNI. This value is obtained using the last_Java_sp() native method and is formatted into the thread dump on line 2886 of **hotspot/share/runtime/thread.cpp:** ```    st->print_cr("[" INTPTR_FORMAT "]", (intptr_t)last_Java_sp() & ~right_n_bits(12));``` For simple thread dumps, this information may not be useful, but for more complex diagnostics, this SP value can be used to trace lock acquisition through a program.|

## jstat
[Java命令行工具之 jstat ](https://mp.weixin.qq.com/s?__biz=MzU3Mjc5NjAzMw==&mid=2247484257&idx=1&sn=555158f962cfa2fad3fd9b5ee43d3f5d&exportkey=AWVZr0rfIXoe7A%2F4RS39IA4%3D&pass_ticket=E6xf44phJMVDAosPSXbBiREJLPMNAecAB%2FfhyIbrCbLED1COVgSeTl9cLBpSwz1u)



[使用jmap排查线上故障：高内存占用 ](https://mp.weixin.qq.com/s?__biz=MzU5MDYxOTc2NQ==&mid=2247483681&idx=1&sn=60edd6cc18cfc59d536fbd77ef751873&chksm=fe3a343bc94dbd2de758b57a228c0c6589c1364160550508f3fe982f33a234720dd77943af66&mpshare=1&scene=1&srcid=0523YV6xXqvxKBgWdfAs1ZHb&sharer_sharetime=1590247120471&sharer_shareid=fc937fe50a97e6c10553c542abe0a39b&exportkey=Aca3MYNxyQgdSh%2FMWImH35g%3D&pass_ticket=aPCoYgXoBsTz6ID87xukGuKUB%2F0jC3shEYI%2BzFX4WzBHZJtlLnSwSzjsGCI93oyx#rd)

[jmap命令的实现原理解析](https://mp.weixin.qq.com/s?__biz=MzIwMzY1OTU1NQ==&mid=2247483746&idx=1&sn=91da774e4be73699b376fc2a8864e6ee&chksm=96cd412ea1bac838548adb281ce2bfdfbd39870e86c8a2bfeb22d522e25a20d6ddd002e9cc57&mpshare=1&scene=1&srcid=0523fLvRBuqDho9ZVyRmWkXM&sharer_sharetime=1590247058554&sharer_shareid=fc937fe50a97e6c10553c542abe0a39b&exportkey=AYGD4k1O17l1WGxxOAq9vCU%3D&pass_ticket=aPCoYgXoBsTz6ID87xukGuKUB%2F0jC3shEYI%2BzFX4WzBHZJtlLnSwSzjsGCI93oyx#rd)


[JVM CPU Profiler技术原理及源码深度解析 ](https://mp.weixin.qq.com/s?__biz=MjM5NjQ5MTI5OA==&mid=2651750821&idx=1&sn=3876eb1ea3963d568a35235a72550e62&chksm=bd1258e88a65d1fed4fc4248398af17537281ca11f90a5808bcb9e2079d0272f3d59cd659c94&mpshare=1&scene=1&srcid=0523O7Lto7wKrJQsEAlQ6v5l&sharer_sharetime=1590241994068&sharer_shareid=fc937fe50a97e6c10553c542abe0a39b&exportkey=AcIcetLP1FaoVWANh0K%2B%2BOk%3D&pass_ticket=aPCoYgXoBsTz6ID87xukGuKUB%2F0jC3shEYI%2BzFX4WzBHZJtlLnSwSzjsGCI93oyx#rd)

[Java命令行工具之 jstat ](https://mp.weixin.qq.com/s?__biz=MzU3Mjc5NjAzMw==&mid=2247484257&idx=1&sn=555158f962cfa2fad3fd9b5ee43d3f5d&exportkey=AWVZr0rfIXoe7A%2F4RS39IA4%3D&pass_ticket=E6xf44phJMVDAosPSXbBiREJLPMNAecAB%2FfhyIbrCbLED1COVgSeTl9cLBpSwz1u)

# Date Time
[Java Date Time](https://www.joda.org/joda-time/)

The new API makes a distinction between how dates and times are used by machines and humans. Machines deal with time as continual ticks as a single incrementing number measured in seconds, milliseconds, etc. Humans use a calendar system to deal with time in terms of year, month, day, hour, minute, and second. The Date-Time API has a separate set of classes to deal with machine-based time and calendar-based human time. It lets you convert machine-based time to human-based time and vice versa.


协调世界时，又称世界统一时间、世界标准时间、国际协调时间,从英文“Coordinated Universal Time”／法文“Temps Universel Cordonné”
而来.协调世界时是以原子时秒长为基础，在时刻上尽量接近于世界时的一种时间计量系统。

国际原子时(TAI，来自法国名字temps atomique International)是一个高精度的原子坐标时间标准:取1958年1月1日0时0分0秒世界时(UT)的瞬间作为同年同月同日0时0分0秒TAI。

规定英国（格林尼治天文台旧址）为中时区（零时区）、东1—12区，西1—12区。每个时区横跨经度15度，时间正好是1小时。最后的东、西第12区各跨经度7.5度，以东、西经180度为界。每个时区的中央经线上的时间就是这个时区内统一采用的时间，称为区时，相邻两个时区的时间相差1小时。


Time Zone Database

String prop = System.getProperty("java.time.zone.DefaultZoneRulesProvider");

TemporalAccessor -> Temporal    
TemporalAmount -> Duration, Period   
Temporal ->  HijrahDate, Instant, JapaneseDate, LocalDate, LocalDateTime, LocalTime, MinguoDate, OffsetDateTime, OffsetTime, ThaiBuddhistDate, Year, YearMonth, ZonedDateTime   
TemporalUnit -> ChronoUnit   
TemporalAdjuster    
ZoneId -> ZoneOffset   
TimeZone   
ZoneRules    
TemporalField ->ChronoField

Calendar ->  GregorianCalendar   
Chronology ->   IsoChronology, JapaneseChronology    
Clock   

TemporalAmount : This is the base interface type for amounts of time. An amount is distinct from a date or time-of-day in that it is not tied to any specific point on the time-line. 

Durations and periods differ in their treatment of daylight savings time when added to ZonedDateTime. A Duration will add an exact number of seconds, thus a duration of one day is always exactly 24 hours. By contrast, a Period will add a conceptual day, trying to maintain the local time.   

The Calendar class is an abstract class that provides methods for converting between a specific instant in time and a set of calendar fields such as YEAR, MONTH, DAY_OF_MONTH, HOUR, and so on, and for manipulating the calendar fields, such as getting the date of the next week.     

A clock providing access to the current instant, date and time using a time-zone.    



# SPI


[Introduction to the Service Provider Interfaces](https://docs.oracle.com/javase/tutorial/sound/SPI-intro.html)

ServiceLoader: A service provider is identified by placing a provider-configuration file in the resource directory META-INF/services. The file's name is the fully-qualified binary name of the service's type. The file contains a list of fully-qualified binary names of concrete provider classes, one per line. Space and tab characters surrounding each name, as well as blank lines, are ignored. 

# Architecture

[架构设计与原则](http://www.rowkey.me/blog/2018/09/20/arch-new/)

架构是从宏观角度对系统的刻画和拆分，用于指导系统构建，以满足需求，包括功能需求和非功能需求。

核心问题是解决复杂性，降低构建和维护成本。

对于复杂系统，架构可能包括多个视图，从不同侧面刻画系统。业务架构、技术架构、数据架构、功能架构、部署架构和集成架构。

业务架构从需求角度，描述系统必须满足的业务功能、业务逻辑、业务流程和业务边界。

技术架构从技术角度，描述系统所依赖的技术栈或核心技术。

数据架构从数据角度，描述系统所基于的数据存储方式以及数据格式/表结构定义。

功能架构从模块角度，描述系统所必须的模块以及模块的功能。

部署架构从运行角度，描述系统的部件/组件如何实际部署和运行以及部件/组件间如何连接。

集成架构从系统角度，描述系统之间的功能调用关系以及所依赖的协议和数据。

[Correct way to find rowcount in Java JDBC](https://stackoverflow.com/questions/13103067/correct-way-to-find-rowcount-in-java-jdbc)

```java
query = "SELECT * FROM customer WHERE username ='"+username+"'";
rs = stmt.executeQuery(query);
ResultSetMetaData metaData = rs.getMetaData();
rowcount = metaData.getColumnCount();
```

```
query = "SELECT * FROM customer WHERE username ='"+username+"'";
rs = stmt.executeQuery(query);
rowcount = rs.last() ? rs.getRow() : 0;
```

```
ResultSet rs = stmt.executeQuery(sql)

Exception in thread "main" java.lang.OutOfMemoryError: Java heap space
	at com.mysql.jdbc.MysqlIO.nextRowFast(MysqlIO.java:2213)
	at com.mysql.jdbc.MysqlIO.nextRow(MysqlIO.java:1992)
	at com.mysql.jdbc.MysqlIO.readSingleRowSet(MysqlIO.java:3413)
	at com.mysql.jdbc.MysqlIO.getResultSet(MysqlIO.java:471)
	at com.mysql.jdbc.MysqlIO.readResultsForQueryOrUpdate(MysqlIO.java:3115)
	at com.mysql.jdbc.MysqlIO.readAllResults(MysqlIO.java:2344)
	at com.mysql.jdbc.MysqlIO.sqlQueryDirect(MysqlIO.java:2739)
	at com.mysql.jdbc.ConnectionImpl.execSQL(ConnectionImpl.java:2482)
	at com.mysql.jdbc.ConnectionImpl.execSQL(ConnectionImpl.java:2440)
	at com.mysql.jdbc.StatementImpl.executeQuery(StatementImpl.java:1381)
	at org.apache.commons.dbcp2.DelegatingStatement.executeQuery(DelegatingStatement.java:206)
	at org.apache.commons.dbcp2.DelegatingStatement.executeQuery(DelegatingStatement.java:206)
```
fix OutOfMemoryError problems
* 设置连接属性useCursorFetch=true ,statement以TYPE_FORWARD_ONLY打开，再设置fetch size参数，表示采用服务器端游标，每次从服务器取fetch_size条数据
```java
try (Connection conn = mysqlDataSource.getConnection();
     Statement stmt = conn.createStatement(ResultSet.TYPE_FORWARD_ONLY,
                                           ResultSet.CONCUR_READ_ONLY)) {
    stmt.setFetchSize(fetchSize);
    try (ResultSet rs = stmt.executeQuery(sql)) {
        rs.setFetchSize(fetchSize);
	// read rs
    }
} catch (SQLException e) {
    //process error
}
```
* stmt.setFetchSize(Integer.MIN_VALUE);
```java
try (Connection conn = mysqlDataSource.getConnection();
     Statement stmt = conn.createStatement(ResultSet.TYPE_FORWARD_ONLY,
                                           ResultSet.CONCUR_READ_ONLY)) {
    stmt.setFetchSize(Integer.MIN_VALUE);
    try (ResultSet rs = stmt.executeQuery(sql)) {
        rs.setFetchSize(fetchSize);
	// read rs
    }
} catch (SQLException e) {
    //process error
}
```


```
java.sql.SQLException: Value '0000-00-00 00:00:00' can not be represented as java.sql.Timestamp
	at com.mysql.jdbc.SQLError.createSQLException(SQLError.java:965) ~[mysql-connector-java-5.1.46.jar:5.1.46]
	at com.mysql.jdbc.SQLError.createSQLException(SQLError.java:898) ~[mysql-connector-java-5.1.46.jar:5.1.46]
	at com.mysql.jdbc.SQLError.createSQLException(SQLError.java:887) ~[mysql-connector-java-5.1.46.jar:5.1.46]
	at com.mysql.jdbc.SQLError.createSQLException(SQLError.java:861) ~[mysql-connector-java-5.1.46.jar:5.1.46]
	at com.mysql.jdbc.ResultSetImpl.getTimestampFromString(ResultSetImpl.java:5676) ~[mysql-connector-java-5.1.46.jar:5.1.46]
	at com.mysql.jdbc.ResultSetImpl.getStringInternal(ResultSetImpl.java:5309) ~[mysql-connector-java-5.1.46.jar:5.1.46]
	at com.mysql.jdbc.ResultSetImpl.getString(ResultSetImpl.java:5138) ~[mysql-connector-java-5.1.46.jar:5.1.46]
	at org.apache.commons.dbcp2.DelegatingResultSet.getString(DelegatingResultSet.java:198) ~[commons-dbcp2-2.2.0.jar:2.2.0]
	at org.apache.commons.dbcp2.DelegatingResultSet.getString(DelegatingResultSet.java:198) ~[commons-dbcp2-2.2.0.jar:2.2.0]
	

connectionProperties=useUnicode=true;characterEncoding=UTF-8;zeroDateTimeBehavior=convertToNull

```

# Books

Richard Warburton, Java 8 Lambdas: Functional Programming for the Masses, O'Reilly, 2014

At the heart of functional programming is thinking about your problem domain in terms of immutable values and functions that translate between them.

This is actually an example of using code as data—we’re giving the button an object that represents an action

A functional interface is an interface with a single abstract method that is used as the type of a lambda expression.


[Package java.util.stream](https://docs.oracle.com/javase/8/docs/api/java/util/stream/package-summary.html)

Streams differ from collections in several ways: 
* No storage. 
* Functional in nature. 
* Laziness-seeking. 
* Possibly unbounded. 
* Consumable. 

Stream operations are divided into intermediate and terminal operations, and are combined to form stream pipelines. A stream pipeline consists of a source (such as a Collection, an array, a generator function, or an I/O channel); followed by zero or more intermediate operations such as Stream.filter or Stream.map; and a terminal operation such as Stream.forEach or Stream.reduce.

Intermediate operations are further divided into stateless and stateful operations. Stateless operations, such as filter and map, retain no state from previously seen element when processing a new element -- each element can be processed independently of operations on other elements. Stateful operations, such as distinct and sorted, may incorporate state from previously seen elements when processing new elements. 


# Java Memory Model (JMM)

Using locks solves the problem. However, performance takes a hit.When multiple threads attempt to acquire a lock, one of them wins, while the rest of the threads are either blocked or suspended.The process of suspending and then resuming a thread is very expensive and affects the overall efficiency of the system.


There is a branch of research focused on creating non-blocking algorithms for concurrent environments. These algorithms exploit low-level atomic machine instructions such as compare-and-swap (CAS), to ensure data integrity.

A typical CAS operation works on three operands:
* The memory location on which to operate (M)
* The existing expected value (A) of the variable
* The new value (B) which needs to be set

The CAS operation updates atomically the value in M to B, but only if the existing value in M matches A, otherwise no action is taken.In both cases, the existing value in M is returned. This combines three steps – getting the value, comparing the value and updating the value – into a single machine level operation. When multiple threads attempt to update the same value through CAS, one of them wins and updates the value. However, unlike in the case of locks, no other thread gets suspended;

使用CAS后，需要判断CAS操作是否成功
1）如果操作成功，继续执行
2）如果操作失败，那么：a)循环CAS操作，直到操作成功，忙等待；b）执行其他操作，空闲在执行CAS操作

Atomic Variables and Collections

[深入理解JVM之Java内存模型](https://segmentfault.com/a/1190000021637869)


https://www.cs.umd.edu/class/spring2013/cmsc433/Notes/07-CMSC433-VolatilityAndOrdering.pdf

[Programming Language Technologies and Paradigms](https://www.cs.umd.edu/class/spring2013/cmsc433/Notes/)

# Functional Programming

Functional Programming in Java

* First-class functions 函数为值
* Anonymous functions  匿名函数
* Closures 闭包
* Currying 柯里化
* Lazy evaluation 惰性求值
* Parametric polymorphism 参数多态
* Algebraic data types 代数数据类型


A referentially transparent program doesn't interfere with the outside world apart from taking an argument as input and outputting a result. Its result only depends on its argument.

Promote Immutability

Prefer Expressions Over Statements

Design with Higher-Order Functions


external iterators

internal iteration
```java
friends.forEach((final String name) -> System.out.println(name))

friends.forEach((name) -> System.out.println(name));

friends.forEach(name -> System.out.println(name));

friends.forEach(System.out::println);

```

Antoine de Saint-Exupéry: “Perfection is achieved not when there is nothing more to add, but when there is nothing left to take away.”

method reference:The Java compiler will take either a lambda expression or a reference to a method where an implementation of a functional interface is expected. With this feature, a short String::toUpperCase can replace name ->name.toUpperCase(),


There are following types of method references in java:
* Reference to a static method.
* Reference to an instance method.
* Reference to a constructor.


lexical scoping and closures
```java
    public static Predicate<String> checkIfStartsWith(final String letter) {
        return name -> name.startsWith(letter);
   }
```


```java
final Function<String, Predicate<String>> startsWithLetter =
      (String letter) -> {
          Predicate<String> checkStartsWith = (String name) -> name.startsWith(letter);
          return checkStartsWith;
      };
```

```java
final Function<String, Predicate<String>> startsWithLetter =
           (String letter) -> (String name) -> name.startsWith(letter);
```

```
final Function<String, Predicate<String>> startsWithLetter = letter -> name -> name.startsWith(letter);
```


```java
final Optional<String> aLongName = friends.stream()
                                         .reduce((name1, name2) -> name1.length() >= name2.length() ? name1 : name2);
aLongName.ifPresent(name -> System.out.println(String.format("A longest name: %s", name)));
```

* Iterating through a Collection
* Finding Elements
* Picking an Element
* Reducing a Collection to a Single Value 
* Joining Elements



Using the collect Method and the Collectors Class

```java
List<Person> olderThan20 = people.stream()
                                 .filter(person -> person.getAge() > 20)
                                 .collect(ArrayList::new, ArrayList::add, ArrayList::addAll);
System.out.println("People older than 20: " + olderThan20);
```
```java
List<Person> olderThan20 = people.stream()
                                 .filter(person -> person.getAge() > 20)
                                 .collect(Collectors.toList());
System.out.println("People older than 20: " + olderThan20);
```


We’ll use lambda expressions to easily separate logic from functions, making them more extensible.

Constructor Reference is used to refer to a constructor without instantiating the named class.



Tell-Don't-Ask
[TellDontAsk](https://www.martinfowler.com/bliki/TellDontAsk.html)

Tell-Don't-Ask is a principle that helps people remember that object-orientation is about bundling data with the functions that operate on that data. It reminds us that rather than asking an object for data and acting on that data, we should instead tell an object what to do.



The Java compiler follows a few simple rules to resolve default methods:
1. Subtypes automatically carry over the default methods from their supertypes.
2. For interfaces that contribute a default method, the implementation in a subtype takes precedence over the one in supertypes.
3. Implementations in classes, including abstract declarations, take precedence over all interface defaults.
4. If there’s a conflict between two or more default method implementations, or there’s a default-abstract conflict between two interfaces, the inheriting class should disambiguate.

Streams have two types of methods: intermediate and terminal



tail-call optimization (TCO)

trampoline calls

Plain-Vanilla Recursion

# 范型

一些常用的泛型类型变量：
* E：元素（Element），多用于java集合框架
* K：关键字（Key）
* N：数字（Number）
* T：类型（Type）
* V：值（Value）

\<? extends T>和<? super T>是Java泛型中的"通配符（Wildcards）"和"边界（Bounds）"的概念。
* \<? extends T>：是指 “上界通配符（Upper Bounds Wildcards）”
* \<? super T>：是指 “下界通配符（Lower Bounds Wildcards）

泛型，即参数化类型
* 泛型类
* 泛型接口
* 泛型方法

PECS（Producer Extends Consumer Super）原则，已经很好理解了：
* 频繁往外读取内容的，适合用上界Extends。
* 经常往里插入的，适合用下界Super。

从上述两方面的分析，总结PECS原则如下：
* 如果要从集合中读取类型T的数据，并且不能写入，可以使用 \<? extends T> 通配符；(Producer Extends)
* 如果要从集合中写入类型T的数据，并且不需要读取，可以使用 \<? super T>通配符；(Consumer Super)

```java
    class Plate<T> {
        private T item;
        public Plate(T t){item=t;}
        public void set(T t){item=t;}
        public T get(){return item;}
    }

   //Lev 1
   class Food{}
   
   //Lev 2
   class Fruit extends Food{}
   class Meat extends Food{}
   
   //Lev 3
   class Apple extends Fruit{}
   class Banana extends Fruit{}
   class Pork extends Meat{}
   class Beef extends Meat{}
   
   //Lev 4
   class RedApple extends Apple{}
   class GreenApple extends Apple{}

   Plate<? extends Fruit> p=new Plate<Apple>(new Apple());
   //不能存入任何元素
   p.set(new Fruit()); //Error
   p.set(new Apple()); //Error
   p.set(new Object()); //Error
   //读取出来的东西只能存放在Fruit或它的基类里。
   Fruit newFruit1=p.get();
   Object newFruit2=p.get();
   Apple newFruit3=p.get(); //Error

   Plate<? super Fruit> p=new Plate<Fruit>(new Fruit());
   //存入元素正常
   p.set(new Fruit());
   p.set(new Apple());
   //读取出来的东西只能存放在Object类里。
   Apple newFruit4=p.get(); //Error
   Fruit newFruit5=p.get(); //Error
   Food newFruit7=p.get(); //Error
   Object newFruit6=p.get();

```
The principles behind this in computer science is called
* Covariance: \<? extends T> MyClass,
* Contravariance: \<? super T> MyClass and
* Invariance/non-variance: MyClass

* Read-only data types (sources) can be covariant;
* write-only data types (sinks) can be contravariant.
* Mutable data types which act as both sources and sinks should be invarian

[Java Generics PECS – Producer Extends Consumer Super](https://howtodoinjava.com/java/generics/java-generics-what-is-pecs-producer-extends-consumer-super/)

泛型中的约束和局限性
* 不能实例化泛型类
* 静态变量或方法不能引用泛型类型变量，但是静态泛型方法是可以的
* 基本类型无法作为泛型类型
* 无法使用instanceof关键字或==判断泛型类的类型
* 泛型类的原生类型与所传递的泛型无关，无论传递什么类型，原生类是一样的
* 泛型数组可以声明但无法实例化
* 泛型类不能继承Exception或者Throwable
* 不能捕获泛型类型限定的异常但可以将泛型限定的异常抛出

型类型继承规则
* 对于泛型参数是继承关系的泛型类之间是没有继承关系的
* 泛型类可以继承其它泛型类，例如: public class ArrayList<E> extends AbstractList<E>
* 泛型类的继承关系在使用中同样会受到泛型类型的影响

这里的Type指java.lang.reflect.Type, 是Java中所有类型的公共高级接口, 代表了Java中的所有类型. Type体系中类型的包括：数组类型(GenericArrayType)、参数化类型(ParameterizedType)、类型变量(TypeVariable)、通配符类型(WildcardType)、原始类型(Class)、基本类型(Class), 以上这些类型都实现Type接口.
* 参数化类型,就是我们平常所用到的泛型List、Map；
* 数组类型,并不是我们工作中所使用的数组String[] 、byte[]，而是带有泛型的数组，即T[] ；
* 通配符类型, 指的是<?>, <? extends T>等等
* 原始类型, 不仅仅包含我们平常所指的类，还包括枚举、数组、注解等；
* 基本类型, 也就是我们所说的java的基本类型，即int,float,double等

The capture-helper trick depends on several things: type inference and capture conversion. The Java compiler doesn't perform type inference in very many places, but one place it does is in inferring the type parameter for generic methods. 

There's a simple rule, called the get-put principle, which tells us which kind of wildcard to use. The get-put principle, as stated in Naftalin and Wadler's fine book on generics, Java Generics and Collections (see Resources), says:   Use an extends wildcard when you only get values out of a structure, use a super wildcard when you only put values into a structure, and don't use a wildcard when you do both.

[Java Generics Interview](https://www.baeldung.com/java-generics-interview-questions)

[Type Erasure](https://docs.oracle.com/javase/tutorial/java/generics/erasure.html)

# 杂项

Comparable<T>  Comparator<T>
	
[Sentinel(https://github.com/alibaba/Sentinel)
	
System.nanoTime与System.currentTimeMillis
* System.nanoTime : This method can only be used to measure elapsed time and is not related to any other notion of system or wall-clock time. 
* System.currentTimeMillis : the difference, measured in milliseconds, between the current time and midnight, January 1, 1970 UTC.


* 强引用（StrongReference）
* 软引用（SoftReference）
* 弱引用（WeakReference）
* 虚引用（PhantomReference）


  
 方法的覆盖(Overriding )vs.重载(Overloading)
 
Overloading occurs when two or more methods in one class have the same method name but different parameters.

Overriding means having two methods with the same method name and parameters (i.e., method signature). One of the methods is in the parent class and the other is in the child class. Overriding allows a child class to provide a specific implementation of a method that is already provided its parent class. 

* Polymorphism applies to overriding, not to overloading.
* Overriding is a run-time concept while overloading is a compile-time concept. 
 
 [ Overriding vs. Overloading in Java ](https://www.programcreek.com/2009/02/overriding-and-overloading-in-java-with-examples/)
 
 [](https://shipilev.net/talks/narnia-2555-jmm-pragmatics-en.pdf)
 
 Inner Class, Anonymous Classes, Local Classes,static nested classes
 
 https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html
 
 [Top 10 Java Performance Problems and How to Solve Them](https://www.eginnovations.com/blog/top-10-java-performance-problems/#JVM-Memory)



|Top 10 Common Java Performance Problems:|
|Memory| 1. Out-of-Memory Errors in the JVM |
         2. Excessive Garbage Collection    |
         3. Improper Data Caching           |
|Thread|                                     |
