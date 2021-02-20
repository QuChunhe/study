

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



数据扩展所面临的两个问题
* 复制或者克隆：一致性问题，CAP
* 拆分或者sharding：事务保障

基于业务和场景进行简化
* 不改和少删，最终保持一致即可：比如weibo这类社交媒体，
* 一写多读，许可不一致，例如12306这类订票系统，查询和订购分别使用读库和写库，允许多个读库与写库之间短时间的不一致，仅仅会短时间增加写库的压力，不会引起其他的问题
* 有事务要求，但是事务所涉及的多个步骤是可逆的，例如转账。

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


在用户向WEb服务器请求服务时，Web服务器
用户与服务器之间的异步操作
* 增加交互，例如返回确认界面，
* 后台操作
   * 基于WebSocket的站内消息
   * 基于定时Ajax的消息

服务器与服务器之间的异步操作
* Future，不同管理域，即属于不同的管理者
* 消息队列，同一管理域
* Callback ，不同管理域和同一管理域都可以


# Papers
[1] Patrick O'Neil, Edward Cheng, Dieter Gawlick, Elizabetch O'Neil. The log-structured merge-tree (LSM-tree). Acta Informatica, 1996, 33(4): 351-385.

[Brewer’s Conjecture and the Feasibility ofConsistent, Available, Partition-Tolerant WebServices](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.67.6951&rep=rep1&type=pdf)

It is impossible for a web service to provide the following three guarantees:
* Consistency
* Availability
* Partition-tolerance

ACID

Interactions with web services are expected to behave in a transactional manner: operations commit or fail in their entirety (atomic), committed transactions are visible to all future transactions (consistent), uncommitted transactions are isolated from each other (isolated), and once a transaction is committed it is permanent (durable).


Atomic , or linearizable , consistency is the condition expected by most web services today.


Alan Fekete, David Gupta, Victor Luchangco, Nancy Lynch, and Alex Shvartsman. Eventually-serializable data services. Theoretical Computer Science, 220(1):113–156, June 1999.

[Keeping CALM: When Distributed Consistency is Easy](https://arxiv.org/pdf/1901.01930.pdf)

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


Kafka Producer配置需要在两个方面的折中考虑
* 吞吐（时延）和可靠性之间的折中
* 丢失消息和重复消息之间的折中
较大的消息吞吐和较小的发送时延需要以降低消息可靠性为代价，容易出现消息丢失或重复消息的问题，反之亦然，提高可靠性需要降低。类似地，
文中介绍的是如果接受到ack，那么确保消息不会丢失。另一种常见情况是在超时之后还没有受到ack，Producer如何处理？如果重传，可能出现消息重复，如果不重传，可能出现消息丢失

可靠性相关的配置参数
* Topic
  * replication-factor:replication-factor不能超过Borker的数量，数值越大，可靠性消息可靠性越高

* Producer
  * acks: 
  * min.insync.replicas

[Kafka 如果丢了消息，怎么处理？](https://mp.weixin.qq.com/s/TcN5kslQxRQOBlkSjg7_Sg)


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

# 一致性（Consensus/Consistency)


[The Raft Consensus Algorithm](https://raft.github.io/)

[Distributed Systems, Failures, and Consensus](https://www2.cs.duke.edu/courses/fall07/cps212/consensus.pdf)

分布式算法的两个属性
* 安全性（safty）
* 活跃性（liveness）

安全性是指坏的事情不会发生，而活跃性是指某些号的事情最终一定会发生。


[Two-phase commit protocol](https://en.wikipedia.org/wiki/Two-phase_commit_protocol)
[二阶段提交](https://zh.wikipedia.org/wiki/%E4%BA%8C%E9%98%B6%E6%AE%B5%E6%8F%90%E4%BA%A4)
two-phase commit protocol (2PC) 

2PC是一种针对分布式环境设计的一种算法，用于协调所有节点（或进程）在参与分布式原子事务时保持一致。在分布式系统中，每个节点虽然可以知晓自己的操作时成功或者失败，却无法知道其他节点的操作的成功或失败。当一个事务跨越多个节点时，为了保持事务的ACID特性，需要引入一个作为协调者的组件来统一掌控所有节点（称作参与者）的操作结果并最终指示这些节点提交或者中止（回滚）这个事务。 即使遇到系统故障（涉及进程、网络节点、通信等的故障）的情况下，该协议也能达到其目标，因此其被广泛使用。 

在2PC协议中将所有的节点（或进程）被划分为两类，其中一个被设计为协调者（coordinator），而其他的被设计为参与者（participants，cohorts或workers）。

The protocol assumes that there is stable storage at each node with a write-ahead log, that no node crashes forever, that the data in the write-ahead log is never lost or corrupted in a crash, and that any two nodes can communicate with each other. The last assumption is not too restrictive, as network communication can typically be rerouted. The first two assumptions are much stronger; if a node is totally destroyed then data can be lost. 
该协议假设每个节点都具有稳定的存储和一个预写日志，并且节点不会永远处于崩溃状态，因此预写日志的数据不会丢失，也不会在崩溃中损坏。任意两个节点之间都能够相互通讯。最后一个假设不太严格，因为网络通讯通常能够重新路由。前两个假设非常强，如果一个节点被完全摧毁，那么数据肯能会丢失。

任何分布式事务在“正常执行”的情况下（也就是说，当没有出现失败的情况下，但是在实际的大型分布式系统中故障是常态），2PC协议有两个阶段组成
1. 请求阶段（commit-request phase，或称表决阶段，voting phase）。在此阶段，一个协调者尝试让所有参与者针对于是提交事务、还是终止这个事务进行投票，或者“Yes”： 提交（如果事务参与这本地部分正确执行），或者“No”：终止（如果检测到本的部分出现问题），
   1. The coordinator sends a query to commit message to all participants and waits until it has received a reply from all participants. 协调者向所有参与者发送询问是否提交操作，并一直等待，直到接收到来自所有参与者的响应。
   2. The participants execute the transaction up to the point where they will be asked to commit. They each write an entry to their undo log and an entry to their redo log. 参与者执行所有截止到询问发起时间的事务操作，并将Undo信息和Redo信息写入日志。
   3. Each participant replies with an agreement message (participant votes Yes to commit), if the participant's actions succeeded, or an abort message (participant votes No, not to commit), if the participant experiences a failure that will make it impossible to commit. 如果参与者成功完成了操作，则响应一个同意消息（参与者投Yes表示提交）。如果节点遭遇到一个使得无法提交的失败，则应答一个”中止”消息。    
   
2. 提交阶段（commit phase）：基于参与者的投票，协调者决定是提交事务（仅当所有参与者投“Yes”）、还是终止这个事务（其他情况），并将结果通告给所有的参与者。按照通告的要求，参与者随后针对其本地事务资源（也被称为可恢复资源，例如数据库数据）执行所需的操作（提交或者终止）。
   * Success： If the coordinator received an agreement message from all participants during the commit-request phase:在请求阶段，如果协调者从所有的参与者接收到同意消息
        1. The coordinator sends a commit message to all the participants. 协调者发送一个提交消息给所有的参与者。
        2. Each participant completes the operation, and releases all the locks and resources held during the transaction.每个参与者完成操作，并释放在此事务期间持有的所有锁和资源。
        3. Each participant sends an acknowledgement to the coordinator. 每个参与者发送一个确认消息给协调者。
        4. The coordinator completes the transaction when all acknowledgments have been received. 当收到所有的确认消息时，协调着完成这个事务。
   * Failure： If any participant votes No during the commit-request phase (or the coordinator's timeout expires)。在请求阶段，如果其中一个参与者投票为No（或者协调者时间过期）。
        1. The coordinator sends a rollback message to all the participants. 协调者发送一个回滚消息给所有的参与者。
        2. Each participant undoes the transaction using the undo log, and releases the resources and locks held during the transaction.每个参与者使用undo日志取消事务，并释放在此事务期间持有的所有锁和资源。
        3. Each participant sends an acknowledgement to the coordinator. 每个参与者发送一个确认消息给协调者。
        4. The coordinator undoes the transaction when all acknowledgements have been received. 当收到所有的确认消息时，协调着取消这个事务。


2PC是安全的。不会有坏数据被写入数据库，但是其活跃性不好。

2PC的第一个问题：同步阻塞问题。
The greatest disadvantage of the two-phase commit protocol is that it is a blocking protocol. If the coordinator fails permanently, some participants will never resolve their transactions: After a participant has sent an agreement message to the coordinator, it will block until a commit or rollback is received
两阶段提交最大的缺点是其是一个阻塞式协议。如果协调者永久地失效，则一些参与者将不会释放它们的事务： 在一个参与者发送一个同意消息给协调者后，这个参与者将会一直阻塞，直到接收到提交或者回滚消息为止。


2PC的第二个问题：单点故障。
A two-phase commit protocol cannot dependably recover from a failure of both the coordinator and a cohort member during the Commit phase. If only the coordinator had failed, and no cohort members had received a commit message, it could safely be inferred that no commit had happened. If, however, both the coordinator and a cohort member failed, it is possible that the failed cohort member was the first to be notified, and had actually done the commit. Even if a new coordinator is selected, it cannot confidently proceed with the operation until it has received an agreement from all cohort members, and hence must block until all cohort members respond.
在提交阶段两阶段提交协议不能可靠地从协调者和参与者的故障中恢复。如果仅仅协调者失败，并且没有参与者收到提交消息，则能够安全地断定没有发生提交。但是，如果协调者和一个参与者都失败了，那么失败的那个参与者可能是第一个被通知的，并且已经完成了提交。即使选择了新的协调者，在收到来自所有参与者的同意之前，新协调者也无法自信地继续操作，因此必须阻止，直到所有参与者做出响应。 

The three-phase commit protocol eliminates this problem by introducing the Prepared to commit state. If the coordinator fails before sending preCommit messages, the cohort will unanimously agree that the operation was aborted. The coordinator will not send out a doCommit message until all cohort members have ACKed that they are Prepared to commit. This eliminates the possibility that any cohort member actually completed the transaction before all cohort members were aware of the decision to do so (an ambiguity that necessitated indefinite blocking in the two-phase commit protocol). 
三阶段提交协议通过引入准备提交（Prepared to commit）状态消除了这个问题。如果协调者在发送preCommit消息之前失败，参与者将一致同意操作被中止。协调者将不会发送doCommit消息，直到所有参与者已经确认他们准备提交。这就消除了如下的可能性，即在所有其他参与者知道决定如何操作之前，任意一个参与者已经完成事务（这种模糊性使得在两阶段提交协议中需要无限阻塞）。 

2PC在这种fail-stop情况下会失败是因为voter在得知Propose Phase结果后就直接commit了, 而并没有在commit之前告知其他voter自己已收到Propose Phase的结果. 从而导致在coordinator和一个voter双双掉线的情况下, 其余voter不但无法复原Propose Phase的结果, 也无法知道掉线的voter是否打算甚至已经commit. 

3PC可以有效的处理fail-stop的模式, 但不能处理网络划分(network partition)的情况---节点互相不能通信. 假设在PreCommit阶段所有节点被一分为二, 收到preCommit消息的voter在一边, 而没有收到这个消息的在另外一边. 在这种情况下, 两边就可能会选出新的coordinator而做出不同的决定.


除了网络划分以外, 3PC也不能处理fail-recover的错误情况. 简单说来当coordinator收到preCommit的确认前crash, 于是其他某一个voter接替了原coordinator的任务而开始组织所有voter commit. 而与此同时原coordinator重启后又回到了网络中, 开始继续之前的回合---发送abort给各位voter因为它并没有收到preCommit. 此时有可能会出现原coordinator和继任的coordinator给不同节点发送相矛盾的commit和abort指令, 从而出现个节点的状态分歧.


3PC就是把2PC的Commit阶段拆成了PreCommit和DoCommit两个阶段. 通过进入增加的这一个PreCommit阶段, 参与者可以得到上一阶段的投票结果, 但不会提交; 而通过进入DoCommit阶段, 参与者才最终提交事务.
1. CanCommit：此阶段类似于2PC的请求阶段。
        1.协调者向所有参与者发出包含事务内容的CanCommit请求，询问是否可以提交事务，然后等待所有参与者的答复。
        2.在收到CanCommit请求后，参与者如果认为自己可以执行事务操作，则应答YES并进入预备状态，否则应答NO。
2. PreCommit
   * 当所有参与者均应答YES时
        1.协调者向所有参与者发出PreCommit请求，进入准备阶段。
        2.参与者收到PreCommit请求后，执行事务操作，将Undo和Redo信息记入事务日志中（但不提交事务）。
        3.各参与者向协调者应答Ack消息或No消息，并等待最终指令。 
   * 当任何一个参与者反馈NO，或者等待超时后协调者尚无法收到所有参与者的应答时
        1.协调者向所有参与者发出abort请求。
        2.无论收到协调者发出的abort请求，或者在等待协调者请求过程中出现超时，参与者均会中断事务
3. DoCommit
   * 当所有参与者均反馈Ack响应时
        1.如果协调者处于工作状态，则向所有参与者发出DoCommit请求。
        2.参与者收到DoCommit请求后，会正式执行事务提交，并释放整个事务期间占用的资源。
        3.各参与者向协调者应答Ack完成的消息。
        4.协调者收到所有参与者的Ack消息后，即完成事务提交。
   * 任何一个参与者反馈NO，或者等待超时后协调者尚无法收到所有参与者的反馈时
        1.如果协调者处于工作状态，向所有参与者发出abort请求。
        2.参与者使用阶段1中的Undo信息执行回滚操作，并释放整个事务期间占用的资源。
        3.各参与者向协调者应答Ack完成的消息。
        4.协调者收到所有参与者的Ack消息后，即完成事务中断

XA规范，XA是由X/Open组织提出的分布式事务的规范，主要是给数据库提供一个标准，各家数据库可以根据这个标准完成自己的分布式事务协议


Google Chubby的作者Mike Burrows说过， there is only one consensus protocol, and that’s Paxos” – all other approaches are just broken versions of Paxos. 意即世上只有一种一致性算法，那就是Paxos，所有其他一致性算法都是Paxos算法的不完整版。

JTA（Java Transaction API）也定义了对XA事务的支持，实际上，JTA是基于XA架构上建模的，在JTA 中，事务管理器抽象为javax.transaction.TransactionManager接口，并通过底层事务服务（即JTS）实现

Best efforts 1 Phase commit 

笼统地讲，与事务在执行中发生错误后立即回滚的方式不同，事务补偿是一种事后检查并补救的措施，它只期望在一个容许时间周期内得到最终一致的结果就可以了。事务补偿的实现与系统业务紧密相关，并没有一种标准的处理方式。一些常见的实现方式有：对数据进行对帐检查;基于日志进行比对;定期同标准数据来源进行同步，等等

[Distributed transactions in Spring, with and without XA](https://www.infoworld.com/article/2077963/distributed-transactions-in-spring--with-and-without-xa.html)

TCC（Try-Confirm-Cancel）又称补偿事务。其核心思想是："针对每个操作都要注册一个与其对应的确认和补偿（撤销操作）"。它分为三个操作：
* Try阶段：主要是对业务系统做检测及资源预留。
* Confirm阶段：确认执行业务操作。
* Cancel阶段：取消执行业务操作。
TCC事务的处理流程与2PC两阶段提交类似，不过2PC通常都是在跨库的DB层面，而TCC本质上就是一个应用层面的2PC，需要通过业务逻辑来实现。这

![Transactions Across Datacenters](pics/TransactionsAcrossDatacenters.png)

[Google I/O 2009 - Transactions Across Datacenters.](https://www.youtube.com/watch?v=srOgpXECblk)
[Google I/O 2009 跨数据中心事务](https://www.bilibili.com/video/av57190094/)

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


[The Fundamental Mechanism of Scaling](http://brooker.co.za/blog/2021/01/22/cloud-scale.html)

A common misconception among people picking up distributed systems is that replication and consensus protocols—Paxos, Raft, and friends—are the tools used to build the largest and most scalable systems.
当人们学习分布式系统时一个常见的错误概念是复制和一致性协议（Paxos、Raft和frients？）是用来构建更大和高伸缩系统的工具。

At the most basic level, though, they don't make systems scale.
但是，在最基本的层面上，这些协议并不会使得系统具有可伸缩性。

Instead, the fundamental approach used to scale distributed systems is avoiding co-ordination. Finding ways to make progress on work that doesn't require messages to pass between machines, between clusters of machines, between datacenters and so on. The fundamental tool of cloud scaling is coordination avoidance
反而，用于扩展分布式系统的最基本方法是避免协作。寻找方法，既能够完成工作，又无需在机器之间、在机器集群之间、在数据中心之间传递消息。云扩展的基本工具是避免协作。

With this in mind, we can build a kind of spectrum of the amount of coordination required in different system designs:
* Coordinated. These are the kind that use paxos, raft, chain replication or some other protocol to make a group of nodes work closely together. The amount of work done by the system generally scales with the offered work (W) and the number of nodes (N), something like O(N * W) (or, potentially, worse under some kinds of failures).
*Data-dependent Coordination. These systems break their workload up into uncoordinated pieces (like shards), but offer ways to coordinate across shards where needed. Probably the most common type of system in this category is sharded databases, which break data up into independent pieces, but then use some kind of coordination protocol (such as two-phase commit) to offer cross-shard transactions or queries. Work done can vary between O(W) and O(N * W) depending on access patterns, customer behavior and so on.
* Leveraged Coordination. These systems take a coordinated system and build a layer on top of it that can do many requests per unit of coordination. Generally, coordination is only needed to handle failures, scale up, redistribute data, or perform other similar management tasks. In the happy case, work done in these kinds of systems is O(W). In the bad case, where something about the work or environment forces coordination, they can change to O(N * W) (see Some risks of coordinating only sometimes for more). Despite this risk, this is a rightfully popular pattern for building scalable systems.
* Uncoordinated These are the kinds of systems where work items can be handled independently, without any need for coordination. You might think of them as embarrassingly parallel, sharded, partitioned, geo-partitioned, or one of many other ways of breaking up work. Uncoordinated systems scale the best. Work is always O(W).


[Amazon Builders' Library中文](https://aws.amazon.com/cn/builders-library/?cards-body.sort-by=item.additionalFields.customSort&cards-body.sort-order=asc)

[Amazon Builders' Library En](https://aws.amazon.com/builders-library/?nc1=h_ls&cards-body.sort-by=item.additionalFields.customSort&cards-body.sort-order=asc)


[ Distributed systems: for fun and profit](http://book.mixu.net/distsys/index.html)

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

[Programming Models for Distributed Computing](https://heather.miller.am/teaching/cs7680/)

[Distributed Systems: Paul Krzyzanowski](https://www.cs.rutgers.edu/%7Epxk/417/notes/index.html)

[Distributed and Operating Systems: Lecture notes, handouts and schedule](http://lass.cs.umass.edu/~shenoy/courses/677/lectures.html)

http://lass.cs.umass.edu/~shenoy/courses/spring19/readings.html

[Distributed DBMS - Concepts](https://www.tutorialspoint.com/distributed_dbms/distributed_dbms_concepts.htm)

Matthieu Perrin, Distributed Systems. Concurrency and Consistency,ISTE Press,2017

Andreas Meier, Michael Kaufmann, SQL & NoSQL Databases: Models, Languages, Consistency Options and Architectures for Big Data Management, Springer Vieweg, 2019

M. Tamer Özsu, Patrick Valduriez, Principles Of Distributed Database Systems, Springer 2020

Alex Petrov, Database Internals: A deep-dive into how distributed data systems work, O’Reilly Media,2019

[Marc's Blog](http://brooker.co.za/blog/)



