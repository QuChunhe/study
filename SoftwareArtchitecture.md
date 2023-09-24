

软件架构由多个不同的架构组成，每个架构是软件的一个视图，用于刻画软件系统的一个方面
* 业务架构
* 功能架构
* 技术架构
* 数据架构
* 集成架构
* 部署架构
* a


eTOM，是enhanced Telecom Operations Map的英文首字母缩写，英文全称为enhanced Telecom Operations MapTM(eTOM)，即增强的电信运营图(eTOM)，是信息和通信服务行业的业务流程框架。客户（Customer）、用户（User）和账户(Account)。eTOM 引入是电信行业营销模型转向“以客户为中心”的理念而产生的成果。围绕客户建立用户和账户。这三个是相互关联的实体，这种关联只是一个归属和映射的关系，而三个实体本身是相互独立的，分别是体现完全不同的几个域的信息。

<<Patterns of Enterprise Application Architecture>>

* Usually, there are two common elements:
  * One is the highest-level breakdown of a system into its parts;
  * The other, decisions that are hard to change.
* There are multiple architectures in a system, and the view of what is architecturally significant is one that can change over a system's lifetime.


Thinking About Performanc
* Response time
* Responsiveness
* Latency
* Throughput
* Load
* Load sensitivity
* efficiency
* The capacity of a system
* Scalability


Layering（分层）
* Use to break apart a complicated software system
  * The principal subsystems in software arranged similar to some form of layer cake
  * The higher layer uses various services defined by the lower layer, but the lower layer in unware of the higher layer
* The hardest part of a layered architecture is deciding what layers to have and what the responsibility of each layer should be


[微服务架构及其最重要的 10 个设计模式](https://www.infoq.cn/article/Kdw69bdimlX6FSGz1bg3)

[微服务架构设计模式](https://www.cnblogs.com/xmzJava/p/12637238.html)

[六种微服务架构的设计模式](https://blog.csdn.net/zl1zl2zl3/article/details/103556901)

[《微服务架构设计模式》之二：服务的拆分策略](http://www.uml.org.cn/wfw/202004242.asp?artid=23208)



Work smarter not harder

* Make code recognizable to other developer
* Easy to find information
* Helps decision-making process

# Architecural Pattern

Categories of Pattern
* Application Landscape pattern
  * Monolith
  * N-tier
  * Service-oriented
  * Microservices
  * Serverless
  * Peer-to-peer
* Application Structure pattern
  * Layered
  * Microkernel
  * Command Query Responsibility Segregation (CQRS)
  * Event Sourcing
  * Command Query Responsibility Segregation and Event Sourcing combined
* User Interface patter
  * Model-view-controller (MVC)
  * Model-view-presenter (MVP)
  * Model-view-viewmodel (MVVM)


As I think about MVC I see two principal separations: separating the presentation from the model and separating the controller from the view.


Reactor： 
The Reactor architectural pattern allows event-driven applications to demultiplex and dispatch service requests that are delivered to an application from one or more clients.
*  'thread-per-connection' model
* event-drived model

a process or thread-based model to handle connections。


Proactor： 
The Proactor architectural pattern allows event-driven applications to efficiently demultiplex and dispatch service requests triggered by the completion of asynchronous operations, to achieve the performance benefits of concurrency without incurring certain of its liabilities.



Asynchronous Completion Token：

The C10K problem (Concurrently handle 10,000 connections.)
1. Event-Driven Programming: This involves organizing the server so that it reacts to events (like the arrival of a new connection or the receipt of data) instead of maintaining a thread for each connection. The server essentially “waits” for events and reacts as they occur.
2.  Multiplexing I/O Operations: Multiplexing involves handling multiple inputs and outputs over a single file descriptor using system calls like select, poll, and epoll.
3. Thread Pooling: This technique involves creating a pool of worker threads at startup, which can be reused to handle multiple connections, thereby reducing the overhead associated with thread creation and destruction.
4. Networking and OS Optimizations: Networking hardware and operating systems have also been enhanced to better support a large number of concurrent connections. These enhancements include improved TCP/IP implementations, advancements in network interface cards, and better scheduling algorithms in the operating system kernel.

[The Secret to 10 Million Concurrent Connections -The Kernel is the Problem, Not the Solution](http://highscalability.com/blog/2013/5/13/the-secret-to-10-million-concurrent-connections-the-kernel-i.html)
C10M Problem


* minimum context-switches
* low-memory footprint,

# Design Pattern

Creational design patterns abstract the instantiation process.
* Abstract Factory: 定义factory接口
  * Provide an interface for creating families of related or dependent objects without specifying their concrete classes.
  * javax.sql.DataSource
* Builder:enable***、add***、with***，具有哪些特性和能力。
  * Separate the construction of a complex object from its representation so that the same construction process can create different representations.
  * GsonBuilder 
* Factory Metohod
  * Define an interface for creating an object, but let subclasses decide which class to instantiate. Factory Method lets a class defer instantiation to subclasses .
  * java.util.concurrent.ThreadFactory  Integer.valueOf
* Prototype
  * Specify the kinds of objects to create using a prototypical instance, and create new objects by copying this prototype.  
  * 很多Collection的实现类，实现了clone方法。
* Singleton
  * Ensure a class only has one instance, and provide a global point of access to it.
  * Runtime

JDBC连接数据库的两种方式：DriverManager及DataSource（DBCP,C3P0,druid）

XMLReaderFactory