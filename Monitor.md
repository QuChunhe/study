

# Prometheus

prometheus的所有数据都存储为时序数据（time series），时序数据是带时间戳的值流，每个时序数据流用指标名（metric name）和标签维度（labelset）识别

Prometheus中有两种类型：
* 指标类型：
  * gauge, 常规计量，瞬时状态的数据
  * counter, gauge的特例，维护一个计数器
  * histogram, 统计数据的分布情况
  * summary, 
  * untyped.
* 表达式类型：string, scalar, instant vector, range vector
  

  $namespace和$service为选择的参数
2.1 业务指标
业务指标为服务粒度。
Uptime
max(process_uptime_seconds{namespace="$namespace", service="$service"})

Starttime
max(process_start_time_seconds{namespace="$namespace", service="$service"}) *1000

GRPC QPS (Spring)
sum(rate(grpc_server_calls_seconds_count{namespace="$namespace", service="$service"}[5m]))

GPRC Result/Hour (Spring)
sum(round(increase(grpc_server_calls_seconds_count{namespace="$namespace", service="$service"}[1h]))) by (result) 

GRPC Latency (Spring)
sum(rate(grpc_server_calls_seconds_sum{namespace="$namespace", service="$service"}[5m])) / sum(rate(grpc_server_calls_seconds_count{namespace="$namespace", service="$service"}[5m]))

GRPC Latency Percentile (Spring)
histogram_quantile(0.9, sum by (le) (irate(grpc_server_calls_seconds_bucket{namespace="$namespace", service="$service"}[5m])))
histogram_quantile(0.99, sum by (le) (irate(grpc_server_calls_seconds_bucket{namespace="$namespace", service="$service"}[5m])))

GRPC Traffic Top 5 (Spring)
label_replace(
  topk(5, round(sum by (method) (
    increase(grpc_server_calls_seconds_count{namespace="$namespace", service="$service"}[1h])
  ))),
  "method", "$1", "method", ".+?\\.([^.]+)"
)

GRPC QPS (Micronaut)
sum(rate(grpc_server_processing_duration_seconds_count{namespace="$namespace", service="$service"}[5m]))

GRPC Result/Hour (Micronaut)
sum(round(increase(grpc_server_processing_duration_seconds_count{namespace="$namespace", service="$service"}[1h]))) by (statusCode)

GRPC Latency (Micronaut)
sum(rate(grpc_server_processing_duration_seconds_sum{namespace="$namespace", service="$service"}[5m])) / sum(rate(grpc_server_processing_duration_seconds_count{namespace="$namespace", service="$service"}[5m]))

Traffic Top 5 (Micronaunt)
label_replace(
  topk(5, round(sum by (method) (
    increase(grpc_server_processing_duration_seconds_count{namespace="$namespace", service="$service"}[1h])
  ))),
  "method", "$1", "method", ".+?\\.([^.]+)"
)

HTTP Status Code QPS
sum(rate(http_server_requests_seconds_count{namespace="$namespace", service="$service", uri!~"/actuator.*",uri!~"/prometheus.*", uri!~"/health.*"}[5m])) by (status)

HTTP QPS
sum(rate(http_server_requests_seconds_count{namespace="$namespace", service="$service", uri!~"/actuator.*",uri!~"/prometheus.*"}[5m]))

Kafka Consumer QPS (Spring)
sum(rate(kafka_consumer_fetch_manager_records_consumed_total{namespace="$namespace", service="$service"}[1m]))

Kafak Listener Lag (Spring)
sum(kafka_consumer_fetch_manager_records_lag{namespace="$namespace", service="$service"}) by(topic)

Kafka Consumer QPS (Micronaut)
sum(rate(kafka_consumer_records_consumed_total_records_total{namespace="$namespace", service="$service"}[1m]))

Kafka Listener Lag (Micronaut)
sum(kafka_consumer_records_lag_records{namespace="$namespace", service="$service"}) by (topic)

Logback Events/Hour
sum(round(increase(logback_events_total{namespace="$namespace", service="$service"}[1h]))) by (level)

2.2 机器指标
机器指标为pod粒度。
Average Load
sum(system_load_average_1m{namespace="$namespace", service="$service"})  by (pod) / sum(system_cpu_count{namespace="$namespace", service="$service"}) by (pod)

System CPU Usage
sum(system_cpu_usage{namespace="$namespace", service="$service" }) by (pod)

Container CPU Usage
sum(node_namespace_pod_container:container_cpu_usage_seconds_total:sum_irate{namespace="$namespace", container="$service"}) by (pod) /sum(cluster:namespace:pod_cpu:active:kube_pod_container_resource_requests{namespace="$namespace", container="$service"}) by (pod)

Container Memory Usage
sum(container_memory_working_set_bytes{namespace="$namespace", container="$service",  image!=""}) by (pod) / sum(cluster:namespace:pod_memory:active:kube_pod_container_resource_requests{namespace="$namespace", container="$service"}) by (pod)

Container  Network Transmit
sum(rate(container_network_transmit_bytes_total{namespace="$namespace", pod=~".*$service.*"}[5m])) by (pod) /1024

Container  Network Receive
sum(rate(container_network_receive_bytes_total{namespace="$namespace", pod=~".*$service.*"}[5m])) by (pod)/ 1024

Containter FS Read
sum(rate(container_fs_reads_bytes_total{namespace="$namespace", pod=~".*$service.*"}[5m])) by (pod) /1024

Containter FS Writes
sum(rate(container_fs_writes_bytes_total{namespace="$namespace", pod=~".*$service.*" }[5m])) by (pod) /1024

JVM NonHeap Usage
sum(jvm_memory_used_bytes{namespace="$namespace", service="$service", area="nonheap"}) by (pod) *100/sum(jvm_memory_max_bytes{namespace="$namespace", service="$service", area="nonheap"}) by (pod)

JVM Heap Usage
sum(jvm_memory_used_bytes{namespace="$namespace", service="$service", area="heap"}) by (pod)*100/sum(jvm_memory_max_bytes{namespace="$namespace", service="$service", area="heap"}) by (pod)

JVM CPU Usage
sum(process_cpu_usage{namespace="$namespace", service="$service" }) by (pod)

JVM GC  Pause
sum(rate(jvm_gc_pause_seconds_sum{namespace="$namespace", service="$service"}[1m])) by (pod)

JVM GC Count/Second
sum(rate(jvm_gc_pause_seconds_count{namespace="$namespace", service="$service"}[1m])) by (pod)

JVM Live Thread
sum(jvm_threads_live_threads{namespace="$namespace", service="$service"}) by (pod)

JVM Daemon Threads
sum(jvm_threads_daemon_threads{namespace="$namespace", service="$service"}) by (pod)

JVM Peak Threads
sum(jvm_threads_peak_threads{namespace="$namespace", service="$service"}) by (pod)

2.3 中间件指标
HikariCP Usage Time
sum(increase(hikaricp_connections_usage_seconds_sum{namespace="$namespace", service="$service"}[1m])) /sum(increase(hikaricp_connections_usage_seconds_count{namespace="$namespace", service="$service"}[1m]))

HikariCP Usage Count/Minute
sum(increase(hikaricp_connections_usage_seconds_count{namespace="$namespace", service="$service"}[1m]))

Redis RT (Lettuce)
sum(increase(lettuce_command_completion_seconds_sum{namespace="$namespace", service="$service",command!~"AUTH",command!~"HELLO",command!~"SELECT"}[1m])) /sum(increase(lettuce_command_completion_seconds_count{namespace="$namespace", service="$service",command!~"AUTH",command!~"HELLO",command!~"SELECT"}[1m]))

