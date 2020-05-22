
# Concurrency

Phaser

 CyclicBarrier 
 
 CountDownLatch

* thread-saft Collections
* concurrent Collecttions


## Lock


JDK中的所机制
* 内置锁 synchronized
* 锁对象 Lock接口的的实现，包括ReentrantLock, ReentrantReadWriteLock.ReadLock, ReentrantReadWriteLock.WriteLock，本质上依赖于Unsafe.unpark()和Unsafe.park(LockSupport类调用Unsafte)。

ReentrantLock, ReentrantReadWriteLock.ReadLock, ReentrantReadWriteLock.WriteLock --> AbstractOwnableSynchronizer --> LockSupport --> Unsafe

```
class X {
   private final ReentrantLock lock = new ReentrantLock();
   // ...

   public void m() {
     lock.lock();  // block until condition holds
     try {
       // ... method body
     } finally {
       lock.unlock()
     }
   }
   
   public void n() {
       if (lock.tryLock()) {
           try {
              
           } finally {
              lock. unlock();
            }
       }
   }
 }
```

在JAVA中ReentrantLock相对于内置锁有如下优势:
1. 可中断锁，
2. 可超时锁；
3. 能够获得运行线程和阻塞线程,可以通过发起中断，唤醒阻塞的线程
4. 多个条件。
5. 设置不同的加锁策略，fair和unfair 

1)和2)能够使线程优雅地退出加锁阻塞状态，而3)适用于需要等待多个Condition的复杂场景，例如读写锁。


## Concurrent Collections

copy-on-write collections

“写时复制”——要写的时候复制一份副本，往副本里面写，然后引用到这个副本，在引用到这个副本之前有读操作的话，读的还是之前的老版本，读写分离，写不影响读可以并发读读，读写，但是写写的时候还是冲突的，如果拷贝了N个副本，最后到底引用谁呢，引用某个副本，写到其他副本上的数据就丢失了，所以写要加锁，也就是一个一个来，串行写。
* CopyOnWriteArrayList
* CopyOnWriteArraySet

The way it does this is to make a brand new copy of the list every time it is altered.
* Reads do not block, and effectively pay only the cost of a volatile read;
* Writes do not block reads (or vice versa), but only one write can occur at once; 

Copy-on-write collections are designed for cases where:
* reads hugely outnumber writes;
* the size of collections array is small (or writes are very infrequent); 

ConcurrentLinkedQueue

# Performance

提高性能的三个方面
* 减小服务时延，能够更快的得到服务的响应或者输出
* 提高系统吞吐，能够处理更多的输入，例如更多的服务请求以及更大的数据规模等
* 降低系统负载，充分利用系统硬件资源，能够在相同的硬件条件下服务更多的服务请求和输入数据

减小服务时延的方法
* 更快的硬件，比如采用固态硬盘(Solid Stat Drive)，以取代机械硬盘(Hard Disk Drive)
* 并行化，挖掘问题/任务的并行性，将问题/任务分解为子问题/任务，并通过并行处理这些子问题/子任务，以减小处理时间
* cache(缓存)，通过缓存数据，避免重复处理 
* 更快的子系统或子任务，比如优化MySQL查询或者采用Redis替换MySQL
* 功能优化，包括算法优化、数据结构优化和编程语言优化

throughtput=concurrency/latency

提高系统吞入的方法
* 提高并发度，即采用更多的线程提供服务，但是随着线程数量的增加，线程之间的互扰会逐渐增加，从而不断增加服务响应时间
* 减小服务时延，即减小服务响应时间
* 采用非阻塞式调用或异步调用
* 避免或减小共享资源，包括共享硬件和共享的数据，例如避免使用锁或者减小所额粒度

降低系统负载的方法

## 原子操作


[多核系统上的 Java 并发缺陷模式（bug patterns）](https://www.ibm.com/developerworks/cn/java/j-concurrencybugpatterns/)

一定要谨记 volatile 关键字在 Java 代码中仅仅保证这个变量是可见的：它不保证原子性。

i++,
read-modify-write


# Tools


[async-profiler](https://github.com/jvm-profiling-tools/async-profiler)

## jstack
[How to Read a Thread Dump ](https://dzone.com/articles/how-to-read-a-thread-dump)

A thread dump is a snapshot of the state of all the threads of a Java process. The state of each thread is presented with a stack trace, showing the content of a thread's stack. A thread dump is useful for diagnosing problems as it displays the thread's activity.

jstack prints Java stack traces of Java threads for a given Java process or core file or a remote debug server. For each Java frame, the full class name, method name, 'bci' (byte code index) and line number, if available, are printed. With the -m option, jstack prints both Java and native frames of all threads along with the 'pc' (program counter). 
```
jstack [ option ] pid
jstack [ option ] executable core
jstack [ option ] [server-id@]remote-hostname-or-IP

```
Option
* -F:  Force a stack dump when 'jstack [-l] pid' does not respond.
* -l:  Long listing. Prints additional information about locks such as list of owned java.util.concurrent ownable synchronizers.
* -m:  prints mixed mode (both Java and native C/C++ frames) stack trace.
* -h:  prints a help message.
* -help: prints a help message

The second line represents the current state of the thread. The possible states for a thread are captured in the Thread.State enumeration:
* NEW
* RUNNABLE
* BLOCKED
* WAITING
* TIMED_WAITING
* TERMINATED

线程的状态
* waiting on condition: TIMED_WAITING (sleeping), WAITING (parking)
* runnable: RUNNABLE
* in Object.wait(): TIMED_WAITING (on object monitor)
* sleeping: TIMED_WAITING (sleeping)


Within this stack trace, we can see that locking information has been added, which tells us that this thread is waiting for a lock on an object with an address of 0x00000006c861e938 (and a type of java.lang.Object) and, at this point in the stack trace, holds a lock on an object with an address of x00000006cad83ca8 (also of type java.lang.Object). This supplemental lock information is important when diagnosing deadlocks, as we will see in the following sections
```
- parking to wait for  <0x00000006c861e938>

  Locked ownable synchronizers:
        - <0x00000006cad83ca8> 
```
[Class LockInfo](https://docs.oracle.com/javase/8/docs/api/java/lang/management/LockInfo.html)   
An ownable synchronizer is a synchronizer that may be exclusively owned by a thread and uses AbstractOwnableSynchronizer (or its subclass) to implement its synchronization property. ReentrantLock and ReentrantReadWriteLock are two examples of ownable synchronizers provided by the platform.


```
"Reference Handler" #2 daemon prio=10 os_prio=0 tid=0x00007f06001ae800 nid=0x4f03 in Object.wait() [0x00007f05e39f8000]
   java.lang.Thread.State: WAITING (on object monitor)
	at java.lang.Object.wait(Native Method)
	- waiting on <0x0000000782c06c08> (a java.lang.ref.Reference$Lock)
	at java.lang.Object.wait(Object.java:502)
	at java.lang.ref.Reference.tryHandlePending(Reference.java:191)
	- locked <0x0000000782c06c08> (a java.lang.ref.Reference$Lock)
	at java.lang.ref.Reference$ReferenceHandler.run(Reference.java:153)

   Locked ownable synchronizers:
	- None

```
|  Section   |   Example  |   Description  |
| :------------ | :------------ | :------------ |
Name | "Reference Handler"  |Human-readable name of the thread. This name can be set by calling the setName method on a Threadobject and be obtained by calling getName on the object.|
ID   | #2  | A unique ID associated with each Thread object. This number is generated, starting at 1, for all threads in the system. Each time a Thread object is created, the sequence number is incremented and then assigned to the newly created Thread. This ID is read-only and can be obtained by calling getId on a Thread object.|
Daemon status | daemon |A tag denoting if the thread is a daemon thread. If the thread is a daemon, this tag will be present; if the thread is a non-daemon thread, no tag will be present. For example, Thread-0 is not a daemon thread and therefore has no associated daemon tag in its summary: Thread-0" #12 prio=5....|
Priority | prio=10 | The numeric priority of the Java thread. Note that this does not necessarily correspond to the priority of the OS thread to with the Java thread is dispatched. The priority of a Thread object can be set using the setPriority method and obtained using the getPriority method.|
OS Thread Priority | os_prio=2 |The OS thread priority. This priority can differ from the Java thread priority and corresponds to the OS thread on which the Java thread is dispatched.|
Address | tid=0x00000250e4979000 |The address of the Java thread. This address represents the pointer address of the Java Native Interface (JNI) native Thread object (the C++ Thread object that backs the Java thread through the JNI). This value is obtained by converting the pointer to this (of the C++ object that backs the Java Thread object) to an integer on line 879 of **hotspot/share/runtime/thread.cpp:** ```st->print("tid=" INTPTR_FORMAT " ", p2i(this));``` Although the key for this item (tid) may appear to be the thread ID, it is actually the address of the underlying JNI C++ Thread object and thus is not the ID returned when calling getId on a Java Thread object.|
OS Thread ID | nid=0x3c28 | The unique ID of the OS thread to which the Java Thread is mapped. This value is printed on line 42 of **hotspot/share/runtime/osThread.cpp:**  ```st->print("nid=0x%x ", thread_id()); ```|
Status | waiting on condition| A human-readable string depicting the current status of the thread. This string provides supplementary information beyond the basic thread state (see below) and can be useful in discovering the intended actions of a thread (i.e. was the thread trying to acquire a lock or waiting on a condition when it blocked).|
Last Known Java Stack Pointer | [0x000000b82a9ff000] | The last known Stack Pointer (SP) for the stack associated with the thread. This value is supplied using native C++ code and is interlaced with the Java Thread class using the JNI. This value is obtained using the last_Java_sp() native method and is formatted into the thread dump on line 2886 of **hotspot/share/runtime/thread.cpp:** ```    st->print_cr("[" INTPTR_FORMAT "]", (intptr_t)last_Java_sp() & ~right_n_bits(12));``` For simple thread dumps, this information may not be useful, but for more complex diagnostics, this SP value can be used to trace lock acquisition through a program.|


# Date Time
[Java Date Time](https://www.joda.org/joda-time/)

The new API makes a distinction between how dates and times are used by machines and humans. Machines deal with time as continual ticks as a single incrementing number measured in seconds, milliseconds, etc. Humans use a calendar system to deal with time in terms of year, month, day, hour, minute, and second. The Date-Time API has a separate set of classes to deal with machine-based time and calendar-based human time. It lets you convert machine-based time to human-based time and vice versa.


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
TimeZone   
ZoneRules    
TemporalField ->ChronoField

Calendar ->  GregorianCalendar   
Chronology ->   IsoChronology, JapaneseChronology    
Clock   

TemporalAmount : This is the base interface type for amounts of time. An amount is distinct from a date or time-of-day in that it is not tied to any specific point on the time-line. 

Durations and periods differ in their treatment of daylight savings time when added to ZonedDateTime. A Duration will add an exact number of seconds, thus a duration of one day is always exactly 24 hours. By contrast, a Period will add a conceptual day, trying to maintain the local time.   

The Calendar class is an abstract class that provides methods for converting between a specific instant in time and a set of calendar fields such as YEAR, MONTH, DAY_OF_MONTH, HOUR, and so on, and for manipulating the calendar fields, such as getting the date of the next week.     

A clock providing access to the current instant, date and time using a time-zone.    



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


# Java Memory Model (JMM)

Using locks solves the problem. However, performance takes a hit.When multiple threads attempt to acquire a lock, one of them wins, while the rest of the threads are either blocked or suspended.The process of suspending and then resuming a thread is very expensive and affects the overall efficiency of the system.


There is a branch of research focused on creating non-blocking algorithms for concurrent environments. These algorithms exploit low-level atomic machine instructions such as compare-and-swap (CAS), to ensure data integrity.

A typical CAS operation works on three operands:
* The memory location on which to operate (M)
* The existing expected value (A) of the variable
* The new value (B) which needs to be set

The CAS operation updates atomically the value in M to B, but only if the existing value in M matches A, otherwise no action is taken.In both cases, the existing value in M is returned. This combines three steps – getting the value, comparing the value and updating the value – into a single machine level operation. When multiple threads attempt to update the same value through CAS, one of them wins and updates the value. However, unlike in the case of locks, no other thread gets suspended;

使用CAS后，需要判断CAS操作是否成功
1）如果操作成功，继续执行
2）如果操作失败，那么：a)循环CAS操作，直到操作成功，忙等待；b）执行其他操作，空闲在执行CAS操作

Atomic Variables and Collections

[深入理解JVM之Java内存模型](https://segmentfault.com/a/1190000021637869)


https://www.cs.umd.edu/class/spring2013/cmsc433/Notes/07-CMSC433-VolatilityAndOrdering.pdf

[Programming Language Technologies and Paradigms](https://www.cs.umd.edu/class/spring2013/cmsc433/Notes/)

# Functional Programming

Functional Programming in Java

* First-class functions 函数为值
* Anonymous functions  匿名函数
* Closures 闭包
* Currying 柯里化
* Lazy evaluation 惰性求值
* Parametric polymorphism 参数多态
* Algebraic data types 代数数据类型


A referentially transparent program doesn't interfere with the outside world apart from taking an argument as input and outputting a result. Its result only depends on its argument.

# 杂项

Comparable<T>  Comparator<T>
	
[Sentinel(https://github.com/alibaba/Sentinel)
	
System.nanoTime与System.currentTimeMillis
* System.nanoTime : This method can only be used to measure elapsed time and is not related to any other notion of system or wall-clock time. 
* System.currentTimeMillis : the difference, measured in milliseconds, between the current time and midnight, January 1, 1970 UTC.


* 强引用（StrongReference）
* 软引用（SoftReference）
* 弱引用（WeakReference）
* 虚引用（PhantomReference）
