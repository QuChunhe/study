
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


  Log Structured-Merge Tree（日志结构合并树）