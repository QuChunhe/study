


>include/buf0buf.h
>The database buffer pool high-level routines


通常情况下，单个数据页默认的大小是16kb。当然，我们也可以通过参数：innodb_page_size，来重新设置大小。

数据页主要包含如下几个部分：
* 文件头部
* 页头部
* 最大和最小记录
* 用户记录
* 空闲空间
* 页目录
* 文件尾部
