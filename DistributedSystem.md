

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
* 降低时延，降低响应时间。功能和模块的分布式部署，增加了调用的时延，通常会增加服务的响应时间。但是:a)如果充分挖掘任务蕴含的并发性和充分使用分布式系统的并行处理能力，可以弥补分布式处理带来的时间损耗，降低服务时延;b)通过平衡负载，减小等待实际，实现更快的的响应能力


分布式的对象
* 数据(data)，存储的分布化
* 功能(function)，计算和处理的分布化
* 请求(request)，

分布式的方法：
* 分割/划分（partition/split)，通过提高并发度来提高吞吐，通过并行处理来降低服务时间。
* 复制/克隆（replicate/clone)，分担负载来提高吞吐，提高可靠性


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


### Martin L. Abbott and Michael T. Fisher, Scalability Rules：Principles for Scaling Web Sites Second Edition, 2017

#### Reduce the Equation 大道至简

match the effort and approach to the complexity of the problem. Not every solution has the same complexity—take the simplest approach to
achieve the desired outcome。努力和方法要与问题的复杂性相匹配。不是每个方案都有相同的复杂性，选取最简单的方法，实现所期望的结果

keeping things as simple as possible. Our view is that a complex problem is really just a collection of smaller, simpler problems waiting to be solved.保持事情尽可能的简单。从我们的视角来看，一个复杂问题其实仅仅是一些更小的、更简单的待解决问题集合

##### Rule 1—Don’t Overengineer the Solution 不要过度设计方案

The first category covers products designed and implemented to exceed their useful
requirements.


The second category of overengineering deals with making something overly complex
and making something in a complex way.

不要向不需要的需求或功能买单

[Faster Time to Market – How to Avoid Overengineering (Rule 1)](https://akfpartners.com/growth-blog/faster-time-to-market-how-to-avoid-overengineering-yagni)

Overengineering is solving problems you don’t have.

We will look at two sides of overengineering: Exceeding useful requirements, and spending too much effort to get a job done.

##### Rule 2—Design Scale into the Solution　(D-I-D Process) 将可扩展性设计到方案中（设计-实现-部署过程）

How to use:
* Design for 20x capacity.
* Implement for 3x capacity.
* Deploy for roughly 1.5x capacity.


D-I-D provides a cost-effective, JIT method of scaling your product.

Dell, configure-to-order： 按订单配置，just-in-time manufacturing：及时制造

AKF Partners’ Design-Implement-Deploy or D-I-D approach to thinking about scalability.

[The DID Process - Scale Design Principles (Rule 2)](https://akfpartners.com/growth-blog/scale-design-principles-the-did-process)


Ideally, what you want is JIT (just-in-time) scalability. The idea originates from JIT manufacturing, and relates to reducing delivery time. JIT scalability is the ability to scale up or down when needed, as needed.

infrastructure-as-a-service (IaaS) 

有预见性的设计，分阶段性的实现，及时性的部署

##### Rule 3—Simplify the Solution Three Times Over 三重简化方案

How to use:
* Simplify scope using the Pareto Principle.
* Simplify design by thinking about cost effectiveness and scalability.
* Simplify implementation by leveraging the experience of others.

Pareto principle 即帕累托法则，又称80/20法则、马特莱法则、二八定律、帕累托定律、最省力法则、不平衡原则、犹太法则。意大利经济学家帕累托提出的。法则认为原因和结果、投入和产出、努力和报酬之间本来存在着无法解释的不平衡

[Scalability Rules - How to Simplify Scope, Design, and Implementation (Rule 3)](https://akfpartners.com/growth-blog/scalability-rules-how-to-simplify-scope-design-and-implementation)

简化体现在更容易被理解，完成的时间更短，所付出的代价更小


##### Rule 4—Reduce DNS Lookups 减少DNS查找
##### Rule 4—避免重复性工作

方法
* Batch: 打包批量处理
* cache 缓存和复用结果


How to use: Minimize the number of DNS lookups required to download pages, but balance
this with the browser’s limitation for simultaneous connections.

在分割后的功能中包含一些重复的处理，将这个处理分离出来，作为一个公共的前置功能。

[Reduce DNS lookups to improve website performance (Rule 4)](https://akfpartners.com/growth-blog/reduce-dns-lookups-to-improve-website-performance)

##### Rule 5—Reduce Objects Where Possible
##### Rule 5—控制分割的粒度

How to use:
* Reduce or combine objects but balance this with maximizing simultaneous connections.
* Look for opportunities to reduce weight of objects as well.
* Test changes to ensure performance improvements.




无论是对应功能进行分割，还是对应数据进行分割，都会引入高昂的代价。如果分割的粒度过小，那么所付出的代价将远远超过所引入的好处，因而得不偿失。


##### Rule 6—Use Homogeneous Networks使用同构网络


对于操作系统以及数据库、JDK和Nginx等系统软件采用相同的版本。


#### Distribute Your Work 分布你的工作


##### Rule 7-Design To Clone or Replicate Things (X Axis)

##### Rule 7-为克隆或者复制而设计

When to use:
* Databases with a very high read-to-write ratio (5:1 or greater—the higher the better).
* Any system where transaction growth exceeds data growth.
How to use:
* Simply clone services and implement a load balancer.
* For databases, ensure that the accessing code understands the difference between a
read and a write.

There are a couple of ways that you can distribute the read copy of your data depending on the time sensitivity of the data. Time (or temporal) sensitivity is how fresh or completely correct the read copy has to be relative to the write copy.

时间敏感性是指相对于写副本，读副本的一致或者完全正确程度。


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


# 高可用

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

平均无故障时间（MTBF）平均无故障工作时间，英文全称是“Mean Time Between Failure”

Mean Time To Repair (MTTR)

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

