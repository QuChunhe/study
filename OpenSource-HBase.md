


Zookeeper :
HMaster: 

HRegionServer

在HBase体系中，Region是最细粒度的功能单元，一张HBase表即是由一个或多个Region组成。RegionServer运行在HDFS DataNode之上，负责管理存储在它上面的所有Region。

在Region中，每个列族的数据会存储在一起，形成一个Store。每个Store由一批HFile与一个MemStore组成。