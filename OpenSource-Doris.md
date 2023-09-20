
数据模型

分区分桶
* 分桶避免数据倾斜

join的条件字段
* 都是HASH字段
* 相同的桶数
DISTRIBUTION KEY决定于join操作，从而避免shuffle.

优化最常用的查询

Doris 支持两种物理算子，一类是 Hash Join，另一类是 Nest Loop Join。
* Hash Join：在右表上根据等值 Join 列建立哈希表，左表流式的利用哈希表进行 Join 计算，它的限制是只能适用于等值 Join。
  * Shuffle Join: Shuffle Join会将A，B两张表的数据根据哈希计算分散到集群的节点之中，所以它的网络开销为 A + B，网络开销T(S)+T(R)
  * Bucket Shuffle Join: 网络开销T(R)
  * Shuffle Join: Shuffle Join会将A，B两张表的数据根据哈希计算分散到集群的节点之中，所以它的网络开销为 A + B，网络开销T(S)+T(R)
  * Colocate: 网络开销0.
* Nest Loop Join：通过两个 for 循环，很直观。然后它适用的场景就是不等值的 Join，例如：大于小于或者是需要求笛卡尔积的场景。它是一个通用的 Join 算子，但是性能表现差。

说明：R(关系)表示关系的tuple数目

A join B
* Broadcast Join: 如果根据数据分布，查询规划出A表有3个执行的HashJoinNode，那么需要将B表全量的发送到3个HashJoinNode，那么它的网络开销是3B，它的内存开销也是3B。网络开销N*T(R)


>将session变量enable_bucket_shuffle_join设置为true，则FE在进行查询规划时就会默认将能够转换为Bucket Shuffle Join的查询自动规划为Bucket Shuffle Join。

在FE进行分布式查询规划时，优先选择的顺序为 Colocate Join -> Bucket Shuffle Join -> Broadcast Join -> Shuffle Join。但是如果用户显式hint了Join的类型，则上述的选择优先顺序则不生效.


runtime filter：减小数据量

从业务角度看，Key 和 Value 可以分别对应维度列和指标列。

Doris 支持两层的数据划分。第一层是 Partition，支持List Partition 与 Range Partition。第二层是 Bucket（Tablet），仅支持 Hash 的划分方式。


多个 Tablet 在逻辑上归属于不同的分区（Partition）。一个 Tablet 只属于一个 Partition，而一个 Partition 包含若干个 Tablet。因为 Tablet 在物理上是独立存储的，所以可以视为 Partition 在物理上也是独立。Tablet 是数据移动、复制等操作的最小物理存储单元。

若干个 Partition 组成一个 Table。Partition 可以视为是逻辑上最小的管理单元，数据的导入与删除，都可以或仅能针对一个 Partition 进行

* 一个表的 Tablet 总数量等于 (Partition num * Bucket num)。
* 一个表的 Tablet 数量，在不考虑扩容的情况下，推荐略多于整个集群的磁盘数量。


动态 Range Partition。