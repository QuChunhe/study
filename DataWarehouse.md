
设计
* 尽可能多的过滤数据
* 尽可能少的移动数据
* 尽可能多的支持应用：在近可能少的开发情况下


优化策略
* 空间换时间：固定查询，可提前处理
  * 索引
  * 物化视图
  * 缓存
* 数据裁剪：所有查询，包括ad hoc查询。减小数据量：1）从磁盘读取尽可能少的数据；2）在节点之前传输尽可能少的数据
  * 谓词下推
  * Join-Reorder  


：FACT（事实表）和 DIM（维度表）


实时数仓是相对于传统的离线数仓而言，其实时包含两层含义
* 实时入库。传统数仓为T+1处理数据，即今天的数据，明天才能入库。
* 实时查询。传统数仓仅仅支持定时的批量处理任务。


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