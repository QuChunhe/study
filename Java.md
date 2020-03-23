
# Date Time
[Java Date Time](https://www.joda.org/joda-time/)

协调世界时，又称世界统一时间、世界标准时间、国际协调时间,从英文“Coordinated Universal Time”／法文“Temps Universel Cordonné”
而来.协调世界时是以原子时秒长为基础，在时刻上尽量接近于世界时的一种时间计量系统。

国际原子时(TAI，来自法国名字temps atomique International)是一个高精度的原子坐标时间标准:取1958年1月1日0时0分0秒世界时(UT)的瞬间作为同年同月同日0时0分0秒TAI。

规定英国（格林尼治天文台旧址）为中时区（零时区）、东1—12区，西1—12区。每个时区横跨经度15度，时间正好是1小时。最后的东、西第12区各跨经度7.5度，以东、西经180度为界。每个时区的中央经线上的时间就是这个时区内统一采用的时间，称为区时，相邻两个时区的时间相差1小时。


Time Zone Database

String prop = System.getProperty("java.time.zone.DefaultZoneRulesProvider");

TemporalAccessor -> Temporal    
TemporalAmount -> Duration, Period   
Temporal ->  HijrahDate, Instant, JapaneseDate, LocalDate, LocalDateTime, LocalTime, MinguoDate, OffsetDateTime, OffsetTime, ThaiBuddhistDate, Year, YearMonth, ZonedDateTime   
TemporalUnit -> ChronoUnit   
TemporalAdjuster    
ZoneId -> ZoneOffset   
ZoneRules

TemporalAmount : This is the base interface type for amounts of time. An amount is distinct from a date or time-of-day in that it is not tied to any specific point on the time-line. 

Durations and periods differ in their treatment of daylight savings time when added to ZonedDateTime. A Duration will add an exact number of seconds, thus a duration of one day is always exactly 24 hours. By contrast, a Period will add a conceptual day, trying to maintain the local time.   

# SPI


[Introduction to the Service Provider Interfaces](https://docs.oracle.com/javase/tutorial/sound/SPI-intro.html)

ServiceLoader: A service provider is identified by placing a provider-configuration file in the resource directory META-INF/services. The file's name is the fully-qualified binary name of the service's type. The file contains a list of fully-qualified binary names of concrete provider classes, one per line. Space and tab characters surrounding each name, as well as blank lines, are ignored. 

# Architecture

[架构设计与原则](http://www.rowkey.me/blog/2018/09/20/arch-new/)

架构是从宏观角度对系统的刻画和拆分，用于指导系统构建，以满足需求，包括功能需求和非功能需求。

核心问题是解决复杂性，降低构建和维护成本。

对于复杂系统，架构可能包括多个视图，从不同侧面刻画系统。业务架构、技术架构、数据架构、功能架构、部署架构和集成架构。

业务架构从需求角度，描述系统必须满足的业务功能、业务逻辑、业务流程和业务边界。

技术架构从技术角度，描述系统所依赖的技术栈或核心技术。

数据架构从数据角度，描述系统所基于的数据存储方式以及数据格式/表结构定义。

功能架构从模块角度，描述系统所必须的模块以及模块的功能。

部署架构从运行角度，描述系统的部件/组件如何实际部署和运行以及部件/组件间如何连接。

集成架构从系统角度，描述系统之间的功能调用关系以及所依赖的协议和数据。

[Correct way to find rowcount in Java JDBC](https://stackoverflow.com/questions/13103067/correct-way-to-find-rowcount-in-java-jdbc)

```
query = "SELECT * FROM customer WHERE username ='"+username+"'";
rs = stmt.executeQuery(query);
ResultSetMetaData metaData = rs.getMetaData();
rowcount = metaData.getColumnCount();
```

```
query = "SELECT * FROM customer WHERE username ='"+username+"'";
rs = stmt.executeQuery(query);
rowcount = rs.last() ? rs.getRow() : 0;
```

```
ResultSet rs = stmt.executeQuery(sql)

Exception in thread "main" java.lang.OutOfMemoryError: Java heap space
	at com.mysql.jdbc.MysqlIO.nextRowFast(MysqlIO.java:2213)
	at com.mysql.jdbc.MysqlIO.nextRow(MysqlIO.java:1992)
	at com.mysql.jdbc.MysqlIO.readSingleRowSet(MysqlIO.java:3413)
	at com.mysql.jdbc.MysqlIO.getResultSet(MysqlIO.java:471)
	at com.mysql.jdbc.MysqlIO.readResultsForQueryOrUpdate(MysqlIO.java:3115)
	at com.mysql.jdbc.MysqlIO.readAllResults(MysqlIO.java:2344)
	at com.mysql.jdbc.MysqlIO.sqlQueryDirect(MysqlIO.java:2739)
	at com.mysql.jdbc.ConnectionImpl.execSQL(ConnectionImpl.java:2482)
	at com.mysql.jdbc.ConnectionImpl.execSQL(ConnectionImpl.java:2440)
	at com.mysql.jdbc.StatementImpl.executeQuery(StatementImpl.java:1381)
	at org.apache.commons.dbcp2.DelegatingStatement.executeQuery(DelegatingStatement.java:206)
	at org.apache.commons.dbcp2.DelegatingStatement.executeQuery(DelegatingStatement.java:206)
```
fix OutOfMemoryError problems
* 设置连接属性useCursorFetch=true ,statement以TYPE_FORWARD_ONLY打开，再设置fetch size参数，表示采用服务器端游标，每次从服务器取fetch_size条数据
```java
try (Connection conn = mysqlDataSource.getConnection();
     Statement stmt = conn.createStatement(ResultSet.TYPE_FORWARD_ONLY,
                                           ResultSet.CONCUR_READ_ONLY)) {
    stmt.setFetchSize(fetchSize);
    try (ResultSet rs = stmt.executeQuery(sql)) {
        rs.setFetchSize(fetchSize);
	// read rs
    }
} catch (SQLException e) {
    //process error
}
```
* stmt.setFetchSize(Integer.MIN_VALUE);
```java
try (Connection conn = mysqlDataSource.getConnection();
     Statement stmt = conn.createStatement(ResultSet.TYPE_FORWARD_ONLY,
                                           ResultSet.CONCUR_READ_ONLY)) {
    stmt.setFetchSize(Integer.MIN_VALUE);
    try (ResultSet rs = stmt.executeQuery(sql)) {
        rs.setFetchSize(fetchSize);
	// read rs
    }
} catch (SQLException e) {
    //process error
}
```


```
java.sql.SQLException: Value '0000-00-00 00:00:00' can not be represented as java.sql.Timestamp
	at com.mysql.jdbc.SQLError.createSQLException(SQLError.java:965) ~[mysql-connector-java-5.1.46.jar:5.1.46]
	at com.mysql.jdbc.SQLError.createSQLException(SQLError.java:898) ~[mysql-connector-java-5.1.46.jar:5.1.46]
	at com.mysql.jdbc.SQLError.createSQLException(SQLError.java:887) ~[mysql-connector-java-5.1.46.jar:5.1.46]
	at com.mysql.jdbc.SQLError.createSQLException(SQLError.java:861) ~[mysql-connector-java-5.1.46.jar:5.1.46]
	at com.mysql.jdbc.ResultSetImpl.getTimestampFromString(ResultSetImpl.java:5676) ~[mysql-connector-java-5.1.46.jar:5.1.46]
	at com.mysql.jdbc.ResultSetImpl.getStringInternal(ResultSetImpl.java:5309) ~[mysql-connector-java-5.1.46.jar:5.1.46]
	at com.mysql.jdbc.ResultSetImpl.getString(ResultSetImpl.java:5138) ~[mysql-connector-java-5.1.46.jar:5.1.46]
	at org.apache.commons.dbcp2.DelegatingResultSet.getString(DelegatingResultSet.java:198) ~[commons-dbcp2-2.2.0.jar:2.2.0]
	at org.apache.commons.dbcp2.DelegatingResultSet.getString(DelegatingResultSet.java:198) ~[commons-dbcp2-2.2.0.jar:2.2.0]
	

connectionProperties=useUnicode=true;characterEncoding=UTF-8;zeroDateTimeBehavior=convertToNull

```

# Books

Richard Warburton, Java 8 Lambdas: Functional Programming for the Masses, O'Reilly, 2014

At the heart of functional programming is thinking about your problem domain in terms of immutable values and functions that translate between them.

This is actually an example of using code as data—we’re giving the button an object that represents an action

A functional interface is an interface with a single abstract method that is used as the type of a lambda expression.


[Package java.util.stream](https://docs.oracle.com/javase/8/docs/api/java/util/stream/package-summary.html)

Streams differ from collections in several ways: 
* No storage. 
* Functional in nature. 
* Laziness-seeking. 
* Possibly unbounded. 
* Consumable. 

Stream operations are divided into intermediate and terminal operations, and are combined to form stream pipelines. A stream pipeline consists of a source (such as a Collection, an array, a generator function, or an I/O channel); followed by zero or more intermediate operations such as Stream.filter or Stream.map; and a terminal operation such as Stream.forEach or Stream.reduce.

Intermediate operations are further divided into stateless and stateful operations. Stateless operations, such as filter and map, retain no state from previously seen element when processing a new element -- each element can be processed independently of operations on other elements. Stateful operations, such as distinct and sorted, may incorporate state from previously seen elements when processing new elements. 


# Performance


[async-profiler](https://github.com/jvm-profiling-tools/async-profiler)

# 杂项

Comparable<T>  Comparator<T>

