

统计学方法与数据分析

## Streaming Process

A. G. Psaltis. Streaming Data: Understanding the real-time pipeline. Manning Publications Co. 2017

![The streaming data architectural blueprint](https://github.com/QuChunhe/study/pics/TheStreamingDataArchitecturalBlueprint.JPG)

https://github.com/QuChunhe/study/blob/master/pics/TheStreamingDataArchitecturalBlueprint.JPG


|Classification  | Example |Latency measured in |Tolerance for delay|
| :------------ | :------------ | :------------ | :------------| 
|Hard |Pacemaker, anti-lock brakes |Microseconds–milliseconds |None—total system failure, potential loss of life|
|Soft |	Airline reservation system,online stock quotes, VoIP (Skype) |	Milliseconds–seconds |Low—no system failure, no life at risk|  
|Near |Skype video, home automation |Seconds–minutes| High—no system failure,no life at risk |


 The interaction patterns fall into one of the following categories:
* Request/response pattern
    * Basic request/response pattern.Three common strategies can overcome this limitation: one on the client side, one
on the service side, and one a combination of the two.
    * Client making asynchronous request to the service: half-async pattern
    * Service-side half-async pattern
    * Service async request/response pattern：full-async
* Publish/subscribe pattern
* One-way pattern: “fire and forget” message pattern
* Request/acknowledge pattern
* Stream pattern

The two primary approaches to implementing fault tolerance, checkpointing and logging, are designed to protect against data loss and enable speedy recovery of the crashed node.

Numerous checkpoint-based protocols are available to choose from in the literature, but when you boil it down, the following two
characteristics can be found in all of them:
* Global snapshot—The protocols require that a snapshot of the global state of the whole system be regularly saved to storage somewhere, not merely the state of the collection tier.
* Potential for data loss—The protocols only ensure that the system is recoverable up to the most recent recorded global state; any messages that were processed and generated afterward are lost.

Part of the complexity of checkpointing that’s eliminated is the global snapshot, and therefore the management and generation
of the global state. In the end, the goals of the logging technique manifest themselves in the basic idea that underpins all of the logging techniques: if a message can be replayed, then the system can reach a global consistent state without the need for a global snapshot.


Implementing a logging protocol frees us from worrying about maintaining global state, enabling us to focus on how to add
fault tolerance to the collection tier. To do this we’re going to discuss two classic techniques, receiver-based message logging (RBML) and sender-based message logging (SBML), and an emerging technique called hybrid message logging (HML).



## Python

A programming paradigm is a style, or “way” of programming. Major programming
paradigms are,
* Imperative
* Logical
* Functional
* Object-Oriented



```
import os
if 'PYSPARK_SUBMIT_ARGS' in os.environ:
    del os.environ['PYSPARK_SUBMIT_ARGS']

from pyspark import SparkContext, SparkConf
import random

sc_conf = SparkConf()
sc_conf.setAppName("Pi")
sc_conf.setMaster('local')
sc_conf.set('spark.executor.memory', '1g')
sc_conf.set('spark.executor.cores', '8')
sc_conf.set('spark.cores.max', '10')
sc_conf.set('spark.logConf', True)

sc =  SparkContext(conf=sc_conf)

num_samples = 100000000
def inside(p):     
  x, y = random.random(), random.random()
  return x*x + y*y < 1
count = sc.parallelize(range(0, num_samples)).filter(inside).count()
pi = 4 * count / num_samples
print(pi)
sc.stop()
```



```
from cassandra.cluster import Cluster
from cassandra.policies import DCAwareRoundRobinPolicy
from cassandra.cluster import EXEC_PROFILE_DEFAULT
from cassandra.cluster import ExecutionProfile

profile = ExecutionProfile(request_timeout=3000)
cluster = Cluster(contact_points=['192.168.*.*','192.168.*.*'],\
                  execution_profiles={EXEC_PROFILE_DEFAULT: profile})
session = cluster.connect()
session.set_keyspace('revenue_report')
rows = session.execute("SELECT date, SUM(revenue)\
                        FROM * \
                        WHERE date>'2019-02-27'\
                        GROUP BY date ALLOW FILTERING ")
for row in rows :
    print(row[0], " ",row[1])
cluster.shutdown()
```

```

    easy_install mysql-python (mix os)
    pip install mysql-python (mix os/ python 2)
    pip install mysqlclient (mix os/ python 3)
    apt-get install python-mysqldb (Linux Ubuntu, ...)
    cd /usr/ports/databases/py-MySQLdb && make install clean (FreeBSD)
    yum install MySQL-python (Linux Fedora, CentOS ...)

```
