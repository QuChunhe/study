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

hadoop dfsadmin -safemode leave

./schematool -initSchema -dbType mysql

./hive --service metastore &



```


[HDFS 3](http://localhost:9870/)

[HDFS 2](http://127.0.0.1:50070/dfshealth.html#tab-overview)

```sql
set execution.result-mode=tableau;

set read.tasks=1;
set write.tasks=1;
set path=hdfs://127.0.0.1:9000/user/hudi/warehouse;
set read.streaming.enabled=false;
```

export JAVA_HOME=/usr/local/Cellar/openjdk@8/1.8.0+322


export JAVA_HOME=/usr/local/opt/openjdk@8

export HADOOP_CLASSPATH=`$HADOOP_HOME/bin/hadoop classpath`

sbin/yarn-daemon.sh start timelineserver

./bin/yarn --daemon start timelineserver

/usr/local/flink-1.14.4/bin/sql-client.sh embedded -j /usr/local/hudi/hudi-flink-bundle/target/hudi-flink1.14-bundle_2.12-0.11.0.jar -j /usr/local/flink-cdc/flink-sql-connector-mysql-cdc-2.2.1.jar shell


https://developer.aliyun.com/article/852223

https://www.jianshu.com/p/d4a372809e3d

TEZ：是基于Hadoop YARN之上的DAG（有向无环图，Directed Acyclic Graph）计算框架。核心思想是将Map和Reduce两个操作进一步拆分，即Map被拆分成Input、Processor、Sort、Merge和Output， Reduce被拆分成Input、Shuffle、Sort、Merge、Processor和Output等。这样，这些分解后的元操作可以任意灵活组合，产生新的操作，这些操作经过一些控制程序组装后，可形成一个大的DAG作业，从而可以减少Map/Reduce之间的文件存储，同时合理组合其子过程，也可以减少任务的运行时间。


 mvn clean install -DskipTests -Dspark3.2 -Dscala-2.12  -Drat.skip=true -Dhadoop.version=2.10.2 -Dflink1.14 


ORC的全称是(Optimized Record Columnar)

https://cloud.tencent.com/developer/article/1961354


/usr/local/spark-3.2.1-bin-hadoop3.2/bin/spark-sql --jars /Users/chunhequ/Docker/hudi-0.11.0/packaging/hudi-spark-bundle/target/hudi-spark3.2-bundle_2.12-0.11.0.jar,/Users/chunhequ/Docker/hudi-0.11.0/packaging/hudi-utilities-bundle/target/hudi-utilities-bundle_2.12-0.11.0.jar,/Users/chunhequ/Docker/hudi-0.11.0/packaging/hudi-hadoop-mr-bundle/target/hudi-hadoop-mr-bundle-0.11.0.jar \ 
--conf 'spark.serializer=org.apache.spark.serializer.KryoSerializer' \
--conf 'spark.sql.extensions=org.apache.spark.sql.hudi.HoodieSparkSessionExtension' \
--conf 'spark.sql.catalog.spark_catalog=org.apache.spark.sql.hudi.catalog.HoodieCatalog' \
--conf 'hoodie.datasource.write.keygenerator.class=org.apache.hudi.keygen.CustomKeyGenerator' \
--conf 'hoodie.base.path=hdfs://127.0.0.1:9000/user/hudi/warehouse/'
--conf 'hoodie.datasource.write.hive_style_partitionin=false' /
--conf 'dfs.client.block.write.replace-datanode-on-failure.policy=NEVER' \
--conf 'dfs.client.block.write.replace-datanode-on-failure.enable=true' \
--conf 'spark.sql.hive.convertMetastoreParquet=true' \
--conf 'hoodie.datasource.hive_sync.jdbcurl=jdbc:mysql://127.0.0.1:3306/metastore' \
--conf 'hoodie.datasource.hive_sync.username=root' \
--conf 'hoodie.datasource.hive_sync.password=quchunhe' 


```
set hoodie.upsert.shuffle.parallelism = 1;
set hoodie.insert.shuffle.parallelism = 1;
set hoodie.delete.shuffle.parallelism = 1;
set schema.on.read.enable=true;

set hoodie.datasource.meta.sync.enable=false;

set hoodie.sql.bulk.insert.enable=true;
set hoodie.sql.insert.mode=strict;
set hoodie.datasource.write.table.type=MERGE_ON_READ;
```



```
yarn top
yarn logs -applicationId application_1528080031923_0064

yarn application -appStates All -list | grep robot-stream

```

vim /etc/taihao-apps/yarn-conf/yarn-site.xml


task.cancellation.timeout: 0

hadoop dfsadmin -report

hadoop fs -df -h



```
    Map<String, String> map = new HashMap<>();

    map.put("rest.port", "8083");
    Configuration config = Configuration.fromMap(map);
    config = YarnLogConfigUtil.setLogConfigFileInConfig(config, "/Users/chunhequ/Work/robot-stream/src/main/resources");

    final StreamExecutionEnvironment env = StreamExecutionEnvironment.createLocalEnvironmentWithWebUI(config);

```

```
    implementation group: 'org.apache.flink', name: 'flink-runtime-web_2.12', version: "${flinkVersion}"
    implementation group: 'org.slf4j', name: 'slf4j-simple', version: '1.7.25'
    implementation group: 'org.apache.flink', name: 'flink-yarn_2.12', version: "${flinkVersion}"
```



“Elasticsearch Lucene”
。