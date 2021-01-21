
Martin L. Abbott and Michael T. Fisher, Scalability Rules：Principles for Scaling Web Sites Second Edition, 2017
---------------------------------------------------


## Chapter 1 Reduce the Equation 大道至简

match the effort and approach to the complexity of the problem. Not every solution has the same complexity—take the simplest approach to achieve the desired outcome。 努力和方法要与问题的复杂性相匹配。不是每个方案都有相同的复杂性，选取最简单的方法，实现所期望的结果

keeping things as simple as possible. Our view is that a complex problem is really just a collection of smaller, simpler problems waiting to be solved. 保持事情要尽可能的简单。从我们的视角来看，一个复杂问题其实仅仅是一些更小的、更简单的待解决问题的集合

### Rule 1—Don’t Overengineer the Solution 
### 规则1—不要过度设计解决方案

**What:** Guard against complex solutions during design. 在设计过程中严防复杂的解决方案。

**When to use:** Can be used for any project and should be used for all large or complex systems or projects. 可以应用于任何项目，而且也必须应用于所有大型或者复杂的系统或者项目

**How to use:** Resist the urge to overengineer solutions by testing ease of understanding with fellow engineers. 通过与工程师同事测试易懂性，来抵制对于过度工程化的解决方案的冲动。

**Why:** Complex solutions are excessively costly to implement and are expensive to maintain long term. 复杂方案的实现会严重超支，而长期维护费用也高昂，

**Key takeaways:** Systems that are overly complex limit your ability to scale. Simple systems are more easily and cost-effectively maintained and scaled. 过于复杂的系统将会限制你的可扩展能力。简单的系统更简单，并且能够更高效地维护和扩展。

过度工程化可以划归两大类
* The first category covers products designed and implemented to exceed their useful requirements. 第一类涵盖那些设计和实现超过其有用需求的产品。
* The second category of overengineering covers products that are made to be overly complex.第二类过度工程化涵盖那些制造过于复杂的产品。


To explain the first category of overengineering, exceeding useful requirements。第一类是超过了有用需求，即设计和实现了现在比并不需要的功能。

The second category of overengineering deals with making something overly complex and making something in a complex way. 第二类过度工程化涉及使得某些事情过于复杂并且以某种复杂的方式做事情。

不要向不需要的需求或功能买单

[Faster Time to Market – How to Avoid Overengineering (Rule 1)](https://akfpartners.com/growth-blog/faster-time-to-market-how-to-avoid-overengineering-yagni)

Overengineering is solving problems you don’t have.

We will look at two sides of overengineering: Exceeding useful requirements, and spending too much effort to get a job done.
我们将会研究过度工程化的两个方面：超出有用的需求，以及花费更多的精力完成一个工作。

### Rule 2—Design Scale into the Solution　(D-I-D Process) 
### 方案2—将可扩展性设计到方案中（设计-实现-部署过程）

**What:** An approach to provide JIT (just-in-time) scalability. 一种提供及时可扩展性的方法

**When to use:** On all projects; this approach is the most cost-effective (resources and time) to ensure scalability. 在所有的项目中应用；此方法在确保可扩展性上是最为高效（资源和时间）。

**How to use:**
* Design for 20x capacity.针对20倍的容量，设计
* Implement for 3x capacity.针对3倍的容量，实现
* Deploy for roughly 1.5x capacity.针对大约1.5倍容量，部署

**Why:** D-I-D provides a cost-effective, JIT method of scaling your product. 设计-实现-部署提供了一种高性价比的、及时的方式，来扩展你的产品。

**Key takeaways:** Teams can save a lot of money and time by thinking of how to scale solutions early, implementing (coding) them a month or so before they are needed, and deploying them days before the customer rush or demand. 如果在开始的时候考虑如何扩展解决方案，那么需要在扩展前的一个月左右时间实现（编码）或者需要在客户高峰到来前的几天部署，团队就能够节省大量的金钱和时间。


D-I-D provides a cost-effective, JIT method of scaling your product.

Dell, configure-to-order： 按订单配置，just-in-time manufacturing：及时制造

AKF Partners’ Design-Implement-Deploy or D-I-D approach to thinking about scalability.

[The DID Process - Scale Design Principles (Rule 2)](https://akfpartners.com/growth-blog/scale-design-principles-the-did-process)


Ideally, what you want is JIT (just-in-time) scalability. The idea originates from JIT manufacturing, and relates to reducing delivery time. JIT scalability is the ability to scale up or down when needed, as needed. 理想情况下，你所需要的是及时的可扩展性。这个想法来自于及时制造，并涉及缩短交付时间。及时可扩展性是指当需要时，可以根据需要实现向上或者向下的伸缩。

infrastructure-as-a-service (IaaS) 

有预见性的设计，分阶段性的实现，及时性的部署

### Rule 3—Simplify the Solution Three Times Over 
### 方案3—三重简化方案

**What:** Used when designing complex systems, this rule simplifies the scope, design, and implementation. 当设计复杂系统时使用这个规则，简化范围、设计和实现。

**When to use:** When designing complex systems or products where resources (engineering or computational) are limited. 当设计复杂的并且资源（工程或者计算）受到限制的系统或者产品时，


**How to use:**
* Simplify scope using the Pareto Principle. 通过帕累托法则来简化范围
* Simplify design by thinking about cost effectiveness and scalability. 通过考量经济效益和可扩展性来简化设计
* Simplify implementation by leveraging the experience of others.通过充分利用他人的经验来简化实现

**Why:** Focusing just on “not being complex” doesn’t address the issues created in requirements or story and epoch development or the actual implementation. 仅仅聚焦于不复杂并不能解决在需求中和在开发或实际实施时期产生的问题

**Key takeaways:** Simplification needs to happen during every aspect of product development. 在产品开发的各个方面都需要简单化。


Pareto principle 即帕累托法则，又称80/20法则、马特莱法则、二八定律、帕累托定律、最省力法则、不平衡原则、犹太法则。意大利经济学家帕累托提出的。法则认为原因和结果、投入和产出、努力和报酬之间本来存在着无法解释的不平衡

[Scalability Rules - How to Simplify Scope, Design, and Implementation (Rule 3)](https://akfpartners.com/growth-blog/scalability-rules-how-to-simplify-scope-design-and-implementation)

简化体现在更容易被理解，完成的时间更短，所付出的代价更小

Complexity elimination is about cutting off unnecessary trips in a job, and simplification is about finding a shorter path


“How can we leverage the experiences of others and existing solutions to simplify our implementation?”


### Rule 4—Reduce DNS Lookups 减少DNS查找
### 规则4—避免重复性工作


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



### Rule 5—Reduce Objects Where Possible尽可能减少对象
### Rule 5—控制分割的粒度

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


### Rule 6—Use Homogeneous Networks使用同构网络

**What:** Ensure that switches and routers come from a single provider. 确保交换机和路由器都来自单一的提供商。

**When to use:** When designing or expanding your network. 当设计或者扩展你的网络时

**How to use:**
* Do not mix networking gear from different OEMs for switches and routers.不要将来自不同OEM的交换机和路由器混合联网。
* Buy or open-source for other networking gear (firewalls, load balancers, and so on). 购买或使用开源的联网设备（防火墙、负载均衡器等等）

**Why:** Intermittent interoperability and availability issues simply aren’t worth the potential cost savings. 异构网络所带来的间歇互操作和可用性问题并不值得潜在的、所节约的费用

**Key takeaways:** Heterogeneous networking gear tends to cause availability and scalability problems. Choose a single provider. 异构互联设备更容易造成可用性和可扩展性问题。选择单一的提供商。

对于操作系统以及数据库、JDK和Nginx等系统软件采用相同的版本。


## Chapter 2 Distribute Your Work 分布你的工作


### Rule 7-Design To Clone or Replicate Things (X Axis)
### 规则7-设计支持克隆或者复制相同的东西（X轴）

**What:** Typically called horizontal scale, this is the duplication of services or databases to spread transaction load. 复制服务或者数据库，来分担事务负载，因此通常被称为水平可伸缩，

**When to use:**
* Databases with a very high read-to-write ratio (5:1 or greater—the higher the better).数据具有非常号的读/写比（5:1或者更高，越高越好）
* Any system where transaction growth exceeds data growth.任何系统如果其事务的增长超过了数据的增长

**How to use:**
* Simply clone services and implement a load balancer.简单的克隆服务并实现一个负载均衡器
* For databases, ensure that the accessing code understands the difference between a read and a write.对于数据库，确保访问的代码理解读和写的不同

**Why:** Allows for fast scale of transactions at the cost of duplicated data and functionality. 允许以复制数据和功能为代价，快速地实现事务处理的可伸缩性

**Key takeaways:** X axis splits are fast to implement, are low cost from a developer effort perspective, and can scale transaction volumes nicely. However, they tend to be high cost from the perspective of operational cost of data. X轴的分解能够快速地实现，并且从开发者工作的视角具有较低的成本，能够非常好地扩展事务的数量。但是从数据运维代价的角度，X轴分解倾向于更高的成本。

Often, the hardest part of a solution to scale is the database or persistent storage tier. 通常，在实现可伸缩性的解决方案中最为困难的部分是数据库或者持久化存储层。
* 分布式事务：ACID
* 数据一致性：如果写数据，1）如何实现数据多个副本数据的一致性；2）如何避免读到不一致的数据

One technique for scaling databases is to take advantage of the fact that most applications and databases perform significantly more reads than writes. 一种用于扩展数据库的技术是（读写分离）利用了这样一个事实，即大多数应用和数据库的读要远远多于写。


There are a couple of ways that you can distribute the read copy of your data depending on the time sensitivity of the data. Time (or temporal) sensitivity is how fresh or completely correct the read copy has to be relative to the write copy. 依赖于数据的时间敏感性，你可以使用多种方式分布数据的读副本。时间敏感性是指相对于写副本，读副本的一致性的程度或者完全正确的程度。

两个问题：
1. 在写入数据后，最多需要多长时间全部副本才能实现一致性
2. 应用能够忍受多长时间的读副本与写副本之间的不一致性。

the ways to distribute the data.分布数据的方式
* One way is to use a caching tier in front of the database.一种方法是在数据库之前使用缓存层。（对象缓存）
* The next step beyond an object cache between the application tier and the database tier is replicating the database。除了在应用层和数据库层之间对象缓存，下一步是复制数据库。（数据库复制）

X axis—Horizontal Duplication


应用和web服务的克隆相对较为容易实现，允许我们扩展所处理事务的数目。

两个复制/克隆方向
* 数据（名词）
* 功能（动词）

### Rule 8—Design to Split Different Things (Y Axis)

### 规则8—设计支持分拆不同的东西（Y轴）

**What**: Sometimes referred to as scale through services or resources, this rule focuses on scaling by splitting data sets, transactions, and engineering teams along verb (services) or noun (resources) boundaries. 有时指的是通过服务或者资源实现可扩展，这个规则聚焦于沿着动词(服务)或者名词(资源)的边界，通过分割数据集、事务和工程团队，来实现可扩展。
 
**When to use**:
* Very large data sets where relations between data are not necessary.非常大的数据集合，并且集合内数据之间的关系不是必须的。数据之间没有必然的关联，无需考虑JOIN操作。
* Large, complex systems where scaling engineering resources requires specialization. 庞大的、复杂的系统，并且在系统中扩展工程资源需要非常的专业化

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

### Rule 9—Design to Split Similar Things (Z Axis)
### 规则9-设计支持分拆相似的东西(Z轴)

**What:** This is very often a split by some unique aspect of the customer such as customer ID, name, geography, and so on. 非常常见的分离方式是通过客户一些独特的属性，例如客户id、名字和地理位置等。

**When to use:** Very large, similar data sets such as large and rapidly growing customer bases or when response time for a geographically distributed customer base is important. 非常庞大的或者相似的数据集，例如大量并快速增长的客户群或者对于地理分布的客户群而言，响应时间非常重要。

**How to use:** Identify something you know about the customer, such as customer ID, last name, geography, or device, and split or partition both data and services based on that attribute. 识别那些你所知的、有关于客户的信息，例如客户id、姓氏、地理位置或终端，并据此分割或者划分数据和服务。

**Why:** Rapid customer growth exceeds other forms of data growth, or you have the need to perform fault isolation between certain customer groups as you scale. 快速的客户增长超过了其他格式的数据增长，或者在你扩展客户规模的过程，你需要在特定的客户之间实现故障隔离。

**Key takeaways:** Z axis splits are effective at helping you to scale customer bases but can also be applied to other very large data sets that can’t be pulled apart using the Y axis methodology. Z轴分解不仅是一种有效的方式，协助你扩展客户群，而且还可以应用到其他一些巨大数据集合上，这些数据集合使用Y轴方法无法有效得分解，


数据的Sharding或者Partition

Often referred to as sharding and podding, Rule 9 is about taking one data set or service and partitioning it into several pieces. These pieces are often equal in size but may be of different sizes if there is value in having several unequally sized chunks or shards. 规则9经常称为分片或者分割，其获取一个数据集或者服务，然后将其划分为多个部分。这些部分通常大小相等，但如果大小不一的块或者分片有意义，那么也可以大小并不相同。

Summary
* Scale by cloning—Cloning or duplicating data and services allows you to scale transactions easily.
* Scale by splitting different things—Use nouns or verbs to identify data and services to separate. If done properly, both transactions and data sets can be scaled efficiently.
* Scale by splitting similar things—Typically these are customer data sets. Set customers up into unique and separated shards or swim lanes (see Chapter 9 for
the definition of swim lane) to enable transaction and data scaling.

## Chapter 3 Design to Scale Out Horizontally
## 第三章 设计支持水平地向外扩展

In our minds, it is clear: we believe that within hyper-growth environments it is critical that companies plan to scale in a horizontal fashion—what we describe as scaling out. Most often this is done through the segmentation or duplication of workloads across multiple systems. 在我们心中非常显然地认为，在高速增长的环境中公司计划以一种水平方式扩展（也被我们描述为向外扩展）是非常关键的。绝大多数情况下此种方式是通过跨越多个系统，使用分割或者复制来实现。


Here again we see this troubling notion of “complexity.” When used one way, more devices equals more complexity—or as we prefer to indicate, more devices to manage and oversee. But when seen from another perspective, more devices equals lower complexity—lower rates of failure overall and fewer incidents to manage.
这里我们再次看到复杂性这个令人陷入麻烦的概念。从一个方向上使用，更多的设备等于更高的复杂性，或者按照我们喜欢的方式指出，更多的设备需要管理和监控。但是，从另一个角度看，更多的设备等于更低的复杂性，因为更低的整体故障率和更少需要管理的事故。



### Rule 10—Design Your Solution to Scale Out, Not Just Up
### 规则10-设计你的系统支持向外扩展，而不仅仅是向上扩展

**What:** Scaling out is the duplication or segmentation of services or databases to spread transaction load and is the alternative to buying larger hardware, known as scaling up.
向外扩展是针对服务或者数据库的复制或者分割，以扩大事务负载，其是购买更大型的硬件、被称为向上扩展的替换方案。

**When to use:** Any system, service, or database expected to grow rapidly or that you would like to grow cost-effectively.
期望快速增长的或者你期望高性价比增长的任何系统、服务或者数据库

**How to use:**  Use the AKF Scale Cube to determine the correct split for your environment. Usually the horizontal split (cloning) is the easiest. 针对你的环境，使用AKF可扩展立方确定正确地分拆。通常水平分拆（克隆）是最简单的。

**Why:** Allows for fast scale of transactions at the cost of duplicated data and functionality. 允许以复制数据和功能为代价，快速扩展事务。

**Key takeaways:** Plan for success and design your systems to scale out. Don’t get caught in the trap of expecting to scale up only to find out that you’ve run out of faster and larger systems to purchase. 为成功做计划，并设计你的系统实现向外扩展。不要陷入如下如下的陷阱：仅仅期望向上扩展，但是发现你已经没有更快的和更大的系统可供购买了。


Having the ability to run your product on multiple servers through all tiers is scaling out.Continuing to run your systems on larger hardware at any tier is scaling up.
有能力将你的产品在所有的层级都运行在多个服务器是向外扩展。继续将你系统上的任何一个层级运行在更强大的硬件上是向上扩展。



### Rule 11—Use Commodity Systems (Goldfish Not Thoroughbreds)
### 规则11-采用商品化系统

**What:** Use small, inexpensive systems where possible.尽可能使用小规模的和不昂贵的系统

**When to use:** Use this approach in your production environment when going through hypergrowth and adopt it as an architectural principle for more mature products. 当业务飞速增长时在你们的生产环境中使用这个方法，并且针对更多的成熟产品将其作为架构原则。

**How to use:** Stay away from very large systems in your production environment.在你的生产环境中避免使用非常大型的系统。


**Why:** Allows for fast, cost-effective growth. Allows you to purchase the capacity you need rather than spending for unused capacity far ahead of need. 许可快速和高效的增长。允许你购买你需要的容量，而不是在实际需要之前就购买当期并不使用的容量。

**Key takeaways:** Build your systems to be capable of relying on commodity hardware, and don’t get caught in the trap of using high-margin, high-end servers.
能够依赖于商品化硬件构建你的系统，避免陷入使用高利润、高端服务器的陷阱。



使用成熟的和商业化的系统，而不要采用定制化的、高端系统。
* 价格相对便宜，更容易大规模的部署，以支持横向扩展
* 更好的性价比


### Rule 12—Scale Out Your Hosting Solution
### 规则 12-横向扩展你的托管方案


**What:** Design your systems to have three or more live data centers to reduce overall cost, increase availability, and implement disaster recovery. A data center can be an owned facility, a colocation, or a cloud (IaaS or PaaS) instance.
设计你的系统具有三个或者更多的活跃数据中心，以降低综合成本、提高可用性和实现灾后恢复。数据中心可以是自有设施、托管服务器或者一个云实例（IaaS或者PaaS）。

**When to use:** Any rapidly growing business that is considering adding a disaster recovery (cold site) data center or mature business looking to optimize costs with a three-site solution。 任何快速增长并正在考虑添加一个灾难恢复（冷站点）数据中心的业务或者期望通过三个站点解决方案来优化成本的成熟业务。

**How to use:** Scale your data per the AKF Scale Cube. Host your systems in a “multiple live” configuration. Use IaaS/PaaS (cloud) for burst capacity, new ventures, or as part of a three-site solution. 按照AFK可扩展立方来实现你数据的可扩展性。以一种“多个活跃”的配置，托管你的系统。使用IaaS/Paas（云）来支持突发容量、新企业或者部分的三站点解决方案。

**Why:** The cost of data center failure can be disastrous to your business. Design to have three or more as the cost is often less than having two data centers. Consider using the cloud as one of your sites, and scale for peaks in the cloud. Own the base; rent the peak. 数据中心故障的代价对你的业务可能是灾难性。因此，设计具有三个或者更多的数据中心，其综合成本经常低于具有两个数据中心的场景。考虑使用云作为你的站点之一，并且在云中扩展支持突发流量。自有实施处理日常基础流量，租用云来处理突发流量。

**Key takeaways:** When implementing disaster recovery, lower your cost by designing your systems to leverage three or more live data centers. IaaS and PaaS (cloud) can scale systems quickly and should be used for spiky demand periods. Design your systems to be fully functional if only two of the three sites are available, or N-1 sites available if you scale to more than three sites.
当实施灾难恢复时，通过设计你的系统以充分使用三个或者更多的活跃数据中心，从而降低你的成本。IaaS和PaaS（云）能够快速地扩展系统，因为应该在尖峰需求期间使用此种方式。设计你的系统在三个站点中仅有两个可用时或者在扩展具有多于三个站点情况下有N-1个站点可用时，也能提供全部的功能

It is this segmentation, replication, and cloning of data and services as well as statelessness that form the building blocks for us to spread our data centers across multiple sites and geographies. Standardize system configuration, code deployment, and monitoring to enable seamless growth between colocation sites and cloud sites.
正是数据和服务的分割、复制和克隆以及无状态为我们提供了构造基石，可以跨域多个站点和地区分布我们的数据中心。在托管站点和云站点之间实现系统配置、代码部署和监控的标准化，从而能够无缝地增长。


Multiple live site benefits include多个站点的好处包括
* Higher availability as compared to a hot and cold site configuration.与一个冷站和一个热站的配置相比，具有更好的可用性。
* Lower costs compared to a hot and cold site configuration.与一个冷站和一个热站的配置相比，具有更低的成本。
* Faster customer response times if customers are routed to the closest data center for dynamic calls.对于动态调用，如果将用户请求路由到距离最近的数据中心，能够实现更快的客户响应时间。
* Greater flexibility in rolling out products in an SaaS environment.在一个SaaS环境中推出产品，具有更大的灵活性。
* Greater confidence in operations versus a hot and cold site configuration.与一个冷站和一个热站比较，对于运维具有更大的信心。
* Fast and easy “on-demand” growth for spikes using spare capacity in each data center, particularly if PaaS/IaaS/cloud is part of the overall solution. 在每个数据中心中使用富余容量，针对于峰值实现快速简单的按需增长，特别是当PaaS/IaaS/云作为整个方案的一部分时

Drawbacks or concerns of a multiple live site configuration include多个活跃站点配置的缺点或者问题包括
* Greater operational complexity. 更大的运维复杂性
* Likely a small increase in headcount.可能要小幅增加人手
* Increase in travel and network costs. 增加出差和网络成本。

Architectural considerations in moving to a multiple live site environment include 对于多个活跃站点环境，架构上的考虑包括：
* Eliminating the need for state and affinity wherever possible。尽可能地消除对于状态和亲和性的需求
* Routing customers to the closest data center if possible to reduce dynamic call times。 尽可能地将客户路由到最近的数据中心，以减小动态呼叫时间
* Investigating replication technologies for databases and state if necessary。如果必须，研究数据库和状态的复制技术

### Rule 13—Design to Leverage the Cloud
### 规则13-设计充分利用云/为充分利用云而设计

**What:** This is the purposeful utilization of cloud technologies to scale on demand.这是有目的性地使用云技术，以按需可扩展。

**When to use:** When demand is temporary, spiky, and inconsistent and when response time is not a core issue in the product. Consider when you are “renting your risk”—when future demand for new products is uncertain and you need the option of rapid change or walking away from your investment. Companies moving from two active sites to three should consider the cloud for the third site. 当需求是临时的、突发性的和不一致的，并且响应时间不是这些产品中的核心问题的时候。考虑何时真正承担你的风险——当未来对于你产品的需求还不确定并且你需要选择快速改变或者放弃你的投资时。那些将两个活跃站点迁移到三个的公司应该考虑为第三个站点使用云。

**How to use:**
* Make use of third-party cloud environments for temporary demand, such as seasonal business trends, large batch jobs, or quality assurance (QA) environments during testing cycles. 使用第三方云环境满足临时性需求，例如季节性业务趋势、大量批处理作业或者在测试周期中的质量保证环境。
* Design your application to service some requests from a third-party cloud when demand exceeds a certain peak level. Scale in the cloud for the peak, then reduce active nodes to a basic level.设计你的应用，以当需求超过一个特定峰值水平时服务于一些来自第三方云的请求。针对峰值在云中扩展，然后减少活跃的节点到一个基本水平。

**Why:** Provisioning of hardware in a cloud environment takes a few minutes as compared to days or weeks for physical servers in your own colocation facility. When used temporarily, this is also very cost-effective. 在一个云环境中提供硬件仅仅需要花费几分钟的时间，与此相比在你的托管设施中提供物理服务器可能需要数天或者数周时间。当临时使用时，云环境也非常合算。

**Key takeaways:** Design to leverage virtualization in all sites and grow in the cloud to meet unexpected spiky demand. 为了在所有的站点中充分利用虚拟化而设计，在云中增长以满足意外的尖峰需求。

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


### Rule 14—Use Databases Appropriately
### 规则14-恰当地使用数据库

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

### Rule 15—Firewalls, Firewalls Everywhere!
### 规则15-防火墙，处处皆是防火墙

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

### Rule 16—Actively Use Log Files
### 规则16-积极地使用日志文件

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


## Chapter 5 Get Out of Your Own Way
## 第五章 不要固守成规


### Rule 17—Don’t Check Your Work
### 规则17-不要检查你的工作

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

### Rule 18—Stop Redirecting Traffic
### 规则18——停止重定向流量

**What:** Avoid redirects when possible; use the right method when they are necessary.尽量避免重定向；当需要重定向时，使用正确的方法

**When to use:** Always.总是

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


### Rule 19—Relax Temporal Constraints
### 规则19-放松时间约束

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

## Chapter 5 Use Caching Aggressively
## 第5章 大胆地使用缓存

Caching prevents you from needing to look up, create, or serve the same data over and over again. 缓存能够防止你一次又一次地查询、创建或者服务于相同的数据


Scaling static content, such as text and images that don’t change very often, is elementary. A number of rules in this book cover how to make static content highly available and scalable at low cost through the use of caches. Dynamic content, or content that changes over time, is not so elementary to serve quickly and scale out.
例如文本和图片这类静态内容不经常变化，因此实现静态内容的可扩展性比较容易实现。本书中的一些规则涉及如何利用缓存，使得静态内容以较低成本实现高可用和可扩展。动态内容或者随着时间变化的内容不容易实现快速服务和可扩展性。

1）：
To solve latency and scale issues, the first thing Lon’s team did was to add a content distribution network; they chose Akamai. Lon stated, “It was really simple to just take all of our static assets and push them there [Akamai] and let them handle caching closest to the user. And then we could expire [the objects] using their typical cache expiration tools when we published. Expiring objects was part of our deploy process.”
为了解决时延和可扩展性问题，Lon团队所做的一个事情就是添加内容分发网络，他们选择了Akamai。Lon说“真的非常简单，仅仅提取所有静态资产并将它们推送到Akamai，让Akamai将数据缓存到离用户最近的位置。然后当我们要发布时，我们可用使用通常的缓存过期工具将这些缓存的对象设置为过期。将对象设置为过期是我们部署过程的一部分

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


### Rule 20—Leverage Content Delivery Networks
### 规则20-充分利用内容分发网络

**What:** Use CDNs (content delivery networks) to offload traffic from your site. 使用CDN分担你网站的流量

**When to use:** When speed improvements and scale warrant the additional cost. 当需要提高速度并能够承担更多成本时

**How to use:** Most CDNs leverage DNS to serve content on your site’s behalf. Thus you may need to make minor DNS changes or additions and move content to be served from new subdomains.
大多数CDN使用DNS来代表你的网站提供内容。因此，你可能需要对DNS做一些小改动或者添加，并且需要转移内容，以在新的子域名下提供服务。

**Why:** CDNs help offload traffic spikes and are often economical ways to scale parts of a site’s traffic. They also often substantially improve page download times. 
CDN有助于减轻流量峰值，是扩展部分网站流量的一种经济方式。CDN通常还可以提高页面下载速度。

**Key takeaways:** CDNs are a fast and simple way to offset spikiness of traffic as well as traffic growth in general. Make sure you perform a cost-benefit analysis and monitor the CDN usage.
CNDs是一种快速和简单的方式，既能用于分流突发的流量，也能应对一般性的流量增长。确保进行成本效益分析，并监控CDN的使用情况。

### Rule 21—Use Expires Headers
### 规则21-使用过期头部标志

What: Use Expires headers to reduce requests and improve the scalability and performance of your system. 使用过期头部标志，以降低请求次数和提高系统的可扩展性和性能。

When to use: All object types need to be considered. 所有的对象类型都需要考虑

How to use: Headers can be set on Web servers or through application code. 头部标志能够在web服务器上或者通过应用代码来设置。

Why: The reduction of object requests increases the page performance for the user and decreases the number of requests your system must handle per user.
减小对象请求次数不仅可以提高用户的页面访问性能，并且可以减小系统针对每个用户必须处理的请求数量。

Key takeaways: For each object type (image, HTML, CSS, PHP, and so on), consider how long the object can be cached and implement the appropriate header for that time frame.
针对于每个对象类型（图片、HTML、CSS和PHP等），考虑对象可能的缓存时长，并且通过适当的头部标志来实现特定时间的缓存，

通过如下的头部标志实现缓存
* Pragma
* Expires
* Cache-Control
* Last-Modified:
* ETag

Keep-alives, or HTTP persistent connections

### Rule 22—Cache Ajax Calls
### 规则22-缓存Ajax调用

What: Use appropriate HTTP response headers to ensure cacheability of Ajax calls. 使用适当的HTTP应答头部标志，以确保Ajax调用的可缓存性。

When to use: Every Ajax call except for those absolutely requiring real-time data that are likely to have been recently updated. 每个Ajax调用，除了那些绝对需要实时性数据（最近更新的数据）的情况

How to use: Modify Last-Modified, Cache-Control, and Expires headers appropriately. 恰当地更改Last-Modified, Cache-Control, and Expires头部标志。

Why: Decrease user-perceived response time, increase user satisfaction, and increase the scalability of your platform or solution. 降低用户所能感觉到的响应时间，提高用户的满意度，并提高系统或者解决方案的可扩展性。

Key takeaways: Leverage Ajax and cache Ajax calls as much as possible to increase user satisfaction and increase scalability. 尽可能地使用Ajax和缓存Ajax调用，以提高用户满意度和可扩展性。

Ajax is an acronym for Asynchronous JavaScript and XML.Ajax是异步Javascrip和XML的缩写。


### Rule 23—Leverage Page Caches
### 规则23-充分利用页面缓存

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

### Rule 24—Utilize Application Caches
### 规则24-使用应用缓存

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


### Rule 25—Make Use of Object Caches
### 规则25-使用对象缓存

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


### Rule 26—Put Object Caches on Their Own “Tier”
### 规则26——将对象缓存放置到它们自己的层级中

What: Use a separate tier in your architecture for object caches. 在架构中针对于对象缓存使用一个分离的层级。

When to use: Anytime you have implemented object caches. 任何已经实现对象缓存的时候

How to use: Move object caches onto their own servers. 将对象缓存转移到自己的服务器

Why: The benefits of a separate tier are better utilization of memory and CPU resources and having the ability to scale the object cache independently of other tiers. 分离层级的好处是更好地利用CPU和内存资源，能够独立其他层级扩展对象缓存。

Key takeaways: When implementing an object cache, it is simplest to put the service on an existing tier such as the application servers. Consider implementing or moving the object cache to its own tier for better performance and scalability. 当实现对象缓存时，最简单的方式是将服务放置到一个已经存在的层级上，例如应用服务器。为了获得更好的性能和可扩展项，可以考虑在自己的层级上实现对象缓存或者将对象缓存转移到自己的层级上。


A better alternative is to put the object cache on its own tier of servers. This would be between the application servers and the database, if using the object cache to cache query result sets. If caching objects created in the application tier, this object cache tier would reside between the Web and application servers.
一个更好的选择是将对象缓存放置到自己层级中的服务器上。如果使用对象缓存来缓存查询结果集，则这个位置为应用服务器和数据库之间。如果如果在应用层级创建所缓存的对象，则对象缓存层级将位于web和应用服务器之间。

![Object Cache](pics/ObjectCache.JPG)

## Chapter 7 Learn from Your Mistakes
## 第七章 从自己的错误学习


failover architecture or active/active architecture 故障转移架构或者活跃/活跃架构

Organizations must learn both deeply and broadly. Depth of learning comes from asking “why” multiple times until the answers stop coming and causes are clearly identified. Breadth of learning comes not only from looking at the technical and architectural fixes necessary to make a better product, but also from identifying what we need to do with training, people, organizations, and the processes we employ. Incidents like data center failures are costly, and we must learn deeply and broadly from them in order to prevent similar failures.
组织必须深入而广泛地学习。学习的深度来在于多问问"为什么“，直到原因已经被清楚的确定并且答案不再出现。学习的广度不仅来自于研究那些制造更好产品所必须的技术和架构方法，而且来自于识别在培训、人员、组织和我们所部署的流程上我们需要做什么。像数据中心故障这样的事故，代价是非常高昂的，因此我们必须深入而广泛地从中学习，以防止类似的事故。

### Rule 27—Learn Aggressively
### 规则27——积极地学习

**What:** Take every opportunity, especially failures, to learn and teach important lessons. 抓住每个机会，尤其是故障，来学习和吸取重要的经验教训。

**When to use:** Be constantly learning from your mistakes as well as your successes. 持之以恒的从你的错误和成功中学习

**How to use:** Watch your customers or use A/B testing to determine what works. Employ a postmortem process and hypothesize failures in low-failure environments. 观察你的客户或者使用A/B测试，来确定什么是有效的。在低故障环境中使用事后分析过程和假设失效。

**Why:** Doing something without measuring the results or having an incident without learning from it are wasted opportunities that your competitors are taking advantage of. We learn best from our mistakes—not our successes. 做了些事情但是无法测量或者遇到事故但是没有从中学到教训，这都是浪费机遇，但是你的竞争者却会充分利用这些机遇。我们是从失误中而不是成功中学到最好的东西（不是成功，而是失败才是我们最好的老师）。

**Key takeaways:** Be constantly and aggressively learning. The companies that learn best, fastest, and most often are the ones that grow the fastest and are the most scalable. Never let a good failure go to waste. Learn from every one and identify the architecture, people, and process issues that need to be corrected. 要不断地和积极地学习。那些学习最好和最快的公司，往往也是增长最快和扩展性最强的公司。千万不要浪费一个好的故障。从每个故障中学习，并梳理架构、人员和流程方面需要改进的问题。

There are two areas in which learning is critical. The first, as we have been discussing, is from the customers. The second is from the operations of the business/technology. We discuss each briefly in turn. Both rely on excellent listening skills. We believe that we were given two ears and one mouth to remind us to listen more than we talk.
有两个方面的学习非常关键。第一个是我们已经讨论过的，要从的客户身上学习。第二个是从技术运维/业务运营中学习。我们将会按照顺序简要讨论这两个方面的学习。两个方面都依赖于出色的倾听技巧。我们相信我们之所以有两个耳朵和一个嘴巴，是因为要提醒我们多听少说。

Charles Perrow, Normal Accidents (Princeton, NJ: Princeton University Press, 1999).

Todd R. LaPorte and Paula M. Consolini, “Working in Practice but Not in Theory: Theoretical Challenges of ‘High-Reliability Organizations,’” Journal of Public Administration Research and Theory, Oxford Journals,
https://polisci.berkeley.edu/sites/default/files/people/u3825/LaPorte-WorkinginPracticebutNotinTheory.pdf

Charles Perrow’s Normal Accident Theory hypothesizes that the complexity inherent in modern coupled systems makes accidents inevitable. The coupling inherent in these systems allows interactions to escalate rapidly with little opportunity for humans or control systems to interact successfully.
Charles Perrow的正态事故理论假设现代耦合系统所固有的复杂性使得故障不可避免。这些系统所固有的相互耦合会使得相互之间的交互迅速恶化，而没有给人类或者控制系统留下成功交互的机会。

Todd LaPorte, who developed the theory of high reliability organizations, believes that even in the case of an absence of accidents from which an organization can learn, there are organizational strategies to achieve higher reliability。Todd LaPorte，其发展了高可靠组织理论，认为即使在没有故障的情况下，组织也能从中学习到经验，使用组织性策略实现更高的可靠性。

For any major issue that we experience, we believe an organization should attack that issue with a postmortem process that addresses the problem in three distinct but easily described phases 我们相信一个组织应该通过事后处理流程来攻克我们所经历的任何主要问题，解决这问题的流程可用划分为三个迥异但易于描述的阶段。
* Phase 1: Timeline—Focus on generating a timeline of the events leading up to the issue or crisis. Nothing is discussed other than the timeline during this first phase. The phase is complete once everyone in the room agrees that there are no more items to be added to the timeline. We typically find that even after we’ve completed the timeline phase, people continue to remember or identify timeline-worthy events in the next phase of the postmortem. 阶段1 ：时间线——聚焦于生成一个由导致问题或者事故的事件所构成的时间线。在第一个阶段，不要讨论任何事情，仅仅是时间线。当屋子里的所有人都同意没有更多的事项需要添加到时间线上，则完成这个阶段。即使我们已经完成了时间线阶段，我们通常还会发现事件，在下一个阶段的事后分析中人们会不断回想起或者识别出对于时间线有价值的事件。
* Phase 2: Issue identification—The process facilitator walks through the timeline and works with the team to identify issues. Was it OK that the first monitor identified customer failures at 8:00 a.m. but that no one responded until noon? Why didn’t the auto-failover of the database occur as expected? Why did we believe that dropping the table would allow the application to start running again? Each and every issue is identified from the timeline, but no corrections or actions are allowed to be made until the team is done identifying issues. Invariably, team members will start to suggest actions, but it is the responsibility of the process facilitator to focus the team on issue identification during Phase 2.  阶段2： 问题识别——过程协调员与团队一同工作，沿着时间线从头到尾地识别问题。早上8点第一个监控器就已经识别出客户故障，但是到中午还没有反应，这种情况是否正常？为什么数据库的自动故障切换没有按照所预期的发生？为什么我们认为删除这个表就能够使得应用再次开始运行？在时间线上的每一个问题都需要被识别，但是在团队识别完所有的问题之前，不许可修复或者采取措施。在第二个阶段，团体成员总是会开始提出措施，但是过程协调员的职责是将团队聚焦于识别问题。
* Phase 3: State actions—Each item should have at least one action associated with it. For each issue on the list, the process facilitator works with the team to identify an action, an owner, an expected result, and a time by which it should be completed. Using the SMART principles, each action should be specific, measurable, attainable, realistic, and timely. A single owner should be identified, even though the action may take a group or team to accomplish.阐述措施——每个事项都应该至少有一个与之相关联的措施。过程协调员与团队一起工作，对于列表中的每一个问题找到对应的措施、实施者、所期望的结果以及必须完成的时间。使用SMART原则，每个措施应该是具体的、可以量的、可以达到的、具有相关性（Relevant）、有实效性的。每个措施都要指派一个实施者，即使这个措施可能需要一组或者整个团队来完成。


No postmortem should be considered complete until it has addressed the people, process, and architecture issues responsible for the failure. Too often we find that clients stop at “a server died” as a root cause for an incident. Hardware fails, as do people and processes, and as a result no single failure should ever be considered the “true root cause” of any incident. The real question for any failure of scalability or availability is to ask, “Why didn’t the holistic system act more appropriately?” If a database fails due to load, “Why didn’t the organization identify the need earlier?” What process or monitoring should have been in place to help the organization find the issue? Why did it take so long to recover from the failure? Why isn’t the database split up such that any failure has less of an impact on our customer base or services? Why wasn’t there a read replica that could be quickly promoted as the write database? In our experience, you are never finished unless you can answer the question “why” at least five times to cover five different potential problems. Asking “why” five times is common but somewhat arbitrary, and you should continue to ask it until nothing new is revealed. It is a process for identifying multiple causes or contributing factors. Rarely do we see a failure caused by a single root cause.Keep incident logs and review them periodically to identify repeating issues and themes.
直到解决了导致故障的人员、流程和架构问题，才认为事后处理过程已经完成。我们频繁地发现客户将”一个服务器死掉"作为一个事故的根源，并停止了事后处理过程。像人员和流程一样，硬件会发生故障，但是作为结果，单一故障不应被认为是任何一个事故的真实根源。对于可扩展性和可用性方面的任何故障，一个应该询问的问题是：“为什么整个系统不能更加适当地应对？”。如果一个数据库由于负载的原因而发生故障，“为什么组织不能在更早地识别出需要？”。需要设置何种流程或者监控，能够帮助组织发现问题。为什么花费这么长的时间才从故障中恢复？为什么不拆分数据库，使得任何故障可以更少地影响我们的客户群或者服务？为什么一个读副本没有能够快速地提成为写数据库。根据我们的经验，不要结束故障处理过程，除非针对涵盖五个不同的潜在问题，能够至少五次地回答为什么的问题。提问为什么五次是常见的，但也是武断的，你应该继续发问，直到没有新东西揭示出来。这是一个识别多个原因或者影响因素的过程。我们发现一个故障是由单一根源导致的情况非常罕见。保存故障的日志并定期地回顾这些日志，以识别周期性的问题和主题。


Our philosophy is that while mistakes are unavoidable, making the same mistake twice is unacceptable. If a poor-performing query doesn’t get caught until it goes into production and results in a site outage, we must get to the real root cause and fix it. In this case the root cause goes beyond the poorly performing query and includes the process and people that allowed it to get to production. 我们的哲学是犯错是不可避免的，但是两次犯相同的错误是不可接受的。如果一个存在性能问题的查询直到部署到生产系统并且导致网站宕机才被发现，那么我们必须找到真正的根源并加以修复。在这个例子中，根源远不止于有性能问题的查询，还包括许可这个有问题的查询进入生产系统的流程和人员。

### Rule 28—Don’t Rely on QA to Find Mistakes
### 规则 28——不要依赖于质量保证来发现错误

QA：Quality Assurance 质量保证

**What:** Use QA to lower the cost of delivered products, increase engineering throughput, identify quality trends, and decrease defects—not to increase quality. 使用AQ虽然可以降低产品交付成本、提高工程产出、识别质量趋势和减少缺陷，但是并不能提高质量。

**When to use:** Whenever you can, get greater throughput by hiring someone focused on testing rather than writing code. Use QA to learn from past mistakes—always. 在任何可能的时候，通过雇佣一些人专注于测试而不是编写代码的员工能够得到更高的产出。使用QA能够从过去的错误中学习，并且总是如此。

**How to use:** Hire a QA person anytime you get greater than one engineer’s worth of output with the hiring of a single QA person. 一旦与雇佣一个工程师相比，你能够获得更多的产出，就雇佣一个QA员工。

**Why:** Reduce cost, increase delivery volume/velocity, decrease the number of repeated defects. 降低成本、提高交货量和交货速度，降低重复缺陷的数量。

**Key takeaways:** QA doesn’t increase the quality of your system, as you can’t test quality into a system. If used properly, it can increase your productivity while decreasing cost, and most importantly it can keep you from increasing defect rates faster than your rate of organizational growth during periods of rapid hiring. QA不能提高你系统的质量，因为你不能在系统中测试质量。如果使用得当，QA能够在降低成本的同时提高你的生产率，并且更重要的是，其能够在快速招聘期间防止缺陷增加的速率高于你组织增长的速率。

Techniques such as code reviews and test-driven development (TDD) help engineers create quality code, identifying defects before they reach QA. Conducting code reviews one on one with peers helps engineers find and fix mistakes overlooked in the initial development process. Test-driven development is a technique that has the engineer develop the automated test case that defines the new feature or function, then produce the minimum amount of code to pass the test. TDD improves code quality while increasing productivity. These techniques help build quality into the software early in the process and reduce rework.
诸如代码评审和测试驱动开发这样的技术能够帮中工程师创建靠质量代码，使得缺陷在到达QA之前就识别出来。与同事一对一的处理代码评审有助于工程师发现和修复在初始开发过程中被忽视的错误。测试驱动开发是一种技术，首先由工程师开发的自动化测试实例定义新的特性或者功能，然后以最小的代码量通过测试。测试驱动开发在增加生产效率的同时也提高了代码质量。这些技术有助于在初期就将构建质量融入到软件中，从而减小返工。

### Rule 29—Failing to Design for Rollback Is Designing for Failure
### 规则29——不为回滚而设计就是为失败而设计

What: Always have the ability to roll back code. 总是能够回滚代码。

When to use: Ensure that all releases have the ability to roll back, practice it in a staging or QA environment, and use it in production when necessary to resolve customer incidents. 确保所有的发布都能够回滚，在测试环境或者QA环境中演练，然后当能够解决客户的问题时，在生产环境使用。

How to use: Clean up your code and follow a few simple procedures to ensure that you can roll back your code. 清除你的代码并执行若干简单过程，一确保你能够回滚代码。

Why: If you haven’t experienced the pain of not being able to roll back, you likely will at some point if you keep playing with the “fix-forward” fire. 如果你没有经历过不能回滚的痛苦，那么你非常可能

Key takeaways: Don’t accept that the application is too complex or that you release code too often as excuses that you can’t roll back. No sane pilot would take off in an airplane without the ability to land, and no sane engineer would roll code that he or she could not pull back off in an emergency. 不能接受以应用过于复杂或者以发布代码过于频繁为借口来拒绝回滚。理智的飞行员不会登上无能降落的飞机，同样地，一个理智的工程师不会上线在紧急情况下不能退回的代码。