
数据类型
* 业务数据：随机增删改查
* 日志数据：只增不改不删
* 汇总数据：顺序增少量改

两类应用
* OLAP – Online Analytical Processing
* OLTP – Online Transactional Processing

There are two types of schemas:
* Predefined
* Dynamic

There are two types of data models:
* Relational
* Nonrelational

In addition to making updates and reads very fast, normalization eliminates the risk of inconsistent data.


模型的层次
* Conceptual Model (概念模型)
* Logical Model (逻辑模型)
* Pyhsical Model (物理模型)

[The Snowflake Elastic Data Warehouse](http://pages.cs.wisc.edu/~yxy/cs839-s20/papers/snowflake.pdf)

[NoSQL Data Modeling Techniques](https://www.cnblogs.com/balaamwe/archive/2012/05/02/2478699.html)

[NoSQL Data Modeling Techniques](https://www.idc-online.com/technical_references/pdfs/information_technology/NoSQL_Data_Modeling_Techniques.pdf)

![大数据集成架构](pics/big-date-integration.jpg)
* 数据来源：业务数据和日志数据
* 大数据系统：方便地接受来自不同数据源的数据，经过处理后，按需地将数据发送目标系统
  * 传: 
     * 构造插入命令和预处理数据：通用、可配置，少定制化开发
	   * 缓存或者存储：a）传输时延，尤其是跨数据中心的数据传输；b）目标系统的吞吐问题；c）网络或者目标系统不可用，例如网络传输丢包；d）降低系统耦合性、提高系统安全性和提高数据复用性。
     * Kafka和FTP是比较常用的存储/缓存数据工具
  * 存
     * 数据规模：
     * 数据类型：结构化数据和非结构化数据
	   * 访问模式：避免无效访问数据的规模
  * 算
     * 批量处理：大多数为定时任务，少部分为即席计算
	   * 实时处理：流式计算
* 应用系统：
  * 写入存储：大多数是业务数据和汇总数据，少数情况下会访问原始日志数据（经过裁剪的日志数据）
     * 比较常用的就是MySQL（集群）和Redis（集群）
     * 少数情况是HBase和ES这类NoSQL
  * 触发应用：触发报警或者调用接口等	
  * 即席计算：面向公司内部用户，例如数据分析员、开发工程师和机器学习应用等：a）访问频率并不高；建立专用系统，使用/投入比低；b）访问数据规模大，对于其他数据访问应用会有一定影响；c）访问模式差异大

支撑功能
* 定时调度
* 访问控制：身份认证和资源限制
* 监控集成：集成到现有的监控系统
* 持续发布：集成都git的pipeline
* 自动配置：例如调整处理参数，能够自动生效


高度重视实时处理
* 提高时效性，能够提高数据价值
* 批量处理可能造成目标系统的突发负载
* 实时处理+触发应用：有很多业务应用空间

不要忽视非结构化数据 


* 业务目标
   * 有哪些不同的角色
   * 不同角色的核心诉求和痛点
   * 公司和部门发展规划和目标
* 演进步骤
   * 业务效果和基础设施之间的平衡
   * 确保每个季度都要有业务成果
* 技术选型：概念多、系统多、发展快。没有最好的技术，只有最合适的业务。
  * 算：flink，spark
  * 存：MySQL集群、HBase，Hive、...,Data Lake,Data Lakehouse（湖仓一体）


分散在各个平台和数据库的系统 chaos

统一的数仓中，集中仓库  order

Data Warehouse 所有的主题 , Data Mart特定的主题


Modern Data Warehouse
1. Ingest: Data orchestration and monitoring
2. Store; Big Data store
3. PREP: Transform & Clean
4. Model & Serve(& Store): Data warehouse

应用
* BI + reporting
* Advanced Analytics
* AI + ML
  
Use a data lake: 
* All data has potential value 
* Data hoarding 
* No defined schema—stored in native format 
* Schema is imposed and transformations are done at query time (schema-on-read). 
* Apps and users interpret the data as they see fit 

two approaches for building data warehouses
* Kimball methodology(Dimensional Modeling):Bottom up aproach
   * Facts and dimensions, star schema
   * less tables, but have duplicate data
   * Easier for user to understand
   * Slowly changing dimensions, surrogate keys.
* Inmon Methodology (Relation Modeling)： Top-down approach
   * Entity-RelationShip model
   * Many tables using joins
   * History tables, natural keys
   * Goog for indirect end-user access of data

自顶向下的方法
* 先有模型
* 确定需要解决的问题

自底向上的方法
* 后有模型
* 不确定需要解决的问题

两类主键
* natural keys：自然主键，有业务含义。A natural key is a single column or set of columns that uniquely identifies a single record in a table, where the key columns are made up of real data.  A natural key is a column value that has a relationship with the rest of the column values in a given data record。
  * 需要更少的表以及更少的join操作
  * 主键为业务数据，可以之间进行检索，更加利于查询
  * 便于partition和sharding
* surrogate keys：人工主键，自增ID或者UUID。The surrogate key is just a value that is generated and then stored with the rest of the columns in a record.  The key value is typically generated at run time right before the record is inserted into a table. 
  * 一般为整数，4或8个字节，占用更少的键存储，便于索引
  * 

The  "data lake" uses A bottoms-up approach.

* 大宽表：NoSQL，避免JOIN，查询模式固定。数据规模超大，多为日志数据，字段多样并且多为字符串类型，例如商品的特性(不同类型的商品具有迥异的特性)。复杂运算、海量检索
* 小表+业务表：MySQL，可以join，查询模式多样。汇总数据中小，多为汇总数据，字段固定并且多为数字类型。部分检索（条件为主键或者索引）、reduce(例如count、sum、max等)和map运算
  
  汇总表
* 维度：最新粒度+基本维度。为了性能考虑，可能需要建立不同粒度和不同维度的汇总表
* 统计值
完成基本指标的
* 多个粒度：reduce运算+join
* 特定维度：group

Exactly what is a data lake? A storage repository, usually Hadoop, that holds a vast amount of raw data in its native format until it is needed. 
* Inexpensively store unlimited data 
* Centralized place for multiple subjects (single version of the truth) 
* Collect all data “just in case” (data hoarding) 
* Easy integration of differently-structured data
* Store data with no modeling – “Schema on read” 
* Complements enterprise data warehouse (EDW) 
* Frees up expensive EDW resources for queries instead of using EDW resources for transformations (avoiding user contention) • 
* Hadoop cluster offers faster ETL processing over SMP solutions 
* Quick user access to data for power users/data scientists (allowing for faster ROI) 
* Data exploration to see if data valuable before writing ETL and schema for relational database, or use for one-time report 
* Allows use of Hadoop tools such as ETL and extreme analytics • Place to land IoT streaming data • On-line archive or backup for data warehouse data 
* With Hadoop/ADLS, high availability and disaster recovery built in 
* Keep raw data so don’t have to go back to source if need to re-run • Allows for data to be used many times for different analytic needs and use cases 
* Cost savings and faster transformations: storage tiers with lifecycle management; separation of storage and compute resources allowing multiple instances of different sizes working with the same data simultaneously vs scaling data warehouse; low-cost storage for raw data saving space on the EDW 
* Extreme performance for transformations by having multiple compute options each accessing different folders containing data 
* The ability for an end-user or product to easily access the data from any location

Data Analysis Paradigm Shift
* old way: Structure -> ingest -> Analyze
* new way: Ingest -> Analyze -> Structure

Data lake layers
* Raw Data layer 
* cleansed Data layer 
* application data layer 
* sandbox data layer


Organizing a  Data lake - Folder structure
* Plan the structure based on optimal data retrieval
* Avoid a chaotic, unorganized data swamp

Common ways to organize the data
* Time partitioning: 不要过大或者过小
* Subject Area
* Security Boundaries
  * Department
  * Business unit
* Downstream App/Purpose
* Data Retention Policy
   * Temporary Data
   * permanent data
   * Applicable period
* Business Impact /Criticality
  * High
  * Medium
  * Low
* Owner /Steward/SME
* Probability of Data Access
  * Recent /current data
  * historical data
* Confidential Classification
  * public information
  * internal user only
  * supplier/partner confidential
  * sensitive - financial

organizing
* evn
  * test
  * staging
  * product
* report/mysql/video
* data source/subject  
* time


Multidimensional data model (MDDM)
* Data Cube Model
* Start Schema Model: Star join Schema 星形模式（一个事实表，多个维度表）每个维度仅仅存在一个表
* Snow Flake Schema Model：雪花模式（一个事实表，多个维度表）每个维度可能存在多个相关联的表
* Fact Constellations：事实星座模式（多个事实表）

 The two primary component of dimensional model 
 * Dimensions:- Texture Attributes to analyses data. 
 * Facts:- Numeric volume to analyze business. 

Fact Table ◦ Fact table consists of the measurements and facts of the business process. ◦ A fact table typically has two types of columns: those that contains facts(numerical values) and those that are foreign key to dimension tables.

Dimension Table ◦ The dimension table provides the detailed information about the attributes in the fact table. ◦ Fact tables connect to one or more dimension tables, but fact tables do not have direct relationships to one another.

The MDDM involve two types of tables
* Dimension Table:  
   * Consists of tupple of attributes of dimension. 
   * It is Simple Primary Key.  
* Fact Table
   * A Fact table has tuples, one per a recorded fact.  
   * It is Compound primary key. 


Fact Table
*  Measure
*  dimension :keys

Star Scheme 
* In the star schema design, a single object (the fact table) sits in the middle and is connected to other surrounding objects (dimension tables) like a star. 
* A star schema has one dimension table for each dimension.


Snowflake Scheme 
* Snowflake schemas contain several dimension tables for each dimension. *◦ 
* The main advantage of the snowflake schema is that it reduces the space required to hold the data and the number of places where it need to be updated if the data changes. 
* The main disadvantage of the snowflake schema is that it increase the number of tables that need to join in order to perform the given query.

Levels of data modeling:
* Conceptual Data Model • A conceptual data model identifies the highestlevel relationships between the different entities.
* Logical Data Model • A logical data model describes the data in as much detail as possible, without regard to how they will be physical implemented in the database. • Identify entity and relationships. • All attributes of each entity. • Identify primary and foreign key.
* Physical Data Model • Physical data model represents how the model will be built in the database.


* 关系模型
* 维度模型

Entity Relationship models关系-实体模型，表间的交互关系可以表示为实体-关系图
* entities： Attributes:
* relationships
  * 一对一
  * 一对多
  * 多对多
满足3NF

relationships among those entities and relationships among those atributes.

成本、性能和三者之间平衡

recursive relationship

Keys: Natural vs. Surrogate 
* Natural keys are based on business rules and logic that determine how an individual instance can be uniquely identified. 
* Surrogate keys are often used instead, which are system-generated unique identifiers. e.g. Customer ID, Product ID, etc. — While surrogate keys are more efficient, important business rules are lost when they are used. 
It’s a balancing act


OLTP
* 避免数据冗余
* 确保数据一致性



* ODS：Operation Data Store 最贴近数据源的一层，为接收到的最原始数据，用于数据溯源。
* DWD：data warehouse details 细节数据层，是业务层与数据仓库的隔离层。主要对ODS数据层做去噪、去重、异常值处理和规范化等操作。命名规范化、设置维度表
* DWB：data warehouse base 数据基础层，存储的是客观数据，确定核心指标，执行一些轻度聚会和常用计算。
* DWS：data warehouse service 数据服务层，基于DWB上的基础数据，整合汇总成分析某一个主题域的服务数据层，一般是宽表。用于提供后续的业务查询，OLAP分析，数据分发等。
* ADS （ADS，Application Data Service）数据应用层，


Raw Zone -> Gold Zone
* 剔除重复数据
* 处理异常数据
* 规范数据定义
* 汇总业务指标

应用范式 Application paradigm

Data products can process data in real time or in batches.

real-time applications and data products 
* Dashboards 仪表盘
* Automated actions 自动操作，complex event processing (CEP)
* Alerts and notifications 报警和通知
* Data sets


https://www.slideshare.net/ivoandreev/data-warehouse-design-and-best-practices
https://www.slideshare.net/jamserra/is-the-traditional-data-warehouse-dead 
https://www.slideshare.net/jamserra/data-warehousing-trends-best-practices-and-future-outlook

Reasons not to user Hadoop as your DW
* Query performance not as good as relational database 
* Complex query support not good due to lack of query optimizer, in-database operators, advanced memory management, concurrency, dynamic workload management and robust indexing 
* Concurrency limitations • 
* No concept of “hot” and “cold” data storage with different levels of performance to reduce cost 
* Not a DBMS so lack of features such as update/delete of data, referential integrity, statistics, ACID compliance, data security 
* File based so no granular security definition at the column level 
* No metadata stored in HDFS, so another tool required adding complexity and slowing performance 
* Finding expertise in Hadoop is very difficult 
* Super complex, with lot’s of integration with multiple technologies to make it work 
* Many tools/technologies/versions/vendors (fragmentation), no standards, and it is difficult to make it a corporate standard 
* Lack of master data management tools for Hadoop • Requires end-users to learn new reporting tools and Hadoop technologies to query the data • 
* Pace of change is so quick many Hadoop technologies become obsolete, adding risk • Lack of cost savings: cloud consumption, support, licenses, training, and migration costs
* Need conversion process to convert data to a relational format if a reporting tool requires it 
* Some reporting tools don’t work against Hadoop



Data Lake + Data Warehouse


https://www.slideshare.net/ecastrom/data-warehouase-best-practices

Consider partitioning large fact tables 
* Consider partitioning fact tables that are 50 to 100GB or larger. 
* Partitioning can provide manageability and often performance benefits.  
   * Faster, more granular index maintenance. 
   * More flexible backup / restore options. 
   * Faster data loading and deleting 
   * Faster queries when restricted to a single partition.
* Typically partition the fact table on the date key. •
   * Enables sliding window. 
* Enables partition elimination. Source. 


Build clustered index on the date key of the fact table 
* This supports efficient queries to populate cubes or retrieve a historical data slice. 
* If you load data in a batch window for the clustered index on the fact table then use the options 
  
  ALLOW_ROW_LOCKS = OFF and ALLOW_PAGE_LOCKS = OFF 
* This helps speed up table scan operations during query time and helps avoid excessive locking activity during large updates.
* Build nonclustered indexes for each foreign key. 
  *This helps ‘pinpoint queries' to extract rows based on a selective dimension predicate. 
* Use filegroups for administration requirements such as backup / restore, partial database availability, etc. 

Choose partition grain carefully
* 数据规模
* 最多可用的parttion数量


Design dimension tables appropriately 
* Use integer surrogate keys for all dimensions, other than the Date dimension. 
* Use the smallest possible integer for the dimension surrogate keys. This helps to keep fact table narrow. 
* Use a meaningful date key of integer type derivable from the DATETIME data type (for example: 20060215). 
* Don't use a surrogate Key for the Date dimension Source. 
* Build a clustered index on the surrogate key for each dimension table  
* Build a non-clustered index on the Business Key (potentially combined with a row-effective-date) to support surrogate key lookups during loads. 
* Build nonclustered indexes on other frequently searched dimension columns. 
* Avoid partitioning dimension tables. 
* Avoid enforcing foreign key relationships between the fact and the dimension tables, to allow faster data loads. 
* You can create foreign key constraints with NOCHECK to document the relationships; but don’t enforce them. 
* Ensure data integrity though Transform Lookups, or perform the data integrity checks at the source of the data. 


Write effective queries for partition elimination 
* Whenever possible, place a query predicate (WHERE condition) directly on the partitioning key (Date dimension key) of the fact table.

Use Sliding Window technique to maintain data 
* Maintain a rolling time window for online access to the fact tables. Load newest data, unload oldest data. 
* Always keep empty partitions at both ends of the partition range to guarantee that the partition split (before loading new data) and partition merge (after unloading old data) do not incur any data movement. 
* Avoid split or merge of populated partitions. Splitting or merging populated partitions can be extremely inefficient, as this may cause as much as 4 times more log generation, and also cause severe locking.
* Create the load staging table in the same filegroup as the partition you are loading. 
* Create the unload staging table in the same filegroup as the partition you are deleteing. 
* It is fastest to load newest full partition at one time, but only possible when partition size is equal to the data load frequency (for example, you have one partition per day, and you load data once per day). 
* If the partition size doesn't match the data load frequency, incrementally load the latest partition. • 
* Various options for loading bulk data into a partitioned table are discussed in the whitepaper • http://www.microsoft.com/technet/prodtechnol/sql/be stpractice/loading_bulk_data_partitioned_table.mspx. 
*  Always unload one partition at a time. 



数据同步
* full extraction - all data (usually dimension tables)
* incremental extraction - only data changed from last run (fast tables)
* how to determine data that has changed
  * Timestamp - Last updated
  * change data capture (CDC)
  * Partitioning by date
  * Triggers on tables
  * MERGE SQL Statement
  * Column DEFAULT value populated with date
* Online extraction - data from source
  * Replication
  * database snapshot
  * availability groups
* Offline extraction - data from flat file

ETL vs ELT 
* Extract, Transform, and Load (ETL) 
  * Transform while hitting source system 
  * No staging tables 
  * Processing done by ETL tools (SSIS) 
* Extract, Load, Transform (ELT) 
  * Uses staging tables 
  * Processing done by target database engine (SSIS: Execute T-SQL Statement task instead of Data Flow Transform tasks) 
  * Use for big volumes of data 
  * Use when source and target databases are the same 
  * Use with the Analytics Platform System (APS) 
  
  Multiple Parallel processing MPP


Four Types of NoSQL Databases
* Key-Value Store
* Document-Based Store:Full Text Search Engines
* Column-Based Store: BigTable-style 
* Graph-Based Store


One of the most significant shortcomings of the Key-Value model is a poor applicability to cases that require processing of key ranges. Ordered Key-Value model overcomes this limitation and significantly improves aggregation capabilities.


* Relational modeling is typically driven by the structure of available data. The main design theme is “What answers do I have?”
* NoSQL data modeling is typically driven by application-specific access patterns, i.e. the types of queries to be supported. The main design theme is “What questions do I have?”
  * NoSQL data modeling often requires a deeper understanding of data structures and algorithms than relational database modeling does. In this article I describe several well-known data structures that are not specific for NoSQL, but are very useful in practical NoSQL modeling.
  * Data duplication and denormalization are first-class citizens.

In general, denormalization is helpful for the following trade-offs:
* Query data volume or IO per query VS total data volume.
* Processing complexity VS total data volume. 在分布式环境中，join操作显著低增加了处理复杂性和处理时间

 Entity Aggregation：嵌入式的数据或者嵌套的数据，比如数组、map等数据类型

All major genres of NoSQL provide soft schema capabilities in one way or another:
* Key-Value Stores and Graph Databases typically do not place constraints on values, so values can be comprised of arbitrary format.
* BigTable models support soft schema via a variable set of columns within a column family and a variable number of versions for one cell.
* Document databases are inherently schema-less, although some of them allow one to validate incoming data using a user-defined schema.


* Minimization of one-to-many relationships by means of nested entities and, consequently, reduction of joins.
* Masking of “technical” differences between business entities and modeling of heterogeneous business entities using one collection of documents or one table.


Application Side Joins。
Joins are rarely supported in NoSQL solutions.

Query time joins almost always mean a performance penalty, but in many cases one can avoid joins using Denormalization and Aggregates, i.e. embedding nested entities. 


Atomic Aggregates

 Enumerable Keys

 Dimensionality Reduction


Dimensionality Reduction is a technique that allows one to map multidimensional data to a Key-Value model or to other non-multidimensional models.


Traditional geographic information systems use some variation of a Quadtree or R- Tree for indexes.A Geohash uses a Z-like scan to fill 2D space and each move is encoded as 0 or 1 depending on direction.

Index Table

Composite Key Index

[Understanding NoSQL Data Modeling Technique](https://phoenixnap.com/kb/nosql-data-modeling)

NoSQL Data Modeling Techniques
* Conceptual techniques
  * Denormalization 反范式
  * Aggregates 聚合
  * Application Side Joins
* General modeling techniques
  * Enumerable Keys 可枚举的键
  * Dimensionality Reduction.
* Hierarchy modeling techniques
  * Tree Aggregation
  * Adjacency Lists.
  * Materialized Paths
  * Nested Sets.
  * Nested Documents Flattening: Numbered Field Names
  * Nested Documents Flattening: Proximity Queries. 
  * Batch Graph Processing. 

  https://zhuanlan.zhihu.com/p/443564318


[Scaling GIS Data in Non-relational Data Stores](Scaling GIS Data in Non-relational Data Stores)


At the conceptual level, the multidimensional modelling gave birth to the concepts of fact and dimension. The most popular models used to design data warehouses are the star, snowflake, and constellation schemas . These models are then converted to the logical models which depend on the storage mode that will be adapted at the physical level . Classically, the mapping from the conceptual to the logical model is made according to three approaches; ROLAP (Relational-OLAP), MOLAP (Multidimensional-OLAP) and HOLAP (Hybrid-OLAP)


[Data Modeling Guidelines for NoSQL Document-Store Databases](https://thesai.org/Downloads/Volume9No10/Paper_66-Data_Modeling_Guidelines.pdf)

One of the most successful implementation of OLAP systems uses relational databases (R-OLAP implementations). 
* Each dimension is a table that uses the same name. Table attributes are derived from attributes of the dimension (called parameters and weak attributes). The root parameter is the primary key.
* Each fact is a table that uses the same name, with attributes derived from 1) fact attributes (called measures) and 2) the root parameter of each associated dimension. Attributes derived from root parameters are foreign keys linking each dimension table to the fact table and form a compound primary key of the table.


Some of these questions are (i) how to model one-to-N relationships in document databases, (ii) how to know when to reference instead of embedding a document, and (iii) whether document databases allow Entity Relationship modeling at all. 


NoSQL relation- ship modeling
* embedding: Characteristically, embedding provides better read performance when retrieving data from document- store databases. However, when writing data to database, it can be exceedingly slower, unlike refer- encing which uses the concept of writing data hori- zontally into smaller files.
* referencing: Typically referencing provides better write perfor- mance. However reading data may require more round trips to the server.
* bucketing: Bucketing enhances data retrieval by partitioning document with large contents into smaller affordable sizes.
* general: Normalizing data may help to save some space, but with the current advancement of technology, space is not a problem anymore.

Finally, understand the data access patterns, the nature of the data to be used in the application, the rate of updates on a particular field, and the cardinality re- lationships between entities. Such information shapes the design and modeling structure of document-store databases.

* Gl Embed sub-documents unless forced otherwise
* G2 Use array concept when embedding
* G3 Define array upper bound in parent document
* G4 Embed records which are managed together
* G5 Embed dependent documents
* G6 Embed one-to-one relationships
* G7 Group data with same volatility
* G8 Two-way embedding is preferred when N size is close to the M size in N:M relationship
* G9 One-way embedding is preferred if there’s hug gap in size between N to M
* G10 Reference highly volatile document
* G11 Reference standalone entities
* G12 Use array of references for the many side of the relationship
* G13 Parent referencing is recommended for large quantity of entities
* G14 Do not embed sub-documents if they are many
* G15 Index all documents for better performance
* G16 Combine embedding and referencing if necessary
* G17 Bucket documents with large content
* G18 Denormalize document when read write frequency is very low
* G19  Denormalize two connected documents for semi-combined re- trieval
* G20 Use tags implementation style for data transfer
* G21 Use directory hierarchies if security is a priority
* G22 Use document collections implementation style
* G23 Use Non-visible metadata for data transfer between nodes or server


Traditional Model – “Schema on Write”


Relational model vs Aggregate model

Big data Model: Schema on read.  With the Big Data and NoSQL paradigm, “Schema-on-Read” means you do not need to know how you will use your data when you are storing it. 




https://www.slideshare.net/fabiofumarola1/data-modeling-for-nosql-12

https://www.slideshare.net/fabiofumarola1/6-data-modeling-for-nosql-22

Apache HAWQ



lakehouse

Parquet





大数据（Big Data）包括两个部分
* 大数据存储，例如HBase，Cassandra等
* 大数据处理，例如Yarn和Flink等。
不同于MySQL这类关系型数据，大数据存储主要面向于日志型数据，这类数据的操作特点是多读、少写和不改，也就是数据一旦被存储，就不会被更改或者更新，从而无需复杂的事务机制。因此，大数据存储系统往往支持横向扩展，而放弃分布式事务。

类似地，大数据处理系统为了实现横向扩展能力，而放弃了复杂的处理计算，通常仅仅支持具有良好并行（Embarrassingly Parallel）能力的计算，例如SUM、MAX和MAP这类能够轻易分而治之的计算。对于一些复杂的处理，需要根据特定的应用需求和处理模式进行定制开发，通常并不具有良好地可扩展性。

与传统的基于数理统计的数据分析相比，大数据处理具有如下两个特点：
1）处理全量或者海量数据。在传统统计分析中，基于合理设计的采样，仅仅需要处理一小部分数据，就能够获得所需要的结论，而大数据分析往往要求处理海量的数据，甚至全量数据。
2）重视小概率的事件。在传统统计分析中，重视大概率事件，忽略了那些小概率事件或者因素。虽然单类事件或者因素的概率很小，但是这些小概率事件或者因素却很多，即存在长尾分布（Long-Tailed Distribution），而大数据处理非常适合这类场景，从大概率事件到小概率事件都能够处理。
因此，传统的统计分析和大数据处理往往针对于不同的需求和场景，不是相互替代，而是相互补充的关系。例如，对于收视率调查，传统的统计分析就能够非常完美的解决，而不需要大数据处理，但是如果需要向用户个性化的推荐不同的视频内容，那么往往需要大数据处理的支持。



No data, No Truth

No Analytic, No understanding

No Programming, No Cognition

数据分析在实际系统应用的几个阶段
* 支持分析
* 辅助决策
* 协助操作
* 自动处理

数据分析的三个方面
* 数学基础
* 技术实现
* 业务解释


人类知识<-->机器规则
* 将人类已有的知识应用到机器处理规则
* 从机器学得的规则提炼和总结为人类知识

系统的输入与输出
* 输入：可能的各种相关数据
* 输出：统计报表、决策建议和控制动作

统计学方法与数据分析

## Streaming Process

A. G. Psaltis. Streaming Data: Understanding the real-time pipeline. Manning Publications Co. 2017

![The streaming data architectural blueprint](pics/TheStreamingDataArchitecturalBlueprint.JPG)




|Classification  | Example |Latency measured in |Tolerance for delay|
| :------------ | :------------ | :------------ | :------------| 
|Hard |Pacemaker, anti-lock brakes |Microseconds–milliseconds |None—total system failure, potential loss of life|
|Soft |	Airline reservation system,online stock quotes, VoIP (Skype) |	Milliseconds–seconds |Low—no system failure, no life at risk|  
|Near |Skype video, home automation |Seconds–minutes| High—no system failure,no life at risk |


 The interaction patterns fall into one of the following categories:
* Request/response pattern
    * Basic request/response pattern.Three common strategies can overcome this limitation: one on the client side, one
on the service side, and one a combination of the two.
    * Client making asynchronous request to the service: half-async pattern
    * Service-side half-async pattern
    * Service async request/response pattern：full-async
* Publish/subscribe pattern
* One-way pattern: “fire and forget” message pattern
* Request/acknowledge pattern
* Stream pattern

The two primary approaches to implementing fault tolerance, checkpointing and logging, are designed to protect against data loss and enable speedy recovery of the crashed node.

Numerous checkpoint-based protocols are available to choose from in the literature, but when you boil it down, the following two
characteristics can be found in all of them:
* Global snapshot—The protocols require that a snapshot of the global state of the whole system be regularly saved to storage somewhere, not merely the state of the collection tier.
* Potential for data loss—The protocols only ensure that the system is recoverable up to the most recent recorded global state; any messages that were processed and generated afterward are lost.

Part of the complexity of checkpointing that’s eliminated is the global snapshot, and therefore the management and generation
of the global state. In the end, the goals of the logging technique manifest themselves in the basic idea that underpins all of the logging techniques: if a message can be replayed, then the system can reach a global consistent state without the need for a global snapshot.


Implementing a logging protocol frees us from worrying about maintaining global state, enabling us to focus on how to add
fault tolerance to the collection tier. To do this we’re going to discuss two classic techniques, receiver-based message logging (RBML) and sender-based message logging (SBML), and an emerging technique called hybrid message logging (HML).



## Python

A programming paradigm is a style, or “way” of programming. Major programming
paradigms are,
* Imperative
* Logical
* Functional
* Object-Oriented



```
import os
if 'PYSPARK_SUBMIT_ARGS' in os.environ:
    del os.environ['PYSPARK_SUBMIT_ARGS']

from pyspark import SparkContext, SparkConf
import random

sc_conf = SparkConf()
sc_conf.setAppName("Pi")
sc_conf.setMaster('local')
sc_conf.set('spark.executor.memory', '1g')
sc_conf.set('spark.executor.cores', '8')
sc_conf.set('spark.cores.max', '10')
sc_conf.set('spark.logConf', True)

sc =  SparkContext(conf=sc_conf)

num_samples = 100000000
def inside(p):     
  x, y = random.random(), random.random()
  return x*x + y*y < 1
count = sc.parallelize(range(0, num_samples)).filter(inside).count()
pi = 4 * count / num_samples
print(pi)
sc.stop()
```



```
from cassandra.cluster import Cluster
from cassandra.policies import DCAwareRoundRobinPolicy
from cassandra.cluster import EXEC_PROFILE_DEFAULT
from cassandra.cluster import ExecutionProfile

profile = ExecutionProfile(request_timeout=3000)
cluster = Cluster(contact_points=['192.168.*.*','192.168.*.*'],\
                  execution_profiles={EXEC_PROFILE_DEFAULT: profile})
session = cluster.connect()
session.set_keyspace('revenue_report')
rows = session.execute("SELECT date, SUM(revenue)\
                        FROM * \
                        WHERE date>'2019-02-27'\
                        GROUP BY date ALLOW FILTERING ")
for row in rows :
    print(row[0], " ",row[1])
cluster.shutdown()
```

```

    easy_install mysql-python (mix os)
    pip install mysql-python (mix os/ python 2)
    pip install mysqlclient (mix os/ python 3)
    apt-get install python-mysqldb (Linux Ubuntu, ...)
    cd /usr/ports/databases/py-MySQLdb && make install clean (FreeBSD)
    yum install MySQL-python (Linux Fedora, CentOS ...)

```

[Apache Superset](https://superset.apache.org/docs/installation/installing-superset-using-docker-compose)
