

Atul S. Khot, Concurrent Patterns and Best Practices: Build scalable apps with patterns in multithreading, synchronization, and functional programming, 2018

并发的层次
* 架构
* 模式
* 数据结构

# Chapter 1 Concurrency – An Introduction


Concurrency entails communication between the concurrent entities. We will look at two primary concurrency models: message passing and shared memory.
并发性需要并发实体之间的通信。我们将会研究两种主要的并发模型：消息传递和共享内存。

When things happen at the same time, we say that things are happening concurrently. As far as this book is concerned, whenever parts of an executable program run at the same time, we are dealing with concurrent programming. We use the term parallel programming as a synonym for concurrent programming.
当事情同时发生时，我们就说事情处于并发。就本书而言，每当部分可执行程序在一个时间运行时，我们就正在使用并发编程。我们将术语并行编程作为并发编程的同义词。

并发的需求：
* 任务：更小的处理时间，更大的系统吞吐
* 设备：并行处理能力
* 处理速度的失配
* 设备复用

MapReduce pattern

Fault tolerance:redundant

Time sharing

We need to communicate and coordinate with the concurrently executing entities. 我们需要在并发执行的实体之间进行通信和协同。

There are two prominent models for concurrent communications:有两个重要的并发通信模型
* message passing 消息传递
* shared memory 共享内存

We start getting results faster, which means the system is responsive. 我们更快地开始得到结果，这意味着更快的响应。

## The message passing model 消息传递模型

pipes and filters design pattern


Flow control: Flow control is essential in ensuring that the producer (such as a fast speaker) does  not overwhelm the consumer (such as a listener). 流控：流控对于确保生产者（例如快速的发言者）不会冲垮消费者（列如一个听众）是必须的


Divide and conquer 分而治之

并发编程实际两个问题
* Coordination：协同是指线程的创建以及子任务的执行顺序。
* Communication：通信时指在线程间传递数据，这些数据可能时来自文件和数据库的原始输入数据，也可能是线程子任务的处理结果

This notion of state is very important to understand the various upcoming concurrency patterns. We could look at the state as data in a certain stage of processing. 状态这个概念对于下文中的各种并发模式非常重要。我们可以将状态看作特定阶段所处理的数据。

状态是指处理消息或者执行任务所需要的上下文数据，其往往代表处理或者执行的一个特定阶段。状态在特定线程或者node中维护，难以在线程或者node之间共享。
* 电子商务网站中的购物购物篮。
* TCP连接的状态

## The shared memory and shared state model 共享内存和共享状态模型

A thread of execution is a sequence of programming instructions, scheduled and managed by the operating system. A process could contain multiple threads; in other words, a process is a container for concurrently executing threads.
一个执行的线程是一个由操作系统调度和管理的编程指令序列。一个进程可能包括多个线程，换言之，一个进程是一个并发执行线程的容器。

Different concurrent processes have their own address space, while multiple threads within the same process share their address space. Each thread also has a stack of its own.
进程之间是相互独立的，即进程具有独立的内存地址空间和资源，包括文件描述符。在一个进程内的线程共享地址空间，但是每个线程具有自己的栈。这个栈用于处理过程调用，并且在局部范围的变量也在栈中创建。线程之间可以通过进程的全局内存来通信。

Access to the shared data structure needs to be synchronized correctly. This is surprisingly hard to achieve. 访问共享的数据结构需要正确地同步。这是令人吃惊地难以实现。


Threads interleaving – the need for synchronization 线程交织——对于同步的需求

线程一旦开始，其何时运行完全依赖于操作系统的调度，这使得如果不添加额外机制，多个线程会以交织方式获得CPU并且执行操作，即不同线程内的操作会以不可以预料的顺序执行。访问被共享的数据需要正确的同步。

Race conditions and heisenbugs
竞争条件和海森堡原理

A race condition means that the correctness of the program (the way it is expected to work) depends on the relative timing of the threads getting scheduled. 条件竞争意味着程序的正确性（程序预期的工作方式）依赖于线程被调度的相对时间。

These are heisenbugs—essentially nondeterministic and hard to reproduce. If we try debugging a heisenbug by attaching a debugger, the bug may disappear! 这是海森堡——基本上不确定的和难于复现。如果我们尝试通过添加一个调试器来调试一个海森堡，那么bug可能消失了。

Correct memory visibility and happens-before正确的内存可见性和happens-before

incorrect memory visibility. The synchronized keyword prevents the execution of critical sections by more than one thread. The synchronized keyword also makes sure the thread's local memory syncs up correctly with the shared memory. 不正确的内存可见性。sychronized关键字不仅阻止多于一个线程执行临界区，而且确保线程本地内存与共享内存之间相互同步。

What is this local memory? Note that on a multicore CPU, each CPU has a cache for performance reasons. This cache needs to be synced with the main shared memory. The cache coherence needs to be ensured so that each thread running on a CPU has the right view of the shared data.
什么是本地内存？需要注意在多核CPU中，由于性能原因，每个内核都会拥有cache。这个cache需要与主共享内存进行同步。需要确保缓存一致性(cache coherence)，使得在CPU上运行的每个线程都具有共享数据的正确视图。

When a thread exits a synchronized block, it issues a write barrier, thereby syncing the changes in its cache to the shared memory. On the other hand, when a thread enters a synchronized block, it issues a read barrier, so its local cache is updated with the latest changes in the shared memory.
当一个线程退出一个同步块时，其发起一个写屏障，从而将其cache中的更改同步到共享内存。另一个方面，当一个线程进入一个同步块时，其发起一个读屏障，因此会将共享内存中最新的更新同步到其局部cache中。

* write barrier
* read barrier

Java's volatile keyword guarantees correct memory visibility. Java的volatile关键字确保正确的内存可见性。

The volatile keyword, however, does not guarantee atomicity. volatile关键字并不保证原子性。

* pipes and filters design pattern
* Divide and conquer
* double-checked locking pattern

Sharing, blocking, and fairness
共享、阻塞和公平

thread states
* New
* Runnable
* Running
* Blocked
* Waiting
* Timed Wait
* Terminated

Java Thread.State
* NEW：创建了Thread，但是还没有执行start()
* RUNNABLE:执行了start(),但是可能还在等待操作系统调度
* BLOCKED：一个线程被阻塞并等待监视器锁、
* WAITING：一个线程无限期地等待另一个线程执行一个特定行为。一个线程处于等待状态是调用了如下方法
   * 没有过期时间的Object.wait
   * 没有过期时间的Thread.join with no timeout
   * LockSupport.park
* TIMED_WAITING：一个线程等待另一个线程执行一个特定行为，直到一个特定的等待时间。一个线程调用如下方法后将会进入定时等待状态
   * Thread.sleep
   * 有定期时间的Object.wait
   * 有定期时间的Thread.join with timeout
   * LockSupport.parkNanos
   * LockSupport.parkUntil
* TERMINATED：线程执行完毕。

Asynchronous versus synchronous executions 

Blocking operations are bad, as they waste resources.阻塞操作是不好的，因为其浪费了资源。阻塞操作是指当调用需要消耗较长时间时，线程会一直处于等待状态，直到调用返回结果之后才继续执行后续的代码。

Synchronous execution allows tasks to execute in a sequence, waiting for the current operation to complete before starting with the next。同步执行许可任务按照顺序执行，即等待当前操作完成之后才开始下一个操作。

在处理过程中某个调用采用阻塞方式，并不会增加整个处理流程的执行时间，但是会降低程序的并发性，也就是使得执行阻塞调用的线程处于阻塞状态，不能持续地执行代码，而从降低线程的平均执行效率。如果程序采用固定的线程数，那么阻塞方式会大大降低系统的吞吐率。因此，阻塞方式会带来两个直接问题
* 需要更多的线程资源
* 造成更多的上下文切换，从而导致性能损失


asynchronous model

分清楚两个不同的问题
* 阻塞和非阻塞
* 同步和异步

Instead of blocking and wasting the thread doing nothing, we could look at the workflow as a mix of unblocking and blocking tasks. We would then handle a blocking task using a future: an abstraction that will complete eventually and call us back with the results or an error.
相比于阻塞从而浪费线程什么也不做，我们可以将工作流看成非阻塞和阻塞任务的混合。我们通过一个Future来处理阻塞任务，Future是一种抽象，当最终完成的时候，要求我们返回处理结果或者错误。


future， Actor

Futures offer composability. They are monads. You can create a pipeline of future operations to perform higher-level computations. Future提供了可组合性。它们是单元，你能够创建一个Future操作的流水线，执行高级别的计算。


Java's nonblocking I/O

Java NIO (New IO)

* channels：A channel is just a bidirectional I/O stream. 一个管道仅仅是一个双向的输入/输出流。一个单一的的线程能够监控由应用打开的所有管道。在任何管道中接受到数据是一个事件，然后通知监听的线程已经接受到数据。
* buffers
* selectors：The selector uses event notification. 选择器使用事件通知：线程可以无需阻塞，就检查输入/输出是否完成。单一线程就能够处理多个并发连接。


## Of Patterns and paradigms 模式和范式

immutability

copy-on-write

active object

For example, how would you consume a legacy code base from multiple threads? The code base was written without any parallelism in mind, the state is strewn around, and it is almost impossible to figure out. 
例如，如何在多线程环境中使用遗留代码？这些遗留代码是在没有考虑并行性的情况下编写的，状态散落各处，几乎不可能搞清楚。

A brute-force approach could be to just wrap up the code in a big God object. Each thread could lock this object, use it, and relinquish the lock. However, this design would hurt concurrency, as it means that other threads would simply have to wait! Instead, we could use an active object.
一种暴力解决方法是将这些代码包装到一个大的God对象中。每个线程会锁住这个对象、使用它，然后释放锁。但是，这种设计会有害于并发，因为其意味着仅仅有一个线程执行，而其他线程不得不等待。作为一种替换方法，我们可以使用Active Object。


To use this active object, a proxy sits in between the caller threads and the actual code base. It converts each invocation of the API into a runnable and puts it in a blocking queue (a thread-safe FIFO queue). There is just one thread running in the God object. It executes the runnables on the queue one by one, in contrast to how a typical Java object method is invoked (passively). Here, the object itself executes the work placed on the queue, hence the term active object.
为了使用活跃对象，需要在调用线程和实际的代码之间放置一个代理。这个代理将每个API调用转换为一个Runnable，并将其插入阻塞代理（线程安全的先入先出队列）。在God对象中有一个线程在运行，并一个接着一个地执行队列中的Runable。相比于通常的Java对象方法被动地被调用，这个对象本身执行放置于队列中的工作，因此采用术语Active Object。

Event-driven architecture 事件驱动架构

Event-driven programming is a programming style in which code executes in response to an event, such as a keypress or a mouse click. In short, the flow of a program is driven by events.
事件驱动编程是一种编程风格，其执行代码以响应一个事件，例如一个按键或鼠标点击。简而言之，一个程序的流是由事件驱动的。


Event-driven architecture (EDA) helps in decoupling a system's modules. Components communicate using events, which are encapsulated in messages. A component that emits an event does not know anything about the consumers. This makes EDA extremely loosely coupled. The architecture is inherently asynchronous.
事件驱动架构有助于实现系统模块的解耦和。组件间使用封装在消息中的事件进行通信。发出事件的组件对于事件的消费者一无所知。这使得事件驱动架构的耦合性非常松散。这种架构在本质上就是异步的。


Reactive programming响应式编程

Reactive programming is a related programming paradigm. A spreadsheet is an excellent example of a reactive application. If we set a formula and change any column value, the spreadsheet program reacts and computes the new result columns. A message-driven architecture is the foundation of Reactive applications. A message-driven application may be event-driven, actor-based, or a combination of the two.
响应式编程是一种相关的编程范式。电子表格是响应式应用的一个很好的例子。如果我们设置一个公式并修改某一列的值，那么电子表格程序会作出响应并计算新的列结果。消息驱动架构是响应式应用的基础。一个消息驱动应用可以是事件驱动的或者基于actor或者两者的组合。


ReactiveX is a library for composing asynchronous and event-based programs by using observable sequences.

[ReactiveX](http://reactivex.io/intro.html)


The actor paradigm

Actors are the abstraction over threads. We write our code using the message passing model only. The only way of talking to an actor is by sending it a message.
Actor是在线程之上的抽象。我们仅仅通过使用消息传递模型编写我们的代码。与一个actor通话的唯一方式是向其发送一个消息。


We need to be aware of the underlying threading model, though. For example, we should always use the tell and not the ask pattern, as shown in the picture. The tell pattern is where we send a message to an actor and then forget about it, that is, we don't block for an answer. This is essentially the asynchronous way of doing things:
我们要理解底层的穿接模型。例如，我们总是使用tell模式，而不是ask模式。tell模型是我们发送一个消息给一个actor，然后忘记它，这意味着我们不好阻塞等待消息。这本质上是异步的做事方式。


An actor is a lightweight entity (threads are heavyweight).The creation and destruction of actors, monetarily speaking, is similar to the creation and destruction of Java objects.
一个actor是一个轻量级实体（线程是重量级的）。从消耗上来说，创建和销毁actor类似于创建和消耗Java对象。




Message brokers

A message broker is an architectural pattern for enabling application integrations via a message-driven paradigm.Integrations are vital to an enterprise where different applications are made to cooperate with each other.
Message broker是一种使得应用可以通过消息驱动范式集成的架构模式。对于那些构建不同应用以相互协作的企业而言，集成是必不可少的。



software transactional memory 软件的事务性内存


The software transactional memory is a concurrency control mechanism on similar lines. It, again, is a different paradigm, an alternative to lock-based synchronization.

commit， roll back

optimistic locking

Composability is a big theme: lock-based programs do not compose. You cannot take two atomic operations and create one more atomic operation out of them. You need to specifically program a critical section around these. STM, on the other hand, can wrap these two operations inside a transaction block, as shown in the preceding diagram.
可组合性是一个大主题：基于锁方式的程序不能组合。你不能使用两个原子操作创建另一个原子操作。

Parallel collections

线程安全的合集
* 必须保证操作安全性，避免并发读写或写写造成问题。
* 尽量提高操作并发性，尽可能地获取更高的操作吞吐。




# Chapter 2 A Taste of Some Concurrency Patterns 


## A thread and its context 线程和其上下文

the thread context. This context helps a thread keep its runtime information independent of another thread. The thread context holds the register set and the stack. 线程上下文帮助一个线程维护独立于其他线程的运行信息。线程上下文持有线程运行所需的寄存器集合和栈。

The final and local variables (including function arguments) are always thread safe. You don't need any locks to protect them. The final variables are immutable (that is, read-only) so there is no question of multiple threads changing the value at the same time.
常量和本地变量（包括函数参数）都是线程安全的。你无需使用任何锁来保护它们。常量是不变的（也就是只读的），因此没有多个线程在同一事件修改一个值的问题。

Mutable Static and Instance Variables are unsafe! If these are not protected, we could easily create Race Conditions.
可变静态变量和实例变量（对象属性）都不是线程安全的。如果没有保护，会非常容易形成竞争条件。

## Race conditions 竞争条件


Singleton and factory method are two of the many creational design patterns from the famous Gang Of Four (GOF) book.

The need for singletons is pretty common; a classic example of a singleton is a logging service. Thread pools are also expressed as singletons (we will be looking at thread pools in an upcoming chapter). Singletons are used as sentinel nodes in tree data structures, to indicate terminal nodes.


数据的可见性是数据的多个副本所致。由于CPU的操作速度要远远快要主存访问速度，为了优化性能，CPU会将主存中的数据预先装载到访问速度更快的cache中，并直接操作cache中的数据。这种情况导致同一个数据的多个副本在不同内核或者线程中可能并不一致，例如在一个线程更改了一个数据后，另一个线程读取的数据还是之前过期的数值，这被称为线程对于数据的更改不可见。为此，可以在写入数据后，使用Store Barrier以保持cache中的数据被写回到内存或者广播到其他cache（如果该cache缓存该数据）。在读取一个数据之前，使用Load Barrier，以确保cache中的数据与主存中的保持一致。

volatile keyword 


A store barrier makes all CPUs (and threads executing on them) aware of the state change. Similarly, a Load Barrier makes all CPUs read the latest value, thereby avoiding the stale state issue.
Store Barrier使得所有CPU（和在其上执行的线程）意识到状态已经改变。类似地，Load Barrier使得所有CPU读取最新的值，从而避免状态失效问题。


https://dzone.com/articles/memory-barriersfences

### The Monitor Pattern监视器模式

These steps should be atomic, that is, indivisible; either a thread executes all of these operations or none of them. The monitor pattern is used for making such a sequence of operations atomic. Java provides a monitor via its synchronized keyword.
这些步骤需要是原子的，也就是说，不可分割的，或者一个线程执行全部的操作，或者一个都不执行。监视器模式用于将这样的操作序列原子化。Java通过synchronized关键字提供一个监视器。

Every Java object has a built-in lock, also known as an intrinsic lock. A thread entering the synchronized block acquires this lock. The lock is held till the block executes. When the thread exits the method (either because it completed the execution or due to an exception), the lock is released。
每个Java对象都拥有一个内置的锁，也被称为内置锁。一个进入synchronized块的线程需要获取这个锁。这个线程持有该锁，直到整个块执行完为止。当线程结束这个方法（无论是执行完毕退出，还是由于异常跳出），锁都会被释放。

The synchronized blocks are reentrant: the same thread holding the lock can reenter the block again.
synchronized块是可重入的：持有对应锁的同一个线程可以再次进入块。


Thread safety, correctness, and invariants


An invariant is a good vehicle for knowing the correctness of the code. 不变性是一个理解代码正确性的好工具。


Sequential consistency 顺序一致性

Another tool for learning more about concurrent objects is Sequential Consistency.

Visibility and final fields可见性和final字段
