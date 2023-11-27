Apache Hudi (Hadoop Upsert Delete and Incremental)

表 、事务、upsert/delete、高级索引、流取服务、数据集群/压缩优化



[hudi-hadoop-mr 模块和hive版本不兼容问题](https://www.cnblogs.com/tommyjiang/p/17632338.html)

```shell
mvn clean package -DskipTests -Dspark3.3 -Dscala-2.12 -Dflink1.16 -Dcheckstyle.skip -Dhadoop.version=3.2.4 -Pflink-bundle-shade-hive3
```



Hudi支持以下存储类型。
* 写时复制 : 仅使用列文件格式（例如parquet）存储数据。通过在写入过程中执行同步合并以更新版本并重写文件。
* 读时合并 : 使用列式（例如parquet）+ 基于行（例如avro）的文件格式组合来存储数据。更新记录到增量文件中，然后进行同步或异步压缩以生成列文件的新版本。