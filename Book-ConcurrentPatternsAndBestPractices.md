

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

Blocking operations are bad, as they waste resources.阻塞操作是不好的，因为其浪费了资源。阻塞操作是指当调用需要消耗较长时间时，线程等待调用返回之后才继续执行后续代码。

Synchronous execution allows tasks to execute in a sequence, waiting for the current operation to complete before starting with the next。同步执行许可任务顺序执行，即等待当前操作完成之后才开始下一个操作。

在处理过程中某个调用采用阻塞方式，并不会增加整个处理过程的执行时间，但是会降低程序的并发性，也就是使得这些阻塞调用的线程处于阻塞状态，不能持续地执行代码，降低每个线程平均执行效率。如果程序采用固定的线程数，那么阻塞方式会大大降低系统的吞吐率。


asynchronous model

分清楚两个不同的问题
* 阻塞和非阻塞
* 同步和异步

Instead of blocking and wasting the thread doing nothing, we could look at the workflow as a mix of unblocking and blocking tasks. We would then handle a blocking task using a future: an abstraction that will complete eventually and call us back with the results or an error.
相比于阻塞并浪费线程什么也不做，我们可以将工作流看成非阻塞和阻塞任务的混合。我们通过一个Future来处理阻塞任务，Future是一种抽象，当最终完成的时候，要求我们返回处理结果或者错误。


future， Actor

Futures offer composability. They are monads. You can create a pipeline of future operations to perform higher-level computations. Future提供了可组合性。它们是单元，你能够创建一个Future操作的流水线，执行高级别的计算。


Java's nonblocking I/O

* channels：A channel is just a bidirectional I/O stream.
* buffers
* selectors：The selector uses event notification




immutability

copy-on-write

active object


Event-driven architecture

Reactive programming

ReactiveX is a library for composing asynchronous and event-based programs by using observable sequences.

[ReactiveX](http://reactivex.io/intro.html)


The actor paradigm

Message brokers

software transactional memory

parallel collections

# Chapter 1 
