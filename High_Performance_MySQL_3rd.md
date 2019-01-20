[Chapter 1]

MySQL架构
客户端 -> (连接／线程处理，=> (查询缓存，<- 解析器 ->) -> 优化器) -> 存储引擎
连接管理与安全：线程执行（5.5后支持线程池 Thread-Pooling), SSL

并发控制
读写锁(shared lock / exclusive lock, or read lock / write lock)
锁粒度：（1）表锁(table lock) （2）行级锁(row lock)