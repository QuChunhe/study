
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
```

# Performance

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
```
