

[scalability-availability-stability-patterns](https://www.slideshare.net/jboner/scalability-availability-stability-patterns)

https://akfpartners.com/growth-blog


[从事分布式系统、计算、hadoop 等方面工作需要哪些基础](https://www.zhihu.com/question/19868791/answer/88873783l)

* Horizontal scaling(水平缩放):scale out 向外伸缩
* Vertical scaling(垂直缩放):Scale up 向上伸缩


性能指标
* 系统容量，即系统最大的吞吐量
* 响应时间，平均响应时间，总的请求中，响应时间低于一个特定阈值的请求所占比例

# Idea

分布式字面上的意思是通过多个服务器或者阶段协同提高服务

分布式的不同视角或者侧面:目的、对象、方法和问题


分布式的目的
* 提高吞吐量
* 提高可靠性，（可用性）
* 降低响应时间，减小等待时延。功能和模块的分布式部署，增加了调用的时延，通常会增加服务的响应时间。但是: a)如果充分挖掘任务蕴含的并发性和充分使用分布式系统的并行处理能力，可以弥补分布式处理带来的时间损耗，降低服务时延;b)通过平衡负载，减小等待实际，实现更快的的响应能力

上述三个目标是相互冲突和矛盾，虽然降低响应时间，能够提高吞吐量，但是提高吞吐量的很多措施却很增加服务的响应时间。类似于的，为了

分布式的对象
* 数据(data)，存储的分布化
* 功能(function)，计算和处理的分布化
* 请求(request)，

分布式的方法：
* 分割/划分（partition/split)，通过提高并发度来提高吞吐，通过并行处理来降低服务时间。
* 复制/克隆（replicate/clone)，分担负载来提高吞吐，提高可靠性



可扩展性（可伸缩性）描述了一个系统随着添加资源，能够在满足服务水平的情况下处理更多工作的能力，包括更多的请求和更多的数据

线性扩展

分布式引入的问题

The 8 fallacies of distributed computing
1. The network is reliable.
2. Latency is zero.
3. Bandwidth is infinite.
4. The network is secure.
5. Topology doesn't change.
6. There is one administrator.
7. Transport cost is zero.
8. The network is homogeneous.

[Fallacies of Distributed Computing Explained](http://rgoarchitects.com/Files/fallacies.pdf)

[Eight Fallacies of Distributed Computing ](https://samirbehara.com/2019/05/16/eight-fallacies-of-distributed-computing/)

请求分解为多个请求：请求数据，检查数据是否准备完成，下载数据

请求复制：热备



|  |数据 | 功能 | 请求 |
| :------------ | :------------ | :------------ | :------------ |
|分割/划分 |数据划分<br>* 分担写负载 | pipeline | 大任务请求：划分为多个阶段性请求和多个并行请求（页面浏览）|
|复制/克隆 | 数据复制<br>* 分担读负载 <br>* 提高可靠性<br>*   Cache | 负载均衡 |热备| 


数据-分割/划分，提高系统的并发度

data
- partitions
- replication

读多写少，极端情况下一次写入、多次读取

数据复制所带来的问题
* 一致性问题，
* 事务处理
* 时延

数据分割
* 分割相同的数据（根据地理位置、id等分割客户数据
* 分割不同的数据（分割客户、商品、订单和商户数据）

task
- load balancing
- pipeline

[Architecting for Massive Scalability](https://www.slideshare.net/ericdboyd/architecting-for-massive-scalability-st-louis-day-of-net-2011-aug-6-2011?qid=2acd1958-d23a-40d9-b5d6-afb6ff6c99e2&v=&b=&from_search=18)

What is Scalability? A service is said to be scalable if when we increase the resources in a system, it results in increased performance in a manner proportional to resources added. --Werner Vogels, CTO, Amazon.com 

Measures of Performance 
* Response Time 
* Throughput 

Scalability is the property of a system to handle a growing amount of work by adding resources to the system.

可扩展性（可伸缩性）描述了一个系统随着向其添加资源而能够处理更多工作的能力。

Computing capability of a system can be scaled up. Up to a certain point, we observe a performance gain as the system is scaled up. Yet, after a critical point, we observe that we do not get the intended speed up as we provide the system with more and more resources. 

一个系统的计算能力能够向上扩展。当系统向上扩展时，我们会观察到性能提升，但是在经过一个关键点之后，我们发现虽然我们为系统提供越来越多的资源，却无法获得所预计的性能加速。

Measures of Scalability?

What can be Scaled? 
* Servers 
* CPU 
* Memory 
* Hard Disk 
* Network Ports 
* Bandwidth 
* Cooling 
* Power 
* Racks 
* Floor Space

Benefits of Scalability
* Dynamic Capacity 
* Planning Cost is Linear 


In a general sense, scaling is a geometric notion where we make a system bigger by stretching it in several directions. However, every system has its limitations to growth. As the system is scaled up, overheads start to hinder the gains. Beyond a critical point, the capability of the system starts to decrease as the system is further scaled up.

一般而言，缩放是一种几何概念，我们通过在多个方向上拉伸来使系统变大。然而，每个系统都有其增长的限制。随着系统规模的扩大，开销不断增加，而收益却逐渐减少。在超过某个临界点后，随着系统进一步扩展，系统的能力开始下降。


ACID, CAP(Consistency, Availability, Partition Tolerance), BASE(Basically Available, Soft State, Eventually Consistent ) 

 I Need Scalability
 * Loose Coupling
 * Stateless 
 * Messaging & SOA 
 * Async & Background Processes 
 * Queuing 
 * Monitoring and Diagnostics 

Front-End (FE) + Back-End (BE) Architecture 
1. (FE) requests (BE) to perform work 
2. (BE) completes work 
3. (BE) reports results back to (FE) 



复制/克隆的一种特殊形式是跨越多个数据中心的复制/克隆(Multi-Active IDCs/Regions)
* 就近提供服务，减小网络传输时延
* 避免断电、断网和灾难等原因造成数据中心不可用，从而提供更高的可靠性
* 分流流量，避免网络拥塞

静态文件：CDN （Content Delivery Network）

数据的多数据中心异地存储

根据地理位置，部署多个站点：每次域名解析请求都会根据对应的负载均衡算法计算出一个不同的IP地址并返回，这样A记录中配置多个服务器就可以构成一个集群，并可以实现负载均衡


从系统的生命周期看，分布化设计整个周期的各个阶段和环节
Strategies --> design -> implement -> deployment -> operation(monitor, log)

# Papers
[1] Patrick O'Neil, Edward Cheng, Dieter Gawlick, Elizabetch O'Neil. The log-structured merge-tree (LSM-tree). Acta Informatica, 1996, 33(4): 351-385.




# Books

### Ajay D. Kshemkalyani and Mukesh Singhal. Distributed Computing: Principles, Algorithms, and Systems. Cambridge University Press. 2008

causality, physical time, logical time

monotonicity property associated with causality in distributed systems.

Causality (or the causal precedence relation)

[51] Every event is assigned a timestamp and the causality relation between events can be generally inferred from their timestamps. The timestamps assigned to events obey the fundamental monotonicity property; that is, if an event a causally affects an event b, then the timestamp of a is smaller than the timestamp of b.  
[52] A system of logical clocks consists of a time domain T and a logical clock C. Elements of T form a partially ordered set over a relation <. This relation is usually called the happened before or causal precedence. 

This monotonicity property is called the clock consistency condition


clock consistency condition v.t. strongly consistent

[52] Implementation of logical clocks requires addressing two issues [19]: data structures local to every process to represent logical time and a protocol (set of rules) to update the data structures to ensure the consistency condition.


two capabilities:
- A local logical clock, denoted by lci,
- A logical global clock, denoted by gci
A local logical clock v.t. A logical global clock,

two rules:
- R1 This rule governs how the local logical clock is updated by a process when it executes an event (send, receive, or internal).
- R2 This rule governs how a process updates its global logical clock to update its view of the global time and global progress.

scalar time, vector time, and matrix time

Total Ordering

The system of scalar clocks is not strongly consistent;

Isomorphism


### 

#### Reduce the Equation 大道至简

match the effort and approach to the complexity of the problem. Not every solution has the same complexity—take the simplest approach to
achieve the desired outcome。努力和方法要与问题的复杂性相匹配。不是每个方案都有相同的复杂性，选取最简单的方法，实现所期望的结果

keeping things as simple as possible. Our view is that a complex problem is really just a collection of smaller, simpler problems waiting to be solved.保持事情尽可能的简单。从我们的视角来看，一个复杂问题其实仅仅是一些更小的、更简单的待解决问题集合

##### Rule 1—Don’t Overengineer the Solution 
##### 规则1—不要过度设计方案

**What:** Guard against complex solutions during design. 在设计过程中严防复杂的解决方案。

**When to use:** Can be used for any project and should be used for all large or complex systems or projects. 可以应用于任何项目，而且也必须应用于所有大型或者复杂的系统或者项目

**How to use:** Resist the urge to overengineer solutions by testing ease of understanding with fellow engineers. 通过与工程师同事测试易懂性，来抵制对于过度工程化解决方案的冲动。

**Why:** Complex solutions are excessively costly to implement and are expensive to maintain long term. 复杂方案的实现会严重超支，而长期维护费用也高昂，

**Key takeaways:** Systems that are overly complex limit your ability to scale. Simple systems
are more easily and cost-effectively maintained and scaled.

过度工程化可以划归两大类
* The first category covers products designed and implemented to exceed their useful requirements. 第一类涵盖那些设计和实现超过其有用需求的产品。
* The second category of overengineering covers products that are made to be overly complex.第二类过度工程化涵盖那些制造过于复杂的产品。


To explain the first category of overengineering, exceeding useful requirements。第一类是超过了有用需求，即设计和实现了现在比并不需要的功能。

The second category of overengineering deals with making something overly complex and making something in a complex way. 第二类过度工程化处置使得某些事情过于复杂并且以某种复杂的方式制作一些事情。

不要向不需要的需求或功能买单

[Faster Time to Market – How to Avoid Overengineering (Rule 1)](https://akfpartners.com/growth-blog/faster-time-to-market-how-to-avoid-overengineering-yagni)

Overengineering is solving problems you don’t have.

We will look at two sides of overengineering: Exceeding useful requirements, and spending too much effort to get a job done.

##### Rule 2—Design Scale into the Solution　(D-I-D Process) 
##### 方案2—将可扩展性设计到方案中（设计-实现-部署过程）

**What:** An approach to provide JIT (just-in-time) scalability. 一种提供及时可扩展性的方法

**When to use:** On all projects; this approach is the most cost-effective (resources and time) to ensure scalability.

**How to use:**
* Design for 20x capacity.针对20倍的容量，设计
* Implement for 3x capacity.针对3倍的容量，实现
* Deploy for roughly 1.5x capacity.针对大约1.5倍容量，部署

**Why:** D-I-D provides a cost-effective, JIT method of scaling your product. 设计-实现-部署提供了一种高性价比的、及时的方式，来扩展你的产品。

**Key takeaways:** Teams can save a lot of money and time by thinking of how to scale solutions early, implementing (coding) them a month or so before they are needed, and deploying them days before the customer rush or demand.


D-I-D provides a cost-effective, JIT method of scaling your product.

Dell, configure-to-order： 按订单配置，just-in-time manufacturing：及时制造

AKF Partners’ Design-Implement-Deploy or D-I-D approach to thinking about scalability.

[The DID Process - Scale Design Principles (Rule 2)](https://akfpartners.com/growth-blog/scale-design-principles-the-did-process)


Ideally, what you want is JIT (just-in-time) scalability. The idea originates from JIT manufacturing, and relates to reducing delivery time. JIT scalability is the ability to scale up or down when needed, as needed.

infrastructure-as-a-service (IaaS) 

有预见性的设计，分阶段性的实现，及时性的部署

##### Rule 3—Simplify the Solution Three Times Over 
##### 方案3—三重简化方案

**What:** Used when designing complex systems, this rule simplifies the scope, design, and implementation. 当设计复杂系统时使用这个规则，简化范围、设计和实现。

**When to use:** When designing complex systems or products where resources (engineering
or computational) are limited.


**How to use:**
* Simplify scope using the Pareto Principle. 通过帕累托法则来简化范围
* Simplify design by thinking about cost effectiveness and scalability. 通过考量经济效益和可扩展性来简化设计
* Simplify implementation by leveraging the experience of others.通过充分利用他人的经验来简化实现

**Why:** Focusing just on “not being complex” doesn’t address the issues created in requirements
or story and epoch development or the actual implementation.

**Key takeaways:** Simplification needs to happen during every aspect of product development.


Pareto principle 即帕累托法则，又称80/20法则、马特莱法则、二八定律、帕累托定律、最省力法则、不平衡原则、犹太法则。意大利经济学家帕累托提出的。法则认为原因和结果、投入和产出、努力和报酬之间本来存在着无法解释的不平衡

[Scalability Rules - How to Simplify Scope, Design, and Implementation (Rule 3)](https://akfpartners.com/growth-blog/scalability-rules-how-to-simplify-scope-design-and-implementation)

简化体现在更容易被理解，完成的时间更短，所付出的代价更小

Complexity elimination is about cutting off unnecessary trips in a job, and simplification
is about finding a shorter path


“How can we leverage the experiences of others and existing solutions to simplify
our implementation?”


##### Rule 4—Reduce DNS Lookups 减少DNS查找
##### 规则4—避免重复性工作


**What:** Reduce the number of DNS lookups from a user perspective.

**When to use:** On all Web pages where performance matters.

**How to use:** Minimize the number of DNS lookups required to download pages, but balance
this with the browser’s limitation for simultaneous connections.

**Why:** DNS lookups take a great deal of time, and large numbers of them can amount to a large portion of your user experience.

**Key takeaways:** Reduction of objects, tasks, computation, and so on is a great way of
speeding up page load time, but division of labor must be considered as well.


[什么是高并发下的请求合并？](https://mp.weixin.qq.com/s?__biz=MzIxNTQ4MzE1NA==&mid=2247501569&idx=1&sn=1bdce3ec6b00e2a1ec4e71c293fbf8ef&chksm=9795117ca0e2986a85c91e3fd1157d302e25db247ac694f3f80ddb9a44245a45255874cfd68a&mpshare=1&scene=1&srcid=112361PzzD8ACPONUPHVU9HI&sharer_sharetime=1606100477426&sharer_shareid=fc937fe50a97e6c10553c542abe0a39b&exportkey=AUU9f1Fl1KaBL6RENR8Oraw%3D&pass_ticket=fk%2BE1fOYHmI5CyP5XtiiPrUMmfrHPspkwtzMhbIMcZ8RCXV3pYelubWJqWxZuV5q&wx_header=0#rd)

方法
* Batch: 打包批量处理
* cache 缓存和复用结果




在分割后的功能中包含一些重复的处理，将这个处理分离出来，作为一个公共的前置功能。



##### Rule 5—Reduce Objects Where Possible尽可能减少对象
##### Rule 5—控制分割的粒度

**What:** Reduce the number of objects on a page where possible.

**When to use:** On all Web pages where performance matters.

**How to use:**
* Reduce or combine objects but balance this with maximizing simultaneous connections.
* Look for opportunities to reduce weight of objects as well.
* Test changes to ensure performance improvements.

**Why:** The number of objects impacts page download times.

**Key takeaways:** The balance between objects and methods that serve them is a science that requires constant measurement and adjustment; it’s a balance among customer usability, usefulness, and performance.


如果分割的太小，引入的代价将会超过分割带来的好处。因此，在一些情况下可以需要合并

[Reduce DNS lookups to improve website performance (Rule 4)](https://akfpartners.com/growth-blog/reduce-dns-lookups-to-improve-website-performance)


无论是对应功能进行分割，还是对应数据进行分割，都会引入高昂的代价。如果分割的粒度过小，那么所付出的代价将远远超过所引入的好处，因而得不偿失。


##### Rule 6—Use Homogeneous Networks使用同构网络

**What:** Ensure that switches and routers come from a single provider.

**When to use:** When designing or expanding your network. How to use:
* Do not mix networking gear from different OEMs for switches and routers.
* Buy or open-source for other networking gear (firewalls, load balancers, and so on).

**Why:** Intermittent interoperability and availability issues simply aren’t worth the potential cost savings.

**Key takeaways:** Heterogeneous networking gear tends to cause availability and scalability
problems. Choose a single provider.

对于操作系统以及数据库、JDK和Nginx等系统软件采用相同的版本。


#### Distribute Your Work 分布你的工作


##### Rule 7-Design To Clone or Replicate Things (X Axis)

##### 规则7-设计支持克隆或者复制相同的东西（X轴）

**What:** Typically called horizontal scale, this is the duplication of services or databases to spread transaction load. 复制服务或者数据库，来分散事务负载，因此通常被称为水平可伸缩，

**When to use:**
* Databases with a very high read-to-write ratio (5:1 or greater—the higher the better).数据具有非常号的读/写比（5:1或者更高，越高越好）
* Any system where transaction growth exceeds data growth.任何系统如果其事务的增长超过了数据的增长

**How to use:**
* Simply clone services and implement a load balancer.简单的克隆服务并实现一个负载均衡器
* For databases, ensure that the accessing code understands the difference between a read and a write.对于数据库，确保访问的代码理解读和写的不同

**Why:** Allows for fast scale of transactions at the cost of duplicated data and functionality. 许可以复制数据和功能为代价，快速地实现事务处理的可伸缩性

**Key takeaways:** X axis splits are fast to implement, are low cost from a developer effort perspective, and can scale transaction volumes nicely. However, they tend to be high cost from the perspective of operational cost of data. X轴的分解能够快速地实现，并且从开发者工作的视角具有较低的成本，能够非常好地扩展事务的数量。但是从数据操作代价的角度，X轴分解倾向于更高的成本。

Often, the hardest part of a solution to scale is the database or persistent storage tier. 在实现可伸缩性的解决方案中最为困难的部分是数据库或者持久化存储层。
* 分布式事务：ACID
* 数据一致性：如果写数据，1）如何实现数据多个副本数据的一致性；2）如何避免读到不一致的数据

One technique for scaling databases is to take advantage of the fact that most applications and databases perform significantly more reads than writes. 一种用于扩展数据库的技术是利用了这样一个事实，即大多数应用和数据库的读要远远多于写。


There are a couple of ways that you can distribute the read copy of your data depending on the time sensitivity of the data. Time (or temporal) sensitivity is how fresh or completely correct the read copy has to be relative to the write copy. 依赖于数据的时间敏感性，你可以使用多种方式分布数据的读副本。时间敏感性是指相对于写副本，读副本的一致性的程度或者完全正确的程度。

the ways to distribute the data.分布数据的方式
* One way is to use a caching tier in front of the database.一种方法是在数据库之前使用缓存层。
* The next step beyond an object cache between the application tier and the database tier is replicating the database。除了在应用层和数据库层之间对象缓存，下一步是复制数据库。

X axis—Horizontal Duplication


应用和web服务的克隆相对较为容易实现，允许我们扩展所处理事务的数目。



##### Rule 8—Design to Split Different Things (Y Axis)

##### 规则8—设计支持分拆不同的东西（Y轴）

**What**: Sometimes referred to as scale through services or resources, this rule focuses on scaling by splitting data sets, transactions, and engineering teams along verb (services) or noun (resources) boundaries. 有时指的是通过服务或者资源实现可扩展，这个规则聚焦于沿着动词(服务)或者名词(资源)的边界，通过分割数据集、事务和工程团队，来实现可扩展。
 
**When to use**:
* Very large data sets where relations between data are not necessary.非常大的数据集合，并且集合内数据之间的关系不是必须的。数据之间没有必然的关联，无需考虑JOIN操作。
* Large, complex systems where scaling engineering resources requires specialization.庞大的、复杂的系统，并且在系统中扩展工程资源需要非常的专业化

**How to use**:
* Split up actions by using verbs, or resources by using nouns, or use a mix.使用动词分拆分动作，使用名词拆分资源，或者两者混合使用。
* Split both the services and the data along the lines defined by the verb/noun approach.沿着通过动词/名词方法定义的路线拆分服务和数据

**Why:** Allows for efficient scaling of not only transactions but also very large data sets associated with those transactions. Also allows for the efficient scaling of teams. 不仅许可高效地扩展事务，而且许可高效地扩展与这些事务相关联的、非常大的数据集合。此外，还许可高效地扩展团队。

**Key takeaways:** Y axis or data/service-oriented splits allow for efficient scaling of transactions, large data sets, and can help with fault isolation. Y axis splits help reduce the communication overhead of teams. Y轴分解或者面向数据/服务的分解能够实现高效地扩展事务和大数据集合，并且有助于故障隔离。Y轴分解帮助减小团体交流开销。

Let’s split up our site using the verb approach first。让我们首先使用动词方法分解我们的网站。

We might identify certain resources upon which we will ultimately take actions (rather than the verbs that represent the actions we take). 我们可以鉴别我们将最终操作的特定资源（而不是代表我们操作行为的动词）


Because services or resources are now split, the actions we perform and the code necessary to perform them are split up as well. 因为服务或资源已被分拆，所有我们的执行以及操作服务或者资源的代码代码也会被分拆。

One tenet of Brooks’ Law is that developer productivity is reduced as a result of increasing team sizes. The communication effort within any team to coordinate team efforts is a square of the number of participants in the team. Therefore, with increasing team size comes decreasing developer productivity as more developer time is spent on coordination.
Brooks法则的一个原则是团队规模逐渐扩大一个必然结果是开发人员的生产率的降低。在任何团队内部协同团队工作所需要的沟通工作是团队成员数目的平方。因此，增加团队的规模会降低开发人员的生产率，因为开发人员花费更多的时间用于协同。

##### Rule 9—Design to Split Similar Things (Z Axis)
##### 规则9-设计支持分拆相似的东西(Z轴)

**What:** This is very often a split by some unique aspect of the customer such as customer ID, name, geography, and so on. 非常常见的分离方式是通过客户一些独特的属性，例如客户id、名字和地理位置等。

**When to use:** Very large, similar data sets such as large and rapidly growing customer bases or when response time for a geographically distributed customer base is important. 非常庞大的或者相似的数据集，例如大量并快速增长的客户群或者对于地理分布的客户群响应时间非常重要。

**How to use:** Identify something you know about the customer, such as customer ID, last name, geography, or device, and split or partition both data and services based on that attribute. 识别那些你所知的、有关于客户的信息，例如客户id、姓氏、地理位置或终端，并据此分割或者划分数据和服务。

**Why:** Rapid customer growth exceeds other forms of data growth, or you have the need to perform fault isolation between certain customer groups as you scale. 快速的客户增长超过了其他格式的数据增长，或者在你扩展客户规模的过程，你需要在特定的客户之间实现故障隔离。

**Key takeaways:** Z axis splits are effective at helping you to scale customer bases but can also be applied to other very large data sets that can’t be pulled apart using the Y axis methodology. Z轴分解不仅是一种有效的方式，协助你扩展客户群，而且还可以应用到其他一些巨大数据集合上，这些数据集合使用Y轴方法无法有效得分解，


Often referred to as sharding and podding, Rule 9 is about taking one data set or service and partitioning it into several pieces. These pieces are often equal in size but may be of different sizes if there is value in having several unequally sized chunks or shards. 规则9经常称为分片或者分割，其获取一个数据集或者服务，然后将其划分为多个部分。这些部分通常大小相等，但如果大小不一的块或者分片有意义，那么也可以大小并不相同。

Summary
* Scale by cloning—Cloning or duplicating data and services allows you to scale transactions easily.
* Scale by splitting different things—Use nouns or verbs to identify data and services to separate. If done properly, both transactions and data sets can be scaled efficiently.
* Scale by splitting similar things—Typically these are customer data sets. Set customers up into unique and separated shards or swim lanes (see Chapter 9 for
the definition of swim lane) to enable transaction and data scaling.

#### Design to Scale Out Horizontally
#### 设计支持水平地向外扩展

In our minds, it is clear: we believe that within hyper-growth environments it is critical that companies plan to scale in a horizontal fashion—what we describe as scaling
out. Most often this is done through the segmentation or duplication of workloads across multiple systems.在我们的思想中，其非常显然，我们认为在高速增长的环境中，公司计划以一种水平方式扩展（也被我们描述为向外扩展）是非常关键的。绝大多数情况下是通过跨越多个系统，使用分割或者复制来实现。


Here again we see this troubling notion of “complexity.” When used one way, more devices equals more complexity—or as we prefer to indicate, more devices to manage and oversee.
But when seen from another perspective, more devices equals lower complexity—lower rates of failure overall and fewer incidents to manage.
这里我们再次看到复杂性这个令人陷入麻烦的概念。从一个方向上使用，更多的设备等于更高的复杂性，或者按照我们喜欢的方式指出，更多的设备需要管理和监控。但是，从另一个角度看，更多的设备等于更低的复杂性，因为更低的整体故障率和更少需要管理的事故。



##### Rule 10—Design Your Solution to Scale Out, Not Just Up

##### 规则10-设计你的系统支持向外扩展，而不仅仅是向上扩展

**What:** Scaling out is the duplication or segmentation of services or databases to spread transaction load and is the alternative to buying larger hardware, known as scaling up.
向外扩展是针对服务或者数据库的复制或者分割，以扩大事务负载，其是购买更大型的硬件、被称为向上扩展的替换方案。

**When to use:** Any system, service, or database expected to grow rapidly or that you would like to grow cost-effectively.
期望快速增长的或者你期望高性价比的增长的任何系统、服务或者数据库

**How to use:**  Use the AKF Scale Cube to determine the correct split for your environment. Usually the horizontal split (cloning) is the easiest.

**Why:** Allows for fast scale of transactions at the cost of duplicated data and functionality.

**Key takeaways:** Plan for success and design your systems to scale out. Don’t get caught in the trap of expecting to scale up only to find out that you’ve run out of faster and larger systems to purchase.


Having the ability to run your product on multiple servers through all tiers is scaling out.Continuing to run your systems on larger hardware at any tier is scaling up.
有能力将你的产品在所有的层级上运行在多个服务器是向外扩展。继续在更强大的硬件上运行你系统的任何一个层级是向上扩展。



##### Rule 11—Use Commodity Systems (Goldfish Not Thoroughbreds)
##### 规则11-采用商品化系统

**What:** Use small, inexpensive systems where possible.尽可能使用小规模的和不昂贵的系统

**When to use:** Use this approach in your production environment when going through hypergrowth and adopt it as an architectural principle for more mature products.在飞速增长时在你们的生产环境中使用这个方法，并且针对更多的成熟产品采用其作为架构原则。

**How to use:** Stay away from very large systems in your production environment.在你的生产环境中远离非常大型的系统。


**Why:** Allows for fast, cost-effective growth. Allows you to purchase the capacity you need rather than spending for unused capacity far ahead of need.

**Key takeaways:** Build your systems to be capable of relying on commodity hardware, and don’t get caught in the trap of using high-margin, high-end servers.
能够依赖于商品化硬件构建你的系统，避免陷入使用高利润、高端服务器的陷阱。



使用成熟的和商业化的系统，而不要采用定制化的、高端系统。
* 价格相对便宜，更容易大规模的部署，以支持横向扩展
* 更好的性价比


##### Rule 12—Scale Out Your Hosting Solution
##### 规则 12-横向扩展你的托管方案


**What:** Design your systems to have three or more live data centers to reduce overall cost,
increase availability, and implement disaster recovery. A data center can be an owned facility,
a colocation, or a cloud (IaaS or PaaS) instance.
设计你的系统具有三个或者更多的实时数据中心，以降低综合成本、提高可用性和实现灾后恢复。数据中心可以是自有设施、托管服务器或者一个云实例（IaaS或者PaaS）。

**When to use:** Any rapidly growing business that is considering adding a disaster recovery
(cold site) data center or mature business looking to optimize costs with a three-site solution

**How to use:** Scale your data per the AKF Scale Cube. Host your systems in a “multiple live”
configuration. Use IaaS/PaaS (cloud) for burst capacity, new ventures, or as part of a threesite
solution.

**Why:** The cost of data center failure can be disastrous to your business. Design to have
three or more as the cost is often less than having two data centers. Consider using the
cloud as one of your sites, and scale for peaks in the cloud. Own the base; rent the peak.

**Key takeaways:** When implementing disaster recovery, lower your cost by designing your
systems to leverage three or more live data centers. IaaS and PaaS (cloud) can scale
systems quickly and should be used for spiky demand periods. Design your systems to be
fully functional if only two of the three sites are available, or N-1 sites available if you scale
to more than three sites.

It is this segmentation, replication, and cloning of data and services as well as statelessness that form the building blocks for us to spread our data centers across multiple sites and geographies. Standardize system configuration, code deployment, and monitoring to enable seamless growth between colocation sites and cloud sites.
正是数据和服务的分割、复制和克隆以及无状态为我们形成了构造基石，可以跨域多个站点和地区分布我们的数据中心。在托管站点和云站点之间标准化系统配置、代码部署和监控能够无缝地增长。


Multiple live site benefits include
* Higher availability as compared to a hot and cold site configuration
* Lower costs compared to a hot and cold site configuration
* Faster customer response times if customers are routed to the closest data center for dynamic calls
* Greater flexibility in rolling out products in an SaaS environment
* Greater confidence in operations versus a hot and cold site configuration
* Fast and easy “on-demand” growth for spikes using spare capacity in each data center, particularly if PaaS/IaaS/cloud is part of the overall solution

Drawbacks or concerns of a multiple live site configuration include
* Greater operational complexity
* Likely a small increase in headcount
* Increase in travel and network costs

Architectural considerations in moving to a multiple live site environment include
* Eliminating the need for state and affinity wherever possible。尽可能地消除对于状态和亲和性的需求
* Routing customers to the closest data center if possible to reduce dynamic call times。尽可能地将客户路由到最近的数据中心，以减小动态呼叫时间
* Investigating replication technologies for databases and state if necessary。如果必须，研究数据库和状态的复制技术

##### Rule 13—Design to Leverage the Cloud
##### 规则13-设计充分利用云/为充分利用云而设计

**What:** This is the purposeful utilization of cloud technologies to scale on demand.这是有目的性地使用云技术，以按需可扩展。

**When to use:** When demand is temporary, spiky, and inconsistent and when response time is not a core issue in the product. Consider when you are “renting your risk”—when future demand for new products is uncertain and you need the option of rapid change or walking away from your investment. Companies moving from two active sites to three should consider the cloud for the third site. 当需求是临时的、突发性的和不一致的，并且在响应时间不是这些产品中的核心问题的时候。考虑何时真正承担你的风险——当未来对于你产品的需求还不确定并且你需要选择快速改变或者放弃你的投资时。那些将两个活跃站点迁移到三个的公司应该考虑为第三个站点使用云。

**How to use:**
* Make use of third-party cloud environments for temporary demand, such as seasonal business trends, large batch jobs, or quality assurance (QA) environments during
testing cycles. 使用第三方云环境满足临时性需求，例如季节性业务趋势、大量批处理作业或者在测试周期中的质量保证环境。
* Design your application to service some requests from a third-party cloud when demand exceeds a certain peak level. Scale in the cloud for the peak, then reduce
active nodes to a basic level.设计你的应用，以当需求超过一个特定峰值水平时服务于一些来自第三方云的请求。针对峰值在云中扩展，然后减少活跃的节点到一个基本水平。

**Why:** Provisioning of hardware in a cloud environment takes a few minutes as compared to days or weeks for physical servers in your own colocation facility. When used temporarily, this is also very cost-effective.

**Key takeaways:** Design to leverage virtualization in all sites and grow in the cloud to meet unexpected spiky demand.

Vendor-provided clouds have four primary characteristics: pay by usage, scale on demand, multiple tenants, and virtualization.
有供应商提供的云具有四个主要特征：按使用付费、按需扩展、多租户和虚拟化。



#### Chapter 4 Use the Right Tools
#### 使用正确的工具（工欲善其事，必先利其器）

“Law of the Instrument,” otherwise known as Maslow’s Hammer.  “When all you have is a hammer, everything looks like a nail.” There are at least two important implications of this “law.” 当你的所有只是一个锤子时，那么一切看起来都像钉子。

The first is that we all tend to use instruments or tools with which we are familiar to solve the problems before us. 第一个含义是我们都倾向于使用自己熟悉的器械或者工具，来解决我们面前的问题。

The second implication of this law really builds on the first. If within our organizations we consistently bring in people with similar skill sets to solve problems or implement new
products, we will very likely get consistent answers built with similar tools and thirdparty products. The problem with such an approach is that while it has the benefit of
predictability and consistency, it may very well drive us to use tools or solutions that are inappropriate or suboptimal for our task.
这个法则的第二个含义是构建在第一含义的基础上。如果在我们的组织内我们持续地引进那些拥有类似技术能力的人员，来解决问题或者实现新产品，那么我们会非常可能地得到使用类似工具和第三方产品所构建的、一致的答案。使用这种方法的一个问题是虽然其具有可预测性和一致性的好处，但是其非常可能驱动我们针对我们的问题，使用不适当的或者次优的工具或者解决方案。

This one system was carrying all the weight of everything the organization wanted to do. While it worked, and the execution risk for projects was lower, this is a classic example of overusing a tool
一个系统承载了组织想做的所有事情。虽然其有效并且降低了项目的执行风险，但是这是一种经典的、滥用一个工具的例子。

Using the right tool for the right job at the right time in an organization’s lifecycle is critical. This is a balancing act that requires judgment, especially in a large organization. Some teams suffer from always chasing the ‘next cool tool.’ Their infrastructure ends up being littered with a myriad of different tools, none of them hardened, robust, or able to be supported at scale. On the flip side, some organizations get good at just one thing, and they take that one thing way too far.”
在一个组织的生命周期中在正确的时间使用正确的工具完成正确的工作是至关重要的。这需要基于判断做出平衡，尤其是在大型组织中。有些团队容忍经常追逐于“下一个很酷的工具”。他们的基础设施凌乱不堪，遍布大量不同的工具，而这些工具都不是坚固的、健壮的或者能够得到大规模支持的。另一个方面，一些组织仅仅擅长一个事情，将事情做到极致。

These tools present modern approaches to solving problems more effectively than older tools often can. Unfortunately for many organizations, a lack of experimentation and adoption of these newer technologies has led to tool lock-in and overuse.
这些工具提供了比旧有工具更有效的方法解决问题。不幸的是，对于很多组织而言，对这些更新的技术缺乏实验和应用，造成工具的锁定和滥用。

It’s critical that every organization avoid getting trapped in this innovator’s dilemma. While a portion of the R&D portfolio needs to go to critical projects, and making existing tools better, a set portion always needs to be isolated for proactive analysis, piloting, and adoption of new tool capabilities. It’s important that the teams owning core tools are also the teams that are innovating with new advances and new technologies. This will set an organization up to be leading, innovating, and cost-effectively solving problems, with the right tools being used to solve the right problems, and will make the company more successful in the long term
至关重要的是每个组织要避免陷入创新者困境。虽然一部分研发投资需要投向一些关键项目，并优化已有工具，但始终要从研发费用中划拨一部分，用于主动地分析、实现和采用新工具能力。非常重要的是拥有核心工具的团队往往也是正在使用新进展和新技术进行创新的团队。这将使得组织能够使用正确的工具解决正确的问题，从而将组织提升为一个领军的、创新的和高效解决问题的个组织，并使得公司在长期的发展上更加成功。



"The Innovator's Dilemma"  Clayton M. Christensen

The advantages that those technologies can give businesses are massive, but not understanding the trade-offs can kill a business. The company that I spoke of was trying to take advantage of the agility of a nonrelational database; that’s great, but they failed to understand that they had given up some of the analytical capability, such as multitable complex joins, that they used in a relational database. Understanding these differences is just good engineering; it can make the difference between companies that prosper and those that fail.
这些技术的优势是能够为业务提供巨大的容量，但是不能理解这些技术的折中将会扼杀一个业务。我所说的这个公司试图利用非关系型数据库的敏捷性，这非常棒，但是他们没能理解他们不得不放弃一些在关系数据中所使用的分析能力，例如多表复杂的join。正确理解这些差异才是一个好的工程，其将会造成繁荣的公司与失败公司之间的差异。


There is no perfect database. There’s no perfect data store. They all have trade-offs, and that’s kind of the thing that everybody needs to wrap their head around. People have their biases for whatever reason, but the honest answer is that when you’re writing or reading data from or to some kind of storage mechanism, there are a couple of core choices that you have to make that ultimately determine the characteristics of the database. One solution may take twice as much storage space, generally be a bit slower, but give you significantly greater flexibility. Conversely, another choice may give you less storage to worry about, be faster for many things, but constrain you in what you can do with it. Knowing these differences or having an expert to help you understand these trade-offs is critical for designing a modern application and really is a business advantage. 
没有完美的数据库，也没有完美的数据存储，它们都需要折中。这一点需要在每个人的头脑中牢牢记住。人们出于各种原因总是带有偏见，但是最为诚实的回答是当你向一些存储机制写入数据或者从中读取数据时，你必须确定一些核心选项，这些选项最终决定了数据库的特性。一种方案可能使用两倍的存储空间，并且通常会有点慢，但是却给你提供了显著的灵活性。相反地，另一个选择为你带来更少的可用存储空间，并且对很多事情会更快，但是会限制你所做的事情。对于设计现代应用而言，知道这些区别或者让一个专家帮助你理解这些折中是非常重要的，这实际是一个业务优势。


Don’t get locked into only what you are familiar with;spend the time to learn new things and be open to them.
不要仅仅局限于你所熟悉的事物；花些时间学习新东西并对它们保持开放态度。


##### Rule 14—Use Databases Appropriately
##### 规则14-恰当地使用数据库

**What:** Use relational databases when you need ACID properties to maintain relationships between your data and consistency. For other data storage needs consider more appropriate
tools such as NoSQL DBMSs. 当你需要ACID属性以保证数据之间的关系和一致性时，请使用关系数据库。对于其他数据存储需求，请考虑更加适当的工具，例如NoSQL DBMSs。

**When to use:** When you are introducing new data or data structures into the architecture of a system. 

**How to use:** Consider the data volume, amount of storage, response time requirements, relationships, and other factors to choose the most appropriate storage tool. Consider how
your data is structured and your products need to manage and manipulate data. 考虑数据规模、存储容量、响应时间需求、关系和其他因素，以选择最恰当的存储工具。考虑你的数据如何构造以及你的产品需要如何管理和操作数据。

**Why:** An RDBMS provides great transactional integrity but is more difficult to scale, costs more, and has lower availability than many other storage options.关系型数据库管理系统提供了强大的事务完整性，但是与很多其他存储选择相比，其较难实现可扩展、成本更高、具有较低的可用性。

**Key takeaways:** Use the right storage tool for your data. Don’t get lured into sticking everything in a relational database just because you are comfortable accessing data in a
database.



Relational database management systems (RDBMSs), such as Oracle and MySQL, are based on the relational model introduced by Edgar F. Codd in his 1970 paper “A Relational Model of Data for Large Shared Data Banks.”Most RDBMSs provide two huge benefits for storing data. The first is the guarantee of transactional integrity through ACID properties. The second is the relational structure within and between tables. To minimize data redundancy and improve transaction processing, the tables of most OLTP databases are normalized to third normal form, where all records of a table have the same fields, nonkey fields cannot be described by only one of the keys in a composite key, and all nonkey fields must be described by the key. Within the table each piece of data is highly related to other pieces of data. Between tables there are often relationships known as foreign keys. While these are two of the major benefits of using an RDBMS, these are also the reasons for their limitations in terms of scalability.
大多数的关系数据库系统为数据存储提供了两大便利。第一个是通过ACID属性确保事务完整性。第二个是在表内部和表之间的关系型结构。为了最小化数据冗余和提高事务处理，大多数OLTP数据库的表都被正规化为第三范式，其中一个表的所有记录都有相同的字段，非键字段不能仅仅被组合键中的一个键描述，所有的非键字段必须被键所描述。在一个表内部数据的每一个部分紧密地关联到数据的其他部分。在表之间的关联关系通常被称为外键。虽然这些是使用关系型数据库带来的主要便利，但是这也是在可伸缩方面受到限制的原因。

文件系统
* 大型数据，比如文件、图片等
* 一次写入，多次读取

The next set of alternative storage strategies is termed NoSQL. Technologies that fall into this category are often subdivided into key-value stores, extensible record stores, and document stores. There is no universally agreed-upon classification of technologies, and many of them could accurately be placed in multiple categories.


Key-value stores include technologies such as Memcached, Redis, and Amazon DynamoDB and Simple DB. These products have a single key-value index for data and that is stored in memory.
键值存储


Extensible record stores (ERSs), sometimes called wide column stores or table-style DBMSs, include technologies such as Google’s proprietary Bigtable and Facebook’s, now open-source, Cassandra and the open-source HBase.
列存储


Document stores include technologies such as MongoDB, CouchDB, Amazon’s DynamoDB, and Couchbase. The data model used in this category is called a “document” but is more accurately described as a multi-indexed object model. The multi-indexed object (or “document”) can be aggregated into collections of multi-indexed objects (typically called “domains”).
文件存储

You can tune consistency and latency in many of the NoSQL solutions with trade-offs, but immediate consistency is not possible as with an RDBMS.
在很多NoSQL解决方案中你可以利用折中来调整一致性和时延，但是获得像一个关系型数据库那样的实时一致性是不可能的。

There is a trade-off between scalability and flexibility within these systems. The degree of relationship between data entities ultimately drives this trade-off; as relationships increase, flexibility also increases. This flexibility comes at an increase in cost and a decrease in the ability to easily scale the system
在在这些系统中存在着可扩展和灵活性之间的折中。数据实体之间的关系程度最终驱动了这种折中，当关系增加时，灵活性也会得到提高。然而，这种灵活性是增加成本和减小系统的易扩展能力为代价。

Read and write ratios are important as they help drive an understanding of what kind of system we need. Data that is written once and read many times can easily be put on a file system coupled with some sort of application, file, or object cache.Images are great examples of systems that typically can be put on file systems. Data that is written and then updated, or with high write-to-read ratios, is better off within NoSQL or RDBMS solutions.
读和写之间的比非常重要，因为其有助于推动我们更深入地理解我们需要哪种系统。一次写入和多次读取的数据非常容易放入那些与应用、文件或对象缓存相结合的文件系统。


* degree of relationships
* Rate of Growth
* read and write conf licts,
[Database Solution Decision Cube](https://github.com/QuChunhe/study/blob/master/pics/DatabaseSelection.JPG)

A much better approach might be using tiers of data storage; as the data ages in terms of access date, continue to push it off to cheaper and slower-access storage media.We call this the Cost-Value Data Dilemma, which is where the value of data decreases over time and the cost of keeping it increases over time.
一个更好的方法是使用分层的数据存储。随着在数据访问方面数据年龄的增加，持续地将数据转移到更加便宜、访问更慢的存储介质。我们称之为数据的成本-价值困境，即随着时间流失，数据的价值在降低，而保存数据的成本却随着时间在增加。

##### Rule 15—Firewalls, Firewalls Everywhere!
##### 规则15-防火墙，处处皆是防火墙

**What:** Use firewalls only when they significantly reduce risk, and recognize that they cause issues with scalability and availability. 仅仅当能够显著降低风险时才使用防火墙，并且要认识到防火墙会导致可扩展性和可用性问题。

**When to use:** Always.

**How to use:** Employ firewalls for critical PII, PCI (Payment Card Industry) compliance, and so on. Don’t use them for low-value static content.

**Why:** Firewalls can lower availability and cause unnecessary scalability chokepoints.

**Key takeaways:** While firewalls are useful, they are often overused and represent both availability and scalability concerns if not designed and implemented properly.


The decision to employ security measures should ultimately be viewed through the lens of profit maximization.
最终从利润最大化的角度来考量部署安全措施的决定。

Unfortunately, far too many companies view firewalls as an all-or-nothing approach to security. They overuse firewalls and underuse other security approaches that would otherwise make them even more secure. We can’t overstate the impact of firewalls on availability. In our experience, failed firewalls are the number-two driver of site downtime next to failed databases.。
不幸的是，太多的公司将防火墙视为或全有或全无的安全方法。他们过度使用防火墙而没有充分使用其他能够使得他们更加安全的安全方法。我们不能高估防火墙对于可用性的影响。根据我们的经验，防火墙故障是使得网站宕机的第二大因素，仅次于数据库故障。

防火墙是一个边际的安全设备。

However, it is important to keep in mind that any extra hop reduces availability and increases latency regardless of implementation.
但是需要牢记，无论如何实现，任何额外的跳都会降低可用性和增加时延。

##### Rule 16—Actively Use Log Files
##### 规则16-积极地使用日志文件

**What:** Use your application’s log files to diagnose and prevent problems.使用应用日志文件来诊断和防范问题。

**When to use:** Put a process in place that monitors log files and forces people to take action on issues identified.
设置一个过程来监控日志文件，并强迫人们对已经甄别出的问题采取行动

**How to use:** Use any number of monitoring tools from custom scripts to Splunk or the ELK framework to watch your application logs for errors. Export these and assign resources to identify and solve the issue.
可以使用任意数量的监控工具，从自定义脚本到Splunk或者ELK框架，来监视应用日志中的错误。导出这些出错日志并分配资源甄别和解决问题。

**Why:** The log files are excellent sources of information about how your application is performing for your users; don’t throw this resource away without using it.
日志文件是极好的信息来源，其包含了你的应用如何为你的用户提供服务。不要丢掉而不使用这个来源。

**Key takeaways:** Make good use of your log files, and you will have fewer production issues with your system. When issues do occur, you will be able to address them more quickly.

The first step in using log files is to aggregate them.使用日志文件的第一步是聚合它们。

If the amount of data is too large to pull together, there are strategies such as sampling, pulling data from every nth server, that can be implemented. Another strategy is to aggregate the logs from a few servers onto a log server that can then transmit the semiaggregated logs into the final aggregation location. 
如果数据规模过于庞大，无法汇总在一起，那么可以使用一些策略，例如抽样，从第n个服务器提前数据。另一种策略是从一些服务器上汇总日志到一个日志服务器，然后这个日志服务器再发送半聚合的日志到最终的聚合服务器。

This aggregation is generally done through an out-of-band network that is not the same network used for production traffic. What we want to avoid is impacting production traffic from logging, monitoring, or aggregating data.
这种聚合通常是通过带外网络完成的，不同于产品流量所使用的网络。我们所想要的是避免记录、监视和聚合数据影响生产流量。

The next step is to monitor these logs.第二步是监视这些数据。

ELK (Elasticsearch, Logstash, Kibana)

A tool that combines the aggregation and monitoring of log files is Splunk.

Extract, Transform, and Load (ETL)


#### Chapter 5 Get Out of Your Own Way
#### 不要固守成规


##### Rule 17—Don’t Check Your Work
##### 规则17-不要检查你的工作

**What:** Avoid checking and rechecking the work you just performed or immediately reading objects you just wrote within your products. 避免检查或者重复检查你刚刚完成的工作或者理解阅读你刚刚在你的产品中写的对象

**When to use:** Always (see rule conflict in the following explanation). 

**How to use:** Never read what you just wrote for the purpose of validation. Store data in a local or distributed cache if it is required for operations in the near future. 不要为了验证目的而读取刚刚写入的数据。如果在不久的将来需要再次操作数据，那么就将此数据存储在本地或者分布式缓存中。

**Why:** The cost of validating your work is high relative to the unlikely cost of failure. Such activities run counter to cost-effective scaling.
验证你工作的成本要相对高于不太可能发生故障的成本。此类活动与高性价比的可扩展背道而驰。  

**Key takeaways:** Never justify reading something you just wrote for the purpose of validating the data. Trust your persistence tier to notify you of failures, and read and act upon errors associated with the write activity. Avoid other types of reads of recently written data by storing that data locally.


Sure, corruption happens from time to time, but in most cases that corruption is identified during the actual write operation. Writing and then reading a result doubles the transactions on your systems and as a result halves the number of total transactions you may perform to create value. This in turn decreases margins and profitability. A better solution is to simply read the return value of the operation you are performing and trust that it is correct, thereby increasing the number of value-added transactions you can perform. As a side note here, the most appropriate protection against corruption is to properly implement high availability and have multiple copies of data around such as a standby database or replicated storage (see Chapter 9, “Design for Fault Tolerance and Graceful Failure”). Ideally you will ultimately implement multiple live sites (see Chapter 3, “Design to Scale Out Horizontally,” Rule 12).
当然，损坏时常会出现，但是在大多数情况下，损坏能够在写操作过程被发现。写然后查会将你系统中的事务数量翻一番，其后果是你能够执行的、创造价值的事务数量减半。这会降低利润率和盈利能力。一个更高的解决方案是简单地读取你操作所返回的结果并相信其是正确的，从而提高你所执行增值事务的数量。作为此处的旁注，针对于损坏最为合适的保护措施是适当地实现高可用性以及使用数据的多个副本，例如备用数据库或者复制存储。理想情况下，你将最终使用多个活跃站点。

If you just wrote something and you know you are likely to need it again, just keep it around locally.
如果你刚刚写入了一些数据，并且你知道你可能还会读取这些数据，那么将这些数据保存在本地。


Regardless of the case, if the information you are writing is going to be needed in the near future, it makes sense to keep it around, to cache it. See Chapter 6, “Use Caching Aggressively,” for more information on how and what to cache. One nifty trick here in providing users with data they may immediately need is to simply write said data to the screen of the client (again an application or browser) directly rather than requesting the data again. Or pass said data through the URI and use it in subsequent pages.
无论何种情况，如果你正在写入的信息在不远的将来还会需要到，那么通过缓存将这些信息保存在附近是有意义的。参见第6章“勇敢地使用缓存”，以获得更多关于如何和怎样使用缓存的信息。如果在写入数据后，用户立刻需要这些数据，那么一个实用技巧是将数据直接写到客户端（应用或者浏览器）屏幕上，而不是再次查询这些数据。或者通过URI传递这些数据并在后续页面中使用它们。


Storing information locally on a system might be indicative of state and certainly requires affinity to the server to be effective. As such, we’ve violated Rule 40 (see Chapter 10, “Avoid or Distribute State”). At a high level, we agree, and if forced to make a choice we would always develop a stateless application over ensuring that we don’t have to read what we just wrote. That said, our rules are meant to be nomothetic or “generally true” rather than idiographic or “specifically true.” You should absolutely try not to duplicate your work and absolutely try to maintain a largely stateless application. Are these two statements sometimes in conflict? Yes. Is that conf lict resolvable? Absolutely
在一个服务器的本地存储信息可能意味着状态，并且肯定需要对服务器具有亲和性才能有效。如果如此，那么我们就违反了规则40（参考10章避免或者分发状态）。从较高的层次上，我同意，如果被迫作出选择，我将会开发一个无状态的应用，以确保我们不会读取我们刚刚写入的数据。也就是说，我们的规则是普遍适用的或者“通常情况是真实的”，而不是个例或者“特殊情况是真实的”。你绝对不要尝试重复你的工作，并且绝对要尽力维护一个大型的无状态应用。上述两个陈述有时候冲突吗？是的。冲突可以解决吗？当然。


As with any rule, there are likely exceptions.
任何规则都有例外的情况。

##### Rule 18—Stop Redirecting Traffic
##### 规则18——停止重定向流量

**What:** Avoid redirects when possible; use the right method when they are necessary.尽量避免重定向；当需要重定向时，使用正确的方法

**When to use:** Always.

**How to use:** If you must use redirects, consider server configurations instead of HTML or other code-based solutions. 如果你必须使用重定向，考虑服务器配置，以取代HTML或者其他基于代码的方案。

**Why:** Redirects in general delay the user, consume computation resources, are prone to errors, and can negatively affect search engine rankings. 重定向通常会增加用户时延，消耗计算资源，容易出错，并且可能对于搜索引擎排名产生负面影响。

**Key takeaways:** Use redirects correctly and only when necessary.正确使用重定向并且只有当需要时才使用。


HTTP 3xx Status Codes
* 300 Multiple Choices—The requested resource corresponds to any one of many representations and is being provided so that the user can select a preferred representation.
* 301 Moved Permanently—The requested resource has been assigned a new permanent URI, and any future references to this resource should use the URI returned.
* 302 Found—The requested resource resides temporarily under a different URI, but the client should continue to use the Request-URI for future requests.
* 303 See Other—The response to the request can be found under a different URI and should be retrieved using a GET method. This method exists primarily for the PRG design pattern to allow the output of a POST to redirect the user agent.
* 304 Not Modified—If the client has performed a conditional GET request and access is allowed, but the document has not been modified, the server should respond with this status code.
* 305 Use Proxy—The requested resource must be accessed through the proxy given by the Location field.
* 306 (Unused)—This status code is no longer used in the specification.
* 307 Temporary Redirect—The requested resource resides temporarily under a different URI.


##### Rule 19—Relax Temporal Constraints
##### 规则19-放松时间约束

**What:** Alleviate temporal constraints in your system whenever possible. 在你的系统中尽可能地减轻时间约束。

**When to use:** Anytime you are considering adding a constraint that an item or object must maintain a certain state between a user’s actions.当你考虑添加一个约束，使得一个商品或者对象必须在用户行为之间维护一个特定状态时。

**How to use:** Relax constraints in the business rules.在商业规则上放松约束。

**Why:** The difficulty in scaling systems with temporal constraints is significant because of the ACID properties of most RDBMSs.由于大多数RDBMs的ACID属性，具有严格时间约束的可扩展性系统是非常难于实现的。

**Key takeaways:** Carefully consider the need for constraints such as items being available from the time a user views them until the user purchases them. Some possible edge cases where users are disappointed are much easier to compensate for than not being able to scale.请仔细考虑对于约束的需求，例如商品从用户流量到这个用户购买为止一直可用。相对于不能扩展，对一些可能的、令用户失望的极端例子是非常容易弥补的。

constraint satisfaction problems (CSPs) 约束满足问题

temporal constraint satisfaction problem (TCSP),

Most RDBMSs aren’t good at keeping all the data completely consistent between nodes. Even though read replicas or slave databases can be kept within seconds of each other in terms of consistent data, certainly there will be edge cases when two users want to view the last available inventory of a particular item.
大多数的RDBM系统都不擅长于在节点之间保持数据的完全一致性。即使读副本或者从属数据库能够在节点之间实现秒级的数据一致性，当两个用户想要查看一个特定商品的可用库存时，还是可能出现数据不一致的特殊情况。

The CAP Theorem, also known as the Brewer Theorem, so named after computer scientist Eric Brewer, states that three core requirements exist when designing applications in a distributed environment, but it is impossible to simultaneously satisfy
all three requirements. These requirements are expressed in the acronym CAP: 在分布式环境设计应用时，存在三个核心需求，不可能同时满足这三个需求。这个三个需求被缩写为CAP
* Consistency—The client perceives that a set of operations has occurred all at once.一致性
* Availability—Every operation must terminate in an intended response.可用性
* Partition tolerance—Operations will complete, even if individual components are unavailable.抗分区

BASE：“basically available, soft state, and eventually consistent”

A BASE architecture allows for the databases to become consistent, eventually. This might be minutes or even just seconds, but as we saw in the previous example, even milliseconds of inconsistency can cause problems if our application expects to be able to “lock” the data。
BASE架构许可数据库最终变得一致。这个过程可能需要数分钟，或者仅仅数秒钟，但是我们从之前的例子中看到，即使存在毫秒级的不一致。如果我们的应用期望能够锁住数据，那么也能导致问题


The way we would redesign our system to accommodate this eventual consistency would be to relax the temporal constraint. The user just viewing an item would not guarantee that it is available. The application would “lock” the data when the item is placed into a shopping cart, and this would be done on the primary write copy or master database. Because we have ACID properties, we can guarantee that if our transaction completes and we mark the record of the item as “locked,” then that user can continue through the purchase confident that the item is reserved. Other users viewing the item may or may not have it available for them to purchase.
重新设计我们的系统以适应上述最终一致性的方式是放松时间约束。在用户正在浏览一个商品时，并不能保证该商品可以被购买。当商品被放置到购物篮，应用将会“锁定”数据，并且这个操作是在主写拷贝或者主数据库上完成的。由于ACID数据，我们能够保证一旦我们事务完成，我们将商品的记录标记为“已经锁定”，然后在确信商品被预留，用户能够继续购物。其他浏览这个商品的用户，可能会或者可能不会获知这个商品已经不能被订购。

Another area in which temporal constraints are commonly found in applications is the transfer of items (money) or communications between users. The PayPal example with which we opened this chapter is a great example of such a constraint. Guaranteeing that user A gets the money, message, or item in his or her account as soon as user B sends it is easy on a single database. Spreading out the data among several copies of the data makes this consistency much more difficult. The way to solve this is to not expect or require the temporal constraint of instant transfer. More than likely it is totally acceptable that user A waits a few seconds before seeing the money that user B sent. The reason is simply that most dyads don’t synchronously transfer items in a system. Obviously synchronous communication such as chat is different.
另一个经常在应用中发现时间约束的领域是在用户之间的商品（钱）转账或者通信。一旦用户B发送完毕，用户A就能够在他或者她的账号中获得钱、消息或者商品，在单个数据库中非常容易确保上述过程。在多个副本之间扩散数据使得一致性非常难以实现。解决这一问题的方法是不要期望或者不要要求实时转账的时间约束。用户完全可以接受在用户B发送之后需，用户A需要等待几秒钟才能看到钱。原因非常简单，双方不会在一个系统中同步转移商品。显然，例如聊天这样的同步通信是不同的。



两个问题：
* 数据一致性问题：各个副本如何保持与写入数据是一样的
* 分布式事务问题

#### Chapter 5 Use Caching Aggressively
#### 第5章 大胆地使用缓存

Caching prevents you from needing to look up, create, or serve the same data over and over again. 缓存能够阻止你一次又一次地查询、创建或者服务于相同的数据


Scaling static content, such as text and images that don’t change very often, is elementary. A number of rules in this book cover how to make static content highly available and scalable at low cost through the use of caches. Dynamic content, or content that changes over time, is not so elementary to serve quickly and scale out.
例如文本和图片这类静态内容不经常变化，因此实现静态内容的可扩展性比较容易。本书中的一些规则涉及如何利用缓存，使得静态内容以较低成本实现高可用和可扩展。动态内容内容或者随着时间变化的内容不容易实现快速响应和可扩展。

1）：
To solve latency and scale issues, the first thing Lon’s team did was to add a content distribution network; they chose Akamai. Lon stated, “It was really simple to just take all of our static assets and push them there [Akamai] and let them handle caching closest to the user. And then we could expire [the objects] using their typical cache expiration tools when we published. Expiring objects was part of our deploy process.”
为了解决时延和可扩展性问题，Lon团队所做的一个事情就是添加内容分发网络，他们选择了Akamai。Lon说“真的非常简单，仅仅提取所有静态资产并将它们推送到Akamai，让Akamai将数据缓存到离用户最近的位置。然后当我们要发布时，我们可用使用通常的缓存过期工具将这些缓存的对象设置为过期。将对象设置为过期时我们部署过程的一部分

2）
Next Lon’s team started profiling the application to understand what was causing slow load times.
下一步Lon团队开始对于分析应用性能，排查导致加载时间慢的原因。


3）
Another challenge Lon and his team faced was that product detail pages changed on a regular basis.
Each deployment would then invalidate any number of caches, causing high load on servers and slower response times to end customers. Lon’s team closely monitored the cache hit/miss ratios. Determining that most of the changes were really small, Lon decided to build a small content management system that allowed the merchandisers to use a proprietary markup language to change information displayed, such as the price of the product, the SKU, and the content descriptions, without affecting the overall layout, the Cascading Style Sheets (CSS), or other assets, leaving the cache intact. This approach not only reduced the load on his development team but allowed assets to continue to be cached, thereby eliminating the increases in server load and customer response time.
Lon和其团队面临的另一个条件是产品详细页面会定期的更新。每次部署都会使得大量缓存失效，造成服务器的高负载和对终端用户更低的响应时间。Lon团队密切监测系统的命中/没命中之比，确认大多数的更新都是非常小的，因此Lon决定构建一个小型的内容管理系统，许可商户需用一个专门的标记语言修改所展示的信息，例如商品的价格、SKU和内容表述，而不影响整个的布局、CSS或其他资产，以保持缓存的完整性。这种方法不仅减小了部署团队的工作，而且许可资产持续被缓存，从而减小了服务器的负载和用户的响应时间。

But the cost of caching full static pages was fairly high. Instead, Lon decided to pre-render sections of the page and then assemble them at the time of request. Lon recalled, “At the top of the page you have a view of the different images related to a product. This stuff didn’t change that much, except for perhaps the price. So we would change the layout of the page in such a way where we could grab a huge chunk of that HTML, pre-render it, and cache a CLOB [character large object] in memory using Memcached. Memcached would distribute it across our cluster of application servers, making it super-easy. We proactively expired that cache based on business changes to data. We wouldn’t proactively pre-render it, so the first request still took some time. Every call but the first call went really, really fast. One of the reasons that netted out to be faster is because we were able to get rid of those Ajax calls that I mentioned when we were doing the full reverse proxy caching.
但是缓存全部静态页面的成本还是比较高。相反地，Lon决定预先提交页面的各个部分，并且在请求的时刻将这些部分组装成页面。Lon回忆道”在每个页面的上部存在一个与产品相关的、由不同图片所组成的视图。除了价格之外，这些内容不会变化太多。因此，我们采用如下方式更改页面的布局，提取HTML的大块并预先提交它们，然后使用Memcached在内存中缓存BLOB（大对象）。Memcached将会跨越应用服务器集群分发这些BLOB，使得缓存非常容易。基于这些数据在业务上的变化，我们会主动地过期缓存数据。我们不会预先提交，因此第一个访问仍然花费一些时间。除了第一个请求，每次请求都会非常非常块的实现。对外连接会更快的一个原因是我们使用了全部的反向代理缓存，从而消除了我们提到的Ajax请求。


As Lon described it, “Those business objects were like compositions. And those are where we had a caching rule. So what would happen, just to give you a sense of this, is a user would request a particular product. A product was a business object that might contain data from 20 different tables or views. So we’d bring these together, form a business object, and then cache that business object. We’d have a nice fully composed concept that was really meaningful to the business. The cost of assembling them is a little high, but the cost of caching them is relatively low because they really are only a bunch of text. A fully composed product model, there’s not that much in there, maybe a few hundred bytes. So we ended up having this business engine that sat in our business access layer that would be able to proactively expire these business objects. And they were really great. We had a lot of debates about what things belonged in there. For example, does it ever make sense to cache a customer object? This was a very hotly debated topic for our organization because if you’re a customer, while you’re on the site we reuse your customer object in your session quite a bit, but it’s just within your session.”
正如Lon描述的“这些业务对象倾向于组合。这也是我们缓存规则所在。所发生的事情给你一种感觉，一个用户将会请求一个特定的产品。这个产品是一个业务对象，其包含来自20多个不同表或者视图的数据。因此我们将这些数据集成在一起，形成一个业务对象，然后缓存这些业务对象。我们已经就有了完整的合成概念，其具有真正的业务意义。组装这些数据的代价有点高，但是缓存这些数据的代价却相对低，因为它们仅仅是一组文本而已。一个完整的合成产品模型，没有那么多数据，可能仅仅是几百字节。因此，我们最终使用了业务引擎，其位于我们业务访问层，并能够主动过期这些业务对象。它们真的很棒。关于能够将什么放入这个业务引擎中，我们有很多争论。例如，缓存业务对象是否有意义？对于我们的组织，这是一个非常火热的争论话题，因为如果你是一个客户，当你登录我们的网站时，我们会在你的会话中复用你的客户对象，但是这种复用仅仅在你的会话中。”


##### Rule 20—Leverage Content Delivery Networks
##### 规则20-充分利用内容分发网络

**What:** Use CDNs (content delivery networks) to offload traffic from your site. 使用CDN分担你网站的流量

**When to use:** When speed improvements and scale warrant the additional cost. 当需要提高速度并能够承担更多成本时

**How to use:** Most CDNs leverage DNS to serve content on your site’s behalf. Thus you may need to make minor DNS changes or additions and move content to be served from new subdomains.
大多数CDN使用DNS来代表你的网站提供内容。因此，你可能需要对DNS做一些小改动或者添加，并且需要转移内容，以在新的子域名下提供服务。

**Why:** CDNs help offload traffic spikes and are often economical ways to scale parts of a site’s traffic. They also often substantially improve page download times. 
CDN有助于减轻流量峰值，是扩展部分网站流量的一种经济方式。CDN通常还可以提高页面下载速度。

**Key takeaways:** CDNs are a fast and simple way to offset spikiness of traffic as well as traffic growth in general. Make sure you perform a cost-benefit analysis and monitor the CDN usage.
CNDs是一种快速和简单的方式，既能用于分流突发的流量，也能应对一般性的流量增长。确保进行成本效益分析，并监控CDN的使用情况。

##### Rule 21—Use Expires Headers
##### 规则21-使用过期头部标志

What: Use Expires headers to reduce requests and improve the scalability and performance of your system.
使用过期头部标志，以降低请求次数和提高你系统的可扩展性和性能。

When to use: All object types need to be considered.
所有的对象类型都需要考虑

How to use: Headers can be set on Web servers or through application code.
头部标志能够在web服务器上或者通过应用代码来设置。

Why: The reduction of object requests increases the page performance for the user and decreases the number of requests your system must handle per user.
减小对象请求次数不仅可以提高用户的页面访问性能，并且可以减小你系统针对每个用户必须处理的请求数量。

Key takeaways: For each object type (image, HTML, CSS, PHP, and so on), consider how long the object can be cached and implement the appropriate header for that time frame.
针对于每个对象类型（图片、HTML、CSS和PHP等），考虑对象可能的缓存时长，并且通过适当的头部标志来实现特定时间的缓存，

通过如下的头部标志实现缓存
* Pragma
* Expires
* Cache-Control
* Last-Modified:
* ETag

Keep-alives, or HTTP persistent connections

##### Rule 22—Cache Ajax Calls
##### 规则22-缓存Ajax调用

What: Use appropriate HTTP response headers to ensure cacheability of Ajax calls. 使用适当的HTTP应答头部标志，以确保Ajax调用的可缓存性。

When to use: Every Ajax call except for those absolutely requiring real-time data that are likely to have been recently updated. 每个Ajax调用，除了那些绝对需要实时性数据（最近更新的数据）的情况

How to use: Modify Last-Modified, Cache-Control, and Expires headers appropriately. 恰当地更改Last-Modified, Cache-Control, and Expires头部标识。

Why: Decrease user-perceived response time, increase user satisfaction, and increase the scalability of your platform or solution. 降低用户所能感觉到的响应时间，提高用户的满意度，并提高系统或者解决方案的可扩展性。

Key takeaways: Leverage Ajax and cache Ajax calls as much as possible to increase user satisfaction and increase scalability. 尽可能地使用Ajax和缓存Ajax调用，以提高用户满意度和可扩展性。

Ajax is an acronym for Asynchronous JavaScript and XML.Ajax是异步Javascrip和XML的缩写。


##### Rule 23—Leverage Page Caches
##### 规则23-充分利用页面缓存

What: Deploy page caches in front of your Web services. 在Web服务的前端部署页面缓存

When to use: Always.总是

How to use: Choose a caching solution and deploy. 选择并部署一种缓存方案

Why: Decrease load on Web servers by caching and delivering previously generated dynamic requests and quickly answering calls for static objects. 通过缓存和传递之前生成的动态请求以及快速响应静态对象的调用，以减小web服务器的负载。

Key takeaways: Page caches are a great way to offload dynamic requests, decrease customer response time, and scale cost-effectively. 页面缓存是一种强大的方法，用于减少动态请求，降低服务响应时间和实现高成本效益的可扩展性。

A page cache is a caching server you install in front of your Web servers to offload requests for both static and dynamic objects from those servers. Other common names for such a system or server are reverse proxy cache, reverse proxy server, and reverse proxy. 页面缓存是一个安装在Web服务器之前的缓存服务器，用于减小针对这个服务器的动态和静态对象请求。针对这类系统或者服务器的另一些常用名字是反向代理缓存(Reverse Proxy Cache)、反向代理服务器和反向代理。

Page caches handle some or all of the requests until the pages or data that is stored in them is out of date or until the server receives a request for which it does not have the data. A failed request is known as a cache miss and might be a result of either a full cache with no room for the most recent request or an incompletely filled cache having either a low rate of requests or a recent restart. The cache miss is passed along to the Web server, which answers and populates the cache with the request, either replacing the least-recently-used record or taking up an unoccupied space
页面缓存处理部分或者全部的请求，直到所存储的页面或者数据过期为止或者服务器收到没有缓存对应数据的请求。一个失败的请求被称为缓存未命中，造成缓存未命中的原因或者是缓存已满，没有多余的空间用来缓存最近的请求，或者虽然缓存尚未填满，但是请求的速率过低或者最近重启过缓存。缓存未命中的请求将会传递到Web服务器，其将会应答请求并使用请求填充缓存，或者替换最近使用最少的记录或者使用尚未占用的空间。

There are three key points we emphasize in this rule. The first is that you should implement a page (or reverse proxy) cache in front of your Web servers and in doing so you will get a significant scalability benefit. 针对于此规则我们需要强调三点。第一点，你需要在你的Web服务器的前面实现页面缓存，一旦如此，你将会得到显著的可扩展性收益。

The second point is that you need to use the appropriate HTTP headers to ensure the greatest (but also business-appropriate) cache potential of your content and results.第二点，你需要使用适当的HTTP头部标签，以确保将内容和结果的缓存潜力最大化。

Our third point is that where possible you should include another HTTP header from RFC 2616 to help maximize the cacheability of your content. This new header is known as the ETag. The ETag, or entity tag, was developed to facilitate the method of If-None-Match conditional GET requests by clients of a server. ETags are unique identifiers issued by the server for an object at the time of first request by a browser. If the resource on the server side is changed, a new ETag is assigned to it. Assuming appropriate support by the browser (client), the object and its ETag are cached by the browser, and subsequent If-None-Match requests by the browser to the Web server will include the tag. If the tag matches, the server may respond with an HTTP 304 Not Modified response. If the tag is inconsistent with that on the server, the server will issue the updated object and its associated ETag。
第三点，你需要尽可能地包含RFC 2616中的另一个HTTP头部标签，以帮助你将内容的可缓存性最大化。这个新的头部标签被称为ETag。开发ETag，或者实体标签（entity tag），便于服务器处理来自客户端的、IF-None-Match条件的GET请求。ETags是由服务器发布的唯一标识符，用于来自浏览器的第一次请求那些对象。如果在服务端的资源发生改变，那么一个新的ETag会被分配给这个资源。假设浏览器（客户端）能够提供适当的支持，缓存对象和其ETag，那么由浏览器向服务器发起的If-None-Match请求时就会包含这个标签。如果来自浏览器的标签与服务器的标签相互匹配，那么服务器可能返回一个HTTP 304 Not Modified应答。如果tag与服务器上的不一致，那么服务器将会返回被更新的对象和相关联的ETag。

##### Rule 24—Utilize Application Caches
##### 规则24-使用应用缓存

What: Make use of application caching to scale cost-effectively. 利用应用缓存实现经济高效的可扩展性。

When to use: Whenever there is a need to improve scalability and reduce costs. 当需要提高可扩展性和降低成本时

How to use: Maximize the impact of application caching by analyzing how to split the architecture first. 首先通过分析如何分解系统，将应用缓存的作用最大化，

Why: Application caching provides the ability to scale cost-effectively but should be complementary to the architecture of the system. 应用缓存提供了经济高效的可扩展能力，但是应用缓存需要依赖于系统的架构。

Key takeaways: Consider how to split the application by Y axis (Rule 8) or Z axis (Rule 9) before applying application caching in order to maximize the effectiveness from both cost and scalability perspectives. 在使用应用缓存之前为了将成本和可扩展性前景的有效性最大化，考虑如何沿着X轴（规则8）和Z轴（规则9）分解应用。


This isn’t a section on how to develop an application cache.Rather we are going to make two basic but important points:
本节并不介绍如何开发一个应用缓存，而是给出两个基本但是重要的结论
* The first is that you absolutely must employ application-level caching if you want to scale in a cost-effective manner. 第一个是如果你想要一种经济高效的方式实现可扩展性，那么你绝对地需要部署应用级别的缓存
* The second is that such caching must be developed from a systems architecture perspective to be effective long term. 第二个这种缓存必须从系统架构的视角开发，才能长期有效。


With any luck, you’ve identified a pattern in this rule. The first step is to hypothesize as to likely usage and determine ways to split to maximize cacheability. After implementing these splits in both the application and supporting persistent data stores, evaluate their effectiveness in production. Further refine your approach based on production data, and iteratively apply the Pareto Principle and the AKF Scale Cube (Rules 7, 8, and 9) to refine and increase cache hit rates. Lather, rinse, repeat.
运气好的话，你已经识别出这个规则中的模式。第一步是假设可能的使用并确定拆分方式以将可缓存性最大化。在应用和支撑持久化的数据存储中实现上述分解后，评估这些分解在生产上的有效性。基于生产数据，进一步改进你的方法，迭代地应用帕瓦罗原则和AKF可扩展立方（规则7、8和9），持续地改进和提高缓存命中率。


##### Rule 25—Make Use of Object Caches
##### 规则25-使用对象缓存

What: Implement object caches to help scale your persistence tier. 实现对象缓存，帮助持久化层的可扩展。

When to use: Anytime you have repetitive queries or computations. 任何你有重复请求或者技术的时候。

How to use: Select any one of the many open-source or vendor-supported solutions and implement the calls in your application code. 从众多的开源和厂家支持的解决方案中选择任何一个，并在你的应用代码中实现相应的调用

Why: A fairly straightforward object cache implementation can save a lot of computational resources on application servers or database servers. 即使实现一个相对简单的对象缓存，也能够节省大量应用服务器或者数据库服务器的的计算资源。

Key takeaways: Consider implementing an object cache anywhere computations are performed repeatedly, but primarily this is done between the database and application tiers. 虽然任何存在重复计算的地方都需要考虑实现一个对象缓存，但是首先在数据和应用层之间考虑。



Object caches are most often implemented between the database and the application to cache result sets from SQL queries. However, some people use object caches for results of complex application computations such as user recommendations, product prioritization, or reordering advertisements based on recent past performance. The object cache in front of a database tier is the most popular implementation because often the database is the most difficult and most expensive to scale. If you have the ability to postpone the split of a database or the purchase of a larger server, which is not a recommended approach to scaling, by implementing an object cache this is an easy decision. Let’s talk about how to decide when to pull the trigger and implement an object cache.
对象缓存通常位于数据和应用之间，缓存来自SQL查询的结果。然而，一些人使用对象缓存缓存复杂应用计算的结果，例如基于最近的操作的用户推荐、产品排列或者广告重排。在数据库层之前部署对象缓存是最为常见的实现，因为数据库是最难以可扩展，扩展成本也最为高昂。实现对象缓存是一种简单的方式，能够推迟拆分数据库或者购买更大型的服务器（并不推荐使用此种方式实现可扩展）。让我们来讨论如何决定在何时出发并实现对象缓存。


Besides the normal suspects of CPU and memory utilization by the database, one of the most telling pieces of data that indicates when your system is in need of an object cache is the Top SQL report. This is a generic name for any report generated (or tool used) to show the most frequent and most resource-intensive queries run on the database.
除了常规地推测数据库CPU和内存的使用率，另一个具有说服力的数据是TOP SQL报告，可以提示你系统需要对象缓存了。这是针对于一类生成（或者使用工具）报告的通用性名称，这类报告显示在数据库中使用最为频繁和资源最为密集的查询。


Once you’ve decided you need an implementation of an object cache, you need to choose one that best fits your needs. A word of caution for those engineering teams that at this point might be considering building a home-grown solution. There are more than enough production-grade object cache solutions to choose from.
一旦已经决定需要实现对象缓存，你需要选择一个最适合你需求的方案。在此时对于考虑构建自有方案的工程团队需要谨慎，因为具有大量的产品级的对象缓存解决可供选择。
While there are possible reasons that might drive you to make a decision to build an object cache instead of buying/using an open-source product, this decision should be highly scrutinized.
虽然有适当的原因驱动我们作出构建对象缓存而不是购买/使用开源的产品的决定，但是需要仔细的审视这种决定。


The next step is to actually implement the object cache, which is generally straightforward.
下一步是实际地实现对象缓存，这通常非常简单。

The final step in implementing the object cache is to monitor it for the cache hit rate. This ratio is the number of times the system requests an object that is in the cache compared to the total number of requests. Ideally this ratio is 85% or better, meaning that requests for objects not in cache or expired in cache occur only 15% or less of the time. If the cache hit ratio drops, you need to consider adding more object cache servers.
实现对象缓存的最后一个步骤是监控其缓存命中率。这个命中率是对象正好在缓存中的系统请求数量与总的请求数量的比值。理想条件下，命中率为85%，甚至更高，这意味着请求一个对象并且这个对象不在缓存中或者虽然在但是已经过期的情况仅仅占15%，或者更少。如果缓存命中率下降，则需要考虑添加更多的缓存服务器。


##### Rule 26—Put Object Caches on Their Own “Tier”
##### 规则26——将对象缓存放置到它们自己的层级中

What: Use a separate tier in your architecture for object caches. 在架构中针对于对象缓存使用一个分离的层级。

When to use: Anytime you have implemented object caches. 任何已经实现对象缓存的时候

How to use: Move object caches onto their own servers. 将对象缓存转移到自己的服务器

Why: The benefits of a separate tier are better utilization of memory and CPU resources and having the ability to scale the object cache independently of other tiers. 分离层级的好处是更好地利用CPU和内存资源，能够独立其他层级扩展对象缓存。

Key takeaways: When implementing an object cache, it is simplest to put the service on an existing tier such as the application servers. Consider implementing or moving the object cache to its own tier for better performance and scalability. 当实现对象缓存时，最简单的方式是将服务放置到一个已经存在的层级上，例如应用服务器。为了获得更好的性能和可扩展项，可以考虑在自己的层级上实现对象缓存或者将对象缓存转移到自己的层级上。


A better alternative is to put the object cache on its own tier of servers. This would be between the application servers and the database, if using the object cache to cache query result sets. If caching objects created in the application tier, this object cache tier would reside between the Web and application servers.
一个更好的选择是将对象缓存放置到其自己层级中的服务器上。如果使用对象缓存来缓存查询结果集，则这个位置为应用服务器和数据库之间。如果如果在应用层级创建所缓存的对象，则对象缓存层级将位于web和应用服务器之间。

![Object Cache]((pics/ObjectCache.JPG)


The AKF Scale Cube is a three dimentional approach to building applications that can scal infinitely.
* X Axis scaling: Cloning/Replicating. X axis scaling consists of running N instances of a cloned application or replicated database. Proxied by a load balancer, each instance handlers 1/Nth the load.
* Y Axis Scaling: Split Disimilar Thing. Scaling on the Y Axis consists of functional decomposition. Monoliths are separated along functional or resource oriented boundaries to create macro and microservices. This allows you to scale earch service independently and apply more resources only the services that need them.
* Z Axis Scaling: Split Similar Things. Scaling on the Z Axis consists of each server running the same code but for only a subset (or shard - 1/Nth) of the data. The most common Z axis split is by geography for B2C implementations, which can also enable faster response times. B2B implementations commonly split along a company or group of companies boundary.


AKF Scale Cube
* X-Axis: Horizontal Duplication and Cloning of services and data
* Y-Axis: Functional Decomposition and Segmentation - Microservices (or micro-services)
* Z-Axis: Service and Data Partitioning along Customer Boundaries - Shards/Pods










[Scalability Rules - Reduce Objects to Improve Website Performance (Rule 5)](https://akfpartners.com/growth-blog/scalability-rules-reduce-objects-to-improve-website-performance)

# 分布式存储

2000 集中式元数据管理：集中式元数据服务器，分布式存储节点。性能高、存储空间利用率高。元数据节点是系统瓶颈、高可用问题

2010s 去中心化，用计算的方式来定位，而不是利用查表的方式。一致性Hash.无单点性能瓶颈、文件数理几乎不受限制；磁盘空间利用率不高、管理困难、目录操作性能低

{},
   author =    {},
   publisher = {},
   isbn =      {3658245484, 978-3658245481},
   year =      {},

Andreas Meier, Michael Kaufmann,SQL & NoSQL Databases: Models, Languages, Consistency Options and Architectures for Big Data Management,Springer,2019


# Course




# Open Source

## Zookeeper

### command

srvr

### configuration

```
tickTime=2000
dataDir=/var/lib/zookeeper
clientPort=2181
#the initLimit is the amount of time to allow followers to connect with a leader.
initLimit=20
#The syncLimit value limits how out-of-sync followers can be with the leader.
syncLimit=5
		
#server.X=hostname:peerPort:leaderPort
server.1=zoo1.example.com:2888:3888
server.2=zoo2.example.com:2888:3888
server.3=zoo3.example.com:2888:3888
```

## Mesos


[Mesos: A Platform for Fine-Grained Resource Sharing in the Data Center](https://people.eecs.berkeley.edu/~alig/papers/mesos.pdf)


## Kafka


[kafka-examples](https://github.com/gwenshap/kafka-examples)

### Broker Configuration

```
zookeeper.connect
broker.id
```

kafka-run-class.sh
```
LOG_DIR="/home/admkafka/logs"
```

```
nohup /usr/local/kafka_2.12-1.1.0/bin/kafka-server-start.sh /usr/local/kafka_2.12-1.1.0/config/server.properties &
nohup /usr/local/kafka_2.12-1.1.0/bin/zookeeper-server-start.sh /usr/local/kafka_2.12-1.1.0/config/zookeeper.properties &
```

Command
```
kafka-topics.sh --zookeeper 127.0.0.1:2181 --list
kafka-topics.sh --zookeeper 127.0.0.1:2181 --create --replication-factor 1 --partitions 1 --topic mysql
kafka-topics.sh --zookeeper 127.0.0.1:2181 --delete --topic mysql
kafka-topics.sh --zookeeper 127.0.0.1:2181 --alter --topic mysql --partitions 5

kafka-consumer-groups.sh --bootstrap-server 127.0.0.1:9092  --list
kafka-consumer-groups.sh --bootstrap-server 127.0.0.1:9092  --describe --group trader

kafka-console-consumer.sh --zookeeper 127.0.0.1:2181 --topic reports --from-beginning

kafka-console-producer.sh --broker-list 127.0.0.1:9092 --topic service-request --property print.key=true
```
#### Neha Narkhede, Gwen Shapira, and Todd Palino. Kafka: The Definitive Guide. O’Reilly Media, Inc. 2017

There are three primary methods of sending messages:
- Fire-and-forget
- Synchronous send
- Asynchronous send

[73]
Setting session.timeout.ms lower than the default will allow consumer groups to detect and recover from failure
sooner, but may also cause unwanted rebalances as a result of consumers taking longer to complete the poll loop or garbage collection. Setting session.timeout.ms higher will reduce the chance of accidental rebalance, but also means it will take
longer to detect a real failure.


[75]
receive.buffer.bytes and send.buffer.bytes: It can be a good idea to increase those when producers or consumers communicate with brokers in a different datacenter, because those network links typically have higher latency and lower bandwidth.


[77]
By setting auto.commit.offset=false, offsets will only be committed when the application explicitly chooses to do so. The simplest and most reliable of the commit APIs is commitSync().


[78]~[80]  
Combining Synchronous and Asynchronous Commits
- commitSync() will retry the commit until it either succeeds or encounters a nonretriable failure,
- commitAsync() will not retry

[86]  
Note that consumer.wakeup() is the only consumer method that is safe to call from a different thread.  
Before exiting the thread, you must call consumer.close().






## Spark

### Build

#if use scala 2.12
./dev/change-scala-version.sh 2.12

build/mvn -Pmesos -DskipTests clean package

[Running Spark on Mesos](https://spark.apache.org/docs/latest/running-on-mesos.html)

hadoop fs -copyFromLocal spark-2.4.0-bin-custom-spark.tgz  hdfs://master.hadoop:10000/spark/lib/

### Configuration

vim conf/spark-env.sh
```
# Options read by executors and drivers running inside the cluster
# - SPARK_LOCAL_IP, to set the IP address Spark binds to on this node
# - SPARK_PUBLIC_DNS, to set the public DNS name of the driver program
# - SPARK_CLASSPATH, default classpath entries to append
# - SPARK_LOCAL_DIRS, storage directories to use on this node for shuffle and RDD data
# - MESOS_NATIVE_JAVA_LIBRARY, to point to your libmesos.so if you use Mesos
MESOS_NATIVE_JAVA_LIBRARY=/usr/local/mesos/lib/libmesos.so
SPARK_EXECUTOR_URI=hdfs://master.hadoop:10000/spark/lib/spark-2.4.0-bin-custom-spark.tgz
SPARK_LOG_DIR=hdfs://master.hadoop:10000/spark/logs
SPARK_LOCAL_IP=192.168.1.5
SPARK_LOCAL_DIRS=/home/hadoop/spark
```

vim conf/spark-defaults.conf
```
spark.executor.uri  hdfs://master.hadoop:10000/spark/lib/spark-2.4.0-bin-custom-spark.tgz
spark.master        mesos://192.168.1.5:7077
spark.eventLog.dir  hdfs://master.hadoop:10000/spark/logs
```
vim /etc/profile
```
SPARK_HOME=/usr/local/spark
EXPORT SPARK_HOME
```

configure hostname for every nodes   

vim /etc/hostname
```
node7.beijing
```
vim /etc/sysconfig/network
```
HOSTNAME=node7.beijing
```
vim /etc/hosts
```
192.168.1.7 node7.beijing
192.168.1.6 node6.beijing
192.168.1.5 node5.beijing
192.168.1.3 node3.beijing
192.168.1.2 node2.beijing
```

```
hostname node5.beijing
```

### Run

```
/usr/local/spark/sbin/start-mesos-dispatcher.sh -m mesos://192.168.1.5:5050 -h 192.168.1.5 --webui-port 8087 --name SparkFramework

http://192.168.1.5:8087/
```

```
export PYSPARK_PYTHON=/usr/local/anaconda3/bin/python3
```



  
## Flink
There are two basic kinds of state in Flink: Keyed State and Operator State.

Keyed State is always relative to keys and can only be used in functions and operators on a KeyedStream.

With Operator State (or non-keyed state), each operator state is bound to one parallel operator instance. The Kafka Connector is a good motivating example for the use of Operator State in Flink. 

Keyed State and Operator State exist in two forms: managed and raw.

Managed State is represented in data structures controlled by the Flink runtime, such as internal hash tables, or RocksDB. Examples are “ValueState”, “ListState”, etc. Flink’s runtime encodes the states and writes them into the checkpoints.

Raw State is state that operators keep in their own data structures. When checkpointed, they only write a sequence of bytes into the checkpoint. Flink knows nothing about the state’s data structures and sees only the raw bytes.

A third type of supported operator state is the Broadcast State. Broadcast state was introduced to support use cases where some data coming from one stream is required to be broadcasted to all downstream tasks, where it is stored locally and is used to process all incoming elements on the other stream.


* Pattern

MapReduce pattern
* map part (distribution of work).


＃ Patterns

[稳定性模式大全（Stability Patterns）](https://mp.weixin.qq.com/s?__biz=MzIxMzEzMjM5NQ==&mid=2651036295&idx=2&sn=84c81f52fd1d915e7a8a70985d3e9d16&chksm=8c4c4f83bb3bc695cad976bbafc7e977995b548e5545c319ec1487fb32bd25dbf554702e7eff&mpshare=1&scene=1&srcid=0504wRpYm31npqZ7x6azDg5r&sharer_sharetime=1588554674432&sharer_shareid=fc937fe50a97e6c10553c542abe0a39b&exportkey=Aa9aSiFEz46Dkrw1Lg%2Be0T8%3D&pass_ticket=a43aJERQMX9BbF%2FHWomrWkZFBaA3Ze0Kb4Lh0aokJrwblRbybCbiYCDvafpfxaWM#rd)


[Scalability, Availability & Stability Patterns](https://tehlug.org/presentations/92_07_23_scalability_Patterns.pdf)

https://www.slideshare.net/jboner/scalability-availability-stability-patterns/164-Stability_Patterns

https://www.slideshare.net/jboner/scalability-availability-stability-patterns

[awesome-scalability](https://github.com/binhnguyennus/awesome-scalability)


[How To Scale Your Software Product](https://www.devteam.space/blog/how-to-scale-your-software-product/)


[Scalability Design Principles](https://elastisys.com/scalability-design-principles/)

The different dimensions of software scalability
* Scalability of performance: You need high performance to support more users, and adding more capacity can help to improve the performance of the software. However, this is subject to limits since performance doesn’t scale linearly.
* Scalability of availability: You need to weigh between consistency, availability, and partition tolerance when designing a scalable system. A system with strong consistency lets users read the most recent updates immediately, however, this impacts the other two. You might need to settle for eventual consistency, i.e., users will eventually see all the updates, although with a minor time lag.
* Scalability of maintenance: Software and their IT infrastructure need regular maintenance, which is a key consideration while designing scalable systems.
* Scalability of expenditure: Building everything by yourselves offers many customization options, however, it increases both development and maintenance costs. Using available market-leading components may give fewer customization options, however, they cost less. It’s easier to find people to support such components, which reduces your maintenance costs.

How do you scale your software product
* Avoid a “Single Point of Failure” (SPOF)
* Scale horizontally instead of scaling vertically
* Use the right architecture pattern
  * Layered (n-tier) architecture
  * Event-driven architecture
  * Microservices architecture
  * Microkernel architecture
  * Space-based architecture:
* Identify the metrics to track scalability
  * Memory utilization;
  * CPU usage;
  * Network I/O;
  * Disk I/O.
* Use cloud computing smartly
* Push workload to clients and use APIs
* Use caching to improve scalability
* Use the right databases to achieve scalability
* Make the right choice of technology


[Availability and Single Points of Failure](https://docs.oracle.com/cd/E19424-01/820-4806/fjdch/index.html)

SPOFs can be divided into three categories:
* Hardware failures, for example, server crashes, network failures, power failures, or disk drive crashes
* Software failures, for example, Directory Server or Directory Proxy Server crashes
* Database corruption


**Timeouts Pattern**

Always use timeouts (if possible)

**Circuit Breaker Pattern（断路器模式）**


# Performance

[8 Key Application Performance Metrics & How to Measure Them](https://stackify.com/application-performance-metrics/)


# Reliability & Avaibility


三个的区别与联系
* Availability
* Reliability
* Resiliency

Stability 


Mean time between failures (MTBF)，平均无故障工作时间或者平均故障间隔时间，在工作环境条件下两个故障之间时间的平均值。MTBF越长表示可靠性越高正确工作能力越强 。

MTBF用于可修复系统（repairable systems）,而MTTF用于表示不可修复系统（non-repairable systems）中的期望故障时间。

mean time to failure (MTTF），平均无故障时间，故障前平均时间

Mean Time To Repair (MTTR) 平均修复时间，就是从出现故障到恢复中间的这段时间。MTTR越短表示易恢复性越好 

故障表现无法按照预期正常地响应服务请求，包括多
* 无法响应服务请求
* 返回错误的应答
* 服务时间或者响应时间超长

及时和正确地处理故障，较小故障所引发的不利影响或者损失。

[MTTR, MTBF, or MTTF? – A Simple Guide To Failure Metrics](https://limblecmms.com/blog/mttr-mtbf-mttf-guide-to-failure-metrics/)


As we’ll show in the failure metrics calculations below, the following inputs must be collected as part of your maintenance history:
* Labor hours spent on maintenance
* Number of breakdowns
* Operational time (can be calculated from total expected operating hours per week – total equipment downtime)


Mean Time To Repair (MTTR) refers to the amount of time required to repair a system and restore it to full functionality.

The MTTR clock starts ticking when the repairs start and it goes on until operations are restored. This includes repair time, testing period, and return to the normal operating condition.

MTTR = (total maintenance time)/(total number of repairs)

MTTR: Mean Time To Repair vs Mean Time To Recovery

Mean Time To Recovery is a measure of the time between the point at which the failure is first discovered until the point at which the equipment returns to operation. So, in addition to repair time, testing period, and return to normal operating condition, it captures failure notification time and diagnosis.

MTBF = (total operational time)/(total number of failures)

Mean Time To Failure (MTTF) is a very basic measure of reliability used for non-repairable systems. It represents the length of time that an item is expected to last in operation until it fails.

MTBF is used only when referring to repairable items, MTTF is used to refer to non-repairable items.

MTTF = (total hours of operation)/(total number of units)

![故障率的浴盆曲线(bathtub curve)](https://github.com/QuChunhe/study/raw/master/pics/reliability-bathtub-curve-chart.png)

* Early LifeIf we follow the slope from the leftmost start to where it begins to flatten out this can be considered the first period. The first period is characterized by a decreasing failure rate. It is what occurs during the “early life” of a population of units. The weaker units fail leaving a population that is more rigorous.  
* Useful LifeThe next period is the flat bottom portion of the graph. It is called the “useful life” period. Failures occur more in a random sequence during this time. It is difficult to predict which failure mode will occur, but the rate of failures is predictable. Notice the constant slope.  
* WearoutThe third period begins at the point where the slope begins to increase and extends to the rightmost end of the graph. This is what happens when units become old and begin to fail at an increasing rate. It is called the “wearout” period.


FIT – Failures in Time, number of units failing per billion operating hours. 



Availability of the module is the percentage of time when system is operational. 

A=MTBF/(MTBF+MTTR)

[System Reliability and Availability](https://eventhelix.com/RealtimeMantra/FaultHandling/system_reliability_availability.htm)

System Availability is calculated by modeling the system as an interconnection of parts in series and parallel. The following rules are used to decide if components should be placed in series or parallel:
* If failure of a part leads to the combination becoming inoperable, the two parts are considered to be operating in series
* If failure of a part leads to the other part taking over the operations of the failed part, the two parts are considered to be operating in parallel.

Availability in Series A = Ax * Ay

Availability in Parallel A = 1-(1-Ax)2

[Reliability vs Availability: What’s the Difference?](https://www.bmc.com/blogs/reliability-vs-availability/)

Availability refers to the percentage of time that the infrastructure, system or a solution remains operational under normal circumstances in order to serve its intended purpose.


Reliability refers to the probability that the system will meet certain performance standards in yielding correct output for a desired time duration. Reliability can be used to understand how well the service will be available in context of different real-world conditions.

MTBF = (total elapsed time – sum of downtime)/number of failures

[Weibull Reliability Analysis](http://faculty.washington.edu/fscholz/Reports/weibullanalysis.pdf)




[https://akfpartners.com/growth-blog/akf-availability-cube](https://akfpartners.com/growth-blog/akf-availability-cube)

**Patterns of Resilience-A Small Pattern Language**

Availability ≔ MTTF /(MTTF + MTTR)

* MTTF: Mean Time To Failure
* MTTR: Mean Time To Recovery


Traditional stability approach: Maximize MTTF


Failures in todays complex, distributed and interconnected systems are not the exception.


Do not try to avoid failures. Embrace them.

Resilience approach: Minimize MTTR

the ability of a system to handle unexpected situations
* without the user noticing it (best case)
* with a graceful degradation of service (worst case)

Isolation
* System must not fail as a whole
* Split system in parts and isolate parts against each other
* Avoid cascading failures
* Requires set of measures to implement

**Bulkheads Pattern（隔舱模式）**

Bulkhead 模式是一种容错能力的应用程序设计。 在 bulkhead 体系结构中，应用程序的元素隔离到池中，这样，如果一个应用程序发生故障，其他元素将继续工作。 该名称在分段的分区 (隔舱的) ，并按发货的球面进行命名。 如果船体受到破坏，只有受损的分段才会进水，从而可以防止船只下沉。

资源耗尽问题同样会影响具有多个使用者的服务。 源自一个客户端的大量请求可能耗尽服务中的可用资源。 其他使用者不再能够使用该服务，从而导致连锁故障效应。

根据使用者负载和可用性要求，将服务实例分区成不同的组。 此设计有助于隔离故障，即使在发生故障期间，也能为某些使用者保留服务功能。

使用者也可以将资源分区，确保用于调用一个服务的资源不会影响用于调用另一个服务的资源。 例如，对于调用多个服务的使用者，可为其分配每个服务的连接池。 如果某个服务开始发生故障，只有分配给该服务的连接池才会受到影响，因此，使用者可继续使用其他服务。

[隔舱模式](https://docs.microsoft.com/zh-cn/azure/architecture/patterns/bulkhead)

**Complete Parameter Checking**



Patterns for Fault Tolerant Software

Errors in one part of the system propagate to other parts of the system. If the errors are incorrect computational results, then errors can compound asthey move through the system. If the errors are incorrect actions, they can trigger further erroneous actions.
系统某一个部分的错误会传播到系统的其他部分。如果错误是不正确的计算结果，那么随着这些错误在系统中移动，错误会持续恶化。如果错误是错误的操作，那么它们能够触发更多的错误操作。

How can the time from fault activation to error detection be minimized? The fastest option is to check for error at every operation that the system conducts. 
如何缩短从故障被触发到错误被检查到的时间？最快的选择是在系统执行的每个操作中检查错误。

Perform frequent checks on data and operations to detect errors quickly and prevent errors from propagating to the rest of the system 
频繁地对数据和操作执行检查，能够快速地检测错误并防止错误扩散到系统的其他部分。

Loose Coupling
* Complements isolation
* Reduce coupling between failure units
* Avoid cascading failures
* Different approaches and patterns available


**Asynchronous Communication**
* Decouples sender from receiver
* Sender does not need to wait for receiver’s response
* Useful to prevent cascading failures due to failing/latent resources
* Breaks up the call stack paradigm

**Location Transparency**
* Decouples sender from receiver
* Sender does not need to know receiver’s concrete location
* Useful to implement redundancy and failover transparently
* Usually implemented using dispatchers or mappers

**Event-Driven**
* Popular asynchronous communication style
* Without broker location dependency is reversed
* With broker location transparency is easily achieved
* Very different from request-response paradigm

**Stateless**
* Supports location transparency (amongst other patterns)
* Service relocation is hard with state
* Service failover is hard with state
* Very fundamental resilience and scalability pattern


**Relaxed Temporal Constraints**
* Strict consistency requires tight coupling of the involved nodes
* Any single failure immediately compromises availability
* Use a more relaxed consistency model to reduce coupling
* The real world is not ACID, it is BASE (at best)!

**Idempotency**
* Non-idempotency is complicated to handle in distributed systems
* (Usually) increases coupling between participating parties
* Use idempotent actions to reduce coupling between nodes
* Very fundamental resilience and scalability pattern

**Self-Containment**
* Services are self-contained deployment units
* No dependencies to other runtime infrastructure components
* Reduces coupling at deployment time
* Improves isolation and flexibility


Latency control
* Complements isolation
* Detection and handling of non-timely responses
* Avoid cascading temporal failures
* Different approaches and patterns available


**Timeouts**
* Preserve responsiveness independent of downstream latency
* Measure response time of downstream calls
* Stop waiting after a pre-determined timeout
* Take alternate action if timeout was reached

**Circuit Breaker**
* Probably most often cited resilience pattern
* Extension of the timeout pattern
* Takes downstream unit offline if calls fail multiple times
* Specific variant of the fail fast pattern


Hystrix

**Fail Fast**
* “If you know you’re going to fail, you better fail fast”
* Avoid foreseeable failures
* Usually implemented by adding checks in front of costly actions
* Enhances probability of not failing



Fan out & quickest reply
* Send request to multiple workers
* Use quickest reply and discard all other responses
* Reduces probability of latent responses
* Tradeoff is “waste” of resources


**Bounded Queues**
* Limit request queue sizes in front of highly utilized resources
* Avoids latency due to overloaded resources
* Introduces pushback on the callers
* Another variant of the fail fast pattern

为可用内存设置上限，即为队列和缓存等设置最大可用的内存数量，避免出现过度使用内存，引起内存不够分配而触发错误。

**Shed Load**
* Upstream isolation pattern
* Avoid becoming overloaded due to too many requests
* Install a gatekeeper in front of the resource
* Shed requests based on resource load


http://libgen.gs/ads.php?md5=9BF0FE6A1B5893A6C45B5434F0C1A979

Supervision
* Provides failure handling beyond the means of a single failure unit
* Detect unit failures
* Provide means for error escalation
* Different approaches and patterns available


**Monitor**
* Observe unit behavior and interactions from the outside
* Automatically respond to detected failures
* Part of the system – complex failure handling strategies possible
* Outside the system – more robust against system level failures

**Error Handler**
* Units often don’t have enough time or information to handle errors
* Separate business logic and error handling
* Business logic just focuses on getting the task done (quickly)
* Error handler has sufficient time and information to handle errors

**Escalation**
* Units often don’t have enough time or information to handle errors
* Escalation peer with more time and information needed
* Often multi-level hierarchies
* Pure design issue


Failures are the normal case. Failures are not predictable.
* Isolation
   * Bulkheads Pattern（隔舱模式）
   * Complete Parameter Checking (完成参数检查)
* Loose Coupling   
   * Asynchronous Communication
   * Location Transparency
   * Event-Driven
   * Stateless   
   * Relaxed Temporal Constraints
   * Idempotency
   * Self-Containment 
* Latency control
   * Timeouts 
   * Circuit Breaker
   * Fail Fast
   * Fan out & quickest reply
   * Bounded Queues
   * Shed Load
* Supervision
   * Monitor
   * Error Handler
   * Escalation
   
   
![Patterns of Resilience](https://github.com/QuChunhe/study/blob/master/pics/ResiliencePatterns.png)


”Resilience reloaded-More resilience patterns“

(Almost) every system is a distributed system -- Chas Emerick

Failures in todays complex, distributed and interconnected systems are not the exception.
* They are the normal case
* They are not predictable
* They are not avoidable


[大话高可用](https://mp.weixin.qq.com/s?__biz=MzUzNjAxODg4MQ==&mid=2247483678&idx=1&sn=2091e0f6b52cd859284fb14baec7565c&scene=21#wechat_redirect)

去依赖 弱依赖 超时和重试、蓄洪、限流、熔断、降级

对方故障：快速失败和安全失败

对方恢复：快速回复和安全回复

快速恢复有些策略。最简单的比如心跳检测、事件监听等。

安全恢复一般主要是在恢复前对系统或数据先做一些检查、数据还原等。
  
 单节点-->集群-->多机房-->多地区-->异地多活
 
 多服务策略
 * 负载均衡
 * 主从切换
 * 优先策略
 
 [Redis 缓存和 MySQL 数据如何实现一致性？](http://www.iocoder.cn/Fight/How-do-Redis-cache-and-MySQL-data-achieve-consistency/)
  
  负载均衡来提高系统吞吐和可靠性
  
  
  负载均衡算法
  * Round Robin 轮换
  * Least Connections — 最少连接（Least Connections）这个算法意味着负载均衡器会选择当前连接最少的服务器。
  * 

# 杂项

＃＃　分布式ID

[分布式ID之为什么需要分布式ID以及分布式ID的业务需求](https://www.itqiankun.com/article/1565060480)

[Size does Matter: pattrens for high scalability](https://www.slideshare.net/ufried/scalability-patterns)

Basic of Scalability
* Strive for Simplicity: The system should be made as simple as possible (but no simpler)
* Scale out, not up
* Be stateless.
* Share nothing
* Communicated Asynchronously

Dimensions of Scalability
* Splitting (By function or resource)
* Replication
* Sharding

Replication: High read to write ratio
* Load balancer & shared nothing units
* load balancer & stateless nodes & scalable storage
* master slave replication
* masterless replication

Splitting
* Split up by noun (data) or verb (function)
* Best implemented with shared nothing units and/or anynchronous communication

Sharding
* Consistent Hashing
* Scatter & gather (MapReduce)

Design for high scalability
* Relax temporal constraints: ACID, BASE, CAP
  * Quorum
  * Harvest & Yield
  * Hinted handoffs
* Cache as cache can
  * Short response times and/or high throughput are important
  * High read to write ratio
* Keep dynamic data closer to the computer and static data closer to the end-user

The core principles of scalability: simplicity, scale out, share nothing, asynchronous communication.  
  
  
[No crash allowed - Fault tolerance patterns](https://www.slideshare.net/ufried/no-crash-allowed-fault-tolerance-patterns)  

Fault->Error-> Failure

Error detection and handling is a core effort in fault tolerant system design.

Availability: percentage of time performing the designed function (uptime). availability = MTTF /(MTTF+MTTR)

Coverage: Probability to revoer automatically within a given time period given that an error has occured. Prob(Successful error detection) * Prob(Successful recovery)

Reliability: Probablity to perform without devitions from aggeed-upon behaviour for a specific period of time.

Dependability: Trustworthiness to be relied upon to perform the desired function.

Strive for Simpmlicity.The system should be made as simple as possible (but no simpler).

Design for Failure. Whatever can go wrong will go wrong.

Design incrementally.

Fault tolerant architecture: error detection -> error recovery(improves error handling) || error mitigation (reduces error risk) -> fault treatment (core error handling flow)

* Redudancy: Balance costs and level of availability carefully.
* 
  
much request, complex function, big data 大量请求， 复杂功能，海量请求

http://www.redbooks.ibm.com/redpapers/pdfs/redp5109.pdf

[AKF Availability Cube](https://akfpartners.com/growth-blog/akf-availability-cube)

[The Scale Cube](https://akfpartners.com/growth-blog/scale-cube)

[Architectural Principles - Fault Isolation & Swimlanes](https://akfpartners.com/growth-blog/fault-isolation-swim-lane)

[The Domino or Multiplicative Effect of Failure](https://akfpartners.com/growth-blog/the-domino-or-multiplicative-effect-of-failure)

[The AKF Scale Cube: X Axis in the Persistence Tier](https://akfpartners.com/growth-blog/the-akf-scale-cube-x-axis-in-the-persistence-tier)

[Measuring Availability](https://akfpartners.com/growth-blog/measuring-availability)

[The Scale Cube: Achieve Security Through Scalability](https://akfpartners.com/growth-blog/the-scale-cube-achieve-security-through-scalability)

AKF Availability Cube
* X axis: Duplicate Everything. i.e. "N" x firewalls, switches, database instances, power supplies, services etc.- each a clone, increasing availability
* Y Axis: Eliminate the multiplicative effect of Failure in "Deep" or "Broad" chains.
* Z Axis:Fault Isolate Customer Segment. Reduce the impact of outages to smaller customer segments.

The X Axis of the Availability Cube: Any product/service/solution we develop should have multiple instances (deployments) of the service/product. 


[千万级流量的优化策略实战](https://blog.csdn.net/person_limit/article/details/80561196)

[Patterns of Distributed Systems](https://martinfowler.com/articles/patterns-of-distributed-systems/)

[架构设计60-设计原则01-故障隔离(故障的传播方式与隔离办法)](https://www.jianshu.com/p/a88041462150)

[The Art of Scalability - Managing growth ](https://www.slideshare.net/quipo/the-art-of-scalability-managing-growth)

[Scalability wikipedia](https://en.wikipedia.org/wiki/Scalability)

Scalability is the property of a system to handle a growing amount of work by adding resources to the system.

[Consistency model wikipedia](https://en.wikipedia.org/wiki/Consistency_model)

Coherence deals with maintaining a global order in which writes to a single location or single variable are seen by all processors. Consistency deals with the ordering of operations to multiple locations with respect to all processors.

Assume that the following case occurs:
1. The row X is replicated on nodes M and N
2. The client A writes row X to node M
3. After a period of time t, client B reads row X from node N

The consistency model has to determine whether client B sees the write from client A or not. 

There are two methods to define and categorize consistency models; 
* Issue: Issue method describes the restrictions that define how a process can issue operations.
* View: View method which defines the order of operations visible to processes.

two main reasons for replicating; reliability and performance. Reliability can be achieved in a replicated file system by switching to another replica in the case of the current replica failure. The replication also protects data from being corrupted by providing multiple copies of data on different replicas. It also improves the performance by dividing the work. While replication can improve performance and reliability, it can cause consistency problems between multiple copies of data. The multiple copies are consistent if a read operation returns the same value from all copies and a write operation as a single atomic operation (transaction) updates all copies before any other operation takes place. 

可靠性
* 节点损坏。一个副本所在服务器不能响应，则切换到另一个副本所在服务器
* 数据损坏。

读性能
* 平衡负载，减小等待时间
* 并行读取，

[Eventually Consistent](https://www.allthingsdistributed.com/2007/12/eventually_consistent.html)

[Availability & Consistency](https://www.infoq.com/news/2008/01/consistency-vs-availability/)

Inconsistency can be tolerated for two reasons: for improving read and write performance under highly concurrent conditions and for handling partition cases where a majority model would render part of the system unavailable even though the nodes are up and running.


two ways of looking at consistency： One is from the developer / client point of view; how they observe data updates. The second way is from the server side; how updates flow through the system and what guarantees systems can give with respect to updates.


The degree of consistency may vary:  
* Strong consistency. After the update completes any subsequent access (by A, B or C) will return the updated value.  
* Weak consistency. The system does not guarantee that subsequent accesses will return the updated value. A number of conditions need to be met before the value will be returned. Often this condition is the passing of time, [i.e.] the inconsistency window.  
* Eventual consistency. The storage system guarantees that if no new updates are made to the object eventually (after the inconsistency window closes) all accesses will return the last updated value.  



https://www.infoq.com/architecture/presentations/
[Consistency vs. availability: eventual consistency by Werner Vogels](https://www.infoq.com/news/2008/01/consistency-vs-availability/)

[Architectures That Scale Deep - Regaining Control in Deep Systems](https://www.slideshare.net/InfoQ/architectures-that-scale-deep-regaining-control-in-deep-systems)

* Scaling Wide: 功能的克隆+负载平衡，提高可靠性和吞吐量
* Scaling Deep: 功能的分割，系统之间的调用，tier Pattern，增加了系统之间的依赖性，依赖的不可见性，故障扩散


Capacity limits are scalability limits.

Scalability Isn’t Throughput-vs-Latency

Concurrency-vs-Latency is OK。 It’s a simple quadratic per Little’s Law, and is quite useful
* Scalability is formally definable, and black-box observable
* Scalability is nonlinear; this region is the failure boundary
* Scalability is a function with parameters you can estimate


[distributed systems like it or not](https://www.slideshare.net/postwait/distributed-systems-like-it-or-not)

[Monitoring 101](https://www.slideshare.net/postwait/monitoring-101-79494722)

Monitoring is the action of observing and checking static and dynamic properties of a system.
 
Service Level Objects: usually based on percentiles: 95th percentile less 10ms

1. **Do not measue rates.** You can derive the rate of change over time at query time.
2. **Monitor outside the tech stack.** Your tech stack wout not exist without happy customers and a sales pipeline. Monitor that which is important to the health of your organization.
3. **Do not silo data.** The behaior of the parts must be put in context. Correlating disparate systems and even business outcomes is critical.
4. **Value observation of real work** over the measurement of synthesized work.
5. **Synthesize work to ensure function** for business critical, low-value events.
6. **Percentiles are not histograms." For rebust SLO management, you need to store histograms for post-processing. 
7. **History is critical.** not weeks or months, but years of detailed history. Capacity planning, retrospectives, comparative analysis, and modelling all relay on accurate, high-fidelity history.
8. **Alters require documentation.** No ruleset should trigger an alert without: human-readable explanation, business impact description, remediation procedure, escalation documentation.
9. **Be outside the blast radius.** The purpose of monitoring is to detect changes in behavior and assist in answering operational questions.
10. **Something is better than nothing.** Don't let perfect be the enemy of good. You have to start somewhere.


[The Art of Scalability - Managing growth](https://www.slideshare.net/quipo/the-art-of-scalability-managing-growth/2-Scalability_Scalability_is_a_desirable)  good


Scalability is a desirable property of system, a network, a business or a process, which indicates its ability to handle growing amounts of work. 可伸缩性(可扩展性)是系统、网络、业务或者流程期望的一种属性，该属性表明其具有能力，能够处理不断增长的工作量。

scalable not equal fast: 增加资源，能够处理更多的请求或更多的数据

Project Management: Measurement-> Communication->Resolution
* Goals
* Projects
* Tasks
* Individuals

People Management
* Hiring
* Firing
* Growth

Headroom: 余量= Capacity - Current Load

Managing Incidents and Problems
1. Detect
2. Report
3. Investigate
4. Escalate
5. Resolve


Performance (Load) Testing

Stress Testing

Architectural Principle
* N+1 design
* for rollback
* to be disabled
* to be monitoring
* for multiple live sites
* use mature technology
* asynchronous design
* stateless system
* buy when non core: focus on core competencies


Create Fault Isolative Structures: Limit impact of failures, Easier debugging

Scale Directions
* X : cloning of entities or data- unbiased distribution of work
* Y : Seperation of work by activity or data
* Z : separation of work by persion for whom the work is done. 

Splitting Applications for scale
* Mirroring
* split by service
* split by need/location/value


Splitting database for scale
* Data cloing (replication/Clustering)
* Split by service/resource/data affinity
* split by modulus/ hash-based lookups

Caching for performance & Scale
* Object caches : Redis
* Application caches: Squid, Varnish
* CDNs

[Database Scalability](http://horicky.blogspot.com/2008/03/database-scalability.html)

* Indexing
* Data De-normalization: Table join is an expensive operation and should be reduced as much as possible. One technique is to de-normalize the data such that certain information is repeated in different tables.
* DB Replication
* Table Partitioning
* Table Sharding
* Transaction Processing:Avoid mixing OLAP (query intensive) and OLTP (update intensive) operations within the same DB. In the OLTP system, avoid using long running database transaction and choose the isolation level appropriately.


[Web Site Scalability](http://horicky.blogspot.com/2008/03/web-site-scalability.html)

* Web tier : Serving static contents (static pages, photos, videos)
* App tier : Serving dynamic contents and execute the application logic (dynamic pages, order processing, transaction processing)
* Data tier: Storing persistent states (Databases, Filesystems)

Content Delivery
* Dynamic Content
* Static Content


Request Dispatching and Load Balancing
* DNS Resolution based on user proximity
* Load balancer

Client communication
* Designing the granularity of service call
   * Reduce the number of round trips by using a coarse grain API model so your client is making one call rather than many small calls
   * Don't send back more data than your client need
   * Consider using an incremental processing model. Just send back sufficient result for the first page. Use a cursor model to compute more result for subsequent pages in case the client needs it. But it is good to calculate an estimation of the total matched result to return to the client.
* Designing message format
* Consider data compression
* Asynchronous communication

Session state handing
* Memory-based session state with load balancer affinity
* Memory replication session state across App servers
* Persist session state to a DB
* On-demand session state migration
* Embed session state inside cookies

[Scalable System Design](http://horicky.blogspot.com/2008/02/scalable-system-design.html)

General Principles
* "Scalability" is not equivalent to "Raw Performance"
* Understand environmental workload conditions that the system is design for
   * Dimension of growth and growth rate: e.g. Number of users, Transaction volume, Data volume
   * Measurement and their target: e.g. Response time, Throughput
* Understand who is your priority customers
   * Rank the importance of traffic so you know what to sacrifice in case you cannot handle all of them
* Scale out and Not scale up
* Keep your code modular and simple
* Don't guess the bottleneck, Measure it
* Plan for growth
   * Do regular capacity planning. Collect usage statistics, predict the growth rate

Common Techiques
* Server Farm (real time access)
* Data Partitioning
* Map / Reduce (Batch Parallel Processing)
* Content Delivery Network (Static Cache)
* Cache Engine (Dynamic Cache)
* Resources Pool
* Calculate an approximate result
* Filtering at the source
* Asynchronous Processing
  * In callback mode, the caller need to provide a response handler when making the call. The call itself will return immediately before the actually work is done at the server side. When the work is done later, response will be coming back as a separate thread which will execute the previous registered response handler. Some kind of co-ordination may be required between the calling thread and the callback thread.
  * In polling mode, the call itself will return a "future" handle immediately. The caller can go off doing other things and later poll the "future" handle to see if the response if ready. In this model, there is no extra thread being created so no extra thread co-ordination is needed.
* Implementation design considerations


[Scalable System Design Patterns](http://horicky.blogspot.com/2010/10/scalable-system-design-patterns.html)

* Load Balancer
  * Random
  * Round robin
  * Least busy
  * Sticky session/cookies
  * By request parameters
* Scatter and Gather
* Result Cache
* Shared Space: The model also known as "Blackboard"
* Pipe and Filter: This model is also known as "Data Flow Programming"; all workers connected by pipes where data is flow across.
* Map Reduce
* Bulk Synchronous Parellel: This model is based on lock-step execution across all workers, coordinated by a master. Each worker repeat the following steps until the exit condition is reached, when there is no more active workers.
   1. Each worker read data from input queue
   2. Each worker perform local processing based on the read data
   3. Each worker push local result along its direct connection

* Execution Orchestrator: This model is based on an intelligent scheduler / orchestrator to schedule ready-to-run tasks (based on a dependency graph) across a clusters of dumb workers



[A Distributed Systems Reading List](https://dancres.github.io/Pages/)

[Distributed Systems A free online class](https://www.distributedsystemscourse.com/)

[CSE138 Distributed Systems](https://www.youtube.com/user/lindseykuper)

[MIT 6.824 Distributed Systems (Spring 2020)](https://www.youtube.com/watch?v=cQP8WApzIQQ&list=PLrw6a1wE39_tb2fErI4-WkMbsvGQk9_UB)


[Readings in distributed systems](http://christophermeiklejohn.com/distributed/systems/2013/07/12/readings-in-distributed-systems.html)

课程视频官方地址：

https://www.youtube.com/channel/UC_7WrbZTCODu1o_kfUMq88g

爱可可老师也将视频“搬运”到了B站上：

https://www.bilibili.com/video/av89327823/

截止到现在（2月18日），只更新了前三节课。

不过，整个课程的paper和lab已经放出了，如果你觉得视频更新太慢，你也可以先“酸爽”着。

课程地址：

https://pdos.csail.mit.edu/6.824/schedule.ht
