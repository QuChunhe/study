


如下三个方面需要相互匹配
* 数据存储方式
* schema设计
* 数据查询模式


* Replication
* Sharding
* Caching

MySQL中存在三类不同的表
* 业务型 : 维度表
* 日志型：原子
* 汇总型


存储选型问题

采用何种数仓建模

数据规范化问题：1）

数据应用价值问题




* 数据分层问题：ODS (Operational Data Store) 
DWD：data warehouse details，DWB：
data warehouse base，
DWS：data warehouse servic


* 数据规约，1）名称的问题；2）数据范围问题
  * 缺失：应该有，但是没有。
  * 无效：有值但是超过许可范围，例如
  * 无值：在这个维度不可应用，例如，对于40机型，不存在耗材使用量，可以采用默认值-1，
* 原始数据层 schema问题  

There are two types of schemas:
* Predefined。Traditional Model – "Schema on Write"。Schema是预先定义好的，数据在写入表时校验数据是否符合schema定义，只有符合的情况下，才能写入表。
* Dynamic。Big data Model -  "Schema on read".  With the Big Data and NoSQL paradigm, “Schema-on-Read” means you do not need to know how you will use your data when you are storing it. 写入数据时不检查,而是在读取时根据需求采用一个schema来解析数据。



* 报告的简单和灵活，可拖拽，资源压力

技术问题
* hudi如何保留原始数据，不重复，不丢失，比如重复导入的问题，业务主键+message id，broker+offset
* 乱序问题，level
* 急停、手工暂停等时间，小时报表

hudi和doris的问题


丢失、乱序和多版本问题

* 决策支持，报表
* 辅助操作，分析和建议
* 自动处理，


mysql
* 业务表
* 汇总表
* 日志表

软件架构由多个不同的架构组成，每个架构是软件的一个视图，用于刻画软件系统的一个方面
* 业务架构
* 功能架构
* 技术架构
* 数据架构
* 集成架构
* 部署架构
* 安全架构

上述架构既相互关联和相互影响，又有侧重，共同构建了一个系统的架构全貌。




* 不要向不需要的需求或功能买单
* 不要将功能设计得过于复杂


有预见性的设计，分阶段性的实现，及时性的部署


规约：命名和规范等

模板：gradle mvn配置模板


统一：同意的版本