Apache Hudi (Hadoop Upsert Delete and Incremental)

表 、事务、upsert/delete、高级索引、流取服务、数据集群/压缩优化



[hudi-hadoop-mr 模块和hive版本不兼容问题](https://www.cnblogs.com/tommyjiang/p/17632338.html)

```shell
mvn clean package -DskipTests -Dspark3.3 -Dscala-2.12 -Dflink1.16 -Dcheckstyle.skip -Dhadoop.version=3.2.4 -Pflink-bundle-shade-hive3
```