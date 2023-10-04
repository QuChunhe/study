

[](https://mp.weixin.qq.com/mp/appmsgalbum?action=getalbum&__biz=MzIzMDMwNTg3MA==&scene=1&album_id=1351753739203592192&count=3&pass_ticket=pqCbMei%2Fx%2BPd3go9oUeEgdDZdAXq2yefGQDXcb4r2u1PdG3xb5zYIEOuP5j%2BEEfA)


[](https://mp.weixin.qq.com/mp/appmsgalbum?action=getalbum&album_id=1337172142412169216&__biz=MzIxMTE0ODU5NQ==&scene=21#wechat_redirect)


```shell
 docker pull flink:1.12.1

 ./mvnw clean package -DskipTests -Drat.skip=true

```

https://zhuanlan.zhihu.com/p/176855301

https://nightlies.apache.org/flink/flink-docs-release-1.13/docs/deployment/resource-providers/standalone/docker/

https://zhuanlan.zhihu.com/p/102325190

[Flink Checkpoint 参数详解](https://www.cnblogs.com/weijiqian/p/14159326.html)

flink Checkpoint优化

一、设置最小时间间隔
streamExecutionEnvironment.getCheckpointConfig().setMinPauseBetweenCheckpoints(milliseconds)

二、预估状态容量

三、异步Snapshot
1.首先必须是flink托管状态，即使用flink内部提供的托管状态所对应的数据结构，例如常用的有ValueState、ListState、ReducingState等类型状态。

2.StateBackend必须支持异步快照，在flink1.2的版本之前，只有RocksDB完整地支持异步的Snapshot操作，从flink1.3版本以后可以在heap-based StateBackend中支持异步快照功能

四.压缩状态数据
flink中使用的压缩算法在ExecutionConfig中进行指定，通过将setUseSnapshotCompression方法中的值设定为true即可

ExternalizedCheckpointCleanup 可选项如下:

ExternalizedCheckpointCleanup.RETAIN_ON_CANCELLATION： 取消作业时保留检查点。请注意，在这种情况下，您必须在取消后手动清理检查点状态。
ExternalizedCheckpointCleanup.DELETE_ON_CANCELLATION： 取消作业时删除检查点。只有在作业失败时，检查点状态才可用。


Flink 在其内部构建了一套自己的类型系统，Flink 现阶段支持的类型分类如图所示，从图中可以看到 Flink 类型可以分为基础类型（Basic）、数组（Arrays）、复合类型（Composite）、辅助类型（Auxiliary）、泛型和其它类型（Generic）。

[Flink Watermark 机制及总结](https://mp.weixin.qq.com/s?__biz=MzU5MTc1NDUyOA==&mid=2247485947&idx=1&sn=f74d272774ba79ef1648bef2c838c176&chksm=fe2b6db4c95ce4a2e11973b3149a35d98ee19ea7da03d3c46c17cd071c58101773f156569916&mpshare=1&scene=1&srcid=0322nNfVdKf4wu93jQCVN2vi&sharer_sharetime=1647921478130&sharer_shareid=fc937fe50a97e6c10553c542abe0a39b&exportkey=AWTQvILqBI9wZSrcv9OQqjI%3D&acctmode=0&pass_ticket=CgAFL972fvllR0PThPItOFzxZ12DdYKzEKKGXFGcYICDSfM2ts2r3%2FHGxaf8uoNc&wx_header=0#rd)

常用的预定义的窗口分配器，即：滚动窗口、滑动窗口、会话窗口和全局窗口。你也可以通过继承 WindowAssigner 类来自定义自己的分配器。 


flink提供了两种抽取event-time的方式

在stream-source中直接放入event-time并且产生watermark
使用Timestamp Assigners / Watermark Generators 来产生event-time和water-mark

[Enabling savepoints for Flink applications](https://docs.cloudera.com/csa/1.5.1/job-lifecycle/topics/csa-savepoint.html#:~:text=The%20following%20command%20lines%20can%20be%20used%20to,%20%20%24%20bin%2Fflink%20savepoint%20-d%20%3CsavepointPath%3E%20)

```shell

#Trigger savepoint	
flink savepoint -yid <yarnAppID> <jobId> [targetDirectory]
#Cancel job with savepoint	
flink cancel -yid <yarnAppID> <jobId>
#Resume from savepoint	
flink run -s <savepointPath> [runArgs]
#Deleting savepoint	
flink savepoint -d <savepointPath>


sudo flink list  -yid application_1648273333036_0001 

sudo flink cancel -s s3://bigdata-staging-cn-northwest-1-s3-statistics-escargot/tools/flink/robot-cube/savepoints/  -yid application_1648273333036_0001 e5a89464313618b16ea173d60649ab79

sudo flink run -s s3://bigdata-staging-cn-northwest-1-s3-statistics-escargot/tools/flink/robot-cube/savepoints/savepoint-e5a894-87aa19e0e002/ -d -m yarn-cluster -yid application_1648273333036_0001 /mnt/robot-cube/robot-stream-0.1-SNAPSHOT.jar


```



Flink DataStream API 为用户提供了3个算子来实现双流 join，分别是：
* join()
* coGroup()
* intervalJoin()

```java
stream.join(otherStream)
    .where(<KeySelector>)
    .equalTo(<KeySelector>)
    .window(<WindowAssigner>)
    .apply(<JoinFunction>)
```
TimestampsAndWatermarks



* 窗口的划分
* 数据乱序、延迟到达
* 何时触发窗口计算
* 计算状态的存储和过期

状态
* keyed state 
* operator state.

Fink的窗口（Window）可以分成两类：
* CountWindow：按照指定的数据条数生成一个 Window，与时间无关。
* TimeWindow：按照时间生成 Window。

TimeWindow，可以根据窗口实现原理的不同分成三类：
* 滚动窗口（Tumbling Window）
* 滑动窗口（Sliding Window）
* 会话窗口（Session Window）。


客户端

集群：
flink Master
* JobManager:Scheduler
* Dispatcher
* ResourceManager

TaskManager
* Task Slot: container

数据倾斜的定位

1. 步骤1：定位反压
定位反压有2种方式：Flink Web UI 自带的反压监控（直接方式）、Flink Task Metrics（间接方式）。通过监控反压的信息，可以获取到数据处理瓶颈的 Subtask。

2. 步骤2：确定数据倾斜
Flink Web UI 自带Subtask 接收和发送的数据量。当 Subtasks 之间处理的数据量有较大的差距，则该 Subtask 出现数据倾斜。


第一种：数据源source消费不均匀。调整并发度的原则：KafkaSource 并发度与 kafka 分区数是一样的，或者 kafka 分区数是KafkaSource 并发度的整数倍。

第二种：key分布不均匀并且无统计场景，可以通过添加随机前缀打散它们的分布，使得数据不会集中在几个 Task 中。

第三种 可以分布不均匀并有统计场景。两阶段聚会：1）预聚合：加盐局部聚合，在原来的 key 上加随机的前缀或者后缀。2）聚合：去盐全局聚合，删除预聚合添加的前缀或者后缀，然后进行聚合统计。




numberOfTaskSlots

每个任务节点的并行子任务占据不同的 slot；不同的任务节点的子任务可以共享 slot。

slot 共享：将资源密集型和非密集型的任务同时放到一个 slot 中，它们就可以自行分配对资源占用的比例，从而保证最重的活平均分配给所有的TaskManager。slotSharingGroup

task slot 是静态的概念 ， 是指TaskManager 具有的并发执行能力 ， 可以通过参数taskmanager.numberOfTaskSlots 进行配置；


一个特定算子的 子任务（subtask）的个数被称之为其并行度（parallelism）。    
一般情况下，一个 stream 的并行度，可以认为就是其所有算子中最大的并行度


三个位置可以配置并行度
* flink配置文件中
* 代码里
* flink任务提交时

优先级
> 代码>提交>配置文件


算子链：将算了链接成task。Flink默认会将算子尽可能地链接。OperatorChain的优点
* 减少线程切换
* 减少序列化与反序列化
* 减少延迟并且提高吞吐能力。
```java
.flatMap(_.split(" ")).disableChaining()

.startNewChain()

env.disableOperatorChaining()
```

 Per-Job模式

考虑到集群的资源隔离情况，一般生产上的任务都会选择per job模式，也就是每个任务启动一个flink集群，各个集群之间独立运行，互不影响,且每个集群可以设置独立的配置。

```shell
bin/flink run -m yarn-cluster ./examples/batch/WordCount.jar
```


applcation模式

 ```shell
 flink run-application -p $p -Dtaskmanager.numberOfTaskSlots=$3 -Djobmanager.memory.process.size=$4 -Dtaskmanager.memory.process.size=$5 -t yarn-application -Dyarn.application.name=$1 -c $2 ~/robot-stream/robot-stream.jar
 ```

Time
* Event-time Mode:
* Watermark Support: 
* Late Data Handling
* Processing-time Mode


Monitor and Control Your Applications
* Web UI:
* Logging: slf4j logging interface and integrates with the logging frameworks log4j or logback.
* Metrics: JMX, Ganglia, Graphite, Prometheus, StatsD, Datadog, and Slf4j.
* REST API: