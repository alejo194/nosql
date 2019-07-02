#### 启动访问控制
    1. 概述
    在MongoDB部署上启用访问控制强制进行身份验证，要求用户标识自己。当访问启用访问控制的MongoDB部署时，用户只能执行由其角色决定
    的操作。
    下面的教程启用对独立mongod实例的访问控制，并使用默认的身份验证机制。
    
    2. 用户管理员
    启动访问控制后，保证你有一个用户userAdmin或userAdminAnyDatabase角色在admin数据库。此用户可以管理用户和角色，例如：创建用户
    、从用户授予或撤消角色，以及创建或修改自定义角色。
    
    3. 步骤
    下面的过程首先将用户管理员添加到运行时没有访问控制的MongoDB实例中，然后启用访问控制。
    
    3.1 在没有访问控制的情况下启动MongoDB
    在没有访问控制的情况下启动一个独立的mongod实例。
    mongod --port 27017 --dbpath /var/lib/mongodb
    
    3.2 连接实例
    mongo --port 27017
    
    3.3 创建用户管理员
    use admin
    db.createUser(
    {
    user: "myUserAdmin",
    pwd: "abc123",
    roles: [ { role: "userAdminAnyDatabase", db: "admin" }, "readWriteAnyDatabase" ]
    }
    )

    3.4 使用访问控制重新启动MongoDB实例
    a. 关闭mongod实例
    > db.adminCommand({shutdown: 1})
    b. 退出mongo shell
    c. 从客户端重启mongod实例加上--auth命令行选项，如果是配置文件，security.authorization设置
    mongod --auth --port 27017 --dbpath /var/lib/mongodb
    
    3.5 连接并认证用户
    mongo --port 27017 -u "myUserAdmin" --authenticationDatabase "adimin" -p
    or 
    mongo --port 27017
    > use admin
    > db.auth("myUserAdmin", "abc123" )
    
    3.6 创建一个用户到你的部署
    use test
    db.createUser(
    {
    user: "myTester",
    pwd: "xyz123",
    roles: [ { role: "readWrite", db: "test" },
             { role: "read", db: "reporting" } ]
    }
    )
    
    3.7 连接实例并认证myTester
    mongo --port 27017
    > use test
    > db.auth("myTester", "xyz123" )
    or
    mongo --port 27017 -u "myTester" --authenticationDatabase "test" -p
    
    3.8 插入文档
    > db.foo.insert( { x: 1, y: 1 } )
    
    
#### 认证
    1 用户
    2 认证机制
    3 企业级认证机制
    4 内部认证
      4.1 部署新副本集中Keyfile访问控制
      4.2 
      4.3
      4.4 部署分片集中Keyfile访问控制
      4.5 在分片集群中强制密钥文件访问控制（停机）
      4.6 在没有停机的情况下在现有切分集群中强制身份验证(参考官网)
         admin.createUser(
         {
         user: "admin",
         pwd: "111",
         roles: [
         { role: "clusterAdmin", db: "admin" },
         { role: "userAdmin", db: "admin" }
         ]
         }
        );

         db.getSiblingDB("mqtt").createUser(
         {
         "user": "maxwin",
         "pwd": "111",
         "roles": [ { "role" : "readWrite", "db" : "mqtt" },
               { "role" : "readWrite", "db" : "maxbus" } ]
         }
        )
     
