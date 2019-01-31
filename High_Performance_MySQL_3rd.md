[Chapter 1]

MySQL架构
客户端 -> (连接／线程处理，=> (查询缓存，<- 解析器 ->) -> 优化器) -> 存储引擎
连接管理与安全：线程执行（5.5后支持线程池 Thread-Pooling), SSL

并发控制
读写锁(shared lock / exclusive lock, or read lock / write lock)
锁粒度：（1）表锁(table lock) （2）行级锁(row lock)

事务
ACID （1）原子性 （2）一致性 （3）隔离性 （4）持久性
隔离级别：事务内或事务间的可见程度
（1）READ UNCOMMITTED:
	事务中的修改即使没提交也对其他事务可见
	可读未提交的数据（dirty read）
（2）READ COMMITTED:
	事务直到提交前对其他事务不可见
	大多数据库默认级别（非MySQL）
（3）REPEATABLE READ:
	同一事务中多次读取同样的记录的结果是一致的
	MySQL默认级别，解决dirty read，但无法解决幻读phantom read
（4）SERIALIZABLE:
	强制事务串行执行，避免幻读
	最高隔离级别，对读取的每一行数据加锁，可能导致超时和锁争用

死锁：两个或多个事务在同一资源上相互占用，并请求锁定对方占用的资源，从而导致恶性循环
死锁产生原因：数据冲突，存储引擎的实现方式
死锁监测，死锁超时机制
解决死锁：部分或完全回滚其中的一个事务，然后重新执行该事务
InnoDB解决死锁方法：将持有最少行级排他锁的事务进行回滚

事务日志：存储引擎只修改内存拷贝，再将修改行为记录到硬盘的事务日志中

MySQL事务
MySQL事务型存储引擎：InnoDB, NDB Cluster，（第三方）XtraDB, PBXT
默认模式：AUTOCOMMIT
隐式和显式锁定：innodb两段锁定协议
	隐式：随时锁定，只有commit或rollback才同一时刻释放所有锁
	显式：SELECT .. LOCK IN SHARE MODE

多版本并发控制（MVCC）
类似行级锁但避免了加锁操作，开销低
通过保存数据在某个时间点的快照来实现，即每个事务看到的数据是一致的

InnoDB
事务型引擎，处理大量短期(short-lived)事务，多数正常提交很少回滚
数据存储在表空间(spacetable)
MVCC支持高并发
基于聚簇索引
热备份

MyISAM
整张表加锁，并发插入
表修复 CHECK TABLE ...
压缩表，压缩后不能修改，减少磁盘I/O
不支持事务，不支持崩溃后的安全恢复


[Chapter 2]

基准测试
sysbench, oltp和fileio测试


[Chapter 3]

服务器性能剖析
服务器负载（查询日志），单条查询
诊断间歇性问题


[Chapter 4]
 数据类型
 （1）整数类型：TINYINT(8), SMALLINT(16), MEDIUMINT(24), INT(32), BIGINT(64)
 （2）字符串类型：VARCHAR(可变长度), CHAR, BLOB（二进制大数据） & TEXT（字符集大数据）
 （3）日期和时间类型：DATETIME(YYYYMMDDHHMMSS), TIMESTAMP(UNIX)
 （4）位数据类型：BIT
