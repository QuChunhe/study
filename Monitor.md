

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