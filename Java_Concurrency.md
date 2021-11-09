


# 线程(Thread)

线程相关的类和接口包括
* Thread类
* Runnable接口
* ThreadGroup类
* ThreadLocal类
* ThreadFactory接口


## 线程介绍
两类线程
* 用户线程（user thread）
* 守护线程（daemon thread）。

守护线程
* 用于在后台提供服务或者支撑任务
* 其生命周期依赖于用户线程
可以通过调用Thread对象的setDaemon(true)方法来设置守护线程。在使用守护线程时需要注意一下几点：
* thread.setDaemon(true)必须在thread.start()之前设置，否则抛出一个IllegalThreadStateException异常。 
* 在Daemon线程中产生的新线程也是Daemon的。



程序线程是从main()方法开始运行一样，而程序中所创建的新线程是从Thread对象的run()方法开始运行。线程之间是相对独立的，即每一个进程都有自己的Java栈存储局部变量，也就是说，一个线程中每一个方法的局部变量都是和其他线程完全分离的，而对象内部定义的属性变量(不是在方法中定义的实例变量)可以在Java 线程之间共享。

存在两种直接创建新线程的方法：
* 继承方式：创建一个继承自Thread类的子类，并覆盖父类的run()方法。
* 委托方式：创建一个实现Runnable接口的类，并实现接口的run()方法，然后将其作为一个Thread构造函数的参数。
在创建线程之后，上述两种方法都需要调用Thread对象的start()方法，开始一个线程，线程状态由New变为RUNNABLE，JVM调用本地方法分配线程资源，而JVM则负责调用run()方法调度执行线程。主线程(调用start()方法的线程)并不需要调用run()方法。

间接创建线程采用两种方式
* 工厂方法ThreadFactory接口
* 线程池ExecutorService，在本质上ExecutorService也是借助于ThreadFactory创建线程的


Java通过int类型的priority表示线程的优先级，最大优先级不能超过MAX_PRIORITY(10)而最小优先级不能低于MIN_PRIORITY(1)，其默认优先级为5。

范围     |   用途      |
| :------------ | :------------ |
| 10     |   Crisis management（应急处理）   |
| 7-9    |  Interactive, event-driven（交互相关，事件驱动）  |
| 4-6    |    IO-bound（IO密集类） |
| 2-3    |    Background computation（后台计算）  |
| 1      |  Run only if nothing else can（仅在没有任何线程运行时运行的）  |
可以通过调用Thread对象的setPriority(int newPriority)设置线程优先级。

线程状态（Thread.State）
* NEW：刚刚生成线程对象，还没有执行start()
* RUNNABLE：一个处于RUNNABLE状态的线程正在Java虚拟机中执行，当时也可能正在等待操作系统分配其他资源，如处理器。
* BLOCKED：一个处于BLOCKED状态的线程正在等待一个监视器锁。换言之，一个被阻塞的线程正在等待一个监视器锁，以便进入一个synchronized 块/方法或者在调用Object.wait()之后再次进入一个synchronized块/方法。
* WAITING：一个线程处于WAITING状态是因为调用如下三个方法之一
   * 没有超时设置的Object.wait()
   * 没有超时设置的Thread.joint()
   * LockSupport.park()
* TIMED_WAITING：一个线程处于TIMED_WAITING状态是因为调入如下几个方法之一
   * Thread.sleep()
   * 具有定时设置的Object.wait()
   * 具有定时设置的Thread.join()
   * LockSupport.parkNanos
   * LockSupport.parkUntil
* TERMINATED：一个处于TERMIINATED的线程已经执行完毕。
Java线程的RUNNABLE状态含盖了Linux线程的READY和RUNNING状态。之所以Java线程中不包含RUNNING状态，是因为进程/线程的调度是由操作系统负责，而JVM作为运行在操作系统之上的应用，无法感知到自己是否正在使用CPU，即是处于RUNNING状态，还是READY状态。类似于在一个平稳运行的船中，无法确定去是运行，还是停靠在码头上。

Thread.sleep(long millis)是一个静态方法，调用该方法使得当前正线程进入TIMED_WAITING状态，暂停执行一段时间，从而让出CUP给其他线程。作为一个静态方法，其不能改变对象所专有的属性，因此不会放弃出CPU之外的任何资源，也不会失去任何监视器的所有权。此外，中断可信号能终止TIMED_WAITING状态，从而唤醒线程处理InterruptedException。
sleep()方法不能精确保证休眠的时间
* 过了休眠时间后，线程可能不会立即执行，需要等待操作系统调度。
* 虽然还在休眠时间内，但所休眠的线程可能被中断信号唤醒。
sleep方法是一个静态方法，因此不可能通过调用sleep方法使得一个线程暂停运行，也就是说，如果一个线程调用另一个进程t的sleep()方法，线程t并不会进入休眠状态。

 If this thread is blocked in an invocation of the wait(), wait(long), or wait(long, int) methods of the Object class, or of the join(), join(long), join(long, int), sleep(long), or sleep(long, int), methods of this class, then its interrupt status will be cleared and it will receive an InterruptedException.

If this thread is blocked in an I/O operation upon an InterruptibleChannel then the channel will be closed, the thread's interrupt status will be set, and the thread will receive a ClosedByInterruptException.

If this thread is blocked in a Selector then the thread's interrupt status will be set and it will return immediately from the selection operation, possibly with a non-zero value, just as if the selector's wakeup method were invoked.

If none of the previous conditions hold then this thread's interrupt status will be set. 
Thread提供了三个与中断有关的方法
* interrupt() ，用于中断当前线程，
  * 如果线程是由于调用Object方法的join()、join(long)、join(long, int)、sleep(long)或者sleep(long, int)方法而被阻塞的，那么中断标识会被清除，而线程会收到一个InterruptedException。
  * 如果线程是由于在一个InterruptibleChannel上的I/O操作而被阻塞，那么这个线程的中断标识会被设置，并且会收到一个ClosedByInterruptException。
  * 如果线程是由于在一个Selector中被阻塞，那么这个线程的中断标识会被设置，并且会从selection操作理解返回，可能会由一个非零值，类似于调用selector的wakeup方法。
  * 如果不是上述的情况，那么这个线程的中断标识会被设置
* interrupted()，静态方法，测试当前线程是否已经被中断。该线程的中断标识会被此方法清除，换言之，如果该方法被连续调用两次，则除非在两次调用之间再次被中断，否则第二次将返回false
* isInterrupted()，测试一个线程是否被已经被中断，但是不会影响线程的中断标识。

Java在很早期的版本中分别给出了stop()、suspend()和resume ()三个方法用于控制线程的运行，但是很快在随后的版本中弃用了上述三个方法。

实现取消任务的最佳技术是使用线程的中断状态，这个状态由interrupt()设置，可被isInterrupted() 检测到，通过Thread.interrupted()清除。
interrupt()方法并不会中断一个正在运行的线程，而是设置中断状态并且通过抛出InterruptedException的方式使线程退出阻塞状态，在抛出InterruptedException后，中断状态被清空。
* 在使用Object对象的wait()方法以及Thread对象的join()和Thread.sleep()方法时，通过interrupt() 可以终结线程的阻塞状态。
* 如果该线程在可中断的通道上的 I/O 操作中受阻，则该通道将被关闭，该线程的中断状态将被设置并且该线程将收到一个 ClosedByInterruptException。



有两种情况线程会保持休眠而无法检测中断状态或接收InterruptedException：在同步块中和在不可中断IO的阻塞中。线程在等待同步方法或同步块的锁时不会对中断有响应。


多步取消（Multiphase cancellation）


yield()方法是停止当前线程，让同等优先权的线程运行。如果没有同等优先权的线程，那么yield()方法将不会起作用。


join()方法使当前调用线程停止运行进入WAITING状态，直至被调用线程终止后才继续运行。换言之，如果当前线程调用进程t的join()方法，则当前线程会停止运行直到进程t终止。join()是通过调用wait() 来实现，如果isAlive()，则一直wait(delay)


wait()方法将会使得调用对象所在的线程进入WAITING状态，并释放被调用对象的内置锁。如果当前线程不是被调用对象内置锁的拥有者，则会抛出IllegalMonitorStateException异常。在调用wait()后，可以被中断并抛出InterruptedException，因此如果依赖于特定条件才能继续执行，在

```java
     synchronized (obj) {
         while (<condition does not hold>) {
            try{
                obj.wait();
            } catch (InterruptedException ie) {

            }
         }
         ... // Perform action appropriate to condition
     }
```
notify()方法唤醒被调用对象内置锁上等待的单个线程。当它被一个notify()方法唤醒时，等待池中的线程就被放到了锁池中。该线程将等待从锁池中获得机锁，然后回到wait()前的中断现场，从wait()。

notifyAll()唤醒在此上等待的所有线程。

o.waite()和o.notify()必需synchronized(o)修饰的方法或者块中，也就是说waite()和notify()依赖于被调用对象的监视器。


Thread的run()并不会抛出任何异常，但是线程本身会因为所执行的代码抛出一个异常而终止本线程的执行。对于
* 需要长时间运行的服务线程，
* 向线程池提交的任务线程或者工作线程
需要在run()方法中主动地捕获和处理异常，例如如下服务线程，需要一直运行。知道调用stop()方法终止该服务线程为止。
```java

    public void stop() {
        this.doesStop = true;
    }

    @Override
    public void run(){
        while(doesStop){
            try{
                \\do somethine
            }(Throwable e) {
                \\ do log
            }finally{
                \\release resources
            }
        }
    }

    private volatile boolean doesStop = false;

```

此外，JDK中还提供了Thread.UncaughtExceptionHandler接口，当线程由于一个未捕获的异常而终止时，Java虚拟机会调用其处理异常。
```java
    @FunctionalInterface
    public interface UncaughtExceptionHandler {
        /**
         * Method invoked when the given thread terminates due to the
         * given uncaught exception.
         * <p>Any exception thrown by this method will be ignored by the
         * Java Virtual Machine.
         * @param t the thread
         * @param e the exception
         */
        void uncaughtException(Thread t, Throwable e);
    }
```

可以通过两种方式设置UncaughtExceptionHandler。
* 通过Thread类的静态方法setDefaultUncaughtExceptionHandler(UncaughtExceptionHandler eh)，设置默认UncaughtExceptionHandler。
* 通过Thread对象的方法setUncaughtExceptionHandler(UncaughtExceptionHandler eh)，设置特定对象的UncaughtExceptionHandler。

每个Thread对象中存在属性threadLocals，其类型为ThreadLocalMap，为一个定制化的map。采用一个数组Entry[] table保存记录，每个ThreadLocal对象中包含属性threadLocalHashCode，其对应一个自增整数，为ThreadLoacal对象在数组table中初始位置，由于。如下所示，每个记录Entry是WeakReference的子类。WeakReference保存key，在Entry中采用Object value来保存value，

在执行如下两个方法时
* 部分执行get()时，包括：1）获取初始值，即首次执行get()时；2）当前ThreadLocal对象对应的key已经被GC回收
* set(T value)
* remove()
会清理那些key已经被GC回收的记录。


ThreadLocalMap

```java
static class ThreadLocalMap {

        /**
         * The entries in this hash map extend WeakReference, using
         * its main ref field as the key (which is always a
         * ThreadLocal object).  Note that null keys (i.e. entry.get()
         * == null) mean that the key is no longer referenced, so the
         * entry can be expunged from table.  Such entries are referred to
         * as "stale entries" in the code that follows.
         */
        static class Entry extends WeakReference<ThreadLocal<?>> {
            /** The value associated with this ThreadLocal. */
            Object value;

            Entry(ThreadLocal<?> k, Object v) {
                super(k);
                value = v;
            }
        }
}
```

VarHandle是在JDK 9中引入的一个工具 

FutureTask的代码片段
```java
    // VarHandle mechanics
    private static final VarHandle STATE;
    private static final VarHandle RUNNER;
    private static final VarHandle WAITERS;
    static {
        try {
            MethodHandles.Lookup l = MethodHandles.lookup();
            STATE = l.findVarHandle(FutureTask.class, "state", int.class);
            RUNNER = l.findVarHandle(FutureTask.class, "runner", Thread.class);
            WAITERS = l.findVarHandle(FutureTask.class, "waiters", WaitNode.class);
        } catch (ReflectiveOperationException e) {
            throw new ExceptionInInitializerError(e);
        }

        // Reduce the risk of rare disastrous classloading in first call to
        // LockSupport.park: https://bugs.openjdk.java.net/browse/JDK-8074773
        Class<?> ensureLoaded = LockSupport.class;
    }

```

Callable, Future, and FutureTask ...

LockSupport.


CompletionService-->ExecutorCompletionService

通过线程池ThreadPoolExecutor，实现了任务（Runnable/Callable）创建和任务执行之间的去耦合，而使用ExecutorCompletionService，又能够进一步实现任务执行（生产结果）和结果处理（消费结果）之间的去耦合，非常适合于非阻塞调用（在Caller一方）和异步调用（在Callee一方）。ExecutorCompletionService有一个内部类QueueingFuture，其是FutureTask的子类，在任务执行完毕后自动加入阻塞队列，而结果处理一方可以通过take或者poll方法（本质上是take和poll这个阻塞独立）获得执行完毕的Future，并进行后续处理过程，从而避免自己编写定时轮训Future的过程。


-XX:+UseBiasedLocking

# Locks

* ReentrantLock
* StampedLock
* ReentrantReadWriteLock

底层支持
* AbstractQueuedSynchronizer/AbstractQueuedLongSynchronizer
* LockSupport


StampedLock
基于能力的锁，针对于读/写访问具有三种模式。StampedLock的状态由一个版本和模式组成。

Semaphore


CLH lock is Craig, Landin, and Hagersten (CLH) locks, CLH lock is a spin lock, can ensure no hunger, provide fairness first come first service. The CLH lock is a scalable, high performance, fairness and spin lock based on the list, the application thread spin only on a local variable, it constantly polling the precursor state, if it is found that the pre release lock end spin.

* Cache Consistency: order of reads and writes between memory locations. What is the model presented to the programmer?
* Cache Coherence: data movement caused by reads and writes for a single memory location. How is the system implementing the model in the presence of private caches?


Cache coherence in computer architecture refers to the consistency of shared resource data that is stored in multiple local caches. Cache coherence is the discipline that ensures that changes in the values of shared operands are propagated throughout the system in a timely manner.


https://www.geeksforgeeks.org/difference-between-cache-coherence-and-memory-consistency/

MCS也是人名简写：John M. Mellor-Crummey and Michael L. Scott


Nir Shavit-Modern High-Performance Locking