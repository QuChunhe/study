
大数据（Big Data）包括两个部分
* 大数据存储，例如HBase，Cassandra等
* 大数据处理，例如Yarn和Flink等。
不同于MySQL这类关系型数据，大数据存储主要面向于日志型数据，这类数据的操作特点是多读、少写和不改，也就是数据一旦被存储，就不会被更改或者更新，从而无需复杂的事务机制。因此，大数据存储系统往往支持横向扩展，而放弃分布式事务。

类似地，大数据处理系统为了实现横向扩展能力，而放弃了复杂的处理计算，通常仅仅支持具有良好并行（Embarrassingly Parallel）能力的计算，例如SUM、MAX和MAP这类能够轻易分而治之的计算。对于一些复杂的处理，需要根据特定的应用需求和处理模式进行定制开发，通常并不具有良好地可扩展性。

与传统的基于数理统计的数据分析相比，大数据处理具有如下两个特点：
1）处理全量或者海量数据。在传统统计分析中，基于合理设计的采样，仅仅需要处理一小部分数据，就能够获得所需要的结论，而大数据分析往往要求处理海量的数据，甚至全量数据。
2）重视小概率的事件。在传统统计分析中，重视大概率事件，忽略了那些小概率事件或者因素。虽然单类事件或者因素的概率很小，但是这些小概率事件或者因素却很多，即存在长尾分布（Long-Tailed Distribution），而大数据处理非常适合这类场景，从大概率事件到小概率事件都能够处理。
因此，传统的统计分析和大数据处理往往针对于不同的需求和场景，不是相互替代，而是相互补充的关系。例如，对于收视率调查，传统的统计分析就能够非常完美的解决，而不需要大数据处理，但是如果需要向用户个性化的推荐不同的视频内容，那么往往需要大数据处理的支持。



No data, No Truth

No Analytic, No understanding

No Programming, No Cognition

数据分析在实际系统应用的几个阶段
* 支持分析
* 辅助决策
* 协助操作
* 自动处理

数据分析的三个方面
* 数学基础
* 技术实现
* 业务解释


人类知识<-->机器规则
* 将人类已有的知识应用到机器处理规则
* 从机器学得的规则提炼和总结为人类知识

系统的输入与输出
* 输入：可能的各种相关数据
* 输出：统计报表、决策建议和控制动作

统计学方法与数据分析

## Streaming Process

A. G. Psaltis. Streaming Data: Understanding the real-time pipeline. Manning Publications Co. 2017

![The streaming data architectural blueprint](pics/TheStreamingDataArchitecturalBlueprint.JPG)




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

[Apache Superset](https://superset.apache.org/docs/installation/installing-superset-using-docker-compose)