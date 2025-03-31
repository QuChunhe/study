

[Who Needs an Architect?](https://martinfowler.com/ieeeSoftware/whoNeedsArchitect.pdf)

[The Architect’s Blueprint: Understanding Software Styles and Patterns with Cheatsheet](https://readmedium.com/the-architects-blueprint-understanding-software-styles-and-patterns-with-cheatsheet-5c1f5fd55bbd)

系统思维（System thinking）

* 系统：A system is a set of entities and their relationships, whose functionality is greater than the sum of the individual entities.
* 涌现（emergence）

>“A system is not the sum of its parts, but the product of the interactions of those >parts.”   -- russell ackoff
> “The whole is more than the sum of the parts.” -- aristotle, Metaphysics

* 涌现原则（Principle of Emergence）

从如下两个方面入手新系统
* 用户：哪些用户？如何使用和操作系统？
* 业务：业务规则、业务流程和业务处理
* 数据：有哪些数据？这些数据的生产、使用和销毁过程？


软件架构由多个不同的架构组成，每个架构是软件的一个视图，用于刻画软件系统的一个方面
* 业务架构
* 功能架构
* 技术架构
* 数据架构
* 集成架构
* 部署架构
* 安全架构

上述架构既相互关联和相互影响，又有侧重，共同构建了一个系统的架构全貌。


架构师
* 在一定条件的约束下（成本投入和开发周期等约束）
* 设计上述多个架构（文档、接口或者定义）
* 从而满足业务需求和性能指标
* 并简化代码开发、测试、部署和运维

为用户解决实际问题，为用户创造额外价值

架构的几个关键
* 满足业务需求
* 满足客观约束:比如成本成本
* 简化代码开发和部署
* 指标
  * Availability
  * Performance
  * Reliality
  * Scalaility
  * Manageability

In most successful software projects, the expert developers working on that project have a shared understanding of the system design. This shared understanding is called ‘architecture.’ This understanding includes how the system is divided into components and how the components interact through interfaces. These components are usually composed of smaller components, but the architecture only includes the components and interfaces that are understood by all the developers.


架构服务于业务，模块遵循架构要求。

上述架构的用户
* 开发人员
* 运维人员

架构的难点是粒度，要使得开发人员
* 对于系统有一个清晰的和简单的共同理解。
* 既无需陷入细节，增加认知负担，又能相对独立地开发

把握方向，在满足约束和需求的同时，发挥开发人员的才智，不要使得架构师成为瓶颈。
* 太粗：缺乏指导意义，无法规范开发
* 太细：1）增加架构师负担，增加开发人员认知成本；2）不能支持变化

例如，数据架构
* schema层次，详细表定义
* 电信eTOM 三户模型


eTOM，是enhanced Telecom Operations Map的英文首字母缩写，英文全称为enhanced Telecom Operations MapTM(eTOM)，即增强的电信运营图(eTOM)，是信息和通信服务行业的业务流程框架。客户（Customer）、用户（User）和账户(Account)。eTOM 引入是电信行业营销模型转向“以客户为中心”的理念而产生的成果。围绕客户建立用户和账户。这三个是相互关联的实体，这种关联只是一个归属和映射的关系，而三个实体本身是相互独立的，分别是体现完全不同的几个域的信息。
* Market & Sales Domain
* Customer Domain
* Product Domain
* Service Domain
* Resource Domain
* Business Partner Domain
* Enterprise Domain

这种理解包括系统如何被划分为组件，以及组件如何通过接口进行交互。这些组件通常是由更小的组件组成的，但架构只包括所有开发人员都理解的组件和接口。


确保架构能够实时的主要手段
* 规约：行业和企业的规范，开发和命名的规范。
* 模板：各个配置模板和脚本等
* 保障：编码规范的自动检查、自动化的测试和代码review



“Patterns of Enterprise Application Architecture”

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


architecture styles (架构风格)

Roy Thomas Fielding博士，在他的REST论文中，对架构风格做出了定义：
>An architectural style is a coordinated set of architectural constraints that restricts the roles/features of architectural >elements and the allowed relationships among those elements within any architecture that conforms to that style.
>一种架构风格是一组协作的架构约束，这些约束限制了架构元素的角色和功能，以及在任何一个遵循该风格的架构中允许存在的元素之间的关系。

架构模式

架构模式描述了一组组件之间的关系，用以解决特定上下文内的某个常见的架构问题！

Wiki上也给架构模式做了类似的定义：
>An architectural pattern is a general, reusable solution to a commonly occurring problem in software architecture within a >given context
>架构模式是一个通用的、可重用的解决方案，用以解决特定上下文内的某个常见的架构问题！


Work smarter not harder

* Make code recognizable to other developer
* Easy to find information
* Helps decision-making process

# Architecural Pattern


缺乏内聚

高内聚：清洗良好的定义
松耦合：依赖简单

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



Monolith


N-Tier
* Multiple tier
* Tier performs specific task
* Tier can be physically separated
* Tiers arent't layer

3-Tier
* Presentation tier
* Business logic tier
* Data tier

As I think about MVC I see two principal separations: separating the presentation from the model and separating the controller from the view.


Reactor： 
The Reactor architectural pattern allows event-driven applications to demultiplex and dispatch service requests that are delivered to an application from one or more clients.
* 'thread-per-connection' model
* event-drived model

a process or thread-based model to handle connections。


Proactor： 
The Proactor architectural pattern allows event-driven applications to efficiently demultiplex and dispatch service requests triggered by the completion of asynchronous operations, to achieve the performance benefits of concurrency without incurring certain of its liabilities.

The proactor is a completion dispatcher that calls back to the designated concrete completion handler in an application after the corresponding asynchronous operation has finished executing.


Asynchronous Completion Token：
The Asynchronous Completion Token design pattern allows an application to demultiplex and process efficiently the responses of asynchronous operations it invokes on services.


Acceptor-Connector：
The Acceptor-Connector design pattern decouples the connection and initialization of 
cooperating peer services in a networked system from the processing performed by the peer 
services after they are connected and initialized.


The C10K problem (Concurrently handle 10,000 connections.)
1. Event-Driven Programming: This involves organizing the server so that it reacts to events (like the arrival of a new connection or the receipt of data) instead of maintaining a thread for each connection. The server essentially “waits” for events and reacts as they occur.
2.  Multiplexing I/O Operations: Multiplexing involves handling multiple inputs and outputs over a single file descriptor using system calls like select, poll, and epoll.
3. Thread Pooling: This technique involves creating a pool of worker threads at startup, which can be reused to handle multiple connections, thereby reducing the overhead associated with thread creation and destruction.
4. Networking and OS Optimizations: Networking hardware and operating systems have also been enhanced to better support a large number of concurrent connections. These enhancements include improved TCP/IP implementations, advancements in network interface cards, and better scheduling algorithms in the operating system kernel.

[The Secret to 10 Million Concurrent Connections -The Kernel is the Problem, Not the Solution](http://highscalability.com/blog/2013/5/13/the-secret-to-10-million-concurrent-connections-the-kernel-i.html)
C10M Problem


* minimum context-switches
* low-memory footprint,


filter pattern被称为转换器模式更好一些
* 过滤表示清除一些数据
* 转换表示将数据转换为另一种格式

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


Structural patterns are concerned with how classes and objects are composed to form larger structures.
* Adapter
  * Convert the interface of a class into another interface clients expect. Adapter lets classes work together that couldn't otherwise because of incompatible interfaces.
  * Overload方法
* Composite 组合模式
  * Compose objects into tree structures to represent part-whole hierarchies.  
* Decorator 装饰器模式
  * Attach additional responsibilities to an object dynamically. Decorators provide a flexible alternative to subclassing for extending functionality.  
  * JDK IO
* Facade 外观模式
  * Provide a unified interface to a set of interfaces in a subsystem. Facade defines a higher-level interface that makes the subsystem easier to use.
* Flyweight
  * Use sharing to support large numbers of fine-grained objects efficiently.
  

Behavioral patterns are concerned with algorithms and the assignment of responsibilities between objects.
* Chain of Responsibility 责任链
  * Avoid coupling the sender of a request to its receiver by giving more than one object a chance to handle the request. Chain the receiving objects and pass the request along the chain until an object handles it.
  * servlet
* Command
  * Encapsulate a request as an object, thereby letting you parameterize clients with different requests, queue or log requests, and support undoable operations.    



  事件驱动架构


  CQRS(Command-Query Responsibility Segregation) 是一种读写分离的模式，从字面意思上理解Command是命令的意思，其代表写入操作；Query是查询的意思，代表的查询操作，这种模式的主要思想是将数据的写入操作和查询操作分开。


Event Sourcing也叫事件溯源，是这些年另一个越来越流行的概念，是大神Martin Fowler提出的一种架构模式。简单来说，它有几个特点：
* 整个系统以事件为驱动，所有业务都由事件驱动来完成。
* 事件是一等公民，系统的数据以事件为基础，事件要保存在某种存储上。
* 业务数据只是一些由事件产生的视图，不一定要保存到数据库中。


管道 - 过滤器（pipe-filter）模式

[The Onion Architecture : part 1](https://jeffreypalermo.com/2008/07/the-onion-architecture-part-1/)

Onion Architecture
1. The application is built around an independent object model
2. Inner layers define interfaces, while the outer layers implement those interfaces
3. The direction of coupling is toward the center
4. All application core code can be compiled and can run separately from the infrastructure


 The big drawback to this top-down layered architecture is the coupling that it creates.  Each layer is coupled to the layers below it, and each layer is often coupled to various infrastructure concerns.  However, without coupling, our systems wouldn’t do anything useful, but this architecture creates unnecessary coupling.

 The Onion Architecture relies heavily on the Dependency Inversion principle.

 Let’s review Onion Architecture.  The object model is in the center with supporting business logic around it.  The direction of coupling is toward the center.  The big difference is that any outer layer can directly call any inner layer.   With traditionally layered architecture, a layer can only call the layer directly beneath it.  This is one of the key points that makes Onion Architecture different from traditional layered architecture.