
```
http://localhost:60010/master-status
```

关键词
* namespace: 命名空间,对应对于库
* table
* row
* column family: 列的固定部分
* column: 描述的关键词
* timestamp:
* cell

架构
* client
* Zookeeper :协调Hmaster选举以及同步元数据
* HMaster: 协调和元数据,比如负载均衡
* HRegionServer:Mem Store+ HFile(HDFS)

在HBase体系中，Region是最细粒度的功能单元，一张HBase表即是由一个或多个Region组成。RegionServer运行在HDFS DataNode之上，负责管理存储在它上面的所有Region。

在Region中，每个列族的数据会存储在一起，形成一个Store。每个Store由一批HFile与一个MemStore组成。

避免hbase热点
反转
加盐
哈希


对写流程

meta表存储表和region　server信息　Ｚookeeper

1. 写入流传１．先写入HLog,防止数据丢失
2. 数据写入到Memstore
3. Memstore达到阀值,会把Memstore中的数据附录是到StoreFile中
4. 当StoreFile越来越多,达到一定数量时,会触发compact合并操作,将多个小文件合并成一个大文件


```sql
status
version

create_namespace 'database'

create 'student', 'info', 'address'

put 'student','1', 'info:name', 'Qu Chunhe'

flush 'student'

```