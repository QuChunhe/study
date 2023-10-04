


# Ideal(想法) 

数据库在实际使用、部署和设计中需要依次考虑如下几个密切相关的问题
* SQL，还是NoSQL
  * 业务需求：1）对于事务需求；2）数据规模和可扩展性需求。
  * 关系型数据库能够提供完善的事务和查询支持，但是可扩展性较差。相反地，NoSQL数据库具有很好的可扩展性，能够支持大规模的数据存储和并发访问，但是不能支持事务。此外，NoSQL的表设计严重依赖于数据查询模式。为了支持不同的查询，需要设计不同的表结构
* MySQL数据库架构选择
   * 选择单体部署，还是数据库集群
   * 针对于不同的需求，选择不同架构：数据备份、高可用、高吞吐(支持更多的事务或者查询)、低时延（更少响应时间）、大数据规模。主要的架构包括：数据复制、读写分离以及sharding。
* 数据库的表设计
* 数据库访问优化


如下三个方面需要相互匹配
* 数据存储方式
* schema设计
* 数据查询模式

MySQL中存在三类不同的表
* 业务型
* 日志型
* 汇总型

两种处理
* 统计分析
* 事务处理

如果数据规模比较庞大，为了优化性能，建议将上述三类表和两种处理分置到不同数据库中。


MySQL性能优化，包括如下三个方面
* schema设置，
  * 存储引擎的选择
  * 表的划分和关联
  * 列类型的定义
  * 主键和索引的设计以及partition和sharding的设置
* 查询优化，充分利用索引和查询条件，避免无效数据扫描
* 配置设置

MySQL操作的主要瓶颈
* Disk寻址：B+树，随着数据量的增加，层数和叶子节点增加，需要更多的寻址次数。
* Disk读取和写入：1）尽量不要全表扫描
* 内存计算

[](https://docs.aws.amazon.com/athena/latest/ug/alter-table-drop-partition.html#:~:text=ALTER%20TABLE%20DROP%20%20PARTITION%201%20Synopsis%20ALTER,a%20range%20of%20%20partitions%20to%20drop.%20)

Partition需要手工维护
```sql

ALTER TABLE table_name DROP [IF EXISTS] PARTITION (partition_spec) [, PARTITION (partition_spec)]

SHOW PARTITIONS impressions

SELECT * FROM "flight_delays_csv$partitions" ORDER BY year

ALTER TABLE members
    REORGANIZE PARTITION p0 INTO (
        PARTITION n0 VALUES LESS THAN (1970),
        PARTITION n1 VALUES LESS THAN (1980)
);

```

数据库规模扩大
* 单个MySQL。MySQL数据库足够强大，通过选择适当的硬件和设计合理的表结构，单个数据库就能够支持几百G，甚至T级，的数据规模
  * 针对三种不同类型的表，差异化处理。例如对于业务表尽量避免列数过多，而对于日志表和汇总表可以采用基于时间范围的partition以及采用非varchar类型
  * 采用固态硬盘，如果数据规模庞大，可以根据访问频率，将数据表分别存在在固态硬盘和机械硬盘上
* 采用repication机制组合的集群
  *  针对三种不同类型的表和两类不同的处理，分别采用不同的数据库，以分担负载
* 采用sharding  
  * 关系（join）的处理
  * 采用Engine或者中间件工具
* 跨数据中心的数据同步


优化MySQL性能
* 硬件选择
* 配置：
   * 操作系统配置
   * 数据库配置
* Schema设计，包括主键和索引的设计
* 查询优化:monitor, analysize, optimize
  * monitor 发现和记录出现的问题
  * analysize 深入分析问题的根源
  * optimize 采取措施解决性能问题


对于大表（行数多和/或列数多）的查询
* 对表结构进行重构，采用Partition和分表方式，来减小查询锁读取的数据量
* 优化查询语句，以尽量减小扫描和查询大表中的数据，比如放宽业务或者需求约束
* 采用预处理方法，在数据插入大表时进行额外处理，以辅助大表查询。

# Design Schema


C.J. Date, Database Design and Relational Theory: Normal Forms and All That Jazz, 2nd Edition, Apress, 2019.

每个属性的定义域为不可分割的原子类型。

* candidate key
* primary key
* composite key
* Simple key
* alternate keys
* foreign key

Logical design is concerned with what the database looks like to the user (which means, loosely, what relvars exist and what constraints apply to those relvars); physical design,
by contrast, is concerned with how a given logical design maps to physical storage.
为开发者和设计者提供了适用的、可遵循的指南。



C.J. Date, 熊建国译,深度探索关系数据库：实践者的关系理论, 电子工业出版社， 2007


SQL not equal 关系模型

关系、元组和属性


关系不是表，元组不是行，属性也不是列

在1969年当时任职于IBM的E. F. Codd首先提出了关系模型


* 结构
* 完整性
* 操作

结构
* 候选键
* 主键
* 外键

操作
* 限制 restrict
* 投影 Project
* 积 product。笛卡尔积、交积、交叉连接、笛卡尔连接
* 交 Intersect
* 并 Union
* 差 difference
* 连接 join
* 除 Divide

数值原子性(Data value atomicity)

数值原子性和第一范式。 Codd将原子性定义为“不能被DBMS分解为更小个体的数据”

原子性并不是绝对的，
1. 是否作为一个整体看待；
2. 是否需要整体更新；
3. 是否需要复杂的解析；
4. 是否针对于部分进行处理



[Facts and Fallacies about First Normal Form](https://www.red-gate.com/simple-talk/sql/learn-sql-server/facts-and-fallacies-about-first-normal-form/)


A database is in first normal form if it satisfies the following conditions:
* Contains only atomic values.仅仅包含原子类型值
* There are no repeating groups.不存在重复的组


除了字典表和日志表，尽量避免VARCHAR的列

正式表采用InnoDB，导入数据或者中间结果采用的临时表可以可以采用MEMORY或者MyISAM。
* InnoDB具有更好的并发性，采用表锁
* InnoDB具有更好的缓存，InnoDB Buffer

与MyISAM相比，InnoDB的数据插入性能比较差。

范式与例外

[Good Database Design Principle](http://eckstein.rutgers.edu/mis/handouts/rdb2.pdf)

normalization 规范化

normal form 范式

1.没有冗余，一个字段仅仅存储在一个表中，除非其是一个外键。复制外键许可两个表关联起来。

2.没有坏的依赖，在数据库中任何关系的依赖图，列依赖于整个主键或者一个候选键。违法这种规则的情况包括
* 部分依赖
* 传递依赖

规范化是消除坏依赖的过程，通过分解表并通过外键连接它们。

范式是一些类型，归类了如何对一个表进行归类。

有六个公认的范式
* First Normal Form (1NF)
* Second Normal Form (2NF)
* Third Normal Form (3NF)
* Boyce-Codd Normal Form (BCNF)
* Fourth Normal Form (4NF)
* Fifth Normal Form (5NF)

如果一个表是第一范式，那么其所有的属性都必须是原子的。不是原子原子属性的情况包括
* 嵌套关系、嵌套表或字表
* 重复的组或者重复的部分
* 基于列表值的属性

为了消除迭代关系，可以移出迭代关系，形成一个新表。确保在新表中包括原来表的主健，用于将表连接在一起。

在如下情况中发生了部分依赖
* 采用复合主健（composite primary key）
* 一个非健属性依赖于部分主健，而不是全部主健
* 如果一个满足第一范式的表，不包含任何部分依赖，则称其满足第二范式

当一个非健属性依赖于其他一个非健属性并且所依赖的属性不能用于作为一个候选主健时，就发生了传递依赖于。如果一个满足第二范式并且不包含任何可依赖的转递依赖，则称其满足第三范式。

识别第三范式的关键因素
* 所有属性都是原子类型
* 在每个关系中决定性因素时整个主健，或者被选出来作为候选主健：确保没有部分依赖或者转移依赖
* 基于列表值的属性



[11 important database designing rules which I follow](https://www.codeproject.com/articles/359654/11-important-database-designing-rules-which-i-fo-2)

Rule 1: What is the nature of the application (OLTP or OLAP)?

规则１：应用的本质是什么（OLTP或OLAP）

在开始设计一个数据库时，此需要确定数据库之上的应用在本质上是事务型，还是分析型。在不考虑应用本质的情况下，默认应用正规化，造成出现性能和定制化问题。有两类应用：基于事务型和基于分析型。

事务型：面向CRUD，creating, reading, updating, and deleting records

分析型：面向分析、报表、预测等，较少的插入和更新，尽可能快的取出和分析数据。

**如果认为插入、更新和删除占主导，那么需要正规化表设计。反之，需要创建扁平的、非正规化的数据库结构。**


OnLine Transaction Processing 联机事务处理过程(OLTP)，也称为面向交易的处理过程，

联机分析处理（Online Analytical Processing ）的概念最早是由关系数据库之父E. F. Codd博士在1993年提出来的。


OLTP是实时系统，支持并发的增、删、改、查操作。



[OLAP、OLTP的介绍和比较](https://www.cnblogs.com/hhandbibi/p/7118740.html)

Rule 2: Break your data into logical pieces, make life simpler

规则２：将你的数据分解为逻辑字段，使得生活更加简单

该规则实际是来自第一范式的第一个规则。违反此规则的一个迹象是你的查询中使用太多的字符串解析函数，例如substring、charindex等，大概需要一个用此规则。

Rule 3: Do not get overdosed with rule 2

规则３：不能滥用规则２

规则２的滥用将会导致不是期望的结果。判断分解是否合理，逻辑上十分合理。

Rule 4: Treat duplicate non-uniform data as your biggest enemy

规则４：将重复的非规格化的数据作为最大的敌人

聚焦和重构复制的数据，对于复制数据的焦虑不是因为其占用磁盘空间，而是其产生困惑。

Rule 5: Watch for data separated by separators

Rule 6: Watch for partial dependencies

规则6:注意部分依赖

注意部分依赖于主健的域。

Rule 7: Choose derived columns preciously

对于OTLP应用，消除派生的列是一个好的想法，除非存在一些紧迫性的性能原因。对于OLAP的例子，我们需要大量的求和和计算，这些派生域对于提高性能是必不可少。

在第三范式要求不能有列依赖于其他非主健的列。我个人的想法是不要盲目地应用第三范式，而是要看具体情况，不是说冗余数据总是不好的。如果冗余数据是计算数据，要仔细评估得失，然后决定是否要实施第三范式。

Rule 8: Do not be hard on avoiding redundancy, if performance is the key

规则８：如果性能是关键，那么就不要竭尽全力的避免冗余。


不必严格遵守避免冗余的规则。如果迫切需要性能，考虑非规范话。在规范化中，需要join很多表，而在非规范化中，减小了join操作从而提高了性能。


Rule 9: Multidimensional data is a different beast altogether

规则9：多维数据完全是另一种野兽

Rule 10: Centralize name value table design

规则10：集中名值表设计

集中的字典表，采用类型表面用途

Rule 11: For unlimited hierarchical data self-reference PK and FK

规则11：对于没有限制的分层数据，采用自引用主健（PK）和外健（FK）



[Database design basics](https://support.office.com/en-us/article/Database-design-basics-EB2159CF-1E30-401A-8084-BD4F9C9CA1F5)


What is good database design?

第一条原则是重复信息（也被称之为冗余数据）是有害的，因为其不仅浪费存储空间，而且增加了错误和不一致的可能性。第二条原则是信息的正确性和完整性非常重要。

一个好的数据库设计应该满足如下条件
* Divides your information into subject-based tables to reduce redundant data.将信息划分到基于主题的表中，以减小冗余数据
* Provides Access with the information it requires to join the information in the tables together as needed.通过按需将表关联在一起，从而提供访问所需要信息的能力。
* Helps support and ensure the accuracy and integrity of your information.辅助支持和确保信息精确性和完整性
* Accommodates your data processing and reporting needs.满足数据处理和报表需求。

设计过程
* Determine the purpose of your database
* Find and organize the information required
* Divide the information into tables
* Turn information items into columns 
* Specify primary keys 
* Set up the table relationships
* Refine your design
* Apply the normalization rules

Determine the purpose of your database

确定数据库的目标(Determine the purpose of your database):将数据库的目标写在纸上是一个好主意.


查找并组织所需信息(Find and organize the information required)


A Practical Guide to Database Design, 2nd Edition,2018

* Problem Type 1—Synonyms:A synonym is created when two different names are used for the same information ( attribute). If an attribute resides in more than one entity, insure that all entities use the same attribute name.
* Problem Type 2—Homonyms: A homonym is the reverse of a synonym. Just as you cannot use different names for the same attribute, you cannot use the same name for different attributes
* Problem Type 3—Redundant Information: This problem, in which the same information is stored in two different forms or ways, is
a bit harder to spot. One way to check for it is to consider if the value of any attribute is known or is derivable through the other attributes defined.
* Problem Type 4—Mutually Exclusive Data: Mutually exclusive data exist when attributes occur, all the values of which, perhaps expressed as yes/no indicators, cannot be true for any single entity.

More formally stated, normalization is the process of analyzing the dependencies between attributes within entities. Each attribute is checked against three or more sets of rules, then making adjustments as necessary to put each in first, second, and third normal form (3NF).

In his book, An Introduction to Database Systems, C. J. Date gives the definition of first normal form (1NF) as “A relation R is in first normal form (1NF) if and only if all underlying domains contain atomic values only.”

[Codd's 12 rules](https://en.wikipedia.org/wiki/Codd%27s_12_rules)



准则1：信息准则

关系数据库系统的所有信息都应该在逻辑一级上用表中的值这一种方法显式的表示。

准则2：保证访问准则

依靠表名、主码和列名的组合，保证能以逻辑方式访问关系数据库中的每个数据项。

准则3：空值的系统化处理

全关系的关系数据库系统支持空值的概念，并用系统化的方法处理空值。

准则4：基于关系模型的动态的联机数据字典

数据库的描述在逻辑级上和普通数据采用同样的表述方式。

准则5：统一的数据子语言

一个关系数据库系统可以具有几种语言和多种终端访问方式，但必须有一种语言，它的语句可以表示为严格语法规定的字符串，并能全面的支持各种规则。

准则6：视图更新准则

所有理论上可更新的视图也应该允许由系统更新。

准则7：高级的插入、修改和删除操作

系统应该对各种操作进行查询优化。

准则8：数据的物理独立性

无论数据库的数据在存储表示或存取方法上作任何变化，应用程序和终端活动都保持逻辑上的不变性。

准则9：数据逻辑独立性

当对基本关系进行理论上信息不受损害的任何改变时，应用程序和终端活动都保持逻辑上的不变性。

准则10：数据完整的独立性

关系数据库的完整性约束条件必须是用数据库语言定义并存储在数据字典中的。

准则11：分布独立性

关系数据库系统在引入分布数据或数据重新分布时保持逻辑不变。

准则12：无破坏准则

如果一个关系数据库系统具有一个低级语言，那么这个低级语言不能违背或绕过完整性准则

**Rule 0:** The foundation rule: For any system that is advertised as, or claimed to be, a relational data base management system, that system must be able to manage data bases entirely through its relational capabilities.

准则 0 基础规则：对于任何宣传或者声称为一个关系数据库管理系统的系统，其必须具有能力管理 

一个关系形的关系数据库系统必须能完全通过它的关系能力来管理数据库。

Rule 1: The information rule:

All information in a relational data base is represented explicitly at the logical level and in exactly one way – by values in tables.

Rule 2: The guaranteed access rule:

Each and every datum (atomic value) in a relational data base is guaranteed to be logically accessible by resorting to a combination of table name, primary key value and column name.

Rule 3: Systematic treatment of null values:

Null values (distinct from the empty character string or a string of blank characters and distinct from zero or any other number) are supported in fully relational DBMS for representing missing information and inapplicable information in a systematic way, independent of data type.

Rule 4: Dynamic online catalog based on the relational model:

The data base description is represented at the logical level in the same way as ordinary data, so that authorized users can apply the same relational language to its interrogation as they apply to the regular data.

Rule 5: The comprehensive data sublanguage rule:

A relational system may support several languages and various modes of terminal use (for example, the fill-in-the-blanks mode). However, there must be at least one language whose statements are expressible, per some well-defined syntax, as character strings and that is comprehensive in supporting all of the following items:

* Data definition.
* View definition.
* Data manipulation (interactive and by program).
* Integrity constraints.
* Authorization.
* Transaction boundaries (begin, commit and rollback).

Rule 6: The view updating rule:

All views that are theoretically updatable are also updatable by the system.

Rule 7: Possible for high-level insert, update, and delete:

The capability of handling a base relation or a derived relation as a single operand applies not only to the retrieval of data but also to the insertion, update and deletion of data.

Rule 8: Physical data independence:

Application programs and terminal activities remain logically unimpaired whenever any changes are made in either storage representations or access methods.

Rule 9: Logical data independence:

Application programs and terminal activities remain logically unimpaired when information-preserving changes of any kind that theoretically permit unimpairment are made to the base tables.

Rule 10: Integrity independence:

Integrity constraints specific to a particular relational data base must be definable in the relational data sublanguage and storable in the catalog, not in the application programs.

Rule 11: Distribution independence:

The end-user must not be able to see that the data is distributed over various locations. Users should always get the impression that the data is located at one site only.

Rule 12: The nonsubversion rule:

If a relational system has a low-level (single-record-at-a-time) language, that low level cannot be used to subvert or bypass the integrity rules and constraints expressed in the higher level relational language (multiple-records-at-a-time).



[Database normalization](https://en.wikipedia.org/wiki/Database_normalization)

数据库正规化是根据一系列范式构造关系型数据库的过程，以减小数据冗余和提高数据完整性。范式是由Edgar F. Codd首先提出，作为关系模型的一部分。

Normalization entails organizing the columns (attributes) and tables (relations) of a database to ensure that their dependencies are properly enforced by database integrity constraints. It is  accomplished by applying some formal rules either by a process of synthesis (creating a new database design) or decomposition (improving an existing database design). 
正规化需要对于数据库的列（属性）和表（关系）进行组织，以确保它们的依赖性正确地符合数据库完整性约束。应用一些正式的规则并通过合成（创建新的表）或者分解（改进已有的表）的过程来实现上述的组织。



[First normal form](https://en.wikipedia.org/wiki/First_normal_form)

第一范式是关系数据库中关系的基本属性。

Codd states that the "values in the domains on which each relation is defined are required to be atomic with respect to the DBMS." Codd defines an atomic value as one that "cannot be decomposed into smaller pieces by the DBMS (excluding certain special functions)" meaning a column should not be divided into parts with more than one kind of data in it such that what one part means to the DBMS depends on another part of the same column.
Codd表述为“在定义每个关系的域中，其值对于DBMS必须是原子的”。Codd将一个原子值定义为“不能被DBMS分解为更小的部分（不包括某些特殊的函数）”，这意味着一列不应被分割为具有不止一种类型的多个部分，并且对于DBMS而言一部分依赖于同一列的其他部分。

Hugh Darwen and Chris Date have suggested that Codd's concept of an "atomic value" is ambiguous, and that this ambiguity has led to widespread confusion about how 1NF should be understood. In particular, the notion of a "value that cannot be decomposed" is problematic, as it would seem to imply that few, if any, data types are atomic: 
Huge Darwen和Chis Date指出Codd的原子值概念具有歧义，并且这种歧义性会导致对于如何理解第一范式产生普遍的困惑。尤其是，对于“不能被分解的值”这一概念是有问题的，因为这种定义意味着很少（如果有的话）数据类型是原子的。
* A character string would seem not to be atomic, as the RDBMS typically provides operators to decompose it into substrings.字符串似乎不是原子的，因为RDBMS通常提供了用于将字符串分解为子串的操作符。
* A fixed-point number would seem not to be atomic, as the RDBMS typically provides operators to decompose it into integer and fractional components.定点数似乎不是原子数，因为RDBMS通常提供了将其分解为整数和小数部分的运算符。
 * An ISBN would seem not to be atomic, as it includes language and publisher identifier.ISBN似乎不是原子的，因为其包括语言和发行者标识符。
 

Date suggests that "the notion of atomicity has no absolute meaning": a value may be considered atomic for some purposes, but may be considered an assemblage of more basic elements for other purposes. If this position is accepted, 1NF cannot be defined with reference to atomicity. Columns of any conceivable data type (from string types and numeric types to array types and table types) are then acceptable in a 1NF table—although perhaps not always desirable; for example, it may be more desirable to separate a Customer Name column into two separate columns as First Name, Surname.
Date指出“原子性这一概念并不是绝对”：针对于一些使用场合，一个值可以被认为是原子的，但是对于其他一些使用场合这个值也可以被认为是由多个基本元素组合而成。如果上述情况时可以被接受的，那么就不能引用原子性来定义第一范式。任何可以想到的数据类型（从字符串类型和数值类型到数组类型和表类型），其定义的列都是可以被第一范式的表接受，尽管可能并不总是期望如此。例如，可能更可取的做法是将一个Customer Name列分为两个单独的列，分别为first_name(名字）和surname（姓氏）。

According to Date's definition, a table is in first normal form if and only if it is "isomorphic to some relation", which means, specifically, that it satisfies the following five conditions: 根据Date的定义，一个表是第一范式当且仅当它“同构于某个关系”，即它满足以下五个条件
* There's no top-to-bottom ordering to the rows. 行没有从上到下的顺序关系。
* There's no left-to-right ordering to the columns.列没有从左到右的顺序关系
* There are no duplicate rows.没有重复的行
* Every row-and-column intersection contains exactly one value from the applicable domain (and nothing else).在每一行与每一列的交叉处仅仅包含来自适用域的一个值(并没有其他东西)。
* All columns are regular \[i.e. rows have no hidden components such as row IDs, object IDs, or hidden timestamps\].所有的行都是规则的\[亦即，列不存在任何隐藏的部分，例如行id，对象id或者隐藏的时间戳\]

Violation of any of these conditions would mean that the table is not strictly relational, and therefore that it is not in first normal form.违反这些条件中的任何一个都意味着该表不是严格关系型的，因此其不是第一范式。

Examples of tables (or views) that would not meet this definition of first normal form are:
* A table that lacks a unique key constraint. Such a table would be able to accommodate duplicate rows, in violation of condition 3.
* A view whose definition mandates that results be returned in a particular order, so that the row-ordering is an intrinsic and meaningful aspect of the view. (Such views cannot be created using SQL that conforms to the SQL:2003 standard.) This violates condition 1. The tuples in true relations are not ordered with respect to each other.
* A table with at least one nullable attribute. A nullable attribute would be in violation of condition 4, which requires every column to contain exactly one value from its column's domain. This aspect of condition 4 is controversial. It marks an important departure from Codd's later vision of the relational model, which made explicit provision for nulls. First normal form, as defined by Chris Date, permits relation-valued attributes (tables within tables). Date argues that relation-valued attributes, by means of which a column within a table can contain a table, are useful in rare cases.

[Second normal form](https://en.wikipedia.org/wiki/Second_normal_form)

2NF was originally defined by E. F. Codd in 1971.
第二范式最初是由E. F. Codd在1971年定义的。

A relation is in the second normal form if it fulfills the following two requirements:如果满足以下两个要求，则关系是第二范式
* It is in first normal form.它是第一范式。
* It does not have any non-prime attribute that is functionally dependent on any proper subset of any candidate key of the relation. A non-prime attribute of a relation is an attribute that is not a part of any candidate key of the relation.它不具有任何这样的非主属性，其在功能上依赖于关系的一个候选键的真子集。关系的非主属性不是关系的一个候选键一部分的属性。 

Put simply, a relation is in 2NF if it is in 1NF and every non-prime attribute of the relation is dependent on the whole of every candidate key. Note that it does not put any restriction on the non-prime to non-prime attribute dependency. 
简单而言，如果一个关系是第一范式，并且关系的每个非主属性都依赖于每个候选键的整体，而不是一部分，则这个关系是2NF。注意，它没有限制从非主属性到非主属性的依赖关系。

A functional dependency on part of any candidate key is a violation of 2NF. In addition to the primary key, the relation may contain other candidate keys; it is necessary to establish that no non-prime attributes have part-key dependencies on any of these candidate keys. 
对候选键的一部分的函数依赖是违反2NF的。除了主键之外，关系还可能包含其他候选键；必须确定非主属性对这些候选键中的任何一个不具有部分依赖性。 


[Third normal form](https://en.wikipedia.org/wiki/Third_normal_form)

Third normal form (3NF) is a database schema design approach for relational databases which uses normalizing principles to reduce the duplication of data, avoid data anomalies, ensure referential integrity, and simplify data management. It was defined in 1971 by Edgar F. Codd.


A database relation (e.g. a database table) is said to meet third normal form standards if all the attributes (e.g. database columns) are functionally dependent on solely the primary key. Codd defined this as a relation in second normal form where all non-prime attributes depend only on the candidate keys and do not have a transitive dependency on another key.

A hypothetical example of a failure to meet third normal form would be a hospital database having a table of patients which included a column for the telephone number of their doctor. The phone number is dependent on the doctor, rather than the patient, thus would be better stored in a table of doctors. The negative outcome of such a design is that a doctor's number will be duplicated in the database if they have multiple patients, thus increasing both the chance of input error and the cost and risk of updating that number should it change (compared to a third normal form-compliant data model that only stores a doctor's number once on a doctor table).

Codd later realized that 3NF did not eliminate all undesirable data anomalies and developed a stronger version to address this in 1974, known as Boyce–Codd normal form. 

Codd's definition states that a table is in 3NF if and only if both of the following conditions hold:
* The relation R (table) is in second normal form (2NF).
* Every non-prime attribute of R is non-transitively dependent on every key of R.


传递依赖

A non-prime attribute of R is an attribute that does not belong to any candidate key of R. A transitive dependency is a functional dependency in which X → Z (X determines Z) indirectly, by virtue of X → Y and Y → Z (where it is not the case that Y → X).

A 3NF definition that is equivalent to Codd's, but expressed differently, was given by Carlo Zaniolo in 1982. This definition states that a table is in 3NF if and only if for each of its functional dependencies X → A, at least one of the following conditions holds:
* X contains A (that is, A is a subset of X, meaning X → A is trivial functional dependency),
* X is a superkey,
* every element of A\X, the set difference between A and X, is a prime attribute (i.e., each attribute in A\X is contained in some candidate key).

Zaniolo's definition gives a clear sense of the difference between 3NF and the more stringent Boyce–Codd normal form (BCNF). BCNF simply eliminates the third alternative ("Every element of A \ X, the set difference between A and X, is a prime attribute."). 

[Boyce–Codd normal form](https://en.wikipedia.org/wiki/Boyce%E2%80%93Codd_normal_form)

Boyce–Codd normal form (or BCNF or 3.5NF) is a normal form used in database normalization. It is a slightly stronger version of the third normal form (3NF). BCNF was developed in 1974 by Raymond F. Boyce and Edgar F. Codd to address certain types of anomalies not dealt with by 3NF as originally defined.
If a relational schema is in BCNF then all redundancy based on functional dependency has been removed, although other types of redundancy may still exist. A relational schema R is in Boyce–Codd normal form if and only if for every one of its dependencies X → Y, at least one of the following conditions hold:
* X → Y is a trivial functional dependency (Y ⊆ X),
* X is a superkey for schema R.

Only in rare cases does a 3NF table not meet the requirements of BCNF. A 3NF table that does not have multiple overlapping candidate keys is guaranteed to be in BCNF. Depending on what its functional dependencies are, a 3NF table with two or more overlapping candidate keys may or may not be in BCNF. 


[database-normalization](https://www.learncomputerscienceonline.com/database-normalization/)
第一范式
* Each table cell shoul have atomic value 每个表单元应该具有原子值
* Each column (attribute) name should be unique 每列的名称应该是唯一的
* Table must have a primary key 表必须具有主键
* No repeating column groups allowed 不允许重复的列组


[Normalization of Database](https://www.studytonight.com/dbms/database-normalization.php)

For a table to be in the First Normal Form, it should follow the following 4 rules:
* It should only have single(atomic) valued attributes/columns.
* Values stored in a column should be of the same domain
* All the columns in a table should have unique names.
* And the order in which data is stored, does not matter.

[Facts and Fallacies about First Normal Form](https://www.red-gate.com/simple-talk/sql/learn-sql-server/facts-and-fallacies-about-first-normal-form/)

Some of the common definitions of 1NF in tutorials misuse the term “repeating groups”, or “repeated groups”.  Usually it goes like this: If there are no repeating groups in a table, then it is in First Normal Form.  
在教程中对于第一范式一些常用定义误用“重复组”这一术语。通常是这样描述的：“如果在一个表中没有重复的组，那么这个表就是第一个范式“。

Many writers misunderstand the concept of a repeating group and use it to claim that a certain table is in violation of 1NF.  Some people believe that a set of columns, usually similarly named, that are placed adjacent to each other in a table, and have  the same data type constitute a ‘repeating group’. 
很多作者错误理解了重复组的概念，使用其来声称某个表违反第一范式。一些人相信一些命名相似的、在表中的位置彼此相邻的并且具有相同数据类型的列构成了“重复组”

Well, simply put a repeating group is a column that can accommodate multiple values.  (2). The columns in a base table in SQL are explicitly named and typed and therefore can accommodate only a single value of that type (or a null in case of a nullable column which we will discuss in a while).  Therefore strictly speaking, a base table in SQL, cannot have a repeating group.  A SQL column with an integer data type, for example,  cannot contain a repeating group containing a set of several integers
简单的说，重复组指的是一个可以容纳多个值的列。在SQL中一个数据表的列是通过显式命名和定义类型，因此每列仅仅能够容纳此类型的单个值。因此，严格来说，SQL中不可能有重复组。

In the past, most people based their understanding of  1NF on the concept of atomicity — more specifically data value atomicity. That is, each value in a column must be a “single unit of data”. In fact some earlier database pioneers have defined atomic data, paraphrased,  as “data that cannot be decomposed into smaller pieces“. 
在过去，大多数人对于第一范式的理解是基于原则性概念，更具体来说是数值的原子性。也就说，在一列中的每个值必须是单一的数据单元。实际上，一些早期的数据库先驱将所定义的原子性数据解释为“不能分解为更小片段的数据”。

While this was considered appropriate for some time, it has turned out to be very vague and imprecise. For instance, how do we perceive an atomic value? Is a value declared as VARCHAR(10) considered atomic when we can decompose the string into individual characters? How can a value declared as DATETIME, which has year, month and day components and the time portion, have further decomposable elements? Well, the answer is “it depends”. Data value atomicity by itself is not an objective yardstick and has no absolute meaning (3). It depends on how we want to deal with the data. In other words, whether or not a data value is atomic is in the eye of the beholder.
尽管在一段时期内这种理解被认为是正确的，但是其已经被证明是非常模糊和不精确的。例如，我们怎么样认定一个原子值？我们可以将VARCHAR(10)定义的字符串分解成单个字符，是否将字符串视为原子值？ 如何能够将一个值定义为DATETIME类型，其具有年、月和日以及时间部分组成，并能够进一步地分解为元素。 好吧，答案是“取决于情况”。 数据值原子性本身不是客观的标准，也没有绝对意义。这取决于我们要如何处理数据。换句话说，数据值是否是原子的取决于旁观者。


[Normalization: What does “repeating groups” mean?](https://stackoverflow.com/questions/23194292/normalization-what-does-repeating-groups-mean#:~:text=The%20term%20%22repeating%20group%22%20originally%20meant%20the%20concept,exist%20in%20any%20modern%20relational%20or%20SQL-based%20DBMS.)

Eliminate repeating groups in individual tables。消除单个表中的重复组。

误解和误用了重复组这一个概念。重复组在E.F.Codd主要指的是在一个单独的域可能包含一个具有重复值的数组。

The term "repeating group" originally meant the concept in CODASYL and COBOL based languages where a single field could contain an array of repeating values. When E.F.Codd described his First Normal Form that was what he meant by a repeating group. The concept does not exist in any modern relational or SQL-based DBMS.

# Index & Performancey

Clustered Index Accessing a row through the clustered index is fast because the row data is on the same page (on disk) where the index search leads. 
* If in the table is set PRIMARY KEY – this is it. 
* Otherwise, if the table has UNIQUE indexes - this is the first of them. 
* Otherwise, InnoDB itself creates a hidden field with the surrogate ID in size of 6 bytes. 
This is why it’s very important to use a natural primary key whenever possible.


Data Warehouse: Star Index-De-normalize schemas 


聚簇索引 (主键索引)（Clustered Index (Primary Index)）


InnoDB中的聚簇索引采用B-Tree组织起来，每个节点都是一个Page（InnoDB存储记录的最小单位）；非叶节点存 Key 的值和指向孩子节点的指针，叶子节点则存储记录和指向相邻叶节点的指针（所有叶节点构成一个双向链表）


二级索引（Secondary Index）。二级索引同样使用B-Tree数据结构，不同的是叶节点只存储二级索引的键值和聚簇索引键值（通常是Primary Key），聚簇索引键值是用于回表查询该条记录

聚簇索引问题：
* 插入速度严重依赖于插入顺序。按照主键顺序往InnoDB中进行数据导入是最快的。如果不是按照主键插入，最好在导入完成后使用OPTIMIZE TABLE命令重新组织一下表。
* 聚簇索引在插入新行和更新主键时，可能导致“页分裂”问题：当插入到某个已满的叶子结点时，B+树会分裂成两个页来容纳新插入的行数据。页分裂会导致表占用更多的磁盘空间（不要用UUID或随机数做主键，而应该使用单调递增的值做主键）。

主键的选择和设计
* 主键的大小：是否需要通过该主键进行关联？最好是整数或者可枚举类型
* 写入性能和读取性能之间的折中？
* 访问模式：单个访问，还是批量查询和汇总？

[SQL queries on clustered and non-clustered Indexes](https://www.geeksforgeeks.org/sql-queries-on-clustered-and-non-clustered-indexes/?ref=lbp)

There are two types of indexing in SQL.
* Clustered index：数据存储的顺序与数据索引的顺序是一致的。
* Non-clustered index：A Non-clustered index stores the data at one location and indices at another location. The index contains pointers to the location of that data. 

KEY DIFFERENCE
* Cluster index is a type of index that sorts the data rows in the table on their key values whereas the Non-clustered index stores the data at one location and indices at another location.
* Clustered index stores data pages in the leaf nodes of the index while Non-clustered index method never stores data pages in the leaf nodes of the index.
* Cluster index doesn’t require additional disk space whereas the Non-clustered index requires additional disk space.
* Cluster index offers faster data accessing, on the other hand, Non-clustered index is slower.

[Clustered and Secondary Indexes](https://dev.mysql.com/doc/refman/8.0/en/innodb-index-types.html)

通常，聚簇索引是主键索引的同义词。聚簇索引等同于主键索引。

除了空间索引（Spatial index）之外，InnoDB索引采用B树数据结构。空间索引使用R树，其是一种专门用于索引多维数据的数据结构。

Every I
Database Internals： A Deep Dive into How Distributed Data Systems WorknnoDB table has a special index called the clustered index where the data for the rows is stored. Typically, the clustered index is synonymous with the primary key.

All indexes other than the clustered index are known as secondary indexes. In InnoDB, each record in a secondary index contains the primary key columns for the row, as well as the columns specified for the secondary index.

[8.8 Understanding the Query Execution Plan](https://dev.mysql.com/doc/refman/5.7/en/execution-plan-information.html)
[日常 Explain SQL，慢慢就懂得SQL调优了](https://mp.weixin.qq.com/s?__biz=Mzg3NjIxMjA1Ng==&mid=2247484371&idx=1&sn=2dd8269b94188240f0055a03a7ddd62d&chksm=cf34f9e4f84370f27e4a0154ee3f4ae8cf4b0ed78b4ea08adcba2d259a56c541e9083e3abc60&mpshare=1&scene=1&srcid=&sharer_sharetime=1590161808351&sharer_shareid=fc937fe50a97e6c10553c542abe0a39b&exportkey=AVvFPMTM%2BMmRiXHYR%2FX9SLA%3D&pass_ticket=MEmx%2FMYK8VidR%2FIzGjGwl831u7rhFBT3A8aHASx6xXXS8VO%2BGLjQV%2BNTc5FUYxmf#rd)


 派生表（Derived Table）

[EXPLAIN Output Format](https://dev.mysql.com/doc/refman/8.0/en/explain-output.html)

输出
1. id：表示查询中执行select子句或者操作表的顺序，id的值越大，代表优先级越高，越先执行。
2. select_type：select_type：表示 select 查询的类型，主要是用于区分各种复杂的查询，例如：普通查询、联合查询、子查询等
3. table：查询的表名，并不一定是真实存在的表，有别名显示别名，也可能为临时表
4. partitions：查询时匹配到的分区信息，对于非分区表值为NULL，当查询的是分区表时，partitions显示分区表命中的分区情况。
5. type：查询使用了何种类型，它在 SQL优化中是一个非常重要的指标，以下性能从好到坏依次是：system  > const > eq_ref > ref  > ref_or_null > index_merge > unique_subquery > index_subquery > range > index > ALL
6. possible_keys：这个索引并不定一会是最终查询数据时所被用到的索引
7. key：区别于possible_keys，key是查询中实际使用到的索引，若没有使用索引，显示为NULL
8. key_len：表示查询用到的索引长度（字节数），原则上长度越短越好 。
9. ref：表示将哪个字段或常量与key列所使用的字段进行比较
10. rows：全表扫描时表示需要扫描表的行数估计值；索引扫描时表示扫描索引的函数估计值。
11. filtered 表示符合条件的记录数的百分比. rows*filtered/100估算与explain前一个表进行连接的函数
12. Extra ：不适合在其他列中显示的信息
  * Using index：使用非主键索引，并且不需要回表查询
  * Using where：不通过索引查询所需要的数据
  * Using index condition：查询列不被索引覆盖，where条件中是一个索引范围查找，过滤完毕后回表找到符合条件的数据行。
  * Using temporary：使用临时表来处理查询
  * Using filesort
  * Using join buffer
  * Select table optimized away:使用某些聚合函数（min和max）来访问某个索引值。

 select_type 
* SIMPLE: Simple SELECT (not using UNION or subqueries)
* PRIMARY:	Outermost SELECT
* UNION:	Second or later SELECT statement in a UNION
* DEPENDENT UNION:	Second or later SELECT statement in a UNION, dependent on outer query
* UNION RESULT:	Result of a UNION.
* SUBQUERY:	First SELECT in subquery
* DEPENDENT SUBQUERY:	First SELECT in subquery, dependent on outer query
* DERIVED:	Derived table
* DEPENDENT DERIVED	:	Derived table dependent on another table
* MATERIALIZED:	Materialized subquery
* UNCACHEABLE SUBQUERY: A subquery for which the result cannot be cached and must be re-evaluated for each row of the outer query
* UNCACHEABLE UNION	:	The second or later select in a UNION that belongs to an uncacheable subquery (see UNCACHEABLE SUBQUERY)


type
* system
* const
* eq_ref
* ref
* fulltext
* ref_or_null
* index_merge
* unique_subquery
* index_subquery
* range
* index
* all

key_len
* 字符串
  * char(n): n个字节
  * varchar(n)：如果是utf-8，则3n+2字节，加的2个字节存储字符串长度。如果是utf8mb4，则4n+2字节
* 数值类型
  * tinyint：1字节
  * smallint：2字节
  * int：4字节
  * bigint ：8字节
* 时间类型
  * date：3字节
  * timestamp 4字节
  * datetime 8字节



* Using temporary; 
  * 增加tmp_table_size和max_heap_table_size，内存表和临时表的大小取上面两个参数的最小值
  * 下推条件
* Using filesort
  * 去掉order by
  * sort_buffer_size
* Using index: 表示直接访问索引就足够获取到所需要的数据，不需要通过索引回表
* Using where;表示优化器需要通过索引回表查询数据；
* Using index condition:先条件过滤索引，过滤完索引后找到所有符合索引条件的数据行，随后用 WHERE 子句中的其他条件去过滤这些数据行







```sql
show variables like '%profil%';

set  profiling=ON;

show  profile;

show profiles;
show profile all for query 9;
```

[Using temporary与Using filesort](https://blog.csdn.net/sz85850597/article/details/91907988)



ICP（Index Condition Pushdown）索引条件下推
* 尽可量利用二级索引，筛除不符合where条件的记录，从而减少整行记录读取，也就是要减少IO操作
* 对于InnoDB的聚簇索引来说，完整的行记录已经加载到缓存区了，索引下推也就没什么意义了。
* 子查询中的条件不能下推

[Index Condition Pushdown Optimization](https://dev.mysql.com/doc/refman/8.0/en/index-condition-pushdown-optimization.html)


```
SET optimizer_switch = 'index_condition_pushdown=off';
SET optimizer_switch = 'index_condition_pushdown=on';
```




Index Types
* Primary key vs Unique Key
  * Unique can be null
  * InnoDB is clustered based on PK
* B-Tree
  * In B-Tree, data are stored in the leaf nodes
  * Each secondary index has the PK in it. example: INDEX(name) is in fact(name,id)
  * avoid long PKs
  
* R-Tree
* Hash
* Full-text


[MySQL performance tuning](https://www.slideshare.net/anubioinfo/my-sql-performance-tuning-78825290?qid=a3c9f635-e08a-489c-adbb-439394c6e094&v=&b=&from_search=49)

* The IN claused in MySQL is very fast
* keep column alone on left side of condition
* Avoid % at the start of LIKE on an index
* Use Explain to see the execution plan for query
* If column used in order by clause are indeed they help with performance
* Try to convert<> operator to = operator
* Avoid using SELECT *


use mysqldumpslow command to get summaries of slow queries

* In MyISAM data pointers point to physical offset in the data file: All indexes are essentially equivalent
* In Innodb
   * PRIMARY KEY (UNIQUE KEY) stores data in leaf pages of the index, not pointer
   * Secondary indexes store primary key as data pointer
 
 
By default, MySQL sorts all GROUP BY col1, col2, … queries as if you specified ORDER BY col1, col2, … in the query as well. If a query includes GROUP BY but you want to avoid the overhead of sorting the result, you can suppress sorting by specifying ORDER BY NULL. 
```sql
SELECT a, COUNT(*) FROM bar GROUP BY a ORDER BY NULL
```   

* index: multi column efficient sorting。KEY(a,b)，要么按照a进行排序，要么在where a=A并且按照b进行排序。
* indexes are costly. Do not add more than you need.

Mysql sys Schema Find out all unused indexes: 
```sql
select * from sys.schema_unused_indexes;
```
Queries with errors or warnings: 
```sql
select * from sys.statements_with_errors_or_warnings; 
```

[Mysql performance tuning](https://www.slideshare.net/philipzhongl/mysql-performance-tuning?qid=a3c9f635-e08a-489c-adbb-439394c6e094&v=&b=&from_search=30)

Types of I/O schedulers 
* noop: Sorting incoming i/o requests by logical block address, that’s all 
* deadlilne: Prioritize read (sync) requests rather than write requests (async) to some extent (to avoid “write-starving-reads” problem) 
* cfq(default): Fairly scheduling i/o requests per i/o thread –

Default is cfq, but noop / deadline is better in many cases 
```shell
echo noop > /sys/block/sdX/queue/scheduler
```
File System Tunning
* Make sure to use Flash Back Write Cache(FBWC) or Battery Backed up Write Cache (BBWC) on raid cards –
* Do not set “write barrier” on file systems (enabled by default in some cases)
* Consider disabling atime updates on files and directories


*Put sequentially written files on HDD 
   * ibdata, ib_logfile, binary log files 
   * HDD is fast enough for sequential writes 
   * Write performance deterioration can be mitigated 
   * Life expectancy of SSD will be longer
* Put randomly accessed files on SSD 
   * \*ibd files, index files(MYI), data files(MYD) 
   * SSD is 10x -100x faster for random reads than HDD 
   * Archive less active tables/records to HDD 
   * SSD is still much expensive than HDD• 


MySQL Parameters Tuning: Buffered I/O(InnoDB Buffer Pool <--> FileSystem Cache <--> InnoDB data File) --> Direct I/O(InnoDB Buffer Pool <--> InnoDB data File)

MySQL Profile
```sql
Mysql>SET profiling = 1;
Mysql>SHOW PROFILES;
Mysql>SHOW PROFILE CPU FOR QUERY 1;
```


[MySQL Performance Tuning: The Perfect Scalability (OOW2019) ](https://www.slideshare.net/MirkoOrtensi/mysql-performance-tuning-the-perfect-scalability-oow2019?qid=a3c9f635-e08a-489c-adbb-439394c6e094&v=&b=&from_search=46)

data and concurrency grow: more data and more active connections

I/O,CPU and Network bound
* More locks + scans
* Buffer pool should be increased
* More connections thread
* I/O thoughput

I/O Bound Monitoring 
* iostat 
* SHOW ENGINE INNODB STATUS 
* Performance schema (MEM) 
* SYS schema 
```sql
select * from sys.io_by_thread_by_latency; 
select * from sys.io_global_by_file_by_bytes; 
select * from sys.io_global_by_file_by_latency; 
select * from sys.waits_global_by_latency; 
select * from sys.statements_with_temp_tables;
```

I/O Bound: 
* Redo log: innodb_log_group_home_dir, innodb_log_files in_group
* binary log: log_bin
* undo logs: innodb_undo_directory
* external tablespace: file-per_talbe, DATA DIRECTORY, CREATE TABLESPACE
* partitioning
* session and globale temporary tablespace: innodb_temp_data_file_path
* logging:
   * general log: general_log_file
   * slow query log: slow_query_log_file
   * audit log: audit_log_file
* Flush method: Data can travel through different layer before reaching the durable storage. application cache(buffer pool, log file cache)-->Kernel cache(Buffer/Page cache)--> storage cache(eventually battery backed). innodb_flush_method
   * fsync
   * O_DIRECT
   * O_DIRECT_NO_FSYNC
   * O_DSYNC

CPU Bound Monitoring 
* vmstat / mpstat 
* Status 
```sql
SHOW STATUS LIKE "Handler%"; 
SHOW STATUS LIKE "select_full_join"; 
sys schema
```sql
select * from sys.schema_redundant_indexes; 
select * from sys.schema_unused_indexes; 
select * from sys.statements_with_sorting; 
CALL sys.diagnostics(60, 60, 'current');
SELECT * FROM sys.schema_tables_with_full_table_scans; 
```
NETWORK Bound Compression --compress: Compress all information sent between the client and the server if possible

# DevOpt

[Optimizing Database Performance](https://www.xaprb.com/slides/percona-live-2019-optimizing-database-performance-efficiency/#1)

The CELT metrics reveal everything about workload QoS.
* Concurrency is the number of simultaneous requests NNN
* Error Rate is what it sounds like
* Latency is response time, as previously defined RRR
* Throughput is requests per second XXX

These can all be calculated as average (or p99) during intervals or as they apply to individual requests (except for Throughput).


The workload places demand on four key resources.
* CPU cycles
* Memory
* Storage
* Network

The way resources respond to demand often explains performance.


The Three Golden Signals of Resource Sufficiency: Brendan Gregg’s USE method:
* Utilization
* Saturation
* Errors

The CELT and USE metrics are the seven golden signals of overall system health and performance, unifying the external (customer, workload) and internal (resource) perspectives.

There are three primary ways to measure requests (workload):
* Turn on full query logging
* Use internal statistics tables/views, if they exist
* Sniff network traffic


[More mastering the art of indexing ](https://www.slideshare.net/matsunobu/more-mastering-the-art-of-indexing)

* Lock contention and indexing
* deadlock caused by indexes
* covering index and range scan
  * Covering index: Reading only an index. If all columns in the SQL statment are contained within single index, MySQL chooses "Chovering index" execution plan.
* Sorting, indexing and query execution plans

[MySQL Indexing - Best practices for MySQL 5.6](https://www.slideshare.net/myxplain/mysql-indexing-best-practices-for-mysql)

Types of Indexes you might heard about 
* BTREE Indexes – Majority of indexes you deal in MySQL is this type 
* RTREE Indexes – MyISAM only, for GIS 
* HASH Indexes – MEMORY, NDB 
* FULLTEXT Indexes – MyISAM, Innodb starting 5.6

B+ Trees are typically used for Disk storage – Data stored in leaf nodes

In MyISAM data pointers point to physical offset in the data file 
* All indexes are essentially equivalent 
In Innodb 
* PRIMARY KEY (Explicit or Implicit) - stores data in the leaf pages of the index, not pointer 
* Secondary Indexes – store primary key as data pointer 

Impact on Cost of Indexing 
* Long PRIMARY KEY for Innodb – Make all Secondary keys longer and slower 
* Random” PRIMARY KEY for Innodb – Insertion causes a lot of page splits 
* Longer indexes are generally slower 
* Index with insertion in random order – SHA1(‘password’) 
* Low selectivity index cheap for insert – Index on gender 
* Correlated indexes are less expensive – insert_time is correlated with auto_increment id

Index Innodb tables: data is clustered by Primary Key.

The First Rule of MySQL Optimizer 
* MySQL will stop using key parts in multi part index as soon as it met the real range (<,>, BETWEEN), it however is able to continue using key parts further to the right if IN(…) range is used 

MySQL Using Index for Sorting Rules 
* You can’t sort in different order by 2 columns 
* You can only have Equality comparison (=) for columns which are not part of ORDER BY – Not even IN() works in this case

MySQL Can use More than one index – “Index Merge” 
* SELECT * FROM TBL WHERE A=5 AND B=6 
   * Can often use Indexes on (A) and (B) separately 
   * Index on (A,B) is much better 
* SELECT * FROM TBL WHERE A=5 OR B=6 
   * 2 separate indexes is as good as it gets
   * Index (A,B) can’t be used for this query 
   
You can build Index on the leftmost prefix of the column 
```sql
ALTER TABLE TITLE ADD KEY(TITLE(20)); –
```

join_buffer_size

ICP(Index Condition Pushdown)






# Cluster

[Spider Server System Variables](https://mariadb.com/kb/en/library/spider-server-status-variables/)

```sql
SHOW SLAVE STATUS\G;
START SLAVE;
STOP SLAVE;

SHOW BINARY LOGS

SHOW BINLOG EVENTS

SHOW MASTER STATUS

SHOW SLAVE HOSTS 


```shell
/usr/local/mariadb/bin/mysqlbinlog  --start-datetime='2018-07-26 09:50:00' --base64-output=decode-rows -v /var/mariadb/data/mysql-bin.000216 --result-file=binglog.sql
```
[Vitess, A database clustering system for horizontal scaling of MySQL](https://vitess.io/)


## Performance

```sql
OPTIMIZE [NO_WRITE_TO_BINLOG | LOCAL] TABLE tbl_name [, tbl_name] ... [WAIT n | NOWAIT]
```

show profile默认的是关闭的，但是会话级别可以开启这个功能。开启它可以让MySQL收集在执行语句的时候所使用的资源。
```
SET profiling = 1;

execute sql

SHOW PROFILES\G;
```

```
SHOW PROFILE [type [, type] ... ]
    [FOR QUERY n]
    [LIMIT row_count [OFFSET offset]]

type: {
    ALL
  | BLOCK IO
  | CONTEXT SWITCHES
  | CPU
  | IPC
  | MEMORY
  | PAGE FAULTS
  | SOURCE
  | SWAPS
}
```
The values of n correspond to the Query_ID values displayed by SHOW PROFILES.




[SHOW PROFILE Statement](https://dev.mysql.com/doc/refman/5.7/en/show-profile.html)

Profiling information is also available from the INFORMATION_SCHEMA PROFILING table. 

```
HOW PROFILE FOR QUERY 2;

SELECT STATE, FORMAT(DURATION, 6) AS DURATION
FROM INFORMATION_SCHEMA.PROFILING
WHERE QUERY_ID = 2 ORDER BY SEQ;
```

[The INFORMATION_SCHEMA PROFILING Table](https://dev.mysql.com/doc/refman/5.7/en/profiling-table.html)

# Configuration


innodb_log_file_size :larger = longer recovery times


[MariaDB / MySQL tripping hazard and how to get out again?](https://www.slideshare.net/shinguz/mariadb-mysql-tripping-hazard-and-how-to-get-out-again)

ibdata1 is called the System tablespace: Today it contains only "system"data

innodb_file_per_table=on

Do not store BLOBS in the RDBS but on a filter (Disk, NAS, SAN)
* Query latency higher 
* Database throughput lower
* Backup size and time will increase
* DDL operations will take ages
* Buffer Pool (cache) is flooded

Disk full is more or less the worst you can do to your database
* mmonitor your disk space!
* Try to predict how long it will take until disk is full.

```
connection_timeout
max_connections
max_allowed_packet
innodb_numa_interleave
```

Optimization with Innodb 
* Turn off linux caching by disabling O_DIRECT 
* innodb_buffer_pool_size = (.70 * total_mem_size) 
* bulk-insert-buffer-size=256M 
* innodb_buffer_pool_instances = tune for concurrency 
* innodb_thread_concurrency = 2 x CPUs 
* innodb_flush_method = O_DIRECT (avoids double buffering) 



[采坑之使用MySQL，SQL_MODE有哪些坑](https://dev.mysql.com/doc/refman/8.0/en/sql-mode.html)


```sql
SELECT @@GLOBAL.sql_mode;
SELECT @@SESSION.sql_mode;
```

Use IFNULL or COALESCE:

The COALESCE function accepts two arguments and returns the second argument if the first argument is NULL; otherwise, it returns the first argument.

[Server SQL Modes](https://dev.mysql.com/doc/refman/8.0/en/sql-mode.html)


[6 Tips to MySQL Performance Tuning ](https://www.slideshare.net/Oracle_MySQL/6-tips-to-mysql-performance-tuning?qid=a3c9f635-e08a-489c-adbb-439394c6e094&v=&b=&from_search=17)

Ensure all tables hava a PRIMARY KEY

InnoDB organizes the data according to the PRIMARY KEY
* The PRIMARY KEY is included in all secondary indexes in order to be able to locate the actual row -> smaller PRIMARY KEY gives smaller secondary indexes.
* A mostly sequential PRIMARY KEY is in general recommended to avoid inserting rows betwween existing rows.

 If you use InnoDB, enable all the INNODB_METRICS counters: innodb_monitor_enable='%', the overhead has turned out to be small so worth the extra details.
 
 Ensure the performance schema is enabled. The performance schema can also be configured dynamically at runtime.
 
 Capacity settings - innodb_buffer_pool_size
 * How much memory does the host have?
 * Subtract memory required by OS and other processes
 * Subtract memoery required by MySQL other then the InnoDB buffer
 * Choose minimum of the and the size of the "working data set"

Capacity Setting - InnoDB redo log
* total size = innodb_log_file_size * innodb_log_files-in_group
* Should be large enought to avoid "excessive" checkpointing
* the larger redo log, the slower shutdowns potentially

Innodb redo log - Is it large enougth
```sql
MariaDB [**]> show engine innodb status\G;

---
LOG
---
Log sequence number 44272443141888
Log flushed up to   44272443141888
Pages flushed up to 44270928721766
Last checkpoint at  44270908839819
0 pending log flushes, 0 pending chkp writes
32383062 log i/o's done, 427.78 log i/o's/second
----------------------


MariaDB [**]> SELECT name, count FROM information_schema.innodb_metrics WHERE name like "log_lsn_%";

MariaDB [adm]> show global variables like "innodb_log_file%";
+---------------------------+-------------+
| Variable_name             | Value       |
+---------------------------+-------------+
| innodb_log_file_size      | 17179869184 |
| innodb_log_files_in_group | 1           |
+---------------------------+-------------+
```

Calculate the amount of used redo log

Used log = log_lsn_current-log_lsn_last_checkpoint=44272443141888-44270908839819=1534302069

used%= (used log/total log) * 100=1534302069/17179869184*100=8.93

if used% reaches 75% an asychronous flush is tirggered.

InnoDB Undo log
* innodb_undo_tablespaces can only be set before initializing the datadir
* Each undo tablespace file is 10M initially

other capacity options
* max_connecton: be careful setting the too large as each connection requires memory
* table_definition_cache: ensure all tables can be in the cache. If you expect 4000 tables, set table_definition_cache>4000
* table_open_cache: each table can be open more than once
* table_open_cache_instance: typicall a good value is 16.

Buffers and Caches
* join_buffer_size
* sort_buffer_size

Linux glibc malloc change memory allocation algorithm when crossing threshold: Algorithm for larger allocations can be 40 times slower than for smaller allocation.
```
MariaDB [**]> show global status like "sort_merge_passes";
+-------------------+-------+
| Variable_name     | Value |
+-------------------+-------+
| Sort_merge_passes | 0     |
+-------------------+-------+

```

Data Consistency versus Performance
* innodb_flush_log_at_trx_commit
  * 1: is theoretically the slowest, but with fast SSD it may be arount as fast as 2 and 0. Defaults to 1, flush the redo log after each commit. Required for D in ACID
  * 2: flushed every second: transactions may be lost if the OS crashes
  * 0: MySQL never fsyncs  
* sync_binlog: specifies how many transactions between each flush of the binary log
  * 0: when rotating the binary log or when the OS decides
  * 1: at everty transaction commit - this is the saftest
  * N: every N commites
  * MySQL 5.6 and later support group commit for InnoDB giving less overhead of sync_binlog=1
  
I/O Scheduler
```
cat /sys/block/sda/queue/scheduler

echo deadline > /sys/block/sda/queue/scheduler

cat /sys/block/sda/queue/scheduler
```
  
  
[Optimizing MariaDB for maximum performance ](https://www.slideshare.net/MariaDB/optimizing-mariadb-for-maximum-performance?qid=2c51b4b8-e618-4342-a975-2fb06ee22c57&v=&b=&from_search=24)  
We deprecate & hard-wire a number of parameters, including the following:
```
innodb_buffer_pool_instances=1, innodb_page_cleaners=1 
innodb_log_files_in_group=1 (only ib_logfile0) 
innodb_undo_logs=128 (the “rollback segment” component of DB_ROLL_PTR)
```
Operating System System 
```shell
# sysctl -w vm.swappiness=1 
# echo "vm.swappiness=1" >> /etc/sysctl.conf 
``` 
```shell
# echo noop > /sys/block/sda/queue/scheduler  
```
```shell
 # cat /etc/security/limits.conf 
 mysql soft nofile 65535 
 mysql hard nofile 65535  
 ```
 ```shell
# cat /etc/fstab ... rw,noatime,nodiratime,data=writeback 
```
 Server Variables MariaDB Server 
```
max_allowed_packet = e.g. 128G-256G 
max_connections = e.g. 2000-10000 

thread_handling = pool-of-threads 
thread_pool_size = # of cpu cores 
thread_pool_max_threads = 65536 t
hread_pool_min_threads = e.g. 8 
thread_pool_idle_timeout = 60 

query_cache_size = 0 
query_cache_type = 0 

skip_name_resolv = ON 

thread_cache_size = DON'T SET (Auto) 

sync_binlog = e.g. 1000

innodb_buffer_pool_size = e.g. 256M-900G 
#((Total RAM - (OS + Apps)
#- (mysqld memory + query buffers)
#- caches for things like binary log 
#- other possible buffers and caches 
#- memory tables) 
#/ 105% ) | ROUND_DOWN
innodb_log_file_size = e.g. 2G-16G 
innodb_stats_on_metadata = 0 
innodb_flush_log_at_trx_commit = e.g. 0? (IFLATC) 

innodb_flush_method = O_DIRECT 
innodb_io_capacity = e.g. 2000 
innodb_adaptive_hash_index_parts = e.g. 2-8 btr0sea.c

innodb_autoinc_lock_mode = e.g. 2 
innodb_flush_neighbors = e.g. 0 w/SSD 

innodb_lru_scan_depth = e.g. 4096 
innodb_sync_array_size = e.g. 16-32 (but < # of cpu cores) 

innodb_read_io_threads = 4 
innodb_write_io_threads = 4 

```

show information of queries that take long time to execute
```
log_slow_queries=1
slow_query_log_file=<some file name>
```


MySQL uses memory in 2 ways – Global buffers and per connection buffers.

Global memory + (max_connections * session buffers)
 
```sql
SHOW GLOBAL VARIABLES;
SHOW GLOBAL STATUS
```

The Com_xxx statement counter variables indicate the number of times each xxx statement has been executed. 


Handler_*
* Handler_read_first
* Handler_read_key
* Handler_read_next
* Handler_read_prev
* Handler_read_rnd
* Handler_read_rnd_next

innodb_*
* innodb_buffer_pool_pages_data
* innodb_buffer_pool_pages_free
* innodb_buffer_pool_pages_total

* threads_cached
* threads_connected
* thread_created


InnoDB中有共享表空间和独立表空间的概念。共享表空间就是ibdata1，独立表空间放在每个表的.ibd（数据和索引）和.frm（表结构）为后缀的文件中。单独的表空间只存储该表的数据，索引和插入缓冲的BITMAP等信息，其余还放在共享表空间中


[InnoDB File-Per-Table Tablespaces](https://mariadb.com/kb/en/innodb-file-per-table-tablespaces/)


```
innodb_file_per_table=ON
```

* 默认情况下，InnoDB的表空间创建在系统数据目录中，其根据系统配置参数*datadir*来配置
* 也可以通过innodb_data_home_dir系统变量来设置InnoDB的表空间存储位置
* 还可以通过DIRECTORY来设置每个表的存储位置
```
CREATE TABLE test.t1 (
   id INT PRIMARY KEY AUTO_INCREMENT,
   name VARCHAR(50)
) ENGINE=InnoDB
DATA DIRECTORY = "/data/contact";
```



文件目录
* 配置文件
  /etc/my.cnf, /etc/mysql/my.cnf, /usr/local/mysql/etc/my.cnf, ~/.my.cnf
  
* 日志文件
  error log, general log, binary log, relay log, slow query log


InnoDB中有共享表空间和独立表空间的概念。共享表空间就是ibdata1，独立表空间放在每个表的.ibd（数据和索引）和.frm（表结构）为后缀的文件中。单独的表空间只存储该表的数据，索引和插入缓冲的BITMAP等信息，其余还放在共享表空间中

https://mariadb.com/kb/en/innodb-system-tablespaces/

数据文件
* ibdata1: 如果不指定innodb_file_per_table=ON参数单独保存每个表的数据，MySQL的数据都会存放在ibdata1文件里. InnoDB使用这个系统表空间存储数据目录、更改换成和undo日志。
  
  
  
  
  
  
   'utf8_unicode_ci' is a collation of the deprecated character set UTF8MB3. Please consider using UTF8MB4 with an appropriate collation instead. 

   mysql_tzinfo_to_sql /usr/share/zoneinfo | mysql -u root -h 127.0.0.1 mysql -p
  
  
  MySQL FROM_UNIXTIME(date) 函数把 UNIX 时间戳转换为普通格式的日期时间值，与 UNIX_TIMESTAMP 函数互为反函数.TIME_FORMAT(time, format) 

  CONVERT_TZ (datetime, from_tz, to_tz)
  
```
  select @@global.sql_mode;
```

  https://dev.mysql.com/doc/refman/8.0/en/mysql-tzinfo-to-sql.html


## 权限

```
sudo systemctl status mysql

sudo systemctl restart mysql
```

https://dev.mysql.com/doc/refman/8.0/en/grant.html#:~:text=Privileges%20Supported%20by%20MySQL%20%20%20%20Privilege,%20d%20...%20%2029%20more%20rows%20

  ```
ALTER USER 'metabase'@'%' IDENTIFIED BY 'password' PASSWORD EXPIRE NEVER;
alter user 'metabase'@'%' identified with mysql_native_password by 'quchunhe';

  SET GLOBAL validate_password.policy=LOW;
-- 创建用户

CREATE USER 'root'@'localhost' IDENTIFIED BY 'password';

-- 查看用户

SELECT user, host, authentication_string FROM mysql.user WHERE user='myuser';

-- 删除用户
DROP USER 'root'@'localhost';

-- 修改用户密码

SET PASSWORD FOR 'jeffrey'@'localhost' = 'auth_string';


-- 查看权限

SHOW GRANTS FOR myuser;

-- 授予权限

GRANT ALL  PRIVILEGES ON *.* TO 'root'@'localhost' IDENTIFIED BY 'password';

GRANT SELECT ON db2.invoice TO 'jeffrey'@'localhost';

-- 生效(刷新权限)

FLUSH PRIVILEGES;

-- 撤销权限

REVOKE ALL ON robotbi.* FROM 'quchunhe'@'192.168.%';
REVOKE 'role1', 'role2' FROM 'user1'@'localhost', 'user2'@'localhost';
REVOKE SELECT ON world.* FROM 'role3';

```

# Lock

加锁方式划分
* Implicit Locking
* Explicit Locking
   * Select...For Update statement
   * Lock Table statement
   
为了提供更好的并发性，对于读和写操作分别采用不同的锁，分别为
* Shared Lock
* Exclusive Lock

根据锁的粒度，说可以划分为
* Row Lock：行锁只针对操作的当前行进行加锁
* Page Lock：页锁应用于 BDB 存储引擎。
* Table Lock：表锁为表级别的锁，记会锁定整个表

[MySQL介于普通读和锁定读的加锁方式](https://mp.weixin.qq.com/s?__biz=MzIxNTQ3NDMzMw==&mid=2247484352&idx=1&sn=799a109943108ce3ed139d0b684f18f8&chksm=97968a32a0e10324bd808b23ab376796f49c5998c6d917bf8f0073936cf1b128ac30742aebb8&mpshare=1&scene=1&srcid=01046CqxEFUnP5P2zo7hKda5&sharer_sharetime=1578110785863&sharer_shareid=fc937fe50a97e6c10553c542abe0a39b&exportkey=AW49gRrpesj66SITcN8Z3Fg%3D&pass_ticket=kOI4SUiiSQZgtNAcX5IS41mTJmr%2FciBGq3MXwztfKxT51U1FpE7lMYqAa9JxIFu2#rd)


[InnoDB Locking](https://dev.mysql.com/doc/refman/5.7/en/innodb-locking.html)


- A shared (S) lock permits the transaction that holds the lock to read a row.
- An exclusive (X) lock permits the transaction that holds the lock to update or delete a row

InnoDB supports multiple granularity locking which permits coexistence of row locks and table locks. For example, a statement such as LOCK TABLES ... WRITE takes an exclusive lock (an X lock) on the specified table. 

 Intention locks are table-level locks that indicate which type of lock (shared or exclusive) a transaction requires later for a row in a table. There are two types of intention locks:
- An intention shared lock (IS) indicates that a transaction intends to set a shared lock on individual rows in a table.
- An intention exclusive lock (IX) indicates that a transaction intends to set an exclusive lock on individual rows in a table. 

For example, SELECT ... LOCK IN SHARE MODE sets an IS lock, and SELECT ... FOR UPDATE sets an IX lock. 

Intention locks do not block anything except full table requests (for example, LOCK TABLES ... WRITE). The main purpose of intention locks is to show that someone is locking a row, or going to lock a row in the table. 

A record lock is a lock on an index record. 

A gap lock is a lock on a gap between index records, or a lock on the gap before the first or after the last index record.

Gap locks in InnoDB are “purely inhibitive”, which means that their only purpose is to prevent other transactions from inserting to the gap. Gap locks can co-exist. A gap lock taken by one transaction does not prevent another transaction from taking a gap lock on the same gap.


A next-key lock is a combination of a record lock on the index record and a gap lock on the gap before the index record.



[AUTO_INCREMENT Handling in InnoDB](https://dev.mysql.com/doc/refman/5.7/en/innodb-auto-increment-handling.html)

“INSERT-like” statements 
* “Simple inserts”: Statements for which the number of rows to be inserted can be determined in advance (when the statement is initially processed).  
* “Bulk inserts”: Statements for which the number of rows to be inserted (and the number of required auto-increment values) is not known in advance. 
* “Mixed-mode inserts”: These are “simple insert” statements that specify the auto-increment value for some (but not all) of the new rows.

innodb_autoinc_lock_mode
* innodb_autoinc_lock_mode = 0 (“traditional” lock mode) 
* innodb_autoinc_lock_mode = 1 (“consecutive” lock mode) 
* innodb_autoinc_lock_mode = 2 (“interleaved” lock mode) 


[14.7.1 InnoDB Locking](https://dev.mysql.com/doc/refman/5.7/en/innodb-locking.html)

**Dirty Read**:  An operation that retrieves unreliable data, data that was updated by another transaction but not yet committed. It is only possible with the isolation level known as read uncommitted

**Phantom Read**： A row that appears in the result set of a query, but not in the result set of an earlier query. For example, if a query is run twice within a transaction, and in the meantime, another transaction commits after inserting a new row or updating a row so that it matches the WHERE clause of the query.

  This occurrence is known as a phantom read. It is harder to guard against than a non-repeatable read, because locking all the rows from the first query result set does not prevent the changes that cause the phantom to appear

**Repeatable Read**


[划重点！你还在困惑MySQL中的"锁"吗？](https://mp.weixin.qq.com/s?__biz=MzI3NDA4OTk1OQ==&mid=2649903745&idx=1&sn=7cd6111a400186c6c7d4806f4277ceca&chksm=f31fa009c468291f683d6ac1de0a0a5a767e629a9da47b6f9c1f675a4c5a3835b48568b48fe6&mpshare=1&scene=1&srcid=0427WrpaKOREnrzqtACZ1Lwv&sharer_sharetime=1587972414462&sharer_shareid=fc937fe50a97e6c10553c542abe0a39b&exportkey=Af3svVFvaH5D4v6WMzjSpw8%3D&pass_ticket=dQPTuWQMQvIImHS%2Frl41EVuA7Uh8PT6VumsOGO8w14tdeRR2aOM7wmGBoT4lfOSK#rd)

* 乐观锁(optimistic locking)
* 悲观锁(pessimistic locking)

* 记录锁(record locking)
* 间隙锁（gap locking）
* 临键锁（next-key locking），其中临键锁=记录锁+间隙锁


加锁粒度
* 行锁（row-level locking）
* 表锁（table-level locking）

* 共享锁（share locking，S锁）,读锁
* 排他锁（exclusive locking，X锁），写锁

```sql
select ... for update;
select ... lock in share mode;
select * from performance_schema.data_lock;
```



意向锁（intention locking）

普通select语句不加锁，如想加锁只需在select语句后明确指定"for share"或"for update"即可，其中前者就是共享锁（S锁），也叫读锁；后者是排他锁（X锁），也叫写锁

insert、update和delete都会自动加锁，而且加的是排他锁（X锁）

* MVCC（multi-version concurrency control，即多版本并发控制）
* LBCC（locking-based concurrency control）

四大隔离等级
* 读未提交（Read Uncommitted，RU）
* 读已提交（Read Committed，RC）
* 可重复读（Repeatable Read，RR）
* 串行化（Serializable， SE）

read phenomena，主要是指数据库中三种"错误"的读取结果：
* 脏读：dirty read，即A事务读取了B事务更改但未提交的信息，主要发生在RU隔离级别
* 不可重复读，non-repeatable read，即由于B事务在A事务期间对数据更改并已提交，导致A事务前后读取到不一致的结果
* 幻读，phantom read，即A事务在之后的查询中出现了前期未出现的记录。顾名思义，是指读到了之前未曾发现的记录，当然，从某种意义上将之前未曾发觉肯定也属于不可重复读，这样理解本身是没错的，只是二者侧重点不一样。幻读侧重于在本事务执行期间，其他事务插入（insert）了新的记录，造成本事务之后读取到了前期不曾发现的事务，好似发生幻觉一样，是谓幻读。

快照读，snapshot read，也叫一致读或非加锁读，consistent nonlocking read，指不依靠加锁来保证查询数据一致性，是MySQL中RR和RC级别下的默认查询语句执行方式，通过MVCC机制实现按"快照"版本号执行读操作。RR级别和RC级别采集"快照"原则是不同的，这也是导致两种隔离级别存在不同"读象"（不可重读或幻读）的原因，其中：
* RR级别以进入事务后第一次读操作的时间作为快照版本(注意是第一次读操作的时间，而与开启事务时间无关)，一旦确定快照版本，则在本事务后续读操作中就都应用此快照结果
* RC级别是每次读操作时均采集快照，所以当其他事务提交后它能及时采集到新的快照
 
 SE级别因为是靠加锁（默认对普通select语句加S锁）来实现数据一致，能够确保读取到一致的结果，但已不是原原本本的一致读
 
 当前读，current read，也叫加锁读，即locking read，特指在普通查询语句后增加"for share"或"for update"来指定共享读或排他读的读操作，其中：
* for share，即加S锁，允许多个事务同时获取该S锁，是谓共享
* for update，即加X锁，仅供获取到该X锁的事务操作，是谓排他
由于加锁读是建立在事务的基础上，所以必须显式开启事务后，加锁读才有意义

RR级别中一旦建立了快照版本，则在该事务的后续查询中均采用该快照版本作为结果（当然，通过前面的案例发现也有例外）；与之对应的是，RC级别中，每次查询都采集最新的快照版本作为结果，所以自然也就存在不可重复读的问题。


锁、时间戳、乐观并发控制和悲观并发控制是并发控制主要采用的技术手段。

悲观并发控制（又名“悲观锁”，Pessimistic Concurrency Control，缩写“PCC”）是一种并发控制的方法。它可以阻止一个事务以影响其他用户的方式来修改数据。如果一个事务执行的操作读某行数据应用了锁，那只有当这个事务把锁释放，其他事务才能够执行与该锁冲突的操作。

悲观并发控制主要用于数据争用激烈的环境，以及发生并发冲突时使用锁保护数据的成本要低于回滚事务的成本的环境中。 


乐观并发控制（又名“乐观锁”，Optimistic Concurrency Control，缩写“OCC”）是一种并发控制的方法。它假设多用户并发的事务在处理时不会彼此互相影响，各事务能够在不产生锁的情况下处理各自影响的那部分数据。在提交数据更新之前，每个事务会先检查在该事务读取数据后，有没有其他事务又修改了该数据。如果其他事务有更新的话，正在提交的事务会进行回滚。乐观事务控制最早是由孔祥重（H.T.Kung）教授提出[1]。

乐观并发控制多数用于数据争用不大、冲突较少的环境中，这种环境中，偶尔回滚事务的成本会低于读取数据时锁定数据的成本，因此可以获得比其他并发控制方法更高的吞吐量
乐观并发控制的事务包括以下阶段：
1. 读取：事务将数据读入缓存，这时系统会给事务分派一个时间戳。
2. 校验：事务执行完毕后，进行提交。这时同步校验所有事务，如果事务所读取的数据在读取之后又被其他事务修改，则产生冲突，事务被中断回滚。
3. 写入：通过校验阶段后，将更新的数据写入数据库。


Metadata Locking 元数据上锁。 table metadata lock（DML）不仅适用于表，还适用于模式和存储程序(过程、函数、触发器和计划的事件)

# JDBC


[Configuration Properties](https://dev.mysql.com/doc/connector-j/8.0/en/connector-j-reference-configuration-properties.html)

# SQL


## Subquery 子查询

[Subqueries](https://dev.mysql.com/doc/refman/5.7/en/subqueries.html)


  
  
```
SHOW FULL TABLES 
WHERE table_type = 'VIEW'
```


[Subqueries](https://mariadb.com/kb/en/subqueries/)

[Correlated subquery](https://en.wikipedia.org/wiki/Correlated_subquery)

In a SQL database query, a correlated subquery (also known as a synchronized subquery) is a subquery (a query nested inside another query) that uses values from the outer query. Because the subquery may be evaluated once for each row processed by the outer query, it can be slow.

```sql
SELECT employee_number, name
FROM employees emp
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
    WHERE department = emp.department);
```


# Availability & Reliability


[Best practices for MySQL/MariaDB Server/Percona Server High Availability ](https://www.slideshare.net/bytebot/best-practices-for-mysqlmariadb-serverpercona-server-high-availability?qid=688000eb-0784-40ec-82ba-bda9163b0bf4&v=&b=&from_search=48)

High Availability
* Performance Scalability: Throughtput and latency
* Clustering, Failover
* Replication: Redundancy
* Duarablity: replicas, backup

Estimates of levels of availability

HA is Redundancy
* RAID: disk crashes? Another works 
* Clustering: server crashes? Another works 
* Power: fuse blows? Redundant power supplies 
* Network: Switch/NIC crashes? 2nd network route 
* Geographical: Datacenter ofﬂine/destroyed? Computation to another DC 

Redundancy through client-side XA transactions 
* Client writes to 2 independent but identical databases 
* HA-JDBC (http://ha-jdbc.github.io/) 
* No replication anywhere

Redundancy through shared storage: Oracle RAC, ScaleDB

Redundancy through disk replication

Redundancy through MySQL replication
* MySQL replication
* Tungsten Replicator
* Galera Cluster
* MySQL Cluster(NDBCluster)
* Huge potential for scaling out

The logs 
* Binary log (binlog) - events that describe database changes 
* Relay log - events read from binlog on master, written by slave i/o thread 
* master_info_log - status/conﬁg info for slave’s connection to master
* relay_log_info_log - status info about execution point in slave’s relay log 


Global Transaction ID (GTID)
* supports multi-source replication

log-slave-updates=0 for efficiency

MHA for MySQL: Master High Availability Manager tools for MySQL

[Using all of the high availability options in MariaDB](https://www.slideshare.net/MariaDB/using-all-of-the-high-availability-options-in-mariadb?qid=688000eb-0784-40ec-82ba-bda9163b0bf4&v=&b=&from_search=36)

MariaDB TX provides high availability via asynchronous or semi-synchronous master/slave replication with automatic failover and synchronous multi-master clustering; 

Single Point of Failure
* The mariadb cluster fails can trigger new Master election on MaxScale
* MaxScale can be setup in HA

MariaDB Server Replication 
* Asynchronous - With asynchronous replication, transactions are replicated after being committed;
* Semi-synchronous - With semi-synchronous replication, a transaction is not committed until it has been replicated to a slave; The semi-sync repl plugin was merged into the server on MariaDB Server 10.3.3 

```
replication_user=mariadb #: replication user 
replication_password=ACEEF153D52F8391E3218F9F2B259EAD #: replication password 
switchover_timeout=90 #: time to complet

failcount=5 #: number of passes/checks if a server failed 
monitor_interval=1000 #: time in ms for each of the passes 
auto_failover=true #: if the automatic failover is enabled 
failover_timeout=10 #: time in secs the failover ops has to complete
```

When auto_rejoin is enabled, the monitor will rejoin any standalone database servers or any slaves replicating from a relay master to the main cluster:


MaxScale Highly Available
* Active Redundancy
* Standby Redundancy

Dedicated Server 
* To utilise server resources to max. 
  * --innodb-dedicated-server := boolean (default OFF) 
* Sets values based on physical memory available 
  * —innodb-log-file-size based on physical memory size 
  * —innodb-buffer-pool-size based on physical memory size 
  * —innodb-flush-method = O_DIRECT_NO_FSYNC 
  
 Parallel Select Count(*)  —innodb-parallel-thread-count= [1-256] 
 * Session variable. Default 4. 
 * Maximum threads 256. 
 * Scans partitions in parallel too
 * Only works on the clustered index (yet) 
 
 
# Course

[CMU 15-445/645 :: Intro to Database Systems](https://15445.courses.cs.cmu.edu/fall2020/schedule.html) 

[CMU 15-721 :: Advanced Database Systems](https://15721.courses.cs.cmu.edu/spring2020/schedule.html)

# Books


Jesper Wisborg Krogh, MySQL Concurrency: Locking and Transactions for MySQL Developers and DBAs, Apress, 2021


Jesper Wisborg Krogh, MySQL 8 Query Performance Tuning:A Systematic Method for Improving Execution Speeds, Apress, 2020



Daniel Nichter, Efficient MySQL Performance: Best Practices and Techniques, 2022

[Code Examples](https://github.com/efficient-mysql-performance/examples)


Performance is query response time. 性能指的是查询的响应时间。







在MySQL中float和double用来表示浮点数。 decimal（或numberic）用来表示定点数。 
关于浮点数和定点数的应用中，需要考虑到以下几个原则
1. 浮点数存在误差问题
2. 对货币等，对精度敏感的数据，应该用定点数表示或存储
3. 在编程中，如果用到浮点数，要特别注意误差问题，并尽量避免做浮点数比较
4. 要注意浮点数中一些特殊值的处理


在MySQL 8.0.1及更高版本中采用utf8mb4_0900_ai_ci作为默认排序规则，而之前的版本则采用utf8mb4_general_ci。

MySQL 8.0 默认的是 utf8mb4_0900_ai_ci，属于 utf8mb4_unicode_ci 中的一种，具体含义如下：
* uft8mb4 表示用 UTF-8 编码方案，每个字符最多占 4 个字节。
* 0900 指的是 Unicode 校对算法版本。（Unicode 归类算法是用于比较符合 Unicode 标准要求的两个 Unicode 字符串的方法）。
* ai 指的是口音不敏感。也就是说，排序时 e，è，é，ê 和 ë 之间没有区别。
* ci 表示不区分大小写。也就是说，排序时 p 和 P 之间没有区别。


ai表示accent insensitivity，也就是“不区分音调”，排序时 e，è，é，ê 和 ë 之间没有区别,而ci表示case insensitivity，也就是“不区分大小写”,排序时a和A之间没有区别。

@是用户变量，@@是系统变量。

```sql
select @@wait_timeout  from dual;

select date_add("2023-05-12", interval @i:=@i-1 day) as date
from  (select @i:=1) t
where @i>-7;

WITH t1 AS (
      SELECT SUBDATE(DATE(NOW()), t2*100 + t1*10 + t0) AS date 
      FROM
        (SELECT 0 t0 UNION SELECT 1 UNION SELECT 2 UNION SELECT 3 UNION SELECT 4 UNION SELECT 5 UNION SELECT 6 UNION SELECT 7 UNION SELECT 8 UNION SELECT 9) t0,  
        (SELECT 0 t1 UNION SELECT 1 UNION SELECT 2 UNION SELECT 3 UNION SELECT 4 UNION SELECT 5 UNION SELECT 6 UNION SELECT 7 UNION SELECT 8 UNION SELECT 9) t1,  
        (SELECT 0 t2 UNION SELECT 1 UNION SELECT 2 UNION SELECT 3 UNION SELECT 4 UNION SELECT 5 UNION SELECT 6 UNION SELECT 7 UNION SELECT 8 UNION SELECT 9) t2
```

mysql with recursive
```sql
WITH recursive 表名 AS (
初始语句（非递归部分）
UNION ALL
递归部分语句
)

WITH recursive t AS(
SELECT 1 AS d
UNION ALL
SELECT n+1 FROM t WHERE n<10
)
SELECT * FROM t;


WITH recursive t (date) AS(
SELECT "2023-05-12"
UNION ALL
SELECT date_add(date, interval -1 day) as date FROM t WHERE date>='2023-04-28'
)
SELECT date FROM t
order by date desc;


```

2，查看数据库使用大小
```
SELECT 
  table_schema as '数据库',
  sum(table_rows) as '记录数',
  sum(truncate(data_length/1024/1024, 2)) as '数据容量(MB)',
  sum(truncate(index_length/1024/1024, 2)) as '索引容量(MB)',
  sum(truncate(DATA_FREE/1024/1024, 2)) as '碎片占用(MB)'
FROM information_schema.tables
GROUP BY 1
ORDER BY sum(data_length) DESC, sum(index_length) DESC;
```

3，查看表使用大小

```
SELECT 
  table_name as '表名',
  table_rows as '记录数',
  truncate(data_length/1024/1024, 2) as '数据容量(MB)',
  truncate(index_length/1024/1024, 2) as '索引容量(MB)',
  truncate(DATA_FREE/1024/1024, 2) as '碎片占用(MB)'
FROM information_schema.tables
WHERE table_name='';
```