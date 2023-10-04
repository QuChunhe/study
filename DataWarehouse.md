

# 数仓理论

在数据仓库领域，有两位大师，一位是“数据仓库”之父 Bill Inmon，一位是数据仓库权威专家 Ralph Kimball，两位大师每人都有一本经典著作，Inmon 大师著作《数据仓库》及 Kimball 大师的《数仓工具箱》。




范式建模：Inmon 模型从流程上看是自上而下的，自上而下指的是数据的流向，“上”即数据的上游，“下”即数据的下游，即从分散异构的数据源 -> 数据仓库 -> 数据集市。以数据源头为导向，然后一步步探索获取尽量符合预期的数据，因为数据源往往是异构的，所以会更加强调数据的清洗工作，将数据抽取为实体-关系模型，并不强调事实表和维度表的概念。


维度模型（Dimensional models）：Kimball的维度模型是从需求出发，从数据集市-> 数据仓库 -> 分散异构的数据源。Kimball 是以最终任务为导向，将数据按照目标拆分出不同的表需求，数据会抽取为事实-维度模型，数据源经 ETL 转化为事实表和维度表导入数据集市，以星型模型或雪花模型等方式构建维度数据仓库，架构体系中，数据集市与数据仓库是紧密结合的，数据集市是数据仓库中一个逻辑上的主题域。

维度设计过程的四个步骤
1. Select the business process.
2. Declare the grain.
3. Identify the dimensions.
4. Identify the facts.

Inmon模型
* CIF（Corporate Information Factory） 
* EDW Enterprise Data Warehouse

设计
* 尽可能多的过滤数据
* 尽可能少的移动数据
* 尽可能地使用变化：需求的变化、数据的变化在近可能少的开发情况下

数据的一致性：公告标识和定义在不同数据来源共用。

数据的及时性：

维度建模：FACT（事实表）和 DIM（维度表）

凡事应该尽量简单，直到不能再简单为止。

Einstein “Everything should be made as simple as possible, but no simpler.” or “Make things as simple as possible, but not simpler.”

建立在关系数据库之上
* 星型模型
* 雪花模型
* 星座模型


ETL：Extract Transformation and Load
上钻下钻


* 事实表：用于度量
  * 细节表
  * 汇总表
* 维度表

事实表中的每行对应一个度量的事件。特定级别的数据，别称为粒度。

敏捷：以迭代的和增量的方式开发

事实表
* number类型
* 可枚举类型

维度表
* 可枚举类型，包括时间
* 字符串仅仅出现在字典表红

事实的类型和性质

数值类型
* 可加类型：对关联的任意维度可加
* 半可加类型：对某些维度可加，但不能对所有维度可加，例如剩余电量和剩余水量，仅仅可以按照时间维度相减。
* 不可加实时：对所有维度都不可加，比如清洁效率。

尽最大可能将文本数据放入维度中。不要再事实表中存储冗余的文本信息。

事实表的粒度可以划分为三类
* 事务事实表（Transaction Fact Tables）：每一行对应空间或者时间上某一个点的度量时间。
* 周期快照事实表（Periodic Snapshot Fact Tables）：每一行汇总发生在某一个标砖周期的多个度量时间
* 累积快照事实表（Accumulating Snapshot Fact Tables）
* 无事实事实表（Factless Fact Tables）：
* 汇总事实表或者OLAP立方（Aggregate Fact Tables or OLAP Cubes）
* 合并事实表（Consolidated Fact Tables）：通常将来自多个过程的，以相同粒度表示的事实合并为一个单一的合并事实表。


维度表

退化的维度键

维度的历史纪录表
* 如何去重：如何去除重复数据
* 如何关联：如何关联到事实表


维度表的属性是所有查询约束和报表标识的来源。属性应包含真实使用的词汇，而不是缩写。

如何区分：维度属性与事实属性
* 是否数值类型
* 数值是否可枚举
* 是否参与度量

商品的标价是一个度量事实


维度表和事实表在粒度的定义上保持一致

原子粒度是最低级别的粒度
* 从原子级别的粒度开始设计
* 性能或者资源无法满足需求，上卷汇总粒度

维度主键尽量采用整数
* Natural keys（自然主键）
* durable key （持久主键）
* durable supernatural key 持久超自然主键

维度类型
* Calendar Date Dimensions
* Role-Playing Dimensions
* Junk Dimensions (transaction profile dimension)
* Snowflaked Dimensions
* Outrigger Dimensions

Integration via Conformed Dimensions通过一致维度集成



实时数仓是相对于传统的离线数仓而言，其实时包含两层含义
* 实时入库。传统数仓为T+1处理数据，即今天的数据，明天才能入库。
* 实时查询。传统数仓仅仅支持定时的批量处理任务。



优化策略
* 空间换时间：固定查询，可提前处理
  * 索引
  * 物化视图
  * 缓存
* 数据裁剪：所有查询，包括ad hoc查询。减小数据量：1）从磁盘读取尽可能少的数据；2）在节点之前传输尽可能少的数据
  * 谓词下推
  * Join-Reorder  





OLAP的基本概念
* 维度（Dimension）：刻画数据的特定角度或者特定属性，一般为整数、字符串（包括枚举类型）和时间。
* 层次（Level）/粒度（Granularity）：刻画某一特定维度或者属性的不同细节程度
* 成员（Member）：维度的一个取值
* 度量（Measure）：数据的取值，一般为数值类型，包括整数、定点数和浮点数

OLAP的基本多维分析操作包括
* 钻取：（Drill-up和Drill-down）：改变维度的层次，变化分析的粒度
* 切片（Slice）、切块（Dice）
* 旋转（Pivot）：变换维度的方向

* ODS (Operational Data Store) 简称ODS  操作数据存储 也称为贴源层。
* DWD：data warehouse details 细节数据层，是业务层与数据仓库的隔离层。主要对ODS数据层做一些数据清洗和规范化的操作。
* DWB：data warehouse base 数据基础层，存储的是客观数据，一般用作中间层，可以认为是大量指标的数据层。
* DWS：data warehouse service 数据服务层，基于DWB上的基础数据，整合汇总成分析某一个主题域的服务数据层，一般是宽表。用于提供后续的业务查询，OLAP分析，数据分发等。

ODD：Operation Data Store 数据准备区，也称为贴源层。


个人划分
* 源数据层
* 服务数据层（）
* 应用数据层

https://www.snowflake.com/en/

https://delta.io/


机器人数据
* 重复
* 乱序
* 丢失
* 异常：
  * 缺失：应该有，但是没有。
  * 无效：有值但是超过许可范围，例如
  * 无值：在这个维度不可应用，例如，对于40机型，不存在耗材使用量，可以



缓慢变化维、也就是 SCD（Slowly Changing Dimensions）


数据展示方式
* 分页
* 加载更多
* 无限滚动

[数据模型例子与范式](https://mongoing.com/docs/applications/data-models.html)



# Doris

Doris 的数据模型主要分为3类:
* Aggregate
* Unique
* Duplicate