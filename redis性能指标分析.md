https://www.cnblogs.com/mushroom/p/4738170.html#three</br>
https://blog.csdn.net/u011983531/article/details/53128066
```bash
127.0.0.1:6380> info
# Server
redis_version:4.0.14
redis_git_sha1:00000000
redis_git_dirty:0
redis_build_id:7c215877668b73dc
redis_mode:standalone
os:Linux 3.16.0-6-amd64 x86_64
arch_bits:64
multiplexing_api:epoll
atomicvar_api:atomic-builtin
gcc_version:6.3.0
process_id:1
run_id:1c3d96d634ac986a5b75919bd07ec44830156dab
tcp_port:6380
uptime_in_seconds:78652
uptime_in_days:0
hz:10
lru_clock:13970188
executable:/data/redis-server
config_file:/usr/local/etc/redis/redis.conf

# Clients
connected_clients:5
client_longest_output_list:0
client_biggest_input_buf:0
blocked_clients:0

# Memory
used_memory:229408680
used_memory_human:218.78M   --used_memory和used_memory_human是一样的，
                              由redis分配器分配的内存总量，以字节（byte）为单位，另一以M/G为单位显示
used_memory_rss:281231360
used_memory_rss_human:268.20M  --从操作系统上显示已经分配的内存总量（重点）
used_memory_peak:241806888
used_memory_peak_human:230.61M  --内存使用的峰值大小（重点）
used_memory_peak_perc:94.87%
used_memory_overhead:15810130
used_memory_startup:786616
used_memory_dataset:213598550
used_memory_dataset_perc:93.43%
total_system_memory:16852389888
total_system_memory_human:15.70G
used_memory_lua:222208
used_memory_lua_human:217.00K
maxmemory:0
maxmemory_human:0B
maxmemory_policy:noeviction
mem_fragmentation_ratio:1.23  --内存碎片率由use_memory_rss除以user_memory所得到
       （内存碎片率稍大于1是合理的，这个值表示内存碎片率比较低，也说明redis没有发生内存交换。
       但如果内存碎片率超过1.5，那就说明Redis消耗了实际需要物理内存的150%，其中50%是内存碎片率，
       这些碎片所占用的内存代表的含义是Redis没有把内存归还给操作系统。
       若是内存碎片率低于1的话，说明Redis内存分配超出了物理内存，操作系统正在进行内存交换。）
mem_allocator:jemalloc-4.0.3
active_defrag_running:0
lazyfree_pending_objects:0

# Persistence
loading:0
rdb_changes_since_last_save:29676
rdb_bgsave_in_progress:0
rdb_last_save_time:1557474046
rdb_last_bgsave_status:ok
rdb_last_bgsave_time_sec:1
rdb_current_bgsave_time_sec:-1
rdb_last_cow_size:12984320
aof_enabled:0
aof_rewrite_in_progress:0
aof_rewrite_scheduled:0
aof_last_rewrite_time_sec:-1
aof_current_rewrite_time_sec:-1
aof_last_bgrewrite_status:ok
aof_last_write_status:ok
aof_last_cow_size:0

# Stats
total_connections_received:7  --
total_commands_processed:108179189  --Redis服务处理命令的总数
     （因为Redis是在单线程模型下工作，会把接收到的客户端命令按顺序执行，
      如果执行命令过多或者存在很多慢命令就会让整个队列阻塞而导致延迟。
      由于total_commands_processed的值是递增的，所以需要统计的是每秒的差值，
      这样才能知道每秒处理总数是上升还是下降，以便排查。）
instantaneous_ops_per_sec:1890  --服务器每秒钟执行的命令数量（重点）
total_net_input_bytes:19500797164
total_net_output_bytes:135699207
instantaneous_input_kbps:325.74  --redis网络入口kps
instantaneous_output_kbps:0.06  --redis网络出口kps
rejected_connections:0  --因为最大客户端数量限制而被拒绝的连接请求数量
sync_full:0
sync_partial_ok:0
sync_partial_err:0
expired_keys:0  --因为过期而被自动删除的数据库键数量
expired_stale_perc:0.00
expired_time_cap_reached_count:0
evicted_keys:0  --因为最大内存容量限制而被驱逐（evict）的键数量
keyspace_hits:1755547  --查找数据库键成功的次数
keyspace_misses:4541  --查找数据库键失败的次数
pubsub_channels:0
pubsub_patterns:0
latest_fork_usec:5524
migrate_cached_sockets:0
slave_expires_tracked_keys:0
active_defrag_hits:0
active_defrag_misses:0
active_defrag_key_hits:0
active_defrag_key_misses:0

# Replication
role:slave
master_host:10.40.201.13
master_port:6380
master_link_status:up
master_last_io_seconds_ago:0
master_sync_in_progress:0
slave_repl_offset:10765114540436
slave_priority:100
slave_read_only:0
connected_slaves:0
master_replid:543dde0c13f95560dfced3bddae633127bec82c8
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:10765114540436
second_repl_offset:-1
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:10765113491861
repl_backlog_histlen:1048576

# CPU
used_cpu_sys:901.58
used_cpu_user:974.02
used_cpu_sys_children:160.33
used_cpu_user_children:1647.75

# Cluster
cluster_enabled:0

# Keyspace
db0:keys=155851,expires=141530,avg_ttl=0
```
