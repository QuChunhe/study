
[Linux Performance](http://www.brendangregg.com/linuxperf.html)

[Linux Performance Analysis in 60,000 Milliseconds](https://medium.com/netflix-techblog/linux-performance-analysis-in-60-000-milliseconds-accc10403c55)


[Linux System and Performance Monitoring](http://www.ufsdump.org/papers/linuxcon2010-linux-monitoring.pdf)

[Resource Management Guide](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/resource_management_guide/index)

应用类型
* IO密集型(IO Bound)
* CPU密集型(CPU Bound)

[宋宝华：网上坑爹的Linux资料汇总之内存管理](https://mp.weixin.qq.com/s/4N6MxrR3t68WqJhaOcDJ2Q)  
以文件系统中文件为背景的称为cache，以裸分区/dev/sdax等为背景称为buffer


[Brendan Gregg,LISA2019 Linux Systems Performance](http://www.brendangregg.com/blog/2020-03-08/lisa2019-linux-systems-performance.html)

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
* 硬件选择
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
    
    
 For Linux kernels, the scheduling classes are   
* RT: provides fixed and high priorities for real-time workloads
* O(1): The O(1) scheduler was introduced in Linux 2.6 as the default time-sharing scheduler for user processes.
* CFS: Completely fair scheduling was added to the Linux 2.6.23 kernel as the default timesharing scheduler for user processes.   
    
    
Scheduler policies are as follows:    
* RR: SCHED_RR is round-robin scheduling.
* FIFO: SCHED_FIFO is first-in first-out scheduling, which continues running the thread at the head of the run queue until it voluntarily leaves, or until a higher-priority thread arrives.
* NORMAL: SCHED_NORMAL (previously known as SCHED_OTHER) is time-sharing scheduling and is the default for user processes.
* BATCH: SCHED_BATCH is similar to SCHED_NORMAL, but with the expectation that the thread will be CPU-bound and should not be scheduled to interrupt other I/O-bound interactive work    
    
 
Basic attributes for characterizing CPU workload are
* Load averages (utilization + saturation)
* User-time to system-time ratio
* Syscall rate
* Voluntary context switch rate
* Interrupt rate  
    
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

```
cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_governor，发现CPU工作模式为powersave。
tuned-adm profile latency-performance修改工作模式，解决问题
```

错误信息
```
The current inotify(7) watch limit is too low
```
解决方案

```
vim etc/sysctl.conf

fs.inotify.max_user_watches = 524288

sysctl -p
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

对所有用户有效在/etc/profile增加以下内容。只对当前用户有效在Home目录下的
.bashrc或.bash_profile里增加下面的内容：
(注意：等号前面不要加空格,否则可能出现 command not found)
```
#在PATH中找到可执行文件程序的路径。
export PATH =$PATH:$HOME/bin

#gcc找到头文件的路径
C_INCLUDE_PATH=/usr/include/libxml2:/MyLib
export C_INCLUDE_PATH

#g++找到头文件的路径
CPLUS_INCLUDE_PATH=$CPLUS_INCLUDE_PATH:/usr/include/libxml2:/MyLib
export CPLUS_INCLUDE_PATH

#找到动态链接库的路径
LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/MyLib
export LD_LIBRARY_PATH

#找到静态库的路径
LIBRARY_PATH=$LIBRARY_PATH:/MyLib
export LIBRARY_PATH
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
* resource: all physical server functional components (CPUs, disks, busses, ...) 
* utilization: the average time that the resource was busy servicing work 
* saturation: the degree to which the resource has extra work which it can't service, often queued
* errors: the count of error events


### Monitoring

[Utilization is Virtually Useless as a Metric](http://www.hpts.ws/papers/2007/Cockcroft_HPTS-Useless.pdf)

Headroom is available usable resources
* Total Capacity minus Peak Utilization and Margin
* Applies to CPU, RAM, Net, Disk and OS

![headroom](https://github.com/QuChunhe/study/raw/master/pics/Headroom.png)

Utilization
* Utilization is the proportion of busy time
* Always defined over a time interval


#### CPU

[CPU Utilization is Wrong](http://www.brendangregg.com/blog/2017-05-09/cpu-utilization-is-wrong.html)

The metric we call CPU utilization is really "non-idle time": the time the CPU was not running the idle thread. Your operating system kernel (whatever it is) usually tracks this during context switch. If a non-idle thread begins running, then stops 100 milliseconds later, the kernel considers that CPU utilized that entire time.

Nowadays, CPUs have become much faster than main memory, and waiting on memory dominates what is still called "CPU utilization". When you see high %CPU in top(1), you might think of the processor as being the bottleneck – the CPU package under the heat sink and fan – when it's really those banks of DRAM.

多CPU、多核和超线程加剧了CPU等待内存的停顿。

CPU处理指令的一般步骤
1. Instruction Fetch. Obtain instruction from program memory. The Program Counter (PC) points to the instruction to be processed
2. Instruction Decode. Determine required actions and instruction size
3. Operand Fetch. Locate and obtain operand data. From data memory or registers
4. Execute..Compute result value or status
5. Result Store. Deposit results in storage (data memory or register) for later use

The average instruction executed takes a number of cycles per instruction (CPI) to be completed.
– Measured in: cycles/instruction, CPI, Or Instructions Per Cycle (IPC)

CPU has a fixed clock cycle time C = 1/clock rate
– Measured in: seconds/cycle


CPU performance equation
```
CPU execution time = PU clock cycles x Clock cycle
                   = Instruction count x CPI x Clock cycle
T = I x CPI x C
```

run-queue latency or dispatcher-queue latency, scheduler latency.

cache warmth, CPU affinity

程序执行时间 = 程序总指令数 x 每 CPU 时钟周期时间 x 每指令执行所需平均时钟周期数

cycles-per-instruction(CPI) 每指令周期数; instructions per cycle (IPC) 每周期指令数

CPI = 1/IPC

Execution Time (T) = Instruction Count x Time Per Cycle X CPI

Cycles per instruction (CPI) is an important high-level metric for describing where a CPU is
spending its clock cycles and for understanding the nature of CPU utilization. This metric may also be
expressed as instructions per cycle (IPC), the inverse of CPI.

For real-world applications, here's how I'd interpret the IPC:
* IPC < 1: likely stall cycle bound, also likely memory bound (more PMCs can confirm). Stall cycles are when the CPU isn't making forward progress, likely because it's waiting on memory I/O. In this case, look to tune memory usage: allocate fewer or smaller objects, do zero copy, look at NUMA and memory placement tuning. A CPU flame graph will show which code is on-CPU during these stall cycles, and should be clues for were to look for memory usage.
* IPC > 1: likely instruction bound. Look to tune instructions: a CPU flame graph will show which code is on-CPU doing instructions: find ways to reduce executed code.




CPU utilization  

The measure of CPU utilization spans all clock cycles for eligible activities, including memory
stall cycles. It may seem a little counter intuitive, but a CPU may be highly utilized because it is often
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


* Context Switches   
The higher the volume of context switches on a system, the more work the kernel has to do in
order to manage the scheduling of processes.
* The Run Queue   
A very popular term called “load” is often used to describe the state of the run queue. The system load is a combination of the amount of process threads currently executing along with the amount of threads in the CPU run queue.
* CPU Utilization
   * User Time
   * System Time
   * Wait IO
   * Idle

[The PMCs of EC2: Measuring IPC](http://www.brendangregg.com/blog/2017-05-04/the-pmcs-of-ec2.html)
```
 yum install perf.x86_64
 perf stat -a -- sleep 10
```

```
# uptime gives a one line display of the following information.  The current time, 
# how long the system has been running, how many users are currently logged on, and 
# the system load averages for the past 1, 5, and 15 minutes
uptime
```
 scheduling policies in a LINUX environment
```
chrt -m 
SCHED_OTHER min/max priority	: 0/0
SCHED_FIFO min/max priority	: 1/99
SCHED_RR min/max priority	: 1/99
SCHED_BATCH min/max priority	: 0/0
SCHED_IDLE min/max priority	: 0/0
SCHED_DEADLINE min/max priority	: 0/0


1. SCHED_OTHER   the standard round-robin time-sharing policy
2. SCHED_BATCH   for "batch" style execution of processes
3. SCHED_IDLE    for running very low priority background jobs.
4. SCHED_FIFO    a first-in, first-out policy
5. SCHED_RR      a round-robin policy
```
There are 2 types of processes, the normal ones and the real time.

Nice value is a user-space and priority PR is the process's actual priority that use by Linux kernel. In linux system priorities are 0 to 139 in which 0 to 99 for real time and 100 to 139 for users. Nice value range is -20 to +19 where -20 is highest, 0 default and +19 is lowest.   
PR is calculated as follows:
* for normal processes: PR = 20 + NI (NI is nice and ranges from -20 to 19)
* for real time processes: PR = - 1 - real_time_priority (real_time_priority ranges from 1 to 99)

There are a total of 140 priorities and two distinct priority ranges implemented in Linux. The first one is a nice value (niceness) which ranges from -20 (highest priority value) to 19 (lowest priority value) and the default is 0, this is what we will uncover in this guide. The other is the real-time priority, which ranges from 1 to 99 by default, then 100 to 139 are meant for user-space.
* NI – is the nice value, which is a user-space concept, while
* PR or PRI – is the process’s actual priority, as seen by the Linux kernel.

```
Total number of priorities = 140
Real time priority range(PR or PRI):  0 to 99 
User space priority range: 100 to 139
PR = 0 to 39 which is same as 100 to 139
```

But if you see a **rt** rather than a number as shown in the screenshot below, it basically means the process is running under real-time scheduling priority.

```
top -Hp pid
# The scheduling priority of the task.  If you see `rt' in this field, it means 
# the task is running under real time scheduling priority.
# The status of the task which can be one of:
#     D = uninterruptible sleep
#     R = running
#     S = sleeping
#     T = stopped by job control signal
#     t = stopped by debugger during trace
#     Z = zombie
# 
# command
#     s – 改变画面更新频率
#     l – 关闭或开启第一部分第一行 top 信息的表示
#     t – 关闭或开启第一部分第二行 Tasks 和第三行 Cpus 信息的表示
#     m – 关闭或开启第一部分第四行 Mem 和 第五行 Swap 信息的表示
#     N – 以 PID 的大小的顺序排列表示进程列表
#     P – 以 CPU 占用率大小的顺序排列进程列表
#     M – 以内存占用率大小的顺序排列进程列表
#     h – 显示帮助
#     n – 设置在进程列表所显示进程的数量
#     q – 退出 to
#     f 键可以选择显示的内容
```
* VIRT  --  Virtual Memory Size (KiB)
* RES  --  Resident Memory Size (KiB)
* SHR  --  Shared Memory Size (KiB)
* DATA  --  Data + Stack Size (KiB)
* CODE  --  Code Size (KiB)

* PID     进程id
* PPID    父进程id
* RUSER   Realusername
* UID     进程所有者的用户id
* USER    进程所有者的用户名
* GROUP   进程所有者的组名
* TTY     启动进程的终端名。不是从终端启动的进程则显示为?
* PR      优先级
* NI      nice值。
* P       最后使用的CPU，仅在多CPU环境下有意义
* %CPU    上次更新到现在的CPU时间占用百分比
* TIME    进程使用的CPU时间总计，单位秒
* TIME+   进程使用的CPU时间总计，单位1/100秒
* %MEM    进程使用的物理内存百分比
* VIRT    进程使用的虚拟内存总量，单位kb。VIRT=SWAP+RES
* SWAP    进程使用的虚拟内存中，被换出的大小，单位kb。
* RES     进程使用的、未被换出的物理内存大小，单位kb。RES=CODE+DATA
* CODE    可执行代码占用的物理内存大小，单位kb
* DATA    可执行代码以外的部分(数据段+栈)占用的物理内存大小，单位kb
* SHR     共享内存大小，单位kb
* nFLT    页面错误次数
* nDRT    最后一次写入到现在，被修改过的页面数。
* S       进程状态。
* COMMAND    命令名/命令行
* WCHAN    若该进程在睡眠，则显示睡眠中的系统函数名

```
top -hv|-bcHiOSs -d secs -n max -u|U user -p pid -o fld -w [cols]
COMMAND-LINE Options
  -h | -v  :Help/Version
  -d  :Delay-time interval as:  -d ss.t (secs.tenths)
  -H  :Threads-mode operation
  -p  :Monitor-PIDs mode as:  -pN1 -pN2 ...  or  -pN1,N2,N3 ...

Global-defaults
              A - Alt display      Off (full-screen)
            * d - Delay time       1.5 seconds
            * H - Threads mode     Off (summarize as tasks)
              I - Irix mode        On  (no, `solaris' smp)
            * p - PID monitoring   Off (show all processes)
            * s - Secure mode      Off (unsecured)
              B - Bold enable      On  (yes, bold globally)
           Summary-Area-defaults
              l - Load Avg/Uptime  On  (thus program name)
              t - Task/Cpu states  On  (1+1 lines, see `1')
              m - Mem/Swap usage   On  (2 lines worth)
              1 - Single Cpu       Off (thus multiple cpus)
           Task-Area-defaults
              b - Bold hilite      Off (use `reverse')
            * c - Command line     Off (name, not cmdline)
            * i - Idle tasks       On  (show all tasks)
              J - Num align right  On  (not left justify)
              j - Str align right  Off (not right justify)
              R - Reverse sort     On  (pids high-to-low)
            * S - Cumulative time  Off (no, dead children)
            * u - User filter      Off (show euid only)
            * U - User filter      Off (show any uid)
              V - Forest view      On  (show as branches)
              x - Column hilite    Off (no, sort field)
              y - Row hilite       On  (yes, running tasks)
              z - color/mono       On  (show colors)
```
* us(user)：表示 CPU 在用户态运行的时间百分比，通常用户态 CPU 高表示有应用程序比较繁忙。典型的用户态程序包括：数据库、Web 服务器等。
* sy(sys)：表示 CPU 在内核态运行的时间百分比（不包括中断），通常内核态 CPU 越低越好，否则表示系统存在某些瓶颈。
* ni(nice)：表示用 nice 修正进程优先级的用户态进程执行的 CPU 时间。nice 是一个进程优先级的修正值，如果进程通过它修改了优先级，则会单独统计 CPU 开销。
* id(idle)：表示 CPU 处于空闲态的时间占比，此时，CPU 会执行一个特定的虚拟进程，名为 System Idle Process。
* wa(iowait)：表示 CPU 在等待 I/O 操作完成所花费的时间，通常该指标越低越好，否则表示 I/O 存在瓶颈，可以用 iostat 等命令做进一步分析。
* hi(hardirq)：表示 CPU 处理硬中断所花费的时间。硬中断是由外设硬件（如键盘控制器、硬件传感器等）发出的，需要有中断控制器参与，特点是快速执行。
* si(softirq)：表示 CPU 处理软中断所花费的时间。软中断是由软件程序（如网络收发、定时调度等）发出的中断信号，特点是延迟执行。
* st(steal)：表示 CPU 被其他虚拟机占用的时间，仅出现在多虚拟机场景。如果该指标过高，可以检查下宿主机或其他虚拟机是否异常。


平均负载（Load Average）是指单位时间内，系统处于 可运行状态（Running / Runnable） 和 不可中断态 的平均进程数，也就是 平均活跃进程数。
可运行态进程包括正在使用 CPU 或者等待 CPU 的进程；不可中断态进程是指处于内核态关键流程中的进程，并且该流程不可被打断。  
这 3 个数字分别表示 1分钟、5分钟、15分钟内系统的平均负载。

* UPTIME and LOAD Averages
   * program or window name, depending on display mode
   * current time and length of time since last boot
   * total number of users
   * system load avg over the last 1, 5 and 15 minutes
* TASK and CPU States
   * us, user    : time running un-niced user processes
   * sy, system  : time running kernel processes
   * ni, nice    : time running niced user processes
   * id, idle    : time spent in the kernel idle handler
   * wa, IO-wait : time waiting for I/O completion
   * hi : time spent servicing hardware interrupts
   * si : time spent servicing software interrupts
   * st : time stolen from this vm by the hypervisor
* MEMORY Usage


()[]
Linux always tries to use RAM to speed up disk operations by using available memory for buffers (file system metadata) and cache (pages with actual contents of files or block devices). 

```
mpstat -P ALL 1

mpstat -I SCPU
# cat proc/softirqs


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


CPU cache warmth. On Linux-based systems, the exclusive CPU sets approach can be implemented using cpusets


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

```
yum install dstat.noarch 

dstat -N em1 1
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

vim authorized_keys
chmod g-w authorized_keys
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

# Log


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


# Disk


```
du -h --max-depth=1
```

# Info

查看CPU信息

```
cat /proc/cpuinfo

processor	: 2

physical id	: 0
siblings	: 4
core id		: 2
cpu cores	: 4

```
查看 CPU 个数：
```
cat /proc/cpuinfo | grep 'physical id' | sort | uniq | wc -l
```
查看 CPU 物理核数：
```
cat /proc/cpuinfo | grep 'cpu cores' | sort | uniq
```
查看 CPU 逻辑核数：
```
cat /proc/cpuinfo | grep 'siblings' | sort | uniq
```

display information about the CPU architecture
```
lscpu
```


top free ps df 

sysstat(sar,mpstat, iostat) dstat, iotop

netstat ethstatus arping

perf

pstack

free 内存泄漏判断


ext4 --> xfs

实列解析MySQL性能瓶颈　　　DBA登入服务器后应该先关注啥

set long_query_time=0

select benchmark

list hardware
```
lshw
```
# 杂项

在CentOS中GCC的版本比较老旧。造成无法编译需要c11等版本的软件.

可以选择安装特定版本的devtoolset，其对应响应版本的gcc

```bash
yum search devtoolset

yum install devtoolset-7-all.x86_64

```
在编译软件前，使用如下命令指定后续编译使用的gcc
```bash
scl enable devtoolset-7 bash
```


```
tracker reset -r
```



邹恒明著，计算机的心智：操作系统之哲学原理，机械工业出版社，2009

Wiliam Stallings, Operating Systems: Internals and Design Princiles (Ninth Edition),Pearson Education Limited, 2018

https://www.drdobbs.com/parallel/the-many-faces-of-deadlock/209900973

进程管理、内存管理和文件管理是操作系统的三大核心功能。

进程=程序+执行

进程的三种状态：就绪、执行和阻塞

There are fundamentally two types of processes in Linux
* Foreground processes
* Background processes

Daemons: These are special types of background processes that start at system startup and keep running forever as a service; they don’t die. They are started as system tasks (run as services), spontaneously. 

You can as well run a process directly from the background using the ampersand, **& sign**.

You can also use **nohup** command, which also enables a process to continue running in the background when a user exits a shell.

There are two conventional ways used for creating a new process in Linux:
* Using The System() Function – this method is relatively simple, however, it’s inefficient and has significantly certain security risks.
* Using fork() and exec() Function – this technique is a little advanced but offers greater flexibility, speed, together with security.

process ID (PID)   parent processes ID (PPID),

Print a list of signal names, or convert the given signal number to a name.
```
kill -l
```
The following are signals which are useful to a system user:
* SIGHUP 1 – sent to a process when its controlling terminal is closed.
* SIGINT 2 – sent to a process by its controlling terminal when a user interrupts the process by pressing [Ctrl+C].
* SIGQUIT 3 – sent to a process if the user sends a quit signal [Ctrl+D].
* SIGKILL 9 – this signal immediately terminates (kills) a process and the process will not perform any clean-up operations.
* SIGTERM 15 – this a program termination signal (kill will send this by default).
* SIGTSTP 20 – sent to a process by its controlling terminal to request it to stop (terminal stop); initiated by the user pressing [Ctrl+Z].


interprocess communication
* pipe, named pipe
* socket
* signal
* semaphore
* shared memory
* message queue


线程是进程厘米的一个执行上下文，或者执行序列。

线程共享的资源：地址空间、全局变量、文件、子进程。

线程独享的资源： 程序计数器、寄存器、栈、状态字。

线程的用处
1. 在一个应用中（一个process）中实现并发，同时执行多个任务
2. 线程比进程更轻便，与进程相比，线程更容易地被创建和销毁
3. 重复利用CPU的。如果线程数<=CPU总核数，可以并发执行；如果线程数>CPU总核数，使得I/O操作和计算操作可以相互重叠。
* 



lock unlock

barrier

动态资源使用
1. 请求资源
2. 使用资源
3. 释放资源

资源的分类
* 可重用的
* 有消耗的

一组线程以不适当方式竞争资源，造成相互阻塞和相互等待的问题。在并发编程中，非常常见的问题，在极端情况下导致整个程序无法运行。

产生死锁的必要条件(Coffman 1971)
1. 互斥使用 (Mutual exclusion)：一个资源在一段时间内仅仅许可一个进程使用。
2. 持有等待 (Hold and Wait)：在等待分配其他资源时，进程继续持有已经分配给自己的资源。
3. 不能抢占 (No Preemption)：不能强迫持有一个资源的进程放弃此资源。
4. 循环等待 (Circular Wait)。

1,2,3是必要条件

Deadlock can happen whenever there is a blocking (or waiting) cycle among concurrent tasks.

deadlock: When N concurrent tasks enter a cycle where each one is blocked waiting for the next.

Clearly, blocking operations include all kinds of blocking synchronization


Deadlock Modelling：Resource-Allocation Graph 

A set of resource categories, { R1, R2, R3, . . ., RN }, which appear as square nodes on the graph. Dots inside the resource nodes indicate specific instances of the resource. ( E.g. two dots might represent two laser printers. ) 

A set of processes, { P1, P2, P3, . . ., PN } 

Request Edges - A set of directed arcs from Pi to Rj, indicating that process Pi has requested Rj, and is currently waiting for that resource to become available. 

Assignment Edges - A set of directed arcs from Rj to Pi indicating that resource Rj has been allocated to process Pi, and that Pi is currently holding resource Rj. 


经典的同步问题
* Bounded-Buffer Problem
* Readers and Writers problem
* Dinning-Philosophers Problem

哲学家就餐问题

避免死锁：检查死锁
许可死锁：死锁的恢复，许可抢占


消除死锁的必要条件
* 消除资源独占条件
* 消除保持和请求条件
* 消除非抢占条件
* 消除循环等的

死锁(deadlock)， 活锁(livelock)， 饥饿(Starvation)

 

First, to prevent locking cycles within the code you control, use lock hierarchies and other ordering techniques to ensure that your program always acquires all mutexes in the same order。

Second, to prevent many kinds of message cycles, disciplines have been proposed to express contracts on communication channels, which helps to impose a known ordering on messages.

Probably the best you can do today is to roll your own deadlock detection in code, by adopting a discipline like the following:
* Identify every condition or resource that can be waited for (a mutex, a message, a value of an atomic variable, an exclusive use of a file) and give it a unique name by creating a dummy object to represent it.
* Instrument every "start wait" and "end wait" point in your code by calling two helper functions: The first records that a condition or resource is about to be waited for (e.g,. StartWait(thing)) and should internally record the current thread's ID and the thing being waited for; it can also check to see if there is now a waiting cycle among threads and resources, and report the deadlock if that occurs. The second records that a wait has ended (e.g., EndWait(thing)) and will remove the waiting edge.


ThreadMXBean: ManagementFactory.getThreadMXBean(), findDeadlockedThread()


基本word读写操作是原子性的

对于特点数据结构的独占访问，使用CAS（Compare-and-Swap)，或者TAS（test-and-set)指令
