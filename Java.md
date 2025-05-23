

Power of 2 sized allocation

[Java中的命名规范](https://www.cnblogs.com/liqiangchn/p/12000361.html)

https://jdk.java.net/java-se-ri/22

[Date and Time on the Internet: Timestamps](https://www.ietf.org/rfc/rfc3339.txt)

＃ Parallelism

[Java多线程及并行编程基础 莱斯大学](https://www.bilibili.com/video/BV1St411i7oa?from=search&seid=7184861422555047434)

[Sophomoric Parallelism and Concurrency](https://homes.cs.washington.edu/~djg/teachingMaterials/spac/)

[A Sophomoric∗Introduction to Shared-Memory Parallelism and Concurrenc](https://cs.pomona.edu/classes/cs062-2018sp/handouts/CS62sophomoricParallelismAndConcurrency.pdf)

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

所谓Slipped conditions（已滑动的条件），就是说， 从一个线程检查某一特定条件到该线程操作此条件期间，这个条件已经被其它线程改变，导致第一个线程在该条件上执行了错误的操作。

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
正确的用法
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
   } catch (Exception e) {

   } finally {
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

```java
public class Employees {
   private final ConcurrentHashMap<String,Integer> nameToNumber;
   private final ConcurrentHashMap<Integer,Salary> numberToSalary;

   ... various methods for adding, removing, getting, etc...

   public int geBonusFor(String name) {
      Integer serialNum = nameToNumber.get(name);
      Salary salary = numberToSalary.get(serialNum);
      return salary.getBonus();
   }
}
```


6) 对称锁死锁
```java
public <E> class ConcurrentHeap {
   private E[] elements;
   private final Object lock = new Object(); //protects elements

   public void addAll(ConcurrentHeap other) {
     synchronized(other.lock) {
       synchronized(this.lock) {
         ... //manipulate other.elements and this.elements
       }
     }
  }
}
```


## Concurrent Collections

线程安全(thread-safty)的数据解构
* 添加锁实现单线程访问，实现简单，但是效率不高 
   * StringBuffer
* 并发数据结构

并发数据结构
* copy-on-write， 
   * CopyOnWriteArrayList
   * CopyOnWriteArraySet
* 分解数据结构，通过多个更小的锁，实现更大的并发操作能力
   * ConcurrentHashMap
* 无锁数据结构
   * AbstractQueuedSynchronizer
   * Disruptor   

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

[Introduction to Lock-Free Data Structures with Java Examples](https://www.baeldung.com/lock-free-programming)

* non-blocking data structures 非阻塞式数据结构
  * obstruction-free
  * lock-free
  * wait-free
* lock-based concurrent data structures 基于锁的并发数据结构

non-blocking algorithms like CAS (compare-and-swap). 类似于CAS这样非阻塞式算法


Lock Versus Starvation

the difference between a blocked and a starving thread.

a）锁方式，没有获得访问权的线程需要处于阻塞状态。被阻塞的线程放弃CPU，需要额外的上下文切换消耗。

b）饥饿方式，不使用锁，而是采用check-try方式，即检测，如果有其他线程正在访问数据结构，则返回后，并再尝试检测，直到能够访问数据结构为止。

Thread 2 accesses the data structure but does not acquire a lock. Thread 1 attempts to access the data structure at the same time, detects the concurrent access, and returns immediately, informing the thread that it could not complete (red) the operation. Thread 1 will then try again until it succeeds to complete the operation (green).
线程2访问数据结构，但是没有获得锁。与此同时，线程1尝试访问数据结构，检测到并发访问，然后立即返回，通知线程其不能完成此操作。线程1将会再次尝试，知道成功完成这个操作。

The advantage of this approach is that we don't need a lock. However, what can happen is that if Thread 2 (or other threads) access the data structure with high frequency, then Thread 1 needs a large number of attempts until it finally succeeds. We call this starvation.
这种方法好处是我们不需要锁。然而，如果线程2（或者其他线程）以更高的频率访问数据结构时，将会发生什么？线程1在其最终成功之前需要更多次的尝试。我们称之为饥饿。

**Obstruction-freedom** is the weakest form of a non-blocking data structure. Here, we only require that a thread is guaranteed to proceed if all other threads are suspended.


A data structure provides **lock-freedom** if, at any time, at least one thread can proceed. All other threads may be starving. The difference to obstruction-freedom is that there is at least one non-starving thread even if no threads are suspended.

A data structure is **wait-free** if it's lock-free and every thread is guaranteed to proceed after a finite number of steps, that is, threads will not starve for an “unreasonably large” number of steps.

Non-Blocking Primitives
* Compare and Swap： CAS is an atomic operation, which means that fetch and update together are one single operation。 The important thing here is that CAS does not acquire a lock on the data structure but returns true if the update was successful, otherwise it returns false. Furthermore, compare-and-swap does not prevent the A-B-A problem
* Load-Link/Store-Conditional： AtomicStampedReference v.t.  A-B-A problem
* Fetch and Add



[LMAX Disruptor](https://lmax-exchange.github.io/disruptor/)

## 原子操作




# Performance

两种优化方式
* 业务优化：业务流程、业务处理上的优化
* 技术优化


池化技术

并行
* 多服务器
* 多进程
* 多线程

变同步为异步

缓存（cache）

精简处理和数据：1）不必要的计算；2）不必要的传输

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


[Speedup Your Java Apps with Hardware Counters ](https://www.slideshare.net/InfoQ/speedup-your-java-apps-with-hardware-counters?qid=4285c82d-ad5b-4bb0-ab3b-bf0320612a9d&v=&b=&from_search=55)

Three magic questions What? ⇒ Where? ⇒ How? 
* What prevents my application to work faster? (monitoring) 
* Where does it hide? (profiling) 
* How to stop it messing with performance? (tuning/optimizing)

[Java Performance Engineer's Survival Guide ](https://www.slideshare.net/MonicaBeckwith/java-performance-engineers-survival-guide-67609990?qid=4285c82d-ad5b-4bb0-ab3b-bf0320612a9d&v=&b=&from_search=47)

Monitor, measure and define performance in terms of throughput, latency, capacity, footprint, utilization

Perfromance Requirements/SLAs
* Throughput
* Respone time
* Footprint
* Capacity managment
* Availability


1. Monitor
  * active
  * Passive
  * Offline
2. Profile
3. Analyze
4. Tune + apply

* Tow down approach
* Bottom up approach

[http://tutorials.jenkov.com/java-performance/index.html](Java Performance)


[JAVA 线上故障排查完整套路，从 CPU、磁盘、内存、网络、GC 一条龙！](https://zhuanlan.zhihu.com/p/145180618)


[高性能 性能优化和测试](https://www.jdon.com/performance.html)

[可伸缩性/可扩展性(Scalable/scalability)](https://www.jdon.com/scalable.html)

[分布式系统](https://www.jdon.com/DistributedSystems.html)




```shell
jcmd <pid> JFR.start
jcmd <pid> JFR.dump filename=recording.jfr
jcmd <pid> JFR.stop
```

[Continuous Monitoring with JDK Flight Recorder (JFR) ](https://www.slideshare.net/InfoQ/continuous-monitoring-with-jdk-flight-recorder-jfr)

黑匣子（Flight Recorder 飞行记录仪），在飞机运行期间，不间断记录各种信息，用于飞机发生事故后的调查

JFR = JDK Fligh Recorder

Using JFR (JDK 11+) 
```
# Start a recording 
java -XX:StartFlightRecording ... 

# Start a recording, and store it to file 
java –XX:StartFlightRecording:filename=/tmp/foo.jfr ... 

# Enable recording in an already running VM (pid 4711) # 
jcmd <pid | main class name> JFR.start [options] 
jcmd 4711 JFR.start 
jcmd MyApplication JFR.start 

# Dump a recording from running VM (pid 4711), at most 50MB of data 
jcmd 4711 JFR.dump maxsize=50MB
```

Using bin/jfr 
```
# Print summary of recording 
jfr summary myrecording.jfr 

# Print events 
jfr print myrecording.jfr 

# Print events in JSON format 
jfr print --json myrecording.jfr 

# Print GC related events 
jfr print --categories "GC" myrecording.jfr 
```
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



jps:java process status

jinfo

jvisualvm

jconsole

jstat

jstack

jcmd

jmap

[【JVM进阶之路】十：JVM调优总结](https://www.cnblogs.com/three-fighter/p/14644152.html)


Async-profiler

[超好用的自带火焰图的 Java 性能分析工具 Async-profiler 了解一下](https://cloud.tencent.com/developer/article/1554194)



Arthas

wrk

# Date Time
[Java Date Time](https://www.joda.org/joda-time/)

The new API makes a distinction between how dates and times are used by machines and humans. Machines deal with time as continual ticks as a single incrementing number measured in seconds, milliseconds, etc. Humans use a calendar system to deal with time in terms of year, month, day, hour, minute, and second. The Date-Time API has a separate set of classes to deal with machine-based time and calendar-based human time. It lets you convert machine-based time to human-based time and vice versa.


UTC时间（英文“Coordinated Universal Time”／法文“Temps Universel Cordonné”），也被称为协调世界时、世界统一时间、世界标准时间、国际协调时间。协调世界时是以原子时秒长为基础，在时刻上尽量接近于世界时的一种时间计量系统。协调世界时间原来也被称为格林威治时间（Greenwich Mean Time： GMT） 。日期时间的国际标准

国际原子时(TAI，来自法国名字temps atomique International)是一个高精度的原子坐标时间标准:取1958年1月1日0时0分0秒世界时(UT)的瞬间作为同年同月同日0时0分0秒TAI。

GMT（Greenwich Mean Time）， 格林威治平时（也称格林威治时间）。规定英国（格林尼治天文台旧址）为中时区（零时区）、东1—12区，西1—12区。每个时区横跨经度15度，时间正好是1小时。最后的东、西第12区各跨经度7.5度，以东、西经180度为界。每个时区的中央经线上的时间就是这个时区内统一采用的时间，称为区时，相邻两个时区的时间相差1小时。


Time Zone Database

String prop = System.getProperty("java.time.zone.DefaultZoneRulesProvider");

* TemporalAccessor -> Temporal    
* TemporalAmount -> Duration, Period   
* Temporal ->  HijrahDate, Instant, JapaneseDate, LocalDate, LocalDateTime, LocalTime, MinguoDate, OffsetDateTime, OffsetTime, ThaiBuddhistDate, Year, YearMonth, ZonedDateTime   
* TemporalUnit -> ChronoUnit   
* TemporalAdjuster    
* ZoneId -> ZoneOffset   
* TimeZone   
* ZoneRules    
* TemporalField ->ChronoField

* Calendar ->  GregorianCalendar   
* Chronology ->   IsoChronology, JapaneseChronology    
* Clock  

 ChronoUnit TimeUnit TemporalUnit

 Duration

TemporalAmount : This is the base interface type for amounts of time. An amount is distinct from a date or time-of-day in that it is not tied to any specific point on the time-line. 

Durations and periods differ in their treatment of daylight savings time when added to ZonedDateTime. A Duration will add an exact number of seconds, thus a duration of one day is always exactly 24 hours. By contrast, a Period will add a conceptual day, trying to maintain the local time.   

The Calendar class is an abstract class that provides methods for converting between a specific instant in time and a set of calendar fields such as YEAR, MONTH, DAY_OF_MONTH, HOUR, and so on, and for manipulating the calendar fields, such as getting the date of the next week.     

A clock providing access to the current instant, date and time using a time-zone.    

表示时间的两种方式
* human time 人类时间
* machine time 机器时间

时间的两种形式
* 时刻，某个特点的时间点
* 时长，时间点之间的间隔

rfc3339

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


* Lambda Epression
* Target Typing
* Functional Interface 
* Method Rference

We’ll use lambda expressions to easily separate logic from functions, making them more extensible.

Constructor Reference is used to refer to a constructor without instantiating the named class.

A lambda expression is an unnamed block of code (or an unnamed function) with a list of formal parameters and a body. Sometimes a lambda expression is simply called a lambda. The body of a lambda expression can be a block statement or an expression. An arrow (->) is used to separate the list of parameters and the body. The term “lambda” has its origin in Lambda calculus that uses the Greek letter lambda (λ) to denote a function abstraction.

Unlike a method, a lambda expression does
not have the following four parts:
* A lambda expression does not have a name.
* A lambda expression does not have a return type. It is inferred by the compiler from the context of its use and from its body.
* A lambda expression does not have a throws clause. It is inferred from the context of its use and its body.
* A lambda expression cannot declare type parameters. That is, a lambda expression cannot be generic.


The compiler infers the type of a lambda expression. The context in which a lambda expression is used expects a type, which is called the target type. The process of inferring the type of a lambda expression from the context is known as target typing.

Changing the behavior of a method through its parameters is known as behavior parameterization. This is also known as passing code as data because you pass code (logic, functionality, or behavior) encapsulated in lambda expressions to methods as if it were data.

The following types of methods in an interface do not count for defining a functional interface:
* Default methods
* static methods
* Public methods inherited from the Object class

Java 8 introduced a new type called an intersection type that is an intersection (or subtype) of multiple types. An intersection type may appear as the target type in a cast. An ampersand (&) is used between two types, such as (Type1 & Type2 & Type3), and it represents a new type that is an intersection of Type1, Type2, and Type3.


* Function<T,R>: R apply(T t) 
* BiFunction<T,U,R>: R apply(T t, U u) 
* Predicate<T>: boolean test(T t) 
* BiPredicate<T,U>: boolean test(T t, U u)
* Consumer<T> :void accept(T t) 
* BiConsumer<T,U>: void accept(T t, U u) 
* Supplier<T>: T get() 
* UnaryOperator<T>: T apply(T t)
* BinaryOperator<T>: T apply(T t1, T t2)

Six specializations of the Function<T,R> interface exist:
* IntFunction<R>
* LongFunction<R>
* DoubleFunction<R>
* ToIntFunction<T>
* ToLongFunction<T>
* ToDoubleFunction<T>

Functional interfaces are used in two contexts by two different types of users:
* By library designers for designing APIs
* By library users for using the APIs


A method reference is a shorthand way to create a lambda expression using an existing method. Using method references makes your lambda expressions more readable and concise; it also lets you use the existing methods as lambda expressions. If a lambda expression contains a body that is an expression using a method call, you can use a method reference in place of that lambda expression.

The general syntax for a method reference is
```java
<Qualifier>::<MethodName>
```
A method reference does not call the method when it is declared. The method is called later when the method of its target type is called.

Using method references may be a little confusing in the beginning. The main point of confusion is the process of mapping the number and type of arguments in the actual method to the method reference.


Instance Method References

In a method reference of an instance method, you can specify the receiver of the method invocation explicitly or you can provide it implicitly when the method is invoked. The former is called a bound receiver and the latter is called an unbound receiver. The syntax for an instance method reference supports two variants:
```java
 objectRef::instanceMethod
 ClassName::instanceMethod
```

In the beginning, this is confusing for two reasons:
* The syntax is the same as the syntax for a method reference to a static method.
* It raises a question: which object is the receiver of the instance method invocation?

The first confusion can be cleared up by looking at the method name and checking whether it is a static or instance method. If the method is an instance method, the method reference represents an instance method reference.


Constructor References


The syntax for using a constructor is as follows:
```java
  ClassName::new
  ArrayTypeName::new
```

Like a local and anonymous inner class, a lambda expression can access effectively final local variables. A local variable is effectively final in the following two cases:
* It is declared final.
* It is not declared final, but initialized only once.

A lambda expression can access instance and class variables of a class whether they are effectively final or not. If instance and class variables are not final, they can be modified inside the body of the lambda expressions. A lambda expression keeps a copy of the local variables used in its body. If the local variables are reference variables, a copy of the references is kept, not a copy of the objects.


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

# 范型(Generics)

A type with type parameters in its declaration is called a generic type.
在声明中存在类型参数的类型被称为范型。

They let you specify a type parameter with a type (class or interface). Such a type is called a generic type (more specifically generic class or generic interface). The type parameter value could be specified when you declare a variable of the generic type and create an object of your generic type.泛型许可指定一个具有类型参数的类型（类或接口）。这样的类型被称为泛型类型（更确切地称为是泛型类或泛型接口）。在声明一个泛型类型的变量并创建泛型类型的对象时，可以指定类型参数的值。


The purpose of using generics is to have compiletime type-safety. As long as the compiler is satisfied that the operation will not produce any surprising results at runtime, it allows the operation on the wildcard generic type reference.


Using only a question mark as a parameter type (<?>) is known as an unbounded wildcard. It places no bounds as to what type it can refer. You can also place an upper bound or a lower bound with a wildcard. 
如果仅使用问号作为参数类型（<？>），就被称为无边界通配符，其不限制能够引用什么类型。此外，还可以在通配符上设置上限或下限。

\<? extends T>和<? super T>是Java泛型中的"通配符（Wildcards）"和"边界（Bounds）"的概念。
* \<?> ：是无边界通配符（Unbounded Wildcards），表示任何类型。
* \<? extends T>：是上界通配符（Upper Bounds Wildcards），表示T或者T的子类
* \<? super T>：是指“下界通配符（Lower Bounds Wildcards），表示T或者T的父类。



型类型继承规则
* 对于泛型参数是继承关系的泛型类之间是没有继承关系的
* 泛型类可以继承其它泛型类，例如: public class ArrayList<E> extends AbstractList<E>
* 泛型类的继承关系在使用中同样会受到泛型类型的影响

Type parameters defined for a generic type are not available in static methods of that type. Therefore, if a static method needs to be generic, it must define its own type parameters. If a method needs to be generic, define just that method as generic rather than defining the entire type as generic.在泛型类型中定义的类型参数在该泛型的静态方法中无法使用。为此，如果一个静态方法需要被泛型化，其必须定义自己的类型参数。如果一个方法需被泛型化，只需将该方法定义为泛型即可，而无需将整个类型定义为泛型。


type inference step
1. First, it tries to infer the type parameter from the static type of the constructorarguments. Note that constructor-arguments may be empty, for example, new ArrayList<>(). If the type parameter is inferred in this step, the process continues to the next step.
2. It uses the left side of the assignment operator to infer the type. In the previous statement, it will infer T2 as the type if the constructor-arguments are empty. Note that an object-creation expression may not be part of an assignment statement. In such cases, it will use the next step.
3. If the object-creation expression is used as an actual parameter for a method call, the compiler tries to infer the type by looking at the type of the formal parameter for the method being called.
4. If all else fails and it cannot infer the type using these steps, it infers Object as the type parameter.

No Generic Exception Classes

No Generic Anonymous Classes


Most generic types are non-reifiable because generics are implemented using erasure, which removes the type’s　parameters information at compile time. For example, when you write Wrapper<String>, the compiler　removes the type parameter <String> and the runtime sees only Wrapper instead of Wrapper<String>.

Heap pollution is a situation that occurs when a variable of a parameterized type refers to an object not of the same parameterized type. The compiler issues an unchecked warning if it detects possible heap pollution. If your program compiles without any unchecked warnings, heap pollution will not occur.


一些常用的泛型类型变量：
* E：元素（Element），多用于java集合框架
* K：键（Key），多用于Java Map中的key
* N：数字（Number）
* T：类型（Type）
* V：值（Value），用于Java Map中的value
* R：结果（Result），方法的返回值



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
* 协变(Covariance): \<? extends T> MyClass,
* 逆变(Contravariance): \<? super T> MyClass and
* 抗变(Invariance/non-variance): MyClass

```java
    List<String> stringList = new ArrayList<>();
    List<Object> objectList = stringList;
```
上述代码中stringList的类型List\<String>是Invariance的，在赋值给objectList时编译器会抛出如下错误
>>java: 不兼容的类型: java.util.List<java.lang.String>无法转换为java.util.List<java.lang.Object>

Java中的数组是协变的，因此可以将stringArray赋值给objectArray，编译可以正常通过。
```java
    String[] stringArray = new String[]{"1"};
    Object[] objectArray= stringArray;
    objectArray[0] = 1;
```
对于objectArray的元素进行赋值会在运行时抛出如下异常
>>Exception in thread "main" java.lang.ArrayStoreException: java.lang.Integer


协变与逆变
* Read-only data types (sources) can be covariant;
* write-only data types (sinks) can be contravariant.
* Mutable data types which act as both sources and sinks should be invarian

[Java Generics PECS – Producer Extends Consumer Super](https://howtodoinjava.com/java/generics/java-generics-what-is-pecs-producer-extends-consumer-super/)
[你懂协变(Covariance)逆变(Contravariance)与抗变(Invariant)吗？](https://zhuanlan.zhihu.com/p/268523581)

泛型中的约束和局限性
* 不能实例化泛型类
* 静态变量或方法不能引用泛型类型变量，但是静态泛型方法是可以的
* primitive type无法作为泛型类型
* 无法使用instanceof关键字或==判断泛型类的类型
* 泛型类的原生类型与所传递的泛型无关，无论传递什么类型，原生类是一样的
* 泛型数组可以声明但无法实例化
* 泛型类不能继承Exception或者Throwable
* 不能捕获泛型类型限定的异常但可以将泛型限定的异常抛出

通过反射获取范型中的参数类型
```java
public abstract class AbstractRepository<T> implements Repository<T> {
  protected final Class<T> entityClass;

  public AbstractRepository() {
    entityClass = (Class<T>) ((ParameterizedType) getClass().getGenericSuperclass())
          .getActualTypeArguments()[0];
  }
```



这里的Type指java.lang.reflect.Type, 是Java中所有类型的公共高级接口, 代表了Java中的所有类型. Type体系中类型的包括：数组类型(GenericArrayType)、参数化类型(ParameterizedType)、类型变量(TypeVariable)、通配符类型(WildcardType)、原始类型(Class)、基本类型(Class), 以上这些类型都实现Type接口.
* 参数化类型,就是我们平常所用到的泛型List、Map；
* 数组类型,并不是我们工作中所使用的数组String[] 、byte[]，而是带有泛型的数组，即T[] ；
* 通配符类型, 指的是<?>, <? extends T>等等
* 原始类型, 不仅仅包含我们平常所指的类，还包括枚举、数组、注解等；
* 基本类型(primitive type), 也就是我们所说的java的基本类型，即int,float,double等

The capture-helper trick depends on several things: type inference and capture conversion. The Java compiler doesn't perform type inference in very many places, but one place it does is in inferring the type parameter for generic methods. 

There's a simple rule, called the get-put principle, which tells us which kind of wildcard to use. The get-put principle, as stated in Naftalin and Wadler's fine book on generics, Java Generics and Collections (see Resources), says:   Use an extends wildcard when you only get values out of a structure, use a super wildcard when you only put values into a structure, and don't use a wildcard when you do both.

[Java Generics Interview](https://www.baeldung.com/java-generics-interview-questions)

[Type Erasure](https://docs.oracle.com/javase/tutorial/java/generics/erasure.html)



Generics were introduced to the Java language to provide tighter type checks at compile time and to support generic programming. To implement generics, the Java compiler applies type erasure to:在Java语言中引入泛型，用于在编译过程中提供更加严格的类型检查，并支持泛型编程。为了实现泛型，Java编译器将类型擦除应用于：
* Replace all type parameters in generic types with their bounds or Object if the type parameters are unbounded. The produced bytecode, therefore, contains only ordinary classes, interfaces, and methods. 如果类型参数是无边界的，则将泛型类型中的所有类型参数替换为其Object，否则替换为其边界。因此，生成的字节码只包含普通类、接口和方法。
* Insert type casts if necessary to preserve type safety. 如果需要保持类型的安全性，则插入类型转换
* Generate bridge methods to preserve polymorphism in extended generic types.为了保持在扩展的泛型类型中保持多态性，生成桥方法。

Type erasure ensures that no new classes are created for parameterized types; consequently, generics incur no runtime overhead
类型擦除确保不会为参数化的类型创建新类。因此，泛型不会产生运行时开销。

javap -l -p -v -c可以看方法参数类型的签名。


# 杂项

Comparable<T>  Comparator<T>
	
[Sentinel(https://github.com/alibaba/Sentinel)
	
System.nanoTime与System.currentTimeMillis
* System.nanoTime : This method can only be used to measure elapsed time and is not related to any other notion of system or wall-clock time. 
* System.currentTimeMillis : the difference, measured in milliseconds, between the current time and midnight, January 1, 1970 UTC.


[](https://docs.oracle.com/javase/8/docs/api/java/lang/ref/package-summary.html#reachability)
* 强引用（StrongReference）.强引用是最为常见也是使用最为普遍的一种引用形式。如果一个对象具有强引用，那GC绝不会回收它。当内存空间不足，GC终止程序的正常执行，并抛出OutOfMemoryError错误。
* 软引用（SoftReference）.如果一个对象只具有软引用，那么当内存空间足够时，GC并不会回收它，但是当内存空间不足了，GC就会回收这些对象的内存。一旦软引用的对象被垃圾回收器收回，则该对象就不能被程序所使用。因此，软引用可用来实现内存敏感的缓存。
* 弱引用（WeakReference）.与软引用相比，弱引用的对象拥有更短暂的生命周期。GC一旦发现只具有弱引用的对象，不管当前内存空间是否足够，都会回收其内存空间。由于依赖于GC的执行，弱引用何时被回收是不可确定的。 弱引用用于实现那些不阻止其key(或值）被回收的正规化映射。  
* 虚引用（PhantomReference）

软引用和弱引用应用的场景
* 对象能够被重新构建和初始化
* 对象需要占用或消耗大量内存
 
可达性（Reachability）
从最强到最弱，可达性的不同等级反映了一个对象的生命周期。它们在操作上的定义如下：
* 强可达性（Strong Reachability）。如果一些线程无需遍历任何引用对象就能够到达一个对象，那么这个对象就是强可达的。
* 软可达性（Software Reachability）。如果一个对象不是强可达的，但可以通过遍历软引用到达，那么这个对象就是软可达的。
* 弱可达性（Weak Reachability）。如果一个对象既不是强可达的，也不是软可达的，但是能够通过遍历弱引用对象到达，那么这个对象就是弱可达的。当一个指向一个弱可达对象的弱引用被清除时，那么这个对象就能够被终止。
* 幻影可达性（Phantom Reachability）
在一些场景中在将一个对象注册到一个特定的引用对象后，程序需要知道这个对象的可达性发生了改变，即这个被引用的对象已经被GC所回收。

ReferenceQueue为Java代码提供了三个方法
* poll() 查询队列看是否存在应用。如果存在，则立即返回这个引用并从队列中将其删除，否则立即返回null。
* remove() 删除队列中下一个引用对象，如果不存在，则处于阻塞状态，直到存在引用对象为止。
* remove(long TimeOut) 删除队列中下一个引用对象，如果不存在，则处于阻塞状态，直到存在引用对象或者到达timeout时间为止。


ReferenceQueue: you don't enque stuff in there. gc will do for you. They allows you to know when some references get released, without having to check them one by one.

If the garbage collector discovers an object that is weakly reachable, the following occurs:
1. The WeakReference object's referent field is set to null, thereby making it not refer to the heap object any longer. 
2. The heap object that had been referenced by the WeakReference is declared finalizable. 
3. The WeakReference object is added to its ReferenceQueue. Then the heap object's finalize() method is run and its memory freed. 


```java
public static void main(String[] args) throws InterruptedException {
      SavePoint savePoint = new SavePoint("Random"); // a strong object

      ReferenceQueue<SavePoint> savepointQ = new ReferenceQueue<SavePoint>();// the ReferenceQueue
      WeakReference<SavePoint> savePointWRefernce = new WeakReference<SavePoint>(savePoint, savepointQ);

      System.out.println("SavePoint created as a weak ref " + savePointWRefernce);
      Runtime.getRuntime().gc();
      System.out.println("Any weak references in Q ? " + (savepointQ.poll() != null));
      savePoint = null; // the only strong reference has been removed. The heap
                        // object is now only weakly reachable

      System.out.println("Now to call gc...");
      Runtime.getRuntime().gc(); // the object will be cleared here - finalize will be called.

      System.out.println("Any weak references in Q ? " + (savepointQ.remove() != null));
      System.out.println("Does the weak reference still hold the heap object ? " + (savePointWRefernce.get() != null));
      System.out.println("Is the weak reference added to the ReferenceQ  ? " + (savePointWRefernce.isEnqueued()));

   }
```


[Reference Queues](http://learningviacode.blogspot.com/2014/02/reference-queues.html)


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

* Memory   
  1. Out-of-Memory Errors in the JVM   
  2. Excessive Garbage Collection   
  3. Improper Data Caching   
* Threads  
  4. Thread Deadlocks and Gridlocks   
* Database   
  5. Running Out of Database Connections   
  6. Slow Database Calls   
* Application/Code   
  7. Java Code-Level Issues   
  8. Java Application Server Bottlenecks   
* Infrastructure   
  9. Server Performance Problems
  10.Network Latency and Connectivity Issues

# Input/Output

[Title: Java I/O, NIO and NIO.2](http://libgen.gs/ads.php?md5=6163B19E28BC766958B2F6721E750175)

# 异常（Exception）

Java的异常机制包括Error和Exception两个部分，二者都继承了共同的基类Throwable。 只有实例化Throwable或者其子类的对象才能被Java虚拟机和Java throw 声明抛出。类似地，Throwable 或者其子类才能作为catch子句的参数类型。

作为Throwable的两个直接子类，Error和Exception按照常规被用于表明异常出现的不同位置。Error 通常属于JVM 运行中发生的系统级错误，虽然并不属于开发人员的范畴，但是有些Error还是由代码引起的，例如StackOverflowError 经常由递归操作超过栈的容量限制所引起。这类错误开发者一般无法挽救，只能靠JVM。Exception往往是应用级的，并假设程序员会去处理这些异常。Exception被进一步划分为两类：检查类型（checked）和未检查类型（unchecked）。检查类型的异常需要在编译时通过try..catch..语句来进行处理，如果Java 编译器发现没有所编译的代码没用使用try..catch.. 语句处理检查类型的异常，就会抛出一个编译异常。非检查类型的异常无法在编译时间进行验证，其大部分产生自变成错误，例如空对象、越界访问数组的元素或使用非法参数调用方法等。非检查类型的类型是RuntimeException的直接子类。

Java是目前主流编程语言中唯一一个推崇使用检查类型异常的。一方面，检查类型的异常破坏了代码，降低了代码的可读性，另一方面检查类型的异常增加了代码的健壮性和稳定性。

![Java异常分类](pics/Exception.JPG)



Fail Fast:就是要尽早的抛出异常，这样有有助于更加精确的定位出错的地点和原因。


Catch late:不要在方法内部过早的处理异常，特别是什么也不做的处理。一个好的经验是将异常处理交给调用者，方法只在及时的地方抛出异常，技术上实现的方式就是给方法声明throws，标出所有可能要抛出的异常。

Doc：文档的重要性，特别是非检查的异常，一定要在文档中注明。

在java多线程程序中，所有线程都不允许抛出未捕获的checked exception，也就是说各个线程需要自己把自己的checked exception处理掉。这一点是通过java.lang.Runnable.run() 方法声明(因为此方法声明上没有throw exception 部分)进行了约束。但是线程依然有可能抛出unchecked exception，当此类异常跑抛出时，线程就会终结，而对于主线程和其他线程完全不受影响，且完全感知不到某个线程抛出的异常(也是说完全无法catch 到这个异常)。JVM 的这种设计源自于这样一种理念：“线程是独立执行的代码片断，线程的问题应该由线程自己来解决，而不要委托到外部。”基于这样的设计理念，在Java 中，线程方法的异常(无论是checked 还是unchecked exception)，都应该在线程代码边界之内(run 方法内)进行try catch并处理掉.

但如果线程确实没有自己try catch某个unchecked exception，而我们又想在线程代码边界之外(run 方法之外)来捕获和处理这个异常的话，java 为我们提供了一种线程内发生异常时能够在线程代码边界之外处理异常的回调机制，即Thread对象提供的setUncaughtExceptionHandler(Thread.UncaughtExceptionHandler eh) 方法。

通过该方法给某个thread设置一个UncaughtExceptionHandler，可以确保在该线程出现异常时能通过回调UncaughtExceptionHandler 接口的public void uncaughtException(Thread t, Throwable e) 方法来处理异常，这样的好处或者说目的是可以在线程代码边界之外(Thread 的run() 方法之外)，有一个地方能处理未捕获异常。但是要特别明确的是：虽然是在回调方法中处理异常，但这个回调方法在执行时依然还在抛出异常的这个线程中.


1）为可恢复的错误使用检查型异常，为编程错误使用非检查型错误。

2）在finally程序块中关闭或者释放资源

3）在堆栈跟踪中包含引起异常的原因

4）始终提供关于异常的有意义的完整的信息

5）避免过度使用检查型异常

6）将检查型异常转为运行时异常。这是在像Spring之类的多数框架中用来限制使用检查型异常的技术之一，大部分出自于JDBC 的检查型异常，都被包装进DataAccessException 中，而（DataAccessException）异常是一种非检查型异常。这是Java最佳实践带来的好处，特定的异常限制到特定的模块，像 SQLException 放到DAO 层，将意思明确的运行时异常抛到客户层。


7）记住对性能而言，异常代价高昂

9）使用标准异常

10）记录任何方法抛出的异常



非检查异常 
    非检查异常为 Error 和 RuntimeException 及其子类, javac 在编译时，不会提示和发现这样的异常，不要求在程序处理这些异常。所以如果愿意，我们可以编写代码处理（使用 try…catch…finally ）这样的异常，也可以不处理。对于这些异常，我们应该修正代码，。如除 0 错误 ArithmeticException ，错误的强制类型转换错误 ClassCastException ，数组索引越界 ArrayIndexOutOfBoundsException ，使用了空对象 NullPointerException 等等


检查异常
    检查异常则是除了 Error 和 RuntimeException 的其它异常。javac强制要求程序员为这样的异常做预备处理工作（使用 try…catch…finally 或者 throws ）。在方法中要么用try-catch语句捕获它并处理，要么用 throws 子句
声明抛出它，否则编译不会通过。如 SQLException , IOException , ClassNotFoundException 等




float  BigDecimal: float不能精确比较，只能比较位于一定范围，Math.abs(f1-f2)<diff ，而BigDecimal能过精确比较，bd1.equals(bd2)


serialVersionUID和Serializable：serialVersionUID必须在序列化和反序列化过程中匹配。


chained exception:应用程序通常会通过抛出另一个异常来响应异常。实际上，第一个异常 导致 第二个异常。知道一个异常何时导致另一个异常非常有用。Chained Exceptions (链式异常) 帮助程序员执行此操作


# JSON


com.fasterxml.jackson

Jackson有三种方式处理Json：
1. 使用底层的基于Stream的方式对Json的每一个小的组成部分进行控制
2. 使用Tree Model，通过JsonNode处理单个Json节点
3. 使用databind模块，直接对Java对象进行序列化和反序列化

# XML

XML
①DOM：在现在的Java JDK里都自带了，在xml-apis.jar包里

②SAX：http://sourceforge.net/projects/sax/

③JDOM：http://jdom.org/downloads/index.html

④DOM4J

# 杂项

 Formatter



## SerialVersionUID

[SerialVersionUID in Java](https://www.geeksforgeeks.org/serialversionuid-in-java/)

Serialization at the time of serialization, with every object sender side JVM will save a Unique Identifier. JVM is responsible to generate that unique ID based on the corresponding .class file which is present in the sender system. Deserialization at the time of deserialization, receiver side JVM will compare the unique ID associated with the Object with local class Unique ID i.e. JVM will also create a Unique ID based on the corresponding .class file which is present in the receiver system. If both unique ID matched then only deserialization will be performed. Otherwise, we will get Runtime Exception saying InvalidClassException. This unique Identifier is nothing but SerialVersionUID.


There are also certain problem associations depending on the default SerialVersionUID generated by JVM as listed below: 
1. Both sender and receiver should use the same JVM with respect to platform and version also. Otherwise, the receiver is unable to deserialize because of different SerialVersionUID.
2. Both sender and receiver should use the same ‘.class’ file version. After serialization, if there is any change in the ‘.class’ file at the receiver side then the receiver is unable to deserialize.
3. To generate SerialVersionUID internally JVM may use complex algorithms which may create performance problems.


We can solve the above problem by configuring our own SerialVersionUID.
```java
private static final long serialVersionUID = -6849794470754667710L;
```


# 调度系统

[xxl-job](https://github.com/xuxueli/xxl-job) 

# Collection

* 是否有序
* 是否许可重复元素
* 是否许可null元素
* 
