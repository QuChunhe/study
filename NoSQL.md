

如下三者要相互匹配
* schema设计
* 数据存储和索引方式
* 数据访问模式


[Database index](https://en.wikipedia.org/wiki/Database_index#Types_of_indexes)

实现亚线性查找，从而提高性能。需要在多个目标之间进行折中
* 数据查找性能
* 索引更新性能
* 索引存储大小

索引的类型
* Bitmap index
* Dense index
* Sparse index
* Sparse index
* Primary index
* Hash index


# InfluxDB

https://github.com/influxdata/influxdb


https://jasper-zhang1.gitbooks.io/influxdb/content/Write_protocols/line_protocol.html

概念
* database	
* field set
* field key	
* field value	
* measurement	
* point
* retention policy	
* series	
* tag key
* tag set	
* tag value	
* timestamp

每组field key和field value的集合组成了field set。


field是InfluxDB数据结构所必需的一部分——在InfluxDB中不能没有field。还要注意，field是没有索引的。如果使用field value作为过滤条件来查询，则必须扫描其他条件匹配后的所有值。因此，这些查询相对于tag上的查询（下文会介绍tag的查询）性能会低很多。


tag由tag key和tag value组成。tag key和tag value都作为字符串存储，并记录在元数据中。


tag不是必需的字段，但是在你的数据中使用tag总是大有裨益，因为不同于field， tag是索引起来的。这意味着对tag的查询更快，tag是存储常用元数据的最佳选择。

measurement作为tag，fields和time列的容器，measurement的名字是存储在相关fields数据的描述。 measurement的名字是字符串，对于一些SQL用户，measurement在概念上类似于表。

在InfluxDB中，series是共同retention policy，measurement和tag set的集合。

point就是具有相同timestamp的相同series的field集合。 每个点由其series和timestamp唯一标识。

schema

数据在InfluxDB里面怎么组织。InfluxDB的schema的基础是database，retention policy，series，measurement，tag key，tag value以及field keys。


server

一个运行InfluxDB的服务器，可以使虚拟机也可以是物理机。每个server上应该只有一个InfluxDB的进程。

shard

shard包含实际的编码和压缩数据，并由磁盘上的TSM文件表示。 每个shard都属于唯一的一个shard group。多个shard可能存在于单个shard group中。每个shard包含一组特定的series。给定shard group中的给定series上的所有点将存储在磁盘上的相同shard（TSM文件）中。

shard duration

shard duration决定了每个shard group跨越多少时间。具体间隔由retention policy中的SHARD DURATION决定。


tsm(Time Structured Merge tree)


wal(Write Ahead Log)

最近写的点数的临时缓存。为了减少访问永久存储文件的频率，InfluxDB将最新的数据点缓冲进WAL中，直到其总大小或时间触发然后flush到长久的存储空间。这样可以有效地将写入batch处理到TSM中。

可以查询WAL中的点，并且系统重启后仍然保留。在进程开始时，在系统接受新的写入之前，WAL中的所有点都必须flushed。



一般来说，你的查询可以指引你哪些数据放在tag中，哪些放在field中。
* 把你经常查询的字段作为tag
* 如果你要对其使用GROUP BY()，也要放在tag中
* 如果你要对其使用InfluxQL函数，则将其放到field中
* 如果你需要存储的值不是字符串，则需要放到field中，因为tag value只能是字符串


TLV协议

ASN.1是一种ISO/ITU-T 标准。其中一种编码BER（Basic Encoding Rules）简单好用，它使用三元组编码，简称TLV编码。
它是由数据的类型Tag（T），数据的长度Length（L），数据的值Value（V）构成的一组数据报文。TLV是基于二进制编码的，将数据以（T -L- V）的形式编码为字节数组，即TLV是字节流的数据传输协议。它规定了一帧数据的首个字节或几个字节来表示数据类型，紧接着一个或几个字节表示数据长度，最后是数据的内容。


```
SHOW DATABASES
SHOW RETENTION POLICIES
SHOW SERIES
SHOW MEASUREMENTS
SHOW TAG KEYS
SHOW TAG VALUES
SHOW FIELD KEYS
```





# Cassandra

[Cassandra集群优化与运维](https://www.jianshu.com/p/5bacb06e334b)


[CQL COPY](https://docs.datastax.com/en/cql/3.3/cql/cql_reference/cqlshCopy.html?hl=copy)

[Data Types](http://cassandra.apache.org/doc/latest/cql/types.html)


```
nodetool help

#Rebuild data by streaming from other nodes (similarly to bootstrap)
nodetool rebuild 

#Repair one or more tables
nodetool repair

```
/usr/local/etc/influxdb2



```
influx config create  -n local-config  -u http://127.0.0.1:8086 -o local-test -t ""


influx setup --skip-verify --bucket sandbox --org local-test --username administrator --password quchunhe --retention 0 --token ""
```

[Adding nodes to an existing cluster](https://docs.datastax.com/en/archived/cassandra/3.0/cassandra/operations/opsAddNodeToCluster.html)

[Changing the IP Address of a Cassandra Node](https://www.eventbrite.com/engineering/changing-the-ip-address-of-a-cassandra-node-with-auto_bootstrapfalse/)

[Updating the replication factor](https://docs.datastax.com/en/archived/cql/3.3/cql/cql_using/useUpdateKeyspaceRF.html)

## Book
###### Expert Apache Cassandra Adminitration, Apress, 2018.

[p100]  
  Data modeling in a relational database is driven entirely by data. You can also say that
relational data modeling is table-driven. Normalization theory rules the roost, and this
theory requires that you not duplicate data.  
  Queries and not data drive Cassandra’s data modeling methodology. This means that
you organize your data based on the queries you expect that data to serve. You design
your queries first and create your tables to satisfy those queries. You consider data
duplication as quite normal, as a side effect of nesting data.  

[p105]  
Cassandra Data Modeling Rules
* Spreading Data Evenly Across the Cluster
* Minimizing the Number of Partitions to Be Read
   
[p107]  
Modeling Around Queries and Not Around Relations
* Find out the queries the database must support
* Create appropriate tables.
   
[p114]  
  In a multiple partition batch operation, the coordinator node can turn out to be a bottleneck during a batch operation. The higher the number of partitions in a batch operation, the higher the latency due to batching.
   
[p145]   
  Write operations that use only a single partition are fine performance-wise.
   
[p146]   

  Even in cases with multiple partitions, if the operations involve only small inserts or updates, you’ll be fine with batching those operations to ensure consistency.

[p151]  
  It’s a good idea to have a separate keyspace per application.


[p156]  
  DataStax recommends that you use a small number of seeds, such as three nodes per datacenter. You should specify the same list of nodes
  for all nodes in a cluster. If your cluster has multiple datacenters, include at least one node from each datacenter as seed providers.

[p169]  
  DataStax recommends that you use the parallel and partitioner range options during a repair wherever it’s possible to do so.
```
$nodetool repair -pr hosts 10.2.2.30 10.2.2.31
```

[170] 
  Ideally, you should run incremental repairs every day and a full repair less frequently, like every month, unless you believe you need to do it more often.

[p183]  
  Tip The Murmur3Partitioner is 3-5 times faster in performance than the RandomPartitioner.

[185]  
  The choice of a snitch affects where Cassandra places replicas. Thepurpose of a snitch is to route requests efficiently and to distribute replicas evenly.  
DataStax recommends GossipingPropertyFileSnitch for production usage.


[190]  
  A keyspace is a logical structure where Cassandra stores not only table data, but also all other entities that you create for an application, such as materialized views, functions, aggregates, and UDTs.

[199]
  By default, the replication factor for the system-auth keyspace is set to 1. DataStax recommends that you set the replication factor for the system-auth tablespace to the number of nodes in each of the datacenters. However, you can set the replication factor for this keyspace to 5 or 7, which offers plenty of redundancy.

[201]  
  Note A primary key consists of two things: the first column or columns is the mandatory partition key, followed by one or more clustering columns.

[202]  
  Here’s what the two parts mean:
* Cassandra uses the first part of the definition of a primary key, the partition key, to distribute the data in the table across the cluster’s nodes. The partition key determines which node will store a specific row of the table. A compound partition key can split the data to store related data on separate partitions.
* The database uses the second part of the key definition, called the clustering key or clustering column (or columns), to order or sort the data within the partition.

[203]  
  Note A partition key groups rows in the same replica set. The clustering columns dictate how rows are stored in the replica.

[209]   
  You set the gc_grace_seconds property when creating a table. This property specifies the number of seconds after Cassandra marks data with a tombstone before the data becomes eligible for garbage collection.   

  a table for which you’ve configured the default_time_to_live property.


[305]  
  The nodetool rebuild command is useful when you’re adding a datacenter to your cluster. You can rebuild a single keyspace at a time or specify multiple keyspaces, each separated by a comma.

[306]   
  You don’t have to manually clean up after every such change in a cluster. However, if for any reason you wish to reclaim disk space faster, you can run the nodetool cleanup command.

[326]   
  In situations such as when you’re getting ready to upgrade Cassandra, you want to ensure that you flush all memtables to disk, into the SSTables. You run the nodetool drain command to flush memtables to SSTables on disk.

[341]  
  Key nodetool commands that you’ll often use for checking a cluster’s health are the following:
* nodetool status
* nodetool info
*nodetool tpstats

 [337]    
   The nodetool proxyhistograms command shows the network statistics in a cluster.
 
 [338]   
  Run the nodetool tablestats (formerly nodetool cfstats) command to get statistics about one or more tables.  
You run the nodetool decommission command to make a node send all its data to the next node in the ring. Decommissioning a node is the opposite of bootstrapping a node.  


[379]  
  You can set the bloom_filter_fp_chance attribute for a table to a value between 0 and 1. As you go from 0 to 1, you use less memory. A value of 0 means you set the largest value for the Bloom filter and use the highest amount of memory. Setting it to 1 means that you’ve disabled Bloom filters.

[422]  
  There are two good nodetool commands that help you identify performance issues in a cluster: nodetool proxyhistograms and nodetool tablehistograms. Both commands present performance statistics captured by the database in the form of histograms, hence
the command names.




Alex Petrov，Database Internals： A Deep Dive into How Distributed Data Systems Work



# TiDB

```shell
git clone https://github.com/pingcap/tidb-docker-compose.git

cd tidb-docker-compose 

docker-compose pull

docker-compose up -d

mysql -h127.0.0.1 -P 4000 -u root

http://localhost:3000

admin  admin

```


```sql
ALTER TABLE table_name SET TIFLASH REPLICA count;

```
count 表示副本数，0 表示删除。

```
SELECT * FROM information_schema.tiflash_replica WHERE TABLE_SCHEMA = '<db_name>' and TABLE_NAME = '<table_name>'
```
* VAILABLE 字段表示该表的 TiFlash 副本是否可用。1 代表可用，0 代表不可用。副本状态为可用之后就不再改变，如果通过 DDL 命令修改副本数则会重新计算同步进度。
* PROGRESS 字段代表同步进度，在 0.0~1.0 之间，1 代表至少 1 个副本已经完成同步
  

[Large-scale Incremental Processing Using Distributed Transactions and Notifications](https://storage.googleapis.com/pub-tools-public-publication-data/pdf/36726.pdf)
 # RocksDB
 
[RocksDB](https://rocksdb.org) 


* TiDB  
* TiKV : PRF(gRPC), Transaction, MVCC, Raft, RocksDB
* PD（Placement Driver）
   * Meta data management
   * Load balance management

Join Operator selection
* Hash join
* index lookup join
* sort-merge join

ACID Transaction
* Based on Google Percolator
* 'Almost' decentralizeed 2-phase commit

Fractal Tree: B-Tree



Log Structured-Merge Tree（日志结构合并树）
1. MemTable, Active MemTable -> write 
2. Immutable MemTable: ReadOnly MemTable -> read
3. SSTable(Sorted String Table): LSM-> compaction

Three Basic Constructs of RocksDB 
* Memtable 
  * in-memory data structure 
  * A buffer, temporarily host the incoming writes 
* Logfile 
  * Sequentially-written file 
  * On storage
* SSTable(=SSTfile) 
  * Sorted Static Table on storage 
  * A file which contains a set of arbitrary, sorted key-value pairs inside 
  * Organized in levels 
  * Immutable in its life time 
  * sorted data -> to facilitate easy lookup of keys 
  * Storage of the entire database


MySQL binlog format

Mapping table data to kv store

Secondary index

coprocessor

Multi-Region/Geo-Distributed

Compact操作是十分关键的操作，否则SSTable数量会不断膨胀。在Compact策略上，主要介绍两种基本策略：size-tiered和leveled。
1. 读放大(Read Amplification):读取数据时实际读取的数据量大于真正的数据量。例如在LSM树中需要先在MemTable查看当前key是否存在，不存在继续从SSTable中寻找。
2. 写放大(Write Amplification):写入数据时实际写入的数据量大于真正的数据量。例如在LSM树中写入时可能触发Compact操作，导致实际写入的数据量远大于该key的数据量。
3. 空间放大(Space Amplification):数据实际占用的磁盘空间比数据的真正大小更多。上面提到的冗余存储，对于一个key来说，只有最新的那条记录是有效的，而之前的记录都是可以被清理回收的。

* Memtable, 64MB
* Level 0, 256MB
* Level 1, 512MB
* Level 2, 5GB
* Level 3, 50GB

Writes 
* Foreground: 
  * Writes go to memtable (skiplist) + write-ahead log
* Background: 
  * When memtable is full, we flush to Level 0 
  * When a level is full, we run compaction

Reads 
* Point queries  
  * Bloom filters reduce reads from storage •  
  * Usually only 1 read IO 
* Range scans 
  * Bloom filters don’t help 
  * Depends on amount of memory, 1-2 IO

TiDB 以 Region 为单位对数据进行切分，每个 Region 有大小限制（默认为 96MB）。Region 的切分方式是范围切分。每个 Region 会有多个副本，每一组副本，称为一个 Raft Group。每个 Raft Group 中由 Leader 负责执行这块数据的读和写（TiDB 即将支持 Follower-Read）。Leader 会自动地被 PD 组件均匀调度在不同的物理节点上，以均分读写压力。

对于 Index，TiDB 不止需要支持 Primary Index，还需要支持 Secondary Index。

查询的时候有两种模式，一种是点查.另一种是 Range 查询.

TiDB 对每个表分配一个 TableID，每一个索引都会分配一个 IndexID，每一行分配一个 RowID（如果表有整数型的 Primary Key，那么会用 Primary Key 的值当做 RowID），其中 TableID 在整个集群内唯一，IndexID/RowID 在表内唯一，这些 ID 都是 int64 类型

[三篇文章了解 TiDB 技术内幕 - 说计算](https://pingcap.com/zh/blog/tidb-internal-2)

[三篇文章了解 TiDB 技术内幕 - 说存储](https://pingcap.com/zh/blog/tidb-internal-1)

[为什么要进行调度](https://pingcap.com/zh/blog/tidb-internal-3)

无论是NoSQL，还是MySQL都需要使得如下三者相互匹配
* Schema设计，包括数据拆分、主键/索引/行键/键的设计以及partition/partition的选择和字段的定义
* 存储方式，数据库采用何种方式存储数据和检索数据
* 查询模式，经常以哪些字段为参数访问和检索数据
充分利用数据存储和检索方式，避免不必要的数据读取和传输。


TiDB在技术上的三个优点
* 支持MySQL SQL，通过MySQL Client就能够连接和使用TiDB，从而减小了学习和迁移成本。
* 兼容事务和分析两大类处理场景。TiDB 100%地兼容MySQL OLTP场景，支持80%的OLAP场景， HTAP 数据库
* 具有横向扩展能力，解决了单机容量扩展的问题

在商业模式上，开源，又有专业团队来支撑。

TiDB在逻辑上支持以表方式存储数据和关系模型，在底层采用KV结构（RockDB）存储表数据。将表数据映射到KV存储方式，

Key-Value pair 按照 Key 的二进制顺序有序，也就是我们可以 Seek 到某一个 Key 的位置，然后不断的调用 Next 方法以递增的顺序获取比这个 Key 大的 Key-Value。RocksDB 是一个非常优秀的开源的单机存储引擎。
另一种是分 Range，某一段连续的 Key 都保存在一个存储节点上，将整个 Key-Value 空间分成很多段，每一段是一系列连续的 Key，我们将每一段叫做一个 Region，并且我们会尽量保持每个 Region 中保存的数据不超过一定的大小(这个大小可以配置，目前默认是 96mb)。每一个 Region 都可以用 StartKey 到 EndKey 这样一个左闭右开区间来描述。TiKV 是以 Region 为单位做数据的复制，也就是一个 Region 的数据会保存多个副本，我们将每一个副本叫做一个 Replica。Replica 之间是通过 Raft 来保持数据的一致。每个 Region 负责存储一个 Key Range（从 StartKey 到 EndKey 的左闭右开区间）的数据，每个 TiKV 节点会负责多个 Region

对于 Index，TiDB 不止需要支持 Primary Index，还需要支持 Secondary Index

* TiKV ：采用了行式存储，更适合 TP 类型的业务；负责存储数据，从外部看 TiKV 是一个分布式的提供事务的 Key-Value 存储引擎。存储数据的基本单位是 Region，每个 Region 负责存储一个 Key Range（从 StartKey 到 EndKey 的左闭右开区间）的数据，每个 TiKV 节点会负责多个 Region。
* TiFlash：TiFlash 采用列式存储，擅长 AP 类型的业务，主要的功能是为分析型的场景加速


上述所有编码规则中的 tablePrefix、recordPrefixSep 和 indexPrefixSep 都是字符串常量
    tablePrefix     = []byte{'t'}
    recordPrefixSep = []byte{'r'}
    indexPrefixSep  = []byte{'i'}  

 MaxInt64

    Key:   tablePrefix{TableID}_recordPrefixSep{RowID}
    Value: [col1, col2, col3, col4]


其中
* TiDB 会为每个表分配一个表 ID，用 TableID 表示
* TiDB 会为表中每行数据分配一个行 ID，用 RowID 表示。行 ID 也是一个整数，在表内唯一。对于行 ID，TiDB 做了一个小优化，如果某个表有整数型的主键，TiDB 会使用主键的值当做这一行数据的行 ID。
  

对于主键和唯一索引，需要根据键值快速定位到对应的 RowID，因此，按照如下规则编码成 (Key, Value) 键值对：
    Key:   tablePrefix{tableID}_indexPrefixSep{indexID}_indexedColumnsValue
    Value: RowID

对于不需要满足唯一性约束的普通二级索引，一个键值可能对应多行，需要根据键值范围查询对应的 RowID。

    Key:   tablePrefix{TableID}_indexPrefixSep{IndexID}_indexedColumnsValue_{RowID}
    Value: null

计算应该需要尽量靠近存储节点，以避免大量的 RPC 调用。首先，SQL 中的谓词条件 name = "TiDB" 应被下推到存储节点进行计算，这样只需要返回有效的行，避免无意义的网络传输。然后，聚合函数 Count(*) 也可以被下推到存储节点，进行预聚合，每个节点只需要返回一个 Count(*) 的结果即可，再由 SQL 层将各个节点返回的 Count(*) 的结果累加求和


开启 Region Merge。与 Region Split 相反，Region Merge 是通过调度把相邻的小 Region 合并的过程。在集群有删除数据或者进行过 Drop Table/Truncate Table 后，可以将那些小 Region 甚至空 Region 进行合并以减少资源的消耗。




Delta Tree 的架构设计充分参考了 B+ Tree 和 LSM Tree 的设计思想。从整体上看，Delta Tree 将表数据按照主键进行 range 分区，切分后的数据块称为 Segment；然后 Segment 内部则采用了类似 LSM Tree 的分层结构。

所以 Delta Tree 只需要固定的两层，即 Delta Layer 和 Stable Layer，分别对应 LSM Tree 的 L0 和 L1

[TiDB 的列式存储引擎是如何实现的？](https://zhuanlan.zhihu.com/p/164490310)

Table files are immutable 

 Other files are append-only 

 Universal Style Compaction

 [](http://www.kereno.com/rocksdb-rof.pdf)

 https://zhuanlan.zhihu.com/p/361390089

 https://blog.csdn.net/junior77/article/details/121809037

* TiKV, a row-based storage engine for TiDB Online Transactional Processing (OLTP), row-based storage engine
* TiFlash, a columnar storage engine for TiDB Online Analytical Processing (OLAP).columnar storage engine


https://docs.pingcap.com/tidb/stable/tiflash-configuration

https://docs.pingcap.com/zh/tidb/stable/tidb-storage

Some database management systems refer to clustered indexes as index-organized tables (IOT).


Currently, tables containing primary keys in TiDB are divided into the following two categories:
* NONCLUSTERED: 
* CLUSTERED



```sql
CREATE TABLE t (a BIGINT, b VARCHAR(255), PRIMARY KEY(a, b) CLUSTERED);
CREATE TABLE t (a BIGINT, b VARCHAR(255), PRIMARY KEY(a, b) NONCLUSTERED);
```

Note that keywords KEY and PRIMARY KEY have the same meaning in the column definition.


In v5.0, using the clustered index feature together with TiDB Binlog is not supported. After TiDB Binlog is enabled, TiDB only allows creating a single integer column as the clustered index of a primary key. 

In v5.0, using the clustered index feature together with TiDB Binlog is not supported. After TiDB Binlog is enabled, TiDB only allows creating a single integer column as the clustered index of a primary key. 

json
```sql
CREATE TABLE city (
    id INT PRIMARY KEY,
    detail JSON,
    population INT AS (JSON_EXTRACT(detail, '$.population')),
    index index_name (population)
    );
INSERT INTO city (id,detail) VALUES (1, '{"name": "Beijing", "population": 100}');
SELECT id FROM city WHERE population >= 100;
```

https://docs.pingcap.com/tidb/stable/optimistic-transaction

```sql
CREATE TABLE quarterly_report_status (
    report_id INT NOT NULL,
    report_status VARCHAR(20) NOT NULL,
    report_updated TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
)

PARTITION BY RANGE ( UNIX_TIMESTAMP(report_updated) ) (
    PARTITION p0 VALUES LESS THAN ( UNIX_TIMESTAMP('2008-01-01 00:00:00') ),
    PARTITION p1 VALUES LESS THAN ( UNIX_TIMESTAMP('2008-04-01 00:00:00') ),
    PARTITION p2 VALUES LESS THAN ( UNIX_TIMESTAMP('2008-07-01 00:00:00') ),
    PARTITION p3 VALUES LESS THAN ( UNIX_TIMESTAMP('2008-10-01 00:00:00') ),
    PARTITION p4 VALUES LESS THAN ( UNIX_TIMESTAMP('2009-01-01 00:00:00') ),
    PARTITION p5 VALUES LESS THAN ( UNIX_TIMESTAMP('2009-04-01 00:00:00') ),
    PARTITION p6 VALUES LESS THAN ( UNIX_TIMESTAMP('2009-07-01 00:00:00') ),
    PARTITION p7 VALUES LESS THAN ( UNIX_TIMESTAMP('2009-10-01 00:00:00') ),
    PARTITION p8 VALUES LESS THAN ( UNIX_TIMESTAMP('2010-01-01 00:00:00') ),
    PARTITION p9 VALUES LESS THAN (MAXVALUE)
);
```


```sql
set @@session.tidb_enable_list_partition = ON

CREATE TABLE employees_1 (
    id INT NOT NULL,
    fname VARCHAR(30),
    lname VARCHAR(30),
    hired DATE NOT NULL DEFAULT '1970-01-01',
    separated DATE DEFAULT '9999-12-31',
    job_code INT,
    store_id INT,
    city VARCHAR(15)
)
PARTITION BY LIST COLUMNS(city) (
    PARTITION pRegion_1 VALUES IN('LosAngeles', 'Seattle', 'Houston'),
    PARTITION pRegion_2 VALUES IN('Chicago', 'Columbus', 'Boston'),
    PARTITION pRegion_3 VALUES IN('NewYork', 'LongIsland', 'Baltimore'),
    PARTITION pRegion_4 VALUES IN('Atlanta', 'Raleigh', 'Cincinnati')
);
```


混合事务型和分析型处理的引擎，
基于行式存储，在执行读操作时，具有更高的性能
采用异步复制，以非阻塞方式写入TiKV。智能选择

https://docs.pingcap.com/tidb/stable/tune-tiflash-performance
```sql
set @@tidb_distsql_scan_concurrency = 80;
set @@tidb_allow_batch_cop = 1;
set @@tidb_opt_agg_push_down = 1;
set @@tidb_opt_distinct_agg_push_down = 1;
```

对于 OLAP 类型的 Query，往往需要较高的并发度。所以 TiDB 支持通过 System Variable 来调整查询并发度。
* tidb_distsql_scan_concurrency 在进行扫描数据的时候的并发度，这里包括扫描 Table 以及索引数据。
* tidb_index_lookup_size 如果是需要访问索引获取行 ID 之后再访问 Table 数据，那么每次会把一批行 ID 作为一次请求去访问 Table 数据，这个参数可以设置 Batch 的大小，较大的 Batch 会使得延迟增加，较小的 Batch 可能会造成更多的查询次数。这个参数的合适大小与查询涉及的数据量有关。一般不需要调整。
* tidb_index_lookup_concurrency 如果是需要访问索引获取行 ID 之后再访问 Table 数据，每次通过行 ID 获取数据时候的并发度通过这个参数调节。

https://docs.pingcap.com/tidb/stable/json-functions

如果有 Unique Key 并且业务端可以保证数据中没有冲突，可以在 Session 内打开这个开关：
```
SET @@session.tidb_skip_constraint_check=1;
```
另外为了提高写入性能，可以对 TiKV 的参数进行调优。 请特别注意这个参数：
```
[raftstore]
# 默认为 true，表示强制将数据刷到磁盘上。如果是非金融安全级别的业务场景，建议设置成 false，
# 以便获得更高的性能。
sync-log = true
```


Partition Pruning

TiDB supports several operators which make use of indexes to speed up query execution:
* IndexLookup
* IndexReader
* Point_Get and Batch_Point_Get
* IndexFullScan


https://book.tidb.io/session4/chapter8/add-index-internal.html

OLAP 类的查询通常具有以下几个特点：
* 每次查询读取大量的行，但是仅需要少量的列
* 宽表，即每个表包含着大量的列
* 查询通过一张或多张小表关联一张大表，并对大表上的列做聚合

https://book.tidb.io/session1/chapter7/sequence.html


配合源于 ClickHouse 的极致向量化计算引擎，更少的废指令，SIMD 加速


列存更新的主流设计是 Delta Main 方式，基本思想是，由于列存块本身更新消耗大，因此往往设计上使用缓冲层容纳新写入的数据。然后再逐渐和主列存区进行合并。

<<<<<<< HEAD
[TiDB In Action: based on 4.0](https://github.com/tidb-incubator/tidb-in-action)
=======
[tidb开发规范](https://developer.aliyun.com/article/834144)

[在阿里云上部署 TiDB 集群](https://docs.pingcap.com/zh/tidb-in-kubernetes/stable/deploy-on-alibaba-cloud)


# ClickHouse

两大类表引擎
* MergeTree家族：适合高负载任务，若干子引擎，支持复制和分区
* Log家族。

其中MergeTree作为 家族中最基础的表引擎，提供了主键索引、数据分区、数据副本和数 据采样等基本能力，而家族中其他的表引擎则在MergeTree的基础之 上各有所长。例如ReplacingMergeTree表引擎具有删除重复数据的 特性，而SummingMergeTree表引擎则会按照排序键自动聚合数 据。如果给合并树系列的表引擎加上Replicated前缀，又会得到一组 支持数据副本的表引擎，例如ReplicatedMergeTree、 ReplicatedReplacingMergeTree、 ReplicatedSummingMergeTree等


* partition:分区目录，余下各类数据文件(primary.idx、 [Column].mrk、[Column].bin等)
* columns.txt:列信息文件，使用明文格式存储。用于保存 此数据分区下的列字段信息
* count.txt:计数文件，使用明文格式存储。用于记录当前 数据分区目录下数据的总行数
* primary.idx:一级索引文件，使用二进制格式存储
* [Column].bin:数据文件，使用压缩格式存储，默认为 LZ4压缩格式，用于存储某一列的数据。
* [Column].mrk:列字段标记文件，使用二进制格式存储。 标记文件中保存了.bin文件中数据的偏移量信息。标记文件与稀疏索引 对齐，又与.bin文件一一对应，所以MergeTree通过标记文件建立了 primary.idx稀疏索引与.bin数据文件之间的映射关系。


   PartitionID_MinBlockNum_MaxBlockNum_Level

* MergeTree engine
* ReplacingMergeTree engine
* SummingMergeTree engine
* AggregatingMergeTree engine 
* CollapsingMergeTree engine 
* VersionedCollapsingMergeTree engine 
* ReplicatedMergeTree engine

基于Zookeeper支持数据复制，支持数据分区，基于主键排序和存储，支持数据抽样

在表中存储的数据被划分为颗粒（granule），在读取数据事，ClikHouse会读取颗粒中的全部数据。颗粒大小通过使用index_granularity and index_granularity_bytes来设定。也就是说，每个颗粒就是一个索引的粒度。ClickHouse提供了自适应粒度 大小的特性

ClickHouse使用稀疏索引，从而可以显著减小索引文件大小，使得系统能够将大表的全部索引加载到内存中。在每个分区中索引是在primary.idx文件中维护的。

MarkRange 在ClickHouse中是用于定义标记区间的对象。

```sql
CREATE TABLE [IF NOT EXISTS] [database_name.]table_name [ON CLUSTER cluster_name]
(
  column1 [datatype1] [DEFAULT|MATERIALIZED|ALIAS expr1] [TTL expr1],
  column2 [datatype2] [DEFAULT|MATERIALIZED|ALIAS expr2] [TTL expr2],
  ...
  ...
) ENGINE = MergeTree() [PARTITION BY expr] [ORDER BY expr]
[PRIMARY KEY expr] [SAMPLE BY expr]
[TTL expr]
[SETTINGS name=value, ...]  

```


Minimum time delay in seconds before repeating a merge with TTL.


ReplacingMergeTree:不期望出现重复数据，在合并操作中，基于在order by中指定的列，删除重复

```sql
ENGINE = ReplacingMergeTree(ver)
```
其中，ver是选填参数，会指定一个UInt*、Date或者DateTime 类型的字段作为版本号。这个参数决定了数据去重时所使用的算法。
* 如果没有设置ver版本号，则保留同一组重复数据中的最后一
行。
* 如果设置了ver版本号，则保留同一组重复数据中ver字段取值 最大的那一行。

```sql

OPTIMIZE TABLE mergetree_testing.replacingmergetree FINAL;
```

ReplacingMergeTree接受一个可选的参数，其确定替换重复行的逻辑，如果一行被这个参数指定，那么在出现重复数据时，会保留该列具有最大值的行。

SummingMergeTree接受一个可选的参数，其是列数组，基于所指定的列数组具有相同值的行进行累加，

```sql
ENGINE = SummingMergeTree((col1,col2,...))
```
其中，col1、col2为columns参数值，这是一个选填参数，用于 设置除主键外的其他数值类型字段，以指定被SUM汇总的列字段。如 若不填写此参数，则会将所有非主键的数值类型字段进行SUM汇总。

AggregatingMergeTree

因为SummingMergeTree与
AggregatingMergeTree的聚合都是根据ORDER BY进行的。由此可 以引出两点原因:主键与聚合的条件定义分离，为修改聚合条件留下 空间。

AggregatingMergeTree更为常见的应用方式是结合物化视图使 用，将它作为物化视图的表引擎。
```sql
CREATE MATERIALIZED VIEW mergetree_testing.aggregatingmergetree_mat_view ENGINE = AggregatingMergeTree()
ORDER BY (Name)
AS SELECT
Name,
avgState(toFloat64(Quantity)) as Quantity_Average, 
minState(toFloat64(Quantity)) as Quantity_Minimum,
maxState(toFloat64(Quantity)) as Quantity_Maximum
FROM mergetree_testing.mergetree GROUP BY Name;
```

CollapsingMergeTree:当数据需要持续变更，不得不频繁更新行。 sign 列的取值可以为1或者-1。1位状态行，-1位取消行，

CollapsingMergeTree就是一种通过以增代删的思路，支持行级 数据修改和删除的表引擎。它通过定义一个sign标记位字段，记录数 据行的状态。如果sign标记为1，则表示这是一行有效的数据;如果 sign标记为-1，则表示这行数据需要被删除。

VersionedCollapsing MergeTree
```sql
CREATE TABLE IF NOT EXISTS mergetree_testing.versionedcollapsingmergetree( ID String,
  Count UInt64,
  Sign Int8,
 
   Version UInt32)
ENGINE = VersionedCollapsingMergeTree(Sign, Version) ORDER BY (ID);
```


数据复制仅仅在MergeTree表引擎家族中支持
* ReplicatedMergeTree
* ReplicatedSummingMergeTree 
* ReplicatedReplacingMergeTree 
* ReplicatedAggregatingMergeTree 
* ReplicatedCollapsingMergeTree 
* ReplicatedVersionedCollapsingMergeTree 
* ReplicatedGraphiteMergeTree

 
MergeTree family engines are the most powerful and feature-rich engines in ClickHouse.

ReplacingMergeTree engine is useful when data deduplication based on the primary/sorting key is required.

SummingMergeTree engine is used to sum the numeric columns with the same primary/sorting key.

AggregatingMergeTree is used to store the aggregating states of the columns, which can be later used for getting aggregated values.

CollapsingMergeTree is useful when their records are continuously changing. The data deletion is based on the sign column.

VersionedCollapsingMergeTree is similar to but an additional version column is used for deleting the old records.


目前，MergeTree共支持4种跳数索引，分别是minmax、set、 ngrambf_v1和tokenbf_v1。一张数据表支持同时声明多个跳数索 引，
```sql
CREATE TABLE skip_test (
  ID String,
  URL String,
  Code String,
  EventTime Date,
  INDEX a ID TYPE minmax GRANULARITY 5,
  INDEX b(length(ID) * 8) TYPE **set**(2) GRANULARITY 5,
  INDEX c(ID，Code) TYPE ngrambf_v1(3, 256, 2, 0) GRANULARITY 5, INDEX d ID TYPE tokenbf_v1(256, 2, 0) GRANULARITY 5
) ENGINE = MergeTree()
```


```shell
clickhouse-client -h ch7.nauu.com --send_logs_level=trace <<< 'SELECT * FROM
   hits_v1' > /dev/null
```

通过ClickHouse提供的clickhouse-compressor工具，能够查 询某个.bin文件中压缩数据的统计信息



```sql
CREATE TABLE default.test ON CLUSTER mycluster_1
(
    `id` Int64,
    `ymd` Int64
)
ENGINE = ReplicatedMergeTree('/clickhouse/tables/replicated/{shard}/test', '{replica}')
PARTITION BY ymd
ORDER BY id
```



SSTables

存储和索引比较简洁
 * 存储：SSTable，采用partition，granule和columns.bin文件三个层次
 * 索引：主键/排序列的区间标记，采用primary.idx和[Column].mrk两级
自动实时汇总数据：基于物化试图和AggregatingMergeTree，在插入明细数据时汇总到特定维度（排序列）

合并机制问题：删除更新等操作合并时才会生效，随机写入和更新的性能非常糟糕，仅仅适合增量添加数据
分布式性能？：基于zookeeper实现数据复制。如何在分布式cluster环境提高读写性能？

# Hudi

Hudi经常被拿来跟Delta，Iceberg一起，并称为“数据湖三剑客”

[ApacheHudi](https://www.zhihu.com/column/ApacheHudi)


[分布式和存储的那些事](https://www.zhihu.com/column/distributed-storage)


Hudi的标志性功能——Upsert。

Upsert可以说是Hudi的招牌，正如上一节所说，Hudi最初的设计目标就是在hadoop上实现数据的update。于是这里的核心问题就是

如何在一个只能overwrite的文件系统上实现update操作？

，Hudi的定义是流式数据湖平台，它支持海量数据更新，内置表格式以及支持事务的储存，一系列列表服务包括Clean、Archive、Compaction、Clustering等，以及开箱即用的数据服务，以及本身自带的运维工具和指标监控，提供很好的运维能力。

* Merge on Read（MOR表）
* Transactional（事务）
* Incremental Query（增量查询


对于MOR表，Hudi支持3种query类型，分别是
* Snapshot Query
* Incremental Query
* Read Optimized Query
>>>>>>> 20ba7485168611e7d8b0a220265026768f06f53f
