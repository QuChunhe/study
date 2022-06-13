[Harvard CS 229r: Algorithms for Big Data](http://people.seas.harvard.edu/~minilek/cs229r/)

UIUC CS598CSC


[Sketching Algotithms](https://www.sketchingbigdata.org)

# Hive


libexec/conf/hive-default.xml.template --> libexec/conf/hive-site.xml

mysql-connector-java-5.1.42-bin.jar --> libexec/lib/


‘系统偏好设置’->‘共享’->‘远程登录’，打开远程登录选项

```shell

ssh-keygen -t ed25519 


ssh-copy-id [-i [identity_file]] [user@]machine

chmod 600 ~/.ssh/authorized_keys

HADOOP_COMMON_HOME=$HADOOP_HOME

./hdfs namenode -format



./schematool -initSchema -dbType mysql

./hive --service metastore &


```


[HDFS](http://localhost:9870/)


TEZ：是基于Hadoop YARN之上的DAG（有向无环图，Directed Acyclic Graph）计算框架。核心思想是将Map和Reduce两个操作进一步拆分，即Map被拆分成Input、Processor、Sort、Merge和Output， Reduce被拆分成Input、Shuffle、Sort、Merge、Processor和Output等。这样，这些分解后的元操作可以任意灵活组合，产生新的操作，这些操作经过一些控制程序组装后，可形成一个大的DAG作业，从而可以减少Map/Reduce之间的文件存储，同时合理组合其子过程，也可以减少任务的运行时间。





ORC的全称是(Optimized Record Columnar)
