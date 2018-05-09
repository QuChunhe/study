
#### MySQL

-[Spider Server System Variables](https://mariadb.com/kb/en/library/spider-server-status-variables/)




#### Cassandra

##-Expert Apache Cassandra Adminitration, Apress, 2018.

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
		$nodetool repair -pr hosts 10.2.2.30 10.2.2.31
