
[Linux Performance](http://www.brendangregg.com/linuxperf.html)

[Linux Performance Analysis in 60,000 Milliseconds](https://medium.com/netflix-techblog/linux-performance-analysis-in-60-000-milliseconds-accc10403c55)


[Linux System and Performance Monitoring](http://www.ufsdump.org/papers/linuxcon2010-linux-monitoring.pdf)

应用类型
* IO密集型(IO Bound)
* CPU密集型(CPU Bound)

[宋宝华：网上坑爹的Linux资料汇总之内存管理](https://mp.weixin.qq.com/s/4N6MxrR3t68WqJhaOcDJ2Q)  
以文件系统中文件为背景的称为cache，以裸分区/dev/sdax等为背景称为buffer

# Setting

[The /proc filesystem documentation ](http://linuxinsight.com/proc_filesystem.html)
  
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

vm.max_map_count = 1048575
```
```
 sysctl -p
 sysctl -p --system
```
cat /proc/vmstat | egrep "dirty|writeback"

	nr_dirty 3875
	nr_writeback 29
	nr_writeback_temp 0


# Performance

## Methodologies  
[The USE Method](http://www.brendangregg.com/usemethod.html)
The USE Method can be summarized as:  For every resource, check utilization, saturation, and errors.

Terminology definitions:
* resource: all physical server functional components (CPUs, disks, busses, ...) [1]
* utilization: the average time that the resource was busy servicing work [2]
* saturation: the degree to which the resource has extra work which it can't service, often queued
* errors: the count of error events


### Monitoring

#### CPU

[The PMCs of EC2: Measuring IPC](http://www.brendangregg.com/blog/2017-05-04/the-pmcs-of-ec2.html)
```
 yum install perf.x86_64
 perf stat -a -- sleep 10
```
For real-world applications, here's how I'd interpret the IPC:
* IPC < 1: likely stall cycle bound, also likely memory bound (more PMCs can confirm). Stall cycles are when the CPU isn't making forward progress, likely because it's waiting on memory I/O. In this case, look to tune memory usage: allocate fewer or smaller objects, do zero copy, look at NUMA and memory placement tuning. A CPU flame graph will show which code is on-CPU during these stall cycles, and should be clues for were to look for memory usage.
* IPC > 1: likely instruction bound. Look to tune instructions: a CPU flame graph will show which code is on-CPU doing instructions: find ways to reduce executed code.

```
top -Hp pid

pidstat 1

mpstat -P ALL 1

free -h
cat /proc/meminfo
vmstat -s
vmstat -w 1



cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_available_frequencies
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
