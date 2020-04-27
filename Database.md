
## MySQL

### Index

[Clustered and Secondary Indexes](https://dev.mysql.com/doc/refman/5.7/en/innodb-index-types.html)

Every InnoDB table has a special index called the clustered index where the data for the rows is stored. Typically, the clustered index is synonymous with the primary key.

All indexes other than the clustered index are known as secondary indexes. In InnoDB, each record in a secondary index contains the primary key columns for the row, as well as the columns specified for the secondary index.


### Cluster

[Spider Server System Variables](https://mariadb.com/kb/en/library/spider-server-status-variables/)

```
SHOW SLAVE STATUS\G;
START SLAVE;
STOP SLAVE;

SHOW BINARY LOGS

SHOW BINLOG EVENTS

SHOW MASTER STATUS

SHOW SLAVE HOSTS 


```

```
 /usr/local/mariadb/bin/mysqlbinlog  --start-datetime='2018-07-26 09:50:00' --base64-output=decode-rows -v /var/mariadb/data/mysql-bin.000216 --result-file=binglog.sql



### Performance


OPTIMIZE [NO_WRITE_TO_BINLOG | LOCAL] TABLE tbl_name [, tbl_name] ... [WAIT n | NOWAIT]
```

show profile默认的是关闭的，但是会话级别可以开启这个功能。开启它可以让MySQL收集在执行语句的时候所使用的资源。
```
SET profiling = 1;

execute sql

SHOW PROFILES\G;
```

```
SHOW PROFILE [type [, type] ... ]
    [FOR QUERY n]
    [LIMIT row_count [OFFSET offset]]

type: {
    ALL
  | BLOCK IO
  | CONTEXT SWITCHES
  | CPU
  | IPC
  | MEMORY
  | PAGE FAULTS
  | SOURCE
  | SWAPS
}
```
The values of n correspond to the Query_ID values displayed by SHOW PROFILES.




[SHOW PROFILE Statement](https://dev.mysql.com/doc/refman/5.7/en/show-profile.html)

Profiling information is also available from the INFORMATION_SCHEMA PROFILING table. 

```
HOW PROFILE FOR QUERY 2;

SELECT STATE, FORMAT(DURATION, 6) AS DURATION
FROM INFORMATION_SCHEMA.PROFILING
WHERE QUERY_ID = 2 ORDER BY SEQ;
```

[The INFORMATION_SCHEMA PROFILING Table](https://dev.mysql.com/doc/refman/5.7/en/profiling-table.html)



### Lock

[MySQL介于普通读和锁定读的加锁方式](https://mp.weixin.qq.com/s?__biz=MzIxNTQ3NDMzMw==&mid=2247484352&idx=1&sn=799a109943108ce3ed139d0b684f18f8&chksm=97968a32a0e10324bd808b23ab376796f49c5998c6d917bf8f0073936cf1b128ac30742aebb8&mpshare=1&scene=1&srcid=01046CqxEFUnP5P2zo7hKda5&sharer_sharetime=1578110785863&sharer_shareid=fc937fe50a97e6c10553c542abe0a39b&exportkey=AW49gRrpesj66SITcN8Z3Fg%3D&pass_ticket=kOI4SUiiSQZgtNAcX5IS41mTJmr%2FciBGq3MXwztfKxT51U1FpE7lMYqAa9JxIFu2#rd)


[InnoDB Locking](https://dev.mysql.com/doc/refman/5.7/en/innodb-locking.html)


- A shared (S) lock permits the transaction that holds the lock to read a row.
- An exclusive (X) lock permits the transaction that holds the lock to update or delete a row

InnoDB supports multiple granularity locking which permits coexistence of row locks and table locks. For example, a statement such as LOCK TABLES ... WRITE takes an exclusive lock (an X lock) on the specified table. 

 Intention locks are table-level locks that indicate which type of lock (shared or exclusive) a transaction requires later for a row in a table. There are two types of intention locks:
- An intention shared lock (IS) indicates that a transaction intends to set a shared lock on individual rows in a table.
- An intention exclusive lock (IX) indicates that a transaction intends to set an exclusive lock on individual rows in a table. 

For example, SELECT ... LOCK IN SHARE MODE sets an IS lock, and SELECT ... FOR UPDATE sets an IX lock. 

Intention locks do not block anything except full table requests (for example, LOCK TABLES ... WRITE). The main purpose of intention locks is to show that someone is locking a row, or going to lock a row in the table. 

A record lock is a lock on an index record. 

A gap lock is a lock on a gap between index records, or a lock on the gap before the first or after the last index record.

Gap locks in InnoDB are “purely inhibitive”, which means that their only purpose is to prevent other transactions from inserting to the gap. Gap locks can co-exist. A gap lock taken by one transaction does not prevent another transaction from taking a gap lock on the same gap.


A next-key lock is a combination of a record lock on the index record and a gap lock on the gap before the index record.



[AUTO_INCREMENT Handling in InnoDB](https://dev.mysql.com/doc/refman/5.7/en/innodb-locking.html)



[划重点！你还在困惑MySQL中的"锁"吗？](https://mp.weixin.qq.com/s?__biz=MzI3NDA4OTk1OQ==&mid=2649903745&idx=1&sn=7cd6111a400186c6c7d4806f4277ceca&chksm=f31fa009c468291f683d6ac1de0a0a5a767e629a9da47b6f9c1f675a4c5a3835b48568b48fe6&mpshare=1&scene=1&srcid=0427WrpaKOREnrzqtACZ1Lwv&sharer_sharetime=1587972414462&sharer_shareid=fc937fe50a97e6c10553c542abe0a39b&exportkey=Af3svVFvaH5D4v6WMzjSpw8%3D&pass_ticket=dQPTuWQMQvIImHS%2Frl41EVuA7Uh8PT6VumsOGO8w14tdeRR2aOM7wmGBoT4lfOSK#rd)

* 乐观锁(optimistic locking)
* 悲观锁(pessimistic locking)

* 记录锁(record locking)
* 间隙锁（gap locking）
* 临键锁（next-key locking），其中临键锁=记录锁+间隙锁

加锁粒度
* 行锁（row-level locking）
* 表锁（table-level locking）

* 共享锁（share locking，S锁）,读锁
* 排他锁（exclusive locking，X锁），写锁


意向锁（intention locking）

普通select语句不加锁，如想加锁只需在select语句后明确指定"for share"或"for update"即可，其中前者就是共享锁（S锁），也叫读锁；后者是排他锁（X锁），也叫写锁

insert、update和delete都会自动加锁，而且加的是排他锁（X锁）

* MVCC（multi-version concurrency control，即多版本并发控制）
* LBCC（locking-based concurrency control）

四大隔离等级
* 读未提交（Read Uncommitted，RU）
* 读已提交（Read Committed，RC）
* 可重复读（Repeatable Read，RR）
* 串行化（Serializable， SE）

read phenomena，主要是指数据库中三种"错误"的读取结果：
* 脏读：dirty read，即A事务读取了B事务更改但未提交的信息，主要发生在RU隔离级别
* 不可重复读，non-repeatable read，即由于B事务在A事务期间对数据更改并已提交，导致A事务前后读取到不一致的结果
* 幻读，phantom read，即A事务在之后的查询中出现了前期未出现的记录。顾名思义，是指读到了之前未曾发现的记录，当然，从某种意义上将之前未曾发觉肯定也属于不可重复读，这样理解本身是没错的，只是二者侧重点不一样。幻读侧重于在本事务执行期间，其他事务插入（insert）了新的记录，造成本事务之后读取到了前期不曾发现的事务，好似发生幻觉一样，是谓幻读。

快照读，snapshot read，也叫一致读或非加锁读，consistent nonlocking read，指不依靠加锁来保证查询数据一致性，是MySQL中RR和RC级别下的默认查询语句执行方式，通过MVCC机制实现按"快照"版本号执行读操作。RR级别和RC级别采集"快照"原则是不同的，这也是导致两种隔离级别存在不同"读象"（不可重读或幻读）的原因，其中：
* RR级别以进入事务后第一次读操作的时间作为快照版本(注意是第一次读操作的时间，而与开启事务时间无关)，一旦确定快照版本，则在本事务后续读操作中就都应用此快照结果
* RC级别是每次读操作时均采集快照，所以当其他事务提交后它能及时采集到新的快照
 
 SE级别因为是靠加锁（默认对普通select语句加S锁）来实现数据一致，能够确保读取到一致的结果，但已不是原原本本的一致读
 
 当前读，current read，也叫加锁读，即locking read，特指在普通查询语句后增加"for share"或"for update"来指定共享读或排他读的读操作，其中：
* for share，即加S锁，允许多个事务同时获取该S锁，是谓共享
* for update，即加X锁，仅供获取到该X锁的事务操作，是谓排他
由于加锁读是建立在事务的基础上，所以必须显式开启事务后，加锁读才有意义

RR级别中一旦建立了快照版本，则在该事务的后续查询中均采用该快照版本作为结果（当然，通过前面的案例发现也有例外）；与之对应的是，RC级别中，每次查询都采集最新的快照版本作为结果，所以自然也就存在不可重复读的问题。

## NoSQL

### Cassandra

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




[Adding nodes to an existing cluster](https://docs.datastax.com/en/archived/cassandra/3.0/cassandra/operations/opsAddNodeToCluster.html)

[Changing the IP Address of a Cassandra Node](https://www.eventbrite.com/engineering/changing-the-ip-address-of-a-cassandra-node-with-auto_bootstrapfalse/)

[Updating the replication factor](https://docs.datastax.com/en/archived/cql/3.3/cql/cql_using/useUpdateKeyspaceRF.html)

#### Book
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

