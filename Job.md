
* 数据分层问题：ODS (Operational Data Store) DWD：data warehouse details，DWB：data warehouse base，DWS：data warehouse servic
* 数据规约，1）名称的问题；2）数据范围问题
  * 缺失：应该有，但是没有。
  * 无效：有值但是超过许可范围，例如
  * 无值：在这个维度不可应用，例如，对于40机型，不存在耗材使用量，可以采用默认值-1，
* 原始数据层 schema问题  

There are two types of schemas:
* Predefined。Traditional Model – "Schema on Write"。Schema是预先定义好的，数据在写入表时校验数据是否符合schema定义，只有符合的情况下，才能写入表。
* Dynamic。Big data Model -  "Schema on read".  With the Big Data and NoSQL paradigm, “Schema-on-Read” means you do not need to know how you will use your data when you are storing it. 写入数据时不检查,而是在读取时根据需求采用一个schema来解析数据。

* 大宽表和小窄表的问题，事实表、维度表，
 * 存储方式
 * schema设计
 * 查询模式

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