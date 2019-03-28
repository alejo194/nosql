# mongodb-
#### mongoDB 学习记录
```bash
配置服务器
mongo --port 34000
> rs.initiate({
    "_id":"cfg",
    "members":[
        {
            "_id":0,
            "host":"192.168.101.72:34000"
        },
        {
            "_id":1,
            "host":"192.168.101.73:34000"
        },
        {
            "_id":2,
            "host":"192.168.101.74:34000"
        }
    ]
})

shard 服务器
mongo --port 34001
72上执行
> rs.initiate({
    "_id":"shard1",
    "members":[
        {
            "_id":0,
            "host":"192.168.101.72:34001",
            priority:2
        },
        {
            "_id":1,
            "host":"192.168.101.73:34001",
            priority:1
        },
        {
            "_id":2,
            "host":"192.168.101.74:34001",
            arbiterOnly: true
        }
    ]
})

mongo --port 34002
73上执行
> rs.initiate({
    "_id":"shard2",
    "members":[
        {
            "_id":0,
            "host":"192.168.101.72:34002",
            arbiterOnly: true
        },
        {
            "_id":1,
            "host":"192.168.101.73:34002",
             priority:2
        },
        {
            "_id":2,
            "host":"192.168.101.74:34002",
            priority:1
        }
    ]
})

mongo --port 34003
74上执行
> rs.initiate({
    "_id":"shard3",
    "members":[
        {
            "_id":0,
            "host":"192.168.101.72:34003",
            priority:1
        },
        {
            "_id":1,
            "host":"192.168.101.73:34003",
             arbiterOnly: true
        },
        {
            "_id":2,
            "host":"192.168.101.74:34003",
            priority:2
        }
    ]
})

route服务器
mongos -f ...
任意台执行：mongo 127.0.0.1:34004
 > sh.addShard("shard1/192.168.101.72:34001,192.168.101.73:34001,192.168.101.74:34001")
 > sh.addShard("shard2/192.168.101.72:34002,192.168.101.73:34002,192.168.101.74:34002")
 > sh.addShard("shard3/192.168.101.72:34003,192.168.101.73:34003,192.168.101.74:34003")
 > sh.status()
```
