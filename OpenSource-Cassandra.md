

Partition Key

* Partition Key：将数据分散到集群的 node 上
* Primary Key：在 Single column Primary Key 情况下作用和 Partition Key 一样；在 Composite Primary Key 情况下，组合 Partition key 字段决定数据的分发的节点；
* Clustering Key：决定同一个分区内相同 Partition Key 数据的排序，默认为升序，我们可以在建表语句里面手动设置排序的方式（DESC 或 ASC）