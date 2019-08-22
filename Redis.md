
[configuration](https://raw.githubusercontent.com/antirez/redis/4.0/redis.conf)


```
daemonize yes
pidfile /home/admredis/working/redis-adm/redis.6382.pid
port 6382
bind 127.0.0.1
timeout 0
#tcp-keepalive 1
loglevel warning
logfile /home/admredis/working/redis-adm/redis.6382.log
databases 1
rdbcompression no
maxmemory 20GB
maxmemory-policy allkeys-lru
appendonly no
appendfsync no
no-appendfsync-on-rewrite no
slowlog-log-slower-than 1000
slowlog-max-len 1024
#vm-enabled no
activerehashing yes
#glueoutputbuf yes
#save
#save 9000 100
dir /home/admredis/working/redis-adm
```
