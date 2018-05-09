
#### MySQL

-[Spider Server System Variables](https://mariadb.com/kb/en/library/spider-server-status-variables/)




#### Cassandra

-Expert Apache Cassandra Adminitration, Apress, 2018.

[p114]
   In a multiple partition batch operation, the coordinator node can turn out to be a bottleneck during a batch operation. The higher the number of partitions in a batch operation, the higher the latency due to batching.
[145]   
   Write operations that use only a single partition are fine performance-wise.
[146]   
   Even in cases with multiple partitions, if the operations involve only small inserts or updates, you’ll be fine with batching those operations to ensure consistency.
