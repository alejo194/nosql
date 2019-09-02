参见：https://blog.csdn.net/eagle89/article/details/80609343
##### 集群的监测
+ 1.监测数据库存储统计信息
db.stats()
+ 2.查看数据库统计信息
db.runCommand({serverStatus:1})
+ 3.检查复制集成员状态
rs.status()
##### 基本运维操作
+ 1.设置和查看慢查询
```bash
# 设置慢查询
db.setProfilingLevel(1,200)
# 查看慢查询级别
db.getProfilingLevel()
# 查询慢查询日志，此命令是针对于某一库进行设置
db.system.profile.find({ns:'dbName.collectionName'}).limit(10).sort({ts:-1}).pretty()
```
+ 2.查看执行操作时间较长的动作
> db.currentOp({"active":true,"secs_running":{"$gt":2000}})
+ 3.动态调整日志级别和设置缓存大小
```bash
# 设置日志级别参数
db.adminCommand("getParameter":1, "logLevel":1)
# 设置cache大小参数
db.adminCommand({"setParameter":1,"wiredTigerEngineRuntimeConfig":"cache_size=4G"})
```
+ 4.添加和移除复制集成员
```bash
# 查看复制集成员
rs.status().members
# 添加成员
rs.add('127.0.0.1:20001')
# 移除成员
rs.remove('127.0.0.1:20001')
```
+ 5.设置数据库和集合分片
```bash
# 在mongos admin库设置库允许分片
sh.enableSharding("dbName")
# 在mongos 的admin库设置集合分片片键
sh.shardCollection("dbName.collectionName",{fileName:1})
```
+ 6.添加和移除分片
```bash
# 查看分片状态
sh.status()
# 在mongos执行添加分片（可以为单个实例或复制集）
db.runCommand({removeShard:"shardName"})
db.runCommand({addshard:"rs1/ip-1:20001,ip-2:20001,ip-3:20001"})
# 在mongos执行移除分片
db.runCommand({removeShard:"shard3"})
# 在mongos执行刷新mongos配置信息
db.runCommand("flushRouterConfig")
```
+ 7.导入导出数据
