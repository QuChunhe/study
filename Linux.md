
[Linux Performance](http://www.brendangregg.com/linuxperf.html)

[Linux Performance Analysis in 60,000 Milliseconds](https://medium.com/netflix-techblog/linux-performance-analysis-in-60-000-milliseconds-accc10403c55)


The	USE	Method	
- Utilization: busy time
- Saturation: queue length or queued time
- Errors: easy to interpret (objective)

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
```
cat /proc/vmstat | egrep "dirty|writeback"

	nr_dirty 3875
	nr_writeback 29
	nr_writeback_temp 0


# Command

top -Hp pid

pidstat 1

mpstat -P ALL 1

free -h

iostat -xz 1

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

cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_available_frequencies

