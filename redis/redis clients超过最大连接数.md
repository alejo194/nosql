#### redis clients 超过最大连接数或连接数不释放
参考https://blog.csdn.net/cxhgg/article/details/67640263
```bash
# config get maxclients （查看最大连接数）
# config get timeout （超时配置，0不舍超时）
# config get tcp-keepalive
# info clients
# client list
其中idbe（以秒计算的空闲时长）
```
配置修改 timeout, tcp-keepalive 
