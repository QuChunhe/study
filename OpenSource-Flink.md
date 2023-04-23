

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

* keyed state 
* operator state.

