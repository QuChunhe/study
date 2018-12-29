# Idea

data
- partitions
- replication

task
- load balancing
- pipeline

# Papers
[1] Patrick O'Neil, Edward Cheng, Dieter Gawlick, Elizabetch O'Neil. The log-structured merge-tree (LSM-tree). Acta Informatica, 1996, 33(4): 351-385.




# Books

#### Ajay D. Kshemkalyani and Mukesh Singhal. Distributed Computing: Principles, Algorithms, and Systems. Cambridge University Press. 2008

[51] The timestamps assigned to events obey the fundamental monotonicity property; that is, if an event a causally affects an event b, then the timestamp of a is smaller than the timestamp of b.  
[52] Elements of T form a partially ordered set over a relation <. This relation is usually called the happened before or causal precedence. 


clock consistency condition v.t. strongly consistent

[52] Implementation of logical clocks requires addressing two issues [19]: data structures local to every process to represent logical time and a protocol (set of rules) to update the data structures to ensure the consistency condition.


A local logical clock v.t. A logical global clock,



# Course




# Open Source

## Zookeeper

### command

srvr

### configuration
```
tickTime=2000
dataDir=/var/lib/zookeeper
clientPort=2181
#the initLimit is the amount of time to allow followers to connect with a leader.
initLimit=20
#The syncLimit value limits how out-of-sync followers can be with the leader.
syncLimit=5
		
#server.X=hostname:peerPort:leaderPort
server.1=zoo1.example.com:2888:3888
server.2=zoo2.example.com:2888:3888
server.3=zoo3.example.com:2888:3888
```



## Kafka


https://github.com/gwenshap/kafka-examples

### Broker Configuration
```
zookeeper.connect
broker.id
```	

kafka-run-class.sh
```
LOG_DIR="/home/admkafka/logs"
```

```
nohup /usr/local/kafka_2.12-1.1.0/bin/kafka-server-start.sh /usr/local/kafka_2.12-1.1.0/config/server.properties &
nohup /usr/local/kafka_2.12-1.1.0/bin/zookeeper-server-start.sh /usr/local/kafka_2.12-1.1.0/config/zookeeper.properties &
```
#### Neha Narkhede, Gwen Shapira, and Todd Palino. Kafka: The Definitive Guide. O’Reilly Media, Inc. 2017

There are three primary methods of sending messages:
- Fire-and-forget
- Synchronous send
- Asynchronous send

[73]
Setting session.timeout.ms lower than the default will allow consumer groups to detect and recover from failure
sooner, but may also cause unwanted rebalances as a result of consumers taking longer to complete the poll loop or garbage collection. Setting session.timeout.ms higher will reduce the chance of accidental rebalance, but also means it will take
longer to detect a real failure.


[75]
receive.buffer.bytes and send.buffer.bytes: It can be a good idea to increase those when producers or consumers communicate with brokers in a different datacenter, because those network links typically have higher latency and lower bandwidth.


[77]
By setting auto.commit.offset=false, offsets will only be committed when the application explicitly chooses to do so. The simplest and most reliable of the commit APIs is commitSync().


[78]~[80]  
Combining Synchronous and Asynchronous Commits
- commitSync() will retry the commit until it either succeeds or encounters a nonretriable failure,
- commitAsync() will not retry

[86]  
Note that consumer.wakeup() is the only consumer method that is safe to call from a different thread.  
Before exiting the thread, you must call consumer.close().






## Spark

### Build

#if use scala 2.12
./dev/change-scala-version.sh 2.12

build/mvn -Pmesos -DskipTests clean package

[Running Spark on Mesos](https://spark.apache.org/docs/latest/running-on-mesos.html)

hadoop fs -copyFromLocal spark-2.4.0-bin-custom-spark.tgz  hdfs://master.hadoop:10000/spark/lib/

### Configuration

vim conf/spark-env.sh
```
# Options read by executors and drivers running inside the cluster
# - SPARK_LOCAL_IP, to set the IP address Spark binds to on this node
# - SPARK_PUBLIC_DNS, to set the public DNS name of the driver program
# - SPARK_CLASSPATH, default classpath entries to append
# - SPARK_LOCAL_DIRS, storage directories to use on this node for shuffle and RDD data
# - MESOS_NATIVE_JAVA_LIBRARY, to point to your libmesos.so if you use Mesos
MESOS_NATIVE_JAVA_LIBRARY=/usr/local/mesos/lib/libmesos.so
SPARK_EXECUTOR_URI=hdfs://master.hadoop:10000/spark/lib/spark-2.4.0-bin-custom-spark.tgz
SPARK_LOG_DIR=hdfs://master.hadoop:10000/spark/logs
SPARK_LOCAL_IP=192.168.1.5
SPARK_LOCAL_DIRS=/home/hadoop/spark
```

vim conf/spark-defaults.conf
```
spark.executor.uri  hdfs://master.hadoop:10000/spark/lib/spark-2.4.0-bin-custom-spark.tgz
spark.master        mesos://192.168.1.5:7077
spark.eventLog.dir  hdfs://master.hadoop:10000/spark/logs
```
vim /etc/profile
```
SPARK_HOME=/usr/local/spark
EXPORT SPARK_HOME
```

configure hostname for every nodes   

vim /etc/hostname
```
node7.beijing
```
vim /etc/sysconfig/network
```
HOSTNAME=node7.beijing
```
vim /etc/hosts
```
192.168.1.7 node7.beijing
192.168.1.6 node6.beijing
192.168.1.5 node5.beijing
192.168.1.3 node3.beijing
192.168.1.2 node2.beijing
```

```
hostname node5.beijing
```

### Run

```
/usr/local/spark/sbin/start-mesos-dispatcher.sh -m mesos://192.168.1.5:5050 -h 192.168.1.5 --webui-port 8087 --name SparkFramework

http://192.168.1.5:8087/
```
