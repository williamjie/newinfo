Redis 命令参考
本文档是 Redis Command Reference 和 Redis Documentation 的中文翻译版： 所有 Redis 命令文档均已翻译完毕， Redis 最重要的一部分主题（topic）文档， 比如事务、持久化、复制、Sentinel、集群等文章也已翻译完毕。

文档目前描述的内容以 Redis 2.8 版本为准， 查看更新日志(change log)可以了解本文档对 Redis 2.8 所做的更新。

你可以通过网址 doc.redisfans.com 在线阅览本文档， 也可以下载 PDF 格式 或者 HTML 格式 的离线版本。

命令目录(使用 CTRL + F 快速查找)：
### Key（键）
DEL
DUMP
EXISTS
EXPIRE
EXPIREAT
KEYS
MIGRATE
MOVE
OBJECT
PERSIST
PEXPIRE
PEXPIREAT
PTTL
RANDOMKEY
RENAME
RENAMENX
RESTORE
SORT
TTL
TYPE
SCAN
### String（字符串）
APPEND
BITCOUNT
BITOP
DECR
DECRBY
GET
GETBIT
GETRANGE
GETSET
INCR
INCRBY
INCRBYFLOAT
MGET
MSET
MSETNX
PSETEX
SET
SETBIT
SETEX
SETNX
SETRANGE
STRLEN
### Hash（哈希表）
HDEL
HEXISTS
HGET
HGETALL
HINCRBY
HINCRBYFLOAT
HKEYS
HLEN
HMGET
HMSET
HSET
HSETNX
HVALS
HSCAN
### List（列表）
BLPOP
BRPOP
BRPOPLPUSH
LINDEX
LINSERT
LLEN
LPOP
LPUSH
LPUSHX
LRANGE
LREM
LSET
LTRIM
RPOP
RPOPLPUSH
RPUSH
RPUSHX
### Set（集合）
SADD
SCARD
SDIFF
SDIFFSTORE
SINTER
SINTERSTORE
SISMEMBER
SMEMBERS
SMOVE
SPOP
SRANDMEMBER
SREM
SUNION
SUNIONSTORE
SSCAN
### SortedSet（有序集合）
ZADD
ZCARD
ZCOUNT
ZINCRBY
ZRANGE
ZRANGEBYSCORE
ZRANK
ZREM
ZREMRANGEBYRANK
ZREMRANGEBYSCORE
ZREVRANGE
ZREVRANGEBYSCORE
ZREVRANK
ZSCORE
ZUNIONSTORE
ZINTERSTORE
ZSCAN
### Pub/Sub（发布/订阅）
PSUBSCRIBE
PUBLISH
PUBSUB
PUNSUBSCRIBE
SUBSCRIBE
UNSUBSCRIBE
### Transaction（事务）
DISCARD
EXEC
MULTI
UNWATCH
WATCH
### Script（脚本）
EVAL
EVALSHA
SCRIPT EXISTS
SCRIPT FLUSH
SCRIPT KILL
SCRIPT LOAD
### Connection（连接）
AUTH
ECHO
PING
QUIT
SELECT
### Server（服务器）
BGREWRITEAOF
BGSAVE
CLIENT GETNAME
CLIENT KILL
CLIENT LIST
CLIENT SETNAME
CONFIG GET
CONFIG RESETSTAT
CONFIG REWRITE
CONFIG SET
DBSIZE
DEBUG OBJECT
DEBUG SEGFAULT
FLUSHALL
FLUSHDB
INFO
LASTSAVE
MONITOR
PSYNC
SAVE
SHUTDOWN
SLAVEOF
SLOWLOG
SYNC
TIME
文档
以下文章翻译自 redis.io/documentation 文档。

### 键空间通知（keyspace notification）
功能概览
事件的类型
配置
命令产生的通知
过期通知的发送时间
### 事务（transaction）
用法
事务中的错误
为什么 Redis 不支持回滚（roll back）
放弃事务
使用 check-and-set 操作实现乐观锁
了解 WATCH
使用 WATCH 实现 ZPOP
Redis 脚本和事务
### 发布与订阅（pub/sub）
信息的格式
订阅模式
通过频道和模式接收同一条信息
订阅总数
编程示例
客户端库实现提示
### 复制（Replication）
复制功能的运作原理
部分重同步
配置
只读从服务器
从服务器相关配置
主服务器只在有至少 N 个从服务器的情况下，才执行写操作
### 通信协议（protocol）
网络层
请求
新版统一请求协议
回复
状态回复
错误回复
整数回复
批量回复
多条批量回复
多条批量回复中的空元素
多命令和流水线
内联命令
高性能 Redis 协议分析器
### 持久化（persistence）
Redis 持久化
RDB 的优点
RDB 的缺点
AOF 的优点
AOF 的缺点
RDB 和 AOF ，我应该用哪一个？
RDB 快照
快照的运作方式
只进行追加操作的文件（append-only file，AOF）
AOF 重写
AOF 有多耐久？
如果 AOF 文件出错了，怎么办？
AOF 的运作方式
怎么从 RDB 持久化切换到 AOF 持久化
RDB 和 AOF 之间的相互作用
备份 Redis 数据
容灾备份
### Sentinel
获取 Sentinel
启动 Sentinel
配置 Sentinel
主观下线和客观下线
每个 Sentinel 都需要定期执行的任务
自动发现 Sentinel 和从服务器
Sentinel API
故障转移
TILT 模式
处理 -BUSY 状态
Sentinel 的客户端实现
### 集群教程
集群简介
Redis 集群数据共享
Redis 集群中的主从复制
Redis 集群的一致性保证（guarantee）
创建并使用 Redis 集群
创建集群
集群的客户端
使用 redis-rb-cluster 编写一个示例应用
对集群进行重新分片
一个更有趣的示例应用
故障转移测试
添加新节点到集群
移除一个节点
Redis 集群规范
引言
什么是 Redis 集群？
Redis 集群实现的功能子集
Redis 集群协议中的客户端和服务器
键分布模型
集群节点属性
节点握手（已实现）
MOVED 转向
集群在线重配置（live reconfiguration）
ASK 转向
容错
发布/订阅（已实现，但仍然需要改善）
附录 A： CRC16 算法的 ANSI 实现参考
