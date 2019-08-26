
[Linux Performance](http://www.brendangregg.com/linuxperf.html)

[Linux Performance Analysis in 60,000 Milliseconds](https://medium.com/netflix-techblog/linux-performance-analysis-in-60-000-milliseconds-accc10403c55)


[Linux System and Performance Monitoring](http://www.ufsdump.org/papers/linuxcon2010-linux-monitoring.pdf)

应用类型
* IO密集型(IO Bound)
* CPU密集型(CPU Bound)

[宋宝华：网上坑爹的Linux资料汇总之内存管理](https://mp.weixin.qq.com/s/4N6MxrR3t68WqJhaOcDJ2Q)  
以文件系统中文件为背景的称为cache，以裸分区/dev/sdax等为背景称为buffer


* 编写代码
* 优化性能
* 排除bug

静态(jstack)，死锁或者阻塞分析

动态(perf)，性能热点，耗时分析，profile

整体的系统视角和局部的子系统视角，比如MySQL和Java优化

资源和程序
* 资源，CPU，Memeory,Network,Disk, Cache 
* 程序，MySQL和Java

性能瓶颈涉及多个因素，比较负载和资源等，难于复现。

优化的分类：
* confiuration 配置，包括硬件组件、操作系统、系统软件(MySQL)和应用系统
* 架构，增加缓存等
* 代码优化

The field of performance includes the following activities, listed in an ideal order of execution:
1. Setting performance objectives and performance modeling
2. Performance characterization of prototype software or hardware
3. Performance analysis of development code, pre-integration
4. Performing non-regression testing of software builds, pre- or post-release
5. Benchmarking/benchmarketing for software releases
6. Proof-of-concept testing in the target environment
7. Configuration optimization for production deployment
8. Monitoring of running production software
9. Performance analysis of issues


capacity planning

Two perspectives for performance analysis
* workload analysis
* resource analysis

Performance Is Challenging
* Performance Is Subjective
* Systems Are Complex
* There Can Be Multiple Performance Issues

This can occur due to a cascading failure, when one failed component causes performance issues in others.

Latency

Dynamic Tracing

Terminology
* IOPS: Input/output operations per second
* Throughput: 
* Latency: This includes any time spent waiting and time spent being serviced (service time), including the time to transfer the result.
* Utilization: For resources that service requests, utilization is a measure of how busy a resource
is, based on how much time in a given interval it was actively performing work.
* Saturation: the degree to which a resource has queued work it cannot service.
* Workload: The input to the system or the load applied is the workload. For a database, the workload consists of the database queries and commands sent by the clients.


Utilization can be time-based or capacity-based.　Time-Based Time-based utilization is formally defined in queueing theory. For example the average amount of time the server or resource was busy

This defines utilization in terms of capacity instead of time. It implies that a disk at 100% utilization cannot accept any more work. With the time-based definition, 100% utilization only means it is busy
100% of the time. 100% busy does not mean 100% capacity.

Saturation begins to occur at 100% utilization (capacity-based), as extra work cannot be processed and begins to queue.

In the field of computing performance, profiling is typically performed by sampling the state of the system at timed intervals,
and then studying the set of samples.
Unlike the previous metrics covered, including IOPS and throughput, the use of sampling provides
a coarse view of the target’s activity, depending on the rate of sampling.


Most recently used (MRU) refers to a cache retention policy, which decides what to favor keeping in the cache: the objects that have been used most recently. Least recently used (LRU) can refer to an equivalent cache eviction policy, deciding what objects to remove from the cache when more space is needed. There are also most frequently used (MFU) and least frequently used (LFU)
policies.


These words are commonly used to describe the state of the cache:
* Cold: A cold cache is empty, or populated with unwanted data. The hit ratio for a cold cache is
zero (or near zero as it begins to warm up).
* Hot: A hot cache is populated with commonly requested data and has a high hit ratio, for
example, over 99%.
* Warm: A warm cache is one that is populated with useful data but doesn’t have a high enough
hit ratio to be considered hot.
* Warmth: Cache warmth describes how hot or cold a cache is. An activity that improves cache
warmth is one that aims to improve the cache hit ratio.

There are two common perspectives for performance analysis, each with different audiences, metrics, and approaches. They are workload analysis and resource analysis. They can be thought of as either top-down or bottom-up analysis of the operating system software stack

Resource analysis begins with analysis of the system resources: CPUs, memory, disks, network interfaces, busses, and interconnects.This perspective focuses on utilization, to identify when resources are at or approaching their limit.
Some resource types, such as CPUs, have utilization metrics readily available.

Metrics best suited for resource analysis include
* IOPS
* Throughput
* Utilization
* Saturation

Workload analysis examines the performance of the applications: the workload applied and how the application is responding.
The targets for workload analysis are
* Requests: the workload applied
* Latency: the response time of the application
* Completion: looking for errors

Studying workload requests typically involves checking and summarizing their attributes: the
process of workload characterization


Latency (response time) is the most important metric for expressing application performance.

To investigate latency usually involves drilling down deeper into the application,
libraries, and the operating system (kernel).

* Streetlight Anti-Method
* Random Change Anti-Method
* Blame-Someone-Else Anti-Method
* Ad Hoc Checklist Method


Problem Statement
1. What makes you think there is a performance problem?
2. Has this system ever performed well?
3. What changed recently? Software? Hardware? Load?
4. Can the problem be expressed in terms of latency or runtime?
5. Does the problem affect other people or applications (or is it just you)?
6. What is the environment? What software and hardware are used? Versions? Configuration?

Scientific Method
1. Question
2. Hypothesis
3. Prediction
4. Test
5. Analysis

observational or experimental test

Diagnosis Cycle: hypothesis → instrumentation → data → hypothesis


The utilization, saturation, and errors (USE) method should be used early in a performance investigation, to identify systemic bottlenecks.

The utilization, saturation, and errors (USE) method should be used early in a performance investigation, to identify systemic bottlenecks.
* Resource: all physical server functional components (CPUs, busses, . . .). Some software resources can also be examined, provided the metrics make sense.
* Utilization: for a set time interval, the percentage of time that the resource was busy servicing work. While busy, the resource may still be able to accept more work; the degree to which it cannot do so is identified by saturation.
* Saturation: the degree to which the resource has extra work that it can’t service, often waiting on a queue.
* Errors: the count of error events.


a generic list of server hardware resources
* CPUs: sockets, cores, hardware threads (virtual CPUs)
* Main memory: DRAM
* Network interfaces: Ethernet ports
* Storage devices: disks
* Controllers: storage, network
* Interconnects: CPU, memory, I/O

Workload characterization is a simple and effective method for identifying a class of issues: those
due to the load applied. It focuses on the input to the system, rather than the resulting performance.

Drill-down analysis starts with examining an issue at a high level, then narrowing the focus based on the previous findings, discarding areas that seem uninteresting, and digging deeper into those areas that are.
1. Monitoring: This is used for continually recording high-level statistics over time, and
identifying or alerting if a problem may be present.
2. Identification: Given a suspected problem, this narrows the investigation to particular
resources or areas of interest, identifying possible bottlenecks.
3. Analysis: Further examination of particular system areas is done to attempt to root-cause and
quantify the issue.


Latency analysis examines the time taken to complete an operation, then breaks it into smaller components, continuing to subdivide the components with the highest latency so that the root cause can be identified and quantified.


Static performance tuning focuses on issues of the configured architecture. Other methodologies focus
on the performance of the applied load: the dynamic performance.

Analytical modeling can be considered as the third type of performance evaluation activity, along
with observability of a production system (“measurement”) and experimental testing (“simulation”).

Scalability analysis may reveal that performance stops scaling linearly at a particular point, called the knee point, due to a resource constraint.

* Linear scalability: Performance increases proportionally as the resource is scaled. This may not continue forever and may instead be the early stages of another scalability pattern.
* Contention: Some components of the architecture are shared and can be used only serially, and contention for these shared resources begins to reduce the effectiveness of scaling.
* Coherence: The tax to maintain data coherency including propagation of changes begins to outweigh the benefits of scaling.
* Knee point: A factor is encountered at a scalability point that changes the scalability profile.
* Scalability ceiling: A hard limit is reached. This may be a device bottleneck, such as a bus or interconnect reaching maximum throughput, or a software-imposed limit (system resource control).


A/S/m

These are the arrival process (A), service time distribution (S), and number of service centers (m).

* M/M/1: Markovian arrivals (exponentially distributed arrival times), Markovian service times (exponential distribution), one service center
* M/M/c: same as M/M/1, but multiserver
* M/G/1: Markovian arrivals, general distribution of service times (any), one service center
* M/D/1: Markovian arrivals, deterministic service times (fixed), one service center

Resource Limits
1. Measure the rate of server requests, and monitor this rate over time.
2. Measure hardware and software resource usage. Monitor this rate over time.
3. Express server requests in terms of resources used.
4. Extrapolate server requests to known (or experimentally determined) limits for each resource.

The resources to monitor include
* Hardware: CPU utilization, memory usage, disk IOPS, disk throughput, disk capacity (volume used), network throughput
* Software: virtual memory usage, processes/tasks/threads, file descriptors


There is a way to express variation as a single metric: the ratio of the standard deviation to the
mean, which is called the coefficient of variation (CoV or CV).


Visualizations
* Line Chart
* Scatter Plots
* Heat Maps
* Surface Plot


Workloads can be categorized as either
* CPU-bound: applications that perform heavy compute, for example, scientific and
mathematical analysis, which is expected to have long runtimes (seconds, minutes, hours).
These become limited by CPU resources.
* I/O-bound: applications that perform I/O, with little compute, for example, web servers, file
servers, and interactive shells, where low-latency responses are desirable. When their load
increases, they are limited by I/O to storage or network resources.


Observability Tools


In reality, there were many gaps, and systems performance experts became skilled in the art of inference and interpretation: figuring out activity from indirect tools and statistics.   

Performance observability tools can be categorized as providing system-wide or per-process observability, and most are based on either counters or tracing.


A performance goal provides direction for your performance analysis work and helps you select
which activities to perform.
* Latency: a low application response time
* Throughput: a high application operation rate or data transfer rate
* Resource utilization: efficiency for a given application workload


Application Performance Techniques
* Selecting an I/O Size. “Initialization tax” is paid for small and large I/O alike. For efficiency, the more data
transferred by each I/O, the better.
* Caching. An important aspect of the cache is how it manages integrity, so that lookups do not return stale
data. This is called cache coherency and can be expensive to perform—ideally not more so than the benefit the cache provides.
* Buffering. To improve write performance, data may be coalesced in a buffer before being sent to the next level.
* Polling. Polling is a technique in which the system waits for an event to occur by checking the status of the
event in a loop, with pauses between checks. There are some potential performance problems with polling:
    * Costly CPU overhead of repeated checks
    * High latency between the occurrence of the event and the next polled check
* Concurrency and Parallelism. 
    * Different functions within an application can also be made concurrent. This can be achieved using multiple processes (multiprocess) or multiple threads (multithreaded), each performing its own task.
    * Another approach is event-based concurrency, whereby an application services different functions and switches between them when events occur.
    
* Non-Blocking I/O
* Processor Binding. CPU affinity
    
# Setting

[The /proc filesystem documentation ](http://linuxinsight.com/proc_filesystem.html)
 
```
sysctl -a
```
/etc/sysctl.conf
```
vm.swappiness = 1
	
vm.dirty_background_ratio = 5
vm.dirty_ratio = 

#128 KiB
net.core.wmem_default = 131072
net.core.rmem_default = 131072
#20 MiB
net.core.wmem_max = 20971520
net.core.rmem_max = 20971520
#Set maximum number of packets, queued on the INPUT side, 
#when the interface receives packets faster than kernel can process them
net.core.netdev_max_backlog = 4000
net.core.optmem_max = 40960

#4 KiB minimum, 64 KiB default, and 16 MiB maximum buffer.	
net.ipv4.tcp_rmem = 4096 65536 16777216
net.ipv4.tcp_wmem = 4096 65536 16777216
net.ipv4.tcp_window_scaling = 1
net.ipv4.tcp_max_syn_backlog = 4096

# Increase number of incoming connections
net.core.somaxconn = 4096

vm.max_map_count = 1048575
```
```
 sysctl -p
 sysctl -p --system
 
```


```

# Increase size of file handles and inode cache
fs.file-max = 2097152

# Do less swapping
vm.swappiness = 10
vm.dirty_ratio = 60
vm.dirty_background_ratio = 2

### GENERAL NETWORK SECURITY OPTIONS ###

# Number of times SYNACKs for passive TCP connection.
net.ipv4.tcp_synack_retries = 2

# Allowed local port range
net.ipv4.ip_local_port_range = 2000 65535

# Protect Against TCP Time-Wait
net.ipv4.tcp_rfc1337 = 1

# Decrease the time default value for tcp_fin_timeout connection
net.ipv4.tcp_fin_timeout = 15

# Decrease the time default value for connections to keep alive
net.ipv4.tcp_keepalive_time = 300
net.ipv4.tcp_keepalive_probes = 5
net.ipv4.tcp_keepalive_intvl = 15

### TUNING NETWORK PERFORMANCE ###

# Default Socket Receive Buffer
net.core.rmem_default = 31457280

# Maximum Socket Receive Buffer
net.core.rmem_max = 12582912

# Default Socket Send Buffer
net.core.wmem_default = 31457280

# Maximum Socket Send Buffer
net.core.wmem_max = 12582912

# Increase number of incoming connections
net.core.somaxconn = 4096

# Increase number of incoming connections backlog
net.core.netdev_max_backlog = 65536

# Increase the maximum amount of option memory buffers
net.core.optmem_max = 25165824

# Increase the maximum total buffer-space allocatable
# This is measured in units of pages (4096 bytes)
net.ipv4.tcp_mem = 65536 131072 262144
net.ipv4.udp_mem = 65536 131072 262144

# Increase the read-buffer space allocatable
net.ipv4.tcp_rmem = 8192 87380 16777216
net.ipv4.udp_rmem_min = 16384

# Increase the write-buffer-space allocatable
net.ipv4.tcp_wmem = 8192 65536 16777216
net.ipv4.udp_wmem_min = 16384

# Increase the tcp-time-wait buckets pool size to prevent simple DOS attacks
net.ipv4.tcp_max_tw_buckets = 1440000
net.ipv4.tcp_tw_recycle = 1
net.ipv4.tcp_tw_reuse = 1
```



cat /proc/vmstat | egrep "dirty|writeback"
```
nr_dirty 3875
nr_writeback 29
nr_writeback_temp 0
```
```
ulimit -a

/etc/security/limits.conf

admweb      soft   nofile           655360
admweb      hard   nofile           655360

#64G
admweb           hard    memlock         67108864
admweb           soft    memlock         67108864

```

```
grep Hugepagesize /proc/meminfo

$ grep Hugepagesize /proc/meminfo
Hugepagesize:     2048 kB
$

The output shows that the size of a Huge Page on this system is 2MB. This means if a 1GB Huge Pages pool should be allocated, then 512 Huge Pages need to be allocated. The number of Huge Pages can be configured and activated by setting nr_hugepages in the proc file system. For example, to allocate 512 Huge Pages, execute: 


# sysctl -w vm.nr_hugepages=512

# grep HugePages_Total /proc/meminfo



```

# Performance

```
yum install sysstat
yum install iotop
```

## Methodologies  
[The USE Method](http://www.brendangregg.com/usemethod.html)
The USE Method can be summarized as:  For every resource, check utilization, saturation, and errors.

Terminology definitions:
* resource: all physical server functional components (CPUs, disks, busses, ...) [1]
* utilization: the average time that the resource was busy servicing work [2]
* saturation: the degree to which the resource has extra work which it can't service, often queued
* errors: the count of error events



```
 /etc/logrotate.conf
 
 vim /etc/logrotate.d/nginx
 /var/log/nginx/*.log {
    daily
    dateext
    compress
    rotate 1000
    nodelaycompress
    missingok
    notifempty
    sharedscripts
    nocreate
    noolddir
    postrotate
        kill -USR1 `cat /var/run/nginx.pid`
    endscript
} 
 ```
 
 ```
 vim /etc/crontab
 
  0  0  *  *  * root ntpdate 0.uk.pool.ntp.org
  0  12 *  *  * root ntpdate 1.us.pool.ntp.org
  59 23 *  *  * root /usr/sbin/logrotate -f /etc/logrotate.d/nginx
 ```

### Monitoring

#### CPU

run-queue latency or dispatcher-queue latency, scheduler latency.

cache warmth, CPU affinity

cycles-per-instruction(CPI)

Cycles per instruction (CPI) is an important high-level metric for describing where a CPU is
spending its clock cycles and for understanding the nature of CPU utilization. This metric may also be
expressed as instructions per cycle (IPC), the inverse of CPI.

For real-world applications, here's how I'd interpret the IPC:
* IPC < 1: likely stall cycle bound, also likely memory bound (more PMCs can confirm). Stall cycles are when the CPU isn't making forward progress, likely because it's waiting on memory I/O. In this case, look to tune memory usage: allocate fewer or smaller objects, do zero copy, look at NUMA and memory placement tuning. A CPU flame graph will show which code is on-CPU during these stall cycles, and should be clues for were to look for memory usage.
* IPC > 1: likely instruction bound. Look to tune instructions: a CPU flame graph will show which code is on-CPU doing instructions: find ways to reduce executed code.

CPU utilization  

The measure of CPU utilization spans all clock cycles for eligible activities, including memory
stall cycles. It may seem a little counterintuitive, but a CPU may be highly utilized because it is often
stalled waiting for memory I/O, not just executing instructions, as described in the previous section.

When measured across the entire system, the user-time/kernel-time ratio indicates the type of workload
performed.
* Applications that are computation-intensive may spend almost all their time executing user-level
code and have a user/kernel ratio approaching 99/1. Examples include image processing, genomics,
and data analysis.
* Applications that are I/O-intensive have a high rate of system calls, which execute kernel code to
perform the I/O. For example, a web server performing network I/O may have a user/kernel ratio of
around 70/30.


A CPU at 100% utilization is saturated, and threads will encounter scheduler latency as they wait to
run on-CPU, decreasing overall performance. This latency is the time spent waiting on the CPU run
queue or other structure used to manage threads.



[The PMCs of EC2: Measuring IPC](http://www.brendangregg.com/blog/2017-05-04/the-pmcs-of-ec2.html)
```
 yum install perf.x86_64
 perf stat -a -- sleep 10
```


```
uptime

top -Hp pid

mpstat -P ALL 1

mpstat

top/prstat

pidstat/prstat

perf/dtrace/stap/oprofile

perf/cpustat

```

Basic attributes for characterizing CPU workload are
* Load averages (utilization + saturation)
* User-time to system-time ratio
* Syscall rate
* Voluntary context switch rate
* Interrupt rate


```

pidstat 1



free -h
cat /proc/meminfo
vmstat -s
vmstat -w 1



cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_available_frequencies
tuned-adm list
tuned-adm active
tuned-adm profile latency-performance
```





#### Network
```
netstat -antp

netstat -nltp

//System Activity Reporter

sar -n TCP,ETCP 1

sar -n UDP 1

sar -n DEV 1

ps -ef f


strace –tttT –p 313

tcpdump -i eth0 -w /tmp/out.tcpdump

lsof -iTCP -sTCP:ESTABLISHED

lscpu

more /proc/cpuinfo

ethtool eth0 

 iotop –d 5 -P
```

#### IO

```
#page size
/usr/bin/time -v date

cat /proc/meminfo

iostat -xz 1

iotop –d 5 -P
```
#### Memory



# Command

```
systemctl enable iptables.service
systemctl disable rabbitmq-server.service
systemctl list-unit-files --state=enabled

systemctl stop rabbitmq-server.service

```

```
lscpu

lsof
```

```
groupadd mariadb
useradd -s /sbin/nologin mariadb -g mariadb
```

```
ssh-keygen -t ecdsa -b 521
```


# Firewall

[firewall-cmd](https://firewalld.org/documentation/man-pages/firewall-cmd.html)



1、firewalld的基本使用  
启动： systemctl start firewalld  
查看状态： systemctl status firewalld   
停止： systemctl disable firewalld  
禁用： systemctl stop firewalld  
 
2.systemctl是CentOS7的服务管理工具中主要的工具，它融合之前service和chkconfig的功能于一体。  

启动一个服务：systemctl start firewalld.service  
关闭一个服务：systemctl stop firewalld.service  
重启一个服务：systemctl restart firewalld.service  
显示一个服务的状态：systemctl status firewalld.service  
在开机时启用一个服务：systemctl enable firewalld.service  
在开机时禁用一个服务：systemctl disable firewalld.service  
查看服务是否开机启动：systemctl is-enabled firewalld.service  
查看已启动的服务列表：systemctl list-unit-files|grep enabled  
查看启动失败的服务列表：systemctl --failed  

3.配置firewalld-cmd  
查看版本： firewall-cmd --version  
查看帮助： firewall-cmd --help  
显示状态： firewall-cmd --state  
查看所有打开的端口： firewall-cmd --zone=public --list-ports  
更新防火墙规则： firewall-cmd --reload  
查看区域信息:  firewall-cmd --get-active-zones  
查看指定接口所属区域： firewall-cmd --get-zone-of-interface=eth0  
拒绝所有包：firewall-cmd --panic-on  
取消拒绝状态： firewall-cmd --panic-off  
查看是否拒绝： firewall-cmd --query-panic  
 
那怎么开启一个端口呢  
添加  
firewall-cmd --zone=public --add-port=80/tcp --permanent    （--permanent永久生效，没有此参数重启后失效）  
firewall-cmd --zone=public --add-service=http --permanent
重新载入  
firewall-cmd --reload  
查看  
firewall-cmd --zone=public --query-port=80/tcp  
删除  
firewall-cmd --zone=public --remove-port=80/tcp --permanent  

```
firewall-cmd --zone=public --list-all
firewall-cmd --get-active-zones

```

```
#列出所有zone
firewall-cmd --get-zones
#增加一个zone
firewall-cmd --new-zone=kafka --permanet 
#重启防火墙
firewall-cmd --complete-reload 
#设置默认为kafka
firewall-cmd --set-default-zone=kafka
#查看默认的zone
firewall-cmd --get-default-zone
#要得到所有区域的配置
firewall-cmd --list-all-zones

#要查看默认的可用服务
firewall-cmd --get-services

#在同一台服务器上将 80 端口的流量转发到 12345 端口
firewall-cmd --zone="public" --add-forward-port=port=80:proto=tcp:toport=12345

将端口转发到另外一台服务器上
firewall-cmd --zone=public --add-masquerade
firewall-cmd --zone="public" --add-forward-port=port=80:proto=tcp:toport=8080:toaddr=123.456.78.9

```


[firewalld.richlanguage](https://jpopelka.fedorapeople.org/firewalld/doc/firewalld.richlanguage.html)
```
firewall-cmd --permanent --zone=public --add-rich-rule 'rule family="ipv4" source address=192.168.0.14 accept'

firewall-cmd --permanent --zone=public --add-rich-rule 'rule family="ipv4" source address="192.168.1.10" port port=22 protocol=tcp reject'

firewall-cmd --permanent --zone=public --add-rich-rule 'rule family=ipv4 source address=10.1.0.3 forward-port port=80 protocol=tcp to-port=6532'

firewall-cmd --permanent --zone=public --add-rich-rule 'rule family=ipv4 forward-port port=80 protocol=tcp to-port=8080 to-addr=172.31.4.2'


firewall-cmd --list-rich-rules

firewall-cmd --direct --get-all-chains
firewall-cmd --direct --get-all-rules

```

# iptables

```
vim /etc/sysconfig/iptables
systemctl restart iptables.service
systemctl status iptables.service

systemctl enable iptables.service
systemctl disable iptables.service
```
# Install

```
yum install epel-release
yum install ntfs-3g
efibootmgr -v

sudo grub-install /dev/sda
sudo grub-mkconfig -o /boot/grub/grub.cfg
```
