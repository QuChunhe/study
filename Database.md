
## MySQL

### Design Schema

除了字典表和日志表，不能有VARCHAR的列

正式表采用InnoDB，导入数据或者中间结果采用的临时表可以可以采用MEMORY或者MyISAM。
* InnoDB具有更好的并发性，采用表锁
* InnoDB具有更好的缓存，InnoDB Buffer

InnoDB的插入性能比较差。

范式与例外

[Good Database Design Principle](http://eckstein.rutgers.edu/mis/handouts/rdb2.pdf)

normalization 规范化

normal form 范式

1.没有冗余，一个字段仅仅存储在一个表中，除非其是一个外键。复制外键许可两个表关联起来。

2.没有坏的依赖，在数据库中任何关系的依赖图，列依赖于整个主键或者一个候选键。违法这种规则的情况包括
* 部分依赖
* 传递依赖

规范化是消除坏依赖的过程，通过分解表并通过外键连接它们。

范式是一些类型，归类了如何对一个表进行归类。

有六个公认的范式
* First Normal Form (1NF)
* Second Normal Form (2NF)
* Third Normal Form (3NF)
* Boyce-Codd Normal Form (BCNF)
* Fourth Normal Form (4NF)
* Fifth Normal Form (5NF)

如果一个表是第一范式，那么其所有的属性都必须是原子的。不是原子原子属性的情况包括
* 嵌套关系、嵌套表或字表
* 重复的组或者重复的部分
* 基于列表值的属性

为了消除迭代关系，可以移出迭代关系，形成一个新表。确保在新表中包括原来表的主健，用于将表连接在一起。

在如下情况中发生了部分依赖
* 采用复合主健（composite primary key）
* 一个非健属性依赖于部分主健，而不是全部主健
* 如果一个满足第一范式的表，不保护任何部分依赖，则称其满足第二范式

当一个非健属性依赖于其他一个非健属性并且所依赖的属性不能用于作为一个候选主健时，就发生了传递依赖于。如果一个满足第二范式并且不包含任何可依赖的转递依赖，则称其满足第三范式。

识别第三范式的关键因素
* 所有属性都是原子类型
* 在每个关系中决定性因素时整个主健，或者被选出来作为候选主健：确保没有部分依赖或者转移依赖
* 基于列表值的属性



[11 important database designing rules which I follow](https://www.codeproject.com/articles/359654/11-important-database-designing-rules-which-i-fo-2)

Rule 1: What is the nature of the application (OLTP or OLAP)?

规则１：应用的本质是什么（OLTP或OLAP）

在开始设计一个数据库时，此需要确定数据库之上的应用在本质上是事务型，还是分析型。在不考虑应用本质的情况下，默认应用正规化，造成出现性能和定制化问题。有两类应用：基于事务型和基于分析型。

事务型：面向CRUD，creating, reading, updating, and deleting records

分析型：面向分析、报表、预测等，较少的插入和更新，尽可能快的取出和分析数据。

如果认为插入、更新和删除占主导，那么需要正规化表设计。反之，需要创建扁平的、非正规化的数据库结构。


OnLine Transaction Processing 联机事务处理过程(OLTP)，也称为面向交易的处理过程，

联机分析处理（Online Analytical Processing ）

[OLAP、OLTP的介绍和比较](https://www.cnblogs.com/hhandbibi/p/7118740.html)

Rule 2: Break your data into logical pieces, make life simpler

规则２：将你的数据分解为逻辑字段，使得生活更加简单

该规则实际是来自第一范式的第一个规则。违反此规则的一个迹象是你的查询中使用太多的字符串解析汉书，例如substring、charindex等，大概需要一个用此规则。

Rule 3: Do not get overdosed with rule 2

规则３：不能滥用规则２

规则２的滥用将会导致不是期望的结果。判断分解是否合理，逻辑上十分合理。

Rule 4: Treat duplicate non-uniform data as your biggest enemy

规则４：将重复的非规格化的数据作为最大的敌人

聚焦和重构复制的数据，对于复制数据的焦虑不是因为其占用磁盘空间，而是其产生困惑。

Rule 5: Watch for data separated by separators

Rule 6: Watch for partial dependencies

规则6:注意部分依赖

注意部分依赖于主健的域。

Rule 7: Choose derived columns preciously

对于OTLP应用，消除派生的列是一个好的想法，除非存在一些紧迫性的性能原因。对于OLAP的例子，我们需要大量的求和和计算，这些派生域对于提高性能是必不可少。

在第三范式要求不能有列依赖于其他非主健的列。我个人的想法是不要盲目地应用第三范式，而是要看具体情况，不是说冗余数据总是不好的。如果冗余数据是计算数据，要仔细评估得失，然后决定是否要实施第三范式。

Rule 8: Do not be hard on avoiding redundancy, if performance is the key

规则８：如果性能是关键，那么就不要竭尽全力的避免冗余。


不必严格遵守避免冗余的规则。如果迫切需要性能，考虑非规范话。在规范化中，需要join很多表，而在非规范化中，减小了join操作从而提高了性能。


Rule 9: Multidimensional data is a different beast altogether

规则9：多维数据完全是另一种野兽

Rule 10: Centralize name value table design

规则10：集中名值表设计

集中的字典表，采用类型表面用途

Rule 11: For unlimited hierarchical data self-reference PK and FK

规则11：对于没有限制的分层数据，采用自引用主健（PK）和外健（FK）



[Database design basics](https://support.office.com/en-us/article/Database-design-basics-EB2159CF-1E30-401A-8084-BD4F9C9CA1F5)


What is good database design?

第一条原则是重复信息（也被称之为冗余数据）是有害的，因为其不仅浪费存储空间，而且增加了错误和不一致的可能性。第二条原则是信息的正确性和完整性非常重要。

一个好的数据库设计应该满足如下条件
* Divides your information into subject-based tables to reduce redundant data.将信息划分到基于主题的表中，以减小冗余书记
* Provides Access with the information it requires to join the information in the tables together as needed.通过按需将表关联在一起，从而提供访问所需要信息的能力。
* Helps support and ensure the accuracy and integrity of your information.辅助支持和确保信息精确性和完整性
* Accommodates your data processing and reporting needs.满足数据处理和报表需求。

设计过程
* Determine the purpose of your database
* Find and organize the information required
* Divide the information into tables
* Turn information items into columns 
* Specify primary keys 
* Set up the table relationships
* Refine your design
* Apply the normalization rules

Determine the purpose of your database

确定数据库的目标(Determine the purpose of your database):将数据库的目标写在纸上是一个好主意.


查找并组织所需信息(Find and organize the information required)


[Database normalization](https://en.wikipedia.org/wiki/Database_normalization)

数据库正规化是根据一系列范式构造关系型数据库的过程，以减小数据冗余和提高数据完整性。范式是由Edgar F. Codd首先提出，作为关系模型的一部分。

正规化需要对于数据库的列（属性）和表（关系）进行组织，以确保它们的依赖性正确地符合数据库完整性约束

### Index & Performancey

[Clustered and Secondary Indexes](https://dev.mysql.com/doc/refman/5.7/en/innodb-index-types.html)

Every I
Database Internals： A Deep Dive into How Distributed Data Systems WorknnoDB table has a special index called the clustered index where the data for the rows is stored. Typically, the clustered index is synonymous with the primary key.

All indexes other than the clustered index are known as secondary indexes. In InnoDB, each record in a secondary index contains the primary key columns for the row, as well as the columns specified for the secondary index.

[8.8 Understanding the Query Execution Plan](https://dev.mysql.com/doc/refman/5.7/en/execution-plan-information.html)
[日常 Explain SQL，慢慢就懂得SQL调优了](https://mp.weixin.qq.com/s?__biz=Mzg3NjIxMjA1Ng==&mid=2247484371&idx=1&sn=2dd8269b94188240f0055a03a7ddd62d&chksm=cf34f9e4f84370f27e4a0154ee3f4ae8cf4b0ed78b4ea08adcba2d259a56c541e9083e3abc60&mpshare=1&scene=1&srcid=&sharer_sharetime=1590161808351&sharer_shareid=fc937fe50a97e6c10553c542abe0a39b&exportkey=AVvFPMTM%2BMmRiXHYR%2FX9SLA%3D&pass_ticket=MEmx%2FMYK8VidR%2FIzGjGwl831u7rhFBT3A8aHASx6xXXS8VO%2BGLjQV%2BNTc5FUYxmf#rd)


[6 Tips to MySQL Performance Tuning ](https://www.slideshare.net/Oracle_MySQL/6-tips-to-mysql-performance-tuning?qid=a3c9f635-e08a-489c-adbb-439394c6e094&v=&b=&from_search=17)

Ensure all tables hava a PRIMARY KEY

InnoDB organizes the data according to the PRIMARY KEY
* The PRIMARY KEY is included in all secondary indexes in order to be able to locate the actual row -> smaller PRIMARY KEY gives smaller secondary indexes.
* A mostly sequential PRIMARY KEY is in general recommended to avoid inserting rows betwween existing rows.

 If you use InnoDB, enable all the INNODB_METRICS counters: innodb_monitor_enable='%', the overhead has turned out to be small so worth the extra details.
 
 Ensure the performance schema is enabled. The performance schema can also be configured dynamically at runtime.
 
 Capacity settings - innodb_buffer_pool_size
 * How much memory does the host have?
 * Subtract memory required by OS and other processes
 * Subtract memoery required by MySQL other then the InnoDB buffer
 * Choose minimum of the and the size of the "working data set"

Capacity Setting - InnoDB redo log
* total size = innodb_log_file_size * innodb_log_files-in_group
* Should be large enought to avoid "excessive" checkpointing
* the larger redo log, the slower shutdowns potentially

Innodb redo log - Is it large enougth
```
MariaDB [**]> show engine innodb status\G;

---
LOG
---
Log sequence number 44272443141888
Log flushed up to   44272443141888
Pages flushed up to 44270928721766
Last checkpoint at  44270908839819
0 pending log flushes, 0 pending chkp writes
32383062 log i/o's done, 427.78 log i/o's/second
----------------------


MariaDB [**]> SELECT name, count FROM information_schema.innodb_metrics WHERE name like "log_lsn_%";

MariaDB [adm]> show global variables like "innodb_log_file%";
+---------------------------+-------------+
| Variable_name             | Value       |
+---------------------------+-------------+
| innodb_log_file_size      | 17179869184 |
| innodb_log_files_in_group | 1           |
+---------------------------+-------------+
```

Calculate the amount of used redo log

Used log = log_lsn_current-log_lsn_last_checkpoint=44272443141888-44270908839819=1534302069

used%= (used log/total log) * 100=1534302069/17179869184*100=8.93

if used% reaches 75% an asychronous flush is tirggered.

InnoDB Undo log
* innodb_undo_tablespaces can only be set before initializing the datadir
* Each undo tablespace file is 10M initially

other capacity options
* max_connecton: be careful setting the too large as each connection requires memory
* table_definition_cache: ensure all tables can be in the cache. If you expect 4000 tables, set table_definition_cache>4000
* table_open_cache: each table can be open more than once
* table_open_cache_instance: typicall a good value is 16.

Buffers and Caches
* join_buffer_size
* sort_buffer_size

Linux glibc malloc change memory allocation algorithm when crossing threshold: Algorithm for larger allocations can be 40 times slower than for smaller allocation.
```
MariaDB [**]> show global status like "sort_merge_passes";
+-------------------+-------+
| Variable_name     | Value |
+-------------------+-------+
| Sort_merge_passes | 0     |
+-------------------+-------+

```

Data Consistency versus Performance
* innodb_flush_log_at_trx_commit
  * 1: is theoretically the slowest, but with fast SSD it may be arount as fast as 2 and 0. Defaults to 1, flush the redo log after each commit. Required for D in ACID
  * 2: flushed every second: transactions may be lost if the OS crashes
  * 0: MySQL never fsyncs  
* sync_binlog: specifies how many transactions between each flush of the binary log
  * 0: when rotating the binary log or when the OS decides
  * 1: at everty transaction commit - this is the saftest
  * N: every N commites
  * MySQL 5.6 and later support group commit for InnoDB giving less overhead of sync_binlog=1
  
I/O Scheduler
```
cat /sys/block/sda/queue/scheduler

echo deadline > /sys/block/sda/queue/scheduler

cat /sys/block/sda/queue/scheduler
```
  
  
[Optimizing MariaDB for maximum performance ](https://www.slideshare.net/MariaDB/optimizing-mariadb-for-maximum-performance?qid=2c51b4b8-e618-4342-a975-2fb06ee22c57&v=&b=&from_search=24)  
We deprecate & hard-wire a number of parameters, including the following:
```
innodb_buffer_pool_instances=1, innodb_page_cleaners=1 
innodb_log_files_in_group=1 (only ib_logfile0) 
innodb_undo_logs=128 (the “rollback segment” component of DB_ROLL_PTR)
```
Operating System System 
```shell
# sysctl -w vm.swappiness=1 
# echo "vm.swappiness=1" >> /etc/sysctl.conf 
``` 
```shell
# echo noop > /sys/block/sda/queue/scheduler  
```
```shell
 # cat /etc/security/limits.conf 
 mysql soft nofile 65535 
 mysql hard nofile 65535  
 ```
 ```shell
# cat /etc/fstab ... rw,noatime,nodiratime,data=writeback 
```
 Server Variables MariaDB Server 
```
max_allowed_packet = e.g. 128G-256G 
max_connections = e.g. 2000-10000 

thread_handling = pool-of-threads 
thread_pool_size = # of cpu cores 
thread_pool_max_threads = 65536 t
hread_pool_min_threads = e.g. 8 
thread_pool_idle_timeout = 60 

query_cache_size = 0 
query_cache_type = 0 

skip_name_resolv = ON 

thread_cache_size = DON'T SET (Auto) 

sync_binlog = e.g. 1000

innodb_buffer_pool_size = e.g. 256M-900G 
#((Total RAM - (OS + Apps)
#- (mysqld memory + query buffers)
#- caches for things like binary log 
#- other possible buffers and caches 
#- memory tables) 
#/ 105% ) | ROUND_DOWN
innodb_log_file_size = e.g. 2G-16G 
innodb_stats_on_metadata = 0 
innodb_flush_log_at_trx_commit = e.g. 0? (IFLATC) 

innodb_flush_method = O_DIRECT 
innodb_io_capacity = e.g. 2000 
innodb_adaptive_hash_index_parts = e.g. 2-8 btr0sea.c

innodb_autoinc_lock_mode = e.g. 2 
innodb_flush_neighbors = e.g. 0 w/SSD 

innodb_lru_scan_depth = e.g. 4096 
innodb_sync_array_size = e.g. 16-32 (but < # of cpu cores) 

innodb_read_io_threads = 4 
innodb_write_io_threads = 4 

```
### DevOpt

[Optimizing Database Performance](https://www.xaprb.com/slides/percona-live-2019-optimizing-database-performance-efficiency/#1)

The CELT metrics reveal everything about workload QoS.
* Concurrency is the number of simultaneous requests NNN
* Error Rate is what it sounds like
* Latency is response time, as previously defined RRR
* Throughput is requests per second XXX

These can all be calculated as average (or p99) during intervals or as they apply to individual requests (except for Throughput).


The workload places demand on four key resources.
* CPU cycles
* Memory
* Storage
* Network

The way resources respond to demand often explains performance.


The Three Golden Signals of Resource Sufficiency: Brendan Gregg’s USE method:
* Utilization
* Saturation
* Errors

The CELT and USE metrics are the seven golden signals of overall system health and performance, unifying the external (customer, workload) and internal (resource) perspectives.

There are three primary ways to measure requests (workload):
* Turn on full query logging
* Use internal statistics tables/views, if they exist
* Sniff network traffic


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

### Configuration

[采坑之使用MySQL，SQL_MODE有哪些坑](https://dev.mysql.com/doc/refman/8.0/en/sql-mode.html)

[Server SQL Modes](https://dev.mysql.com/doc/refman/8.0/en/sql-mode.html)

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



[AUTO_INCREMENT Handling in InnoDB](https://dev.mysql.com/doc/refman/5.7/en/innodb-auto-increment-handling.html)

“INSERT-like” statements 
* “Simple inserts”: Statements for which the number of rows to be inserted can be determined in advance (when the statement is initially processed).  
* “Bulk inserts”: Statements for which the number of rows to be inserted (and the number of required auto-increment values) is not known in advance. 
* “Mixed-mode inserts”: These are “simple insert” statements that specify the auto-increment value for some (but not all) of the new rows.

innodb_autoinc_lock_mode
* innodb_autoinc_lock_mode = 0 (“traditional” lock mode) 
* innodb_autoinc_lock_mode = 1 (“consecutive” lock mode) 
* innodb_autoinc_lock_mode = 2 (“interleaved” lock mode) 


[14.7.1 InnoDB Locking](https://dev.mysql.com/doc/refman/5.7/en/innodb-locking.html)

**Dirty Read**:  An operation that retrieves unreliable data, data that was updated by another transaction but not yet committed. It is only possible with the isolation level known as read uncommitted

**Phantom Read**： A row that appears in the result set of a query, but not in the result set of an earlier query. For example, if a query is run twice within a transaction, and in the meantime, another transaction commits after inserting a new row or updating a row so that it matches the WHERE clause of the query.

  This occurrence is known as a phantom read. It is harder to guard against than a non-repeatable read, because locking all the rows from the first query result set does not prevent the changes that cause the phantom to appear

**Repeatable Read**


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

### JDBC


[Configuration Properties](https://dev.mysql.com/doc/connector-j/8.0/en/connector-j-reference-configuration-properties.html)

### SQL

[Subqueries](https://dev.mysql.com/doc/refman/5.7/en/subqueries.html)



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




Alex Petrov，Database Internals： A Deep Dive into How Distributed Data Systems Work

# MySQL Cluster

[Vitess, A database clustering system for horizontal scaling of MySQL](https://vitess.io/)
