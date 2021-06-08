


# 线程(Thread)

线程相关的类和接口包括
* Thread类
* Runnable接口
* ThreadLocal类
* ThreadFactory接口

start()方法用于创建线程，其由本地方法实现，而run() 方法用于调度和运行线程。


Java 中如何停止一个线程？JDK 1.0 本来有一些像 stop ()， suspend () 和 resume ()的控制方法但是由于潜在的死锁威胁因此在后续的 JDK 版本中他们被弃用了，之后 Java API 的设计者就没有提供一个兼容且线程安全的方法来停止一个线程。


daemon threads

两类线程：用户线程（user thread）和精灵线程（daemon thread）

程序是从main()方法开始运行一样，而新线程是从run()方法开始运行。线程之间是相对独立的，即每一个进程都有自己的Java栈存储局部变量，也就是说，一个线程中每一个方法的局部变量都是和其他线程完全分离的，而对象内部定义的属性变量(不是在方法中定义的实例变量)可以在Java 线程之间共享。


通过调用Thread对象的start()方法将导致JVM调用本地方法分配线程资源，而JVM则负责调用run()方法调度执行线程。主线程(调用start()方法的线程)并不需要调用run() 方法，虽然可以调用run()方法，并且其效果相当于一个线程调用另一个对象的方法。

存在两种创建新线程的方法：
* 继承方式：声明一个继承Thread类的子类，该子类必须覆盖Thread的run()方法。
* 委托方式：声明一个实现Runnable接口的类，该类实现了run()方法，并且作为一个Thread对象构造函数的参数。



Java通过int类型的priority表示线程的优先级，最大优先级不能超过MAX_PRIORITY(10)而最小优先级不能低于MIN_PRIORITY(1)，其默认优先级为5。

范围     |   用途      |
| :------------ | :------------ |
| 10     |   Crisis management（应急处理）   |
| 7-9    |  Interactive, event-driven（交互相关，事件驱动）  |
| 4-6    |    IO-bound（IO密集类） |
| 2-3    |    Background computation（后台计算）  |
| 1      |  Run only if nothing else can（仅在没有任何线程运行时运行的）  |



run()并不会抛出任何异常，而是由Thread.UncaughtExceptionHandler接口的实现类来处理未被捕获的异常。

sleep()方法使得当前正在执行的调用线程进入TIMED\_WAITING状态，暂停执行一段时间，从而让出CUP 给其他线程。 作为一个静态方法，其不能改变对象所专有的属性，因此不会放弃出CPU 之外的任何资源，也不会失去任何监视器的所有权。此外，中断可以终止线程休眠，并抛出InterruptedException。 因此，sleep() 方法不能精确保证休眠的时间。需要注意的是一个线程并不能通过sleep 方法使得另一个线程暂停，也就是说如果一个线程调用另一个进程t 的sleep() 方法，t 并不会终止运行。


suspend()和resume()方法不推荐使用，而是由LockSupport的park()和unpark()方法所替代。


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


isInterrupted()方法检测当前线程是否被中断，该线程的中断状态不会被此方法的影响。

interrupted()方法是一个静态方法，检测当前线程是否被中断。该线程的中断标识会被此方法清除，换言之，如果该方法被连续调用两次，则除非在两次调用之间再次被中断，否则第二次将返回false




线程状态（Thread.State）
* NEW：刚刚生成线程对象，还没有执行start()
* RUNNABLE：一个处于RUNNABLE状态的线程正在Java虚拟机中执行，当时也可能正在等待操作系统分配其他资源，如处理器。
*  BLOCKED：一个处于BLOCKED状态的线程正在等待一个监视器锁。换言之，一个被阻塞的线程正在等待一个监视器锁，以便进入一个synchronized 块/方法或者在调用Object.wait()之后再次进入一个synchronized块/方法。
* WAITING：一个线程处于WAITING状态是因为调用如下三个方法之一
   * 没有超时设置的Object.wait()
   * 没有超时设置的Thread.joint()
   * LockSupport.park()
* TIMED_WAITING：一个线程处于TIMED\_WAITING状态是因为调入如下几个方法之一
   * Thread.sleep()
   * 具有定时设置的Object.wait()
   * 具有定时设置的Thread.join()
   * LockSupport.parkNanos
   * LockSupport.parkUntil
* TERMINATED：一个处于TERMIINATED的线程已经执行完毕。
