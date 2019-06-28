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
    > db.adminCommand({shutdown: 1})
