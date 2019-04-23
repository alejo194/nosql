chunk:默认64M，在shard server中，MongoDB会把数据分为chunks,每个chunk代表这个shard server内部一部分数据。</br>
激活数据库分片功能：</br>
```bash
use admin
db.runCommand({enablesharding:"test"})
```

