##### 参数设置
+ writeconcert 设置为1
+ readprefermence设置为secondaryPreferred //优先从secondary读取，无从选择主读取
+ 连接池配置，并设置idletimeout
  > 电台mongos maxConn配置N,mongos台数A，业务实例/机器数B
  > maxpool配置ceil ((N*A)/B)

##### 系统和Server参数调优
+ 系统
  > raid 5 or raid 10 , no raid
  > 使用ext4或者xfs文件系统，关闭atime
  > 关闭numa、关闭hugepage(进程需重启)
  > 设置最大openfile限制（）
