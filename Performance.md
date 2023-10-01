

* Server Farm/Cluster (real time access)
* Asynchronus Processing
* Data Partitioning
* Filtering at the source
* Map/Reduce (Batch Parallel Processing)
* Calculate an approsimate result
* Resources Pool
* Content Delivery Networ (Static Cache)
* Cache Engine (Dynamic Cache)


Scalale System Design Patterns
* Load Balancer: A dispatcher determines which worker instance will handle a request based on different policies.
  * 轮询策略: 在负载均衡领域中，轮询策略主要包括顺序轮询和加权轮询两种方式。
  * 随机策略
  * 哈希和一致性哈希策略
  * 响应速度均衡（Response Time）
  * 最少连接数均衡（Least Connection）
* Scatter and Gather: A dispatcher multicasts requests to all workers in a pool. Each worker will compute a local result and send it back to the dispatcher, who will consolidate them into a single response and then send back to the client.
* Result Cache: A dispatcher will first lookup if the request has been made before and try to find the previous result to return, in order to save the actual execution.
* Shared Space: All workers monitors information from the shared space and contributes partial knowledge back to the blackboard. The information is continuously enriched until a solution is reached.
* Pipe and Filter: All workers connected by pipes across which data flows.
* MapReduce: Targets batch jobs where disk I/O is the major bottleneck. It use a distributed file system so that disk I/O can be done in parallel.
* Bulk Synchronous Parallel: A lock-step execution across all workers, coordinated by a master.
* Execution Orchestrator: An intelligent scheduler / orchestrator schedules ready-to-run tasks (based on a dependency graph) across a clusters of dumb workers.