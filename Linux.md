
[Linux Performance](http://www.brendangregg.com/linuxperf.html)

[Linux Performance Analysis in 60,000 Milliseconds](https://medium.com/netflix-techblog/linux-performance-analysis-in-60-000-milliseconds-accc10403c55)


The	USE	Method	
- Utilization: busy time
- Saturation: queue length or queued time
- Errors: easy to interpret (objective)
  

### Command

top -Hp pid

pidstat 1

mpstat -P ALL 1

free -h

iostat -xz 1

netstat -antp

netstat -nltp


sar -n TCP,ETCP 1

sar -n UDP 1

sar -n DEV 1
