ycsb压测工具
#### 集群部署
> mongodb 的集群搭建主要有三种：主从模式，Replica Set 模式，sharding模式
##### Replica Set模式
参见：https://blog.csdn.net/supermapsupport/article/details/78953080</br>
> Mongodb的Replica Set即副本集方式主要有两个目的，一个是数据冗余做故障恢复使用，当发生硬件故障或者其他原因造成的宕机时，可以使用副本进行恢复。
  另一个是做读写分离，读的请求分流到副本上，减轻主的读压力。
  + (1)主节点（Primary）
  + (2)副本节点（Second）
  + (3)仲裁者（Arbiter）
  + (4)选主过程

##### sharding模式
参见：https://blog.csdn.net/ilovemilk/article/details/79336951</br>

##### 安装参见官网
apt-get install dirmngr -y (我安装时少了依赖包)
