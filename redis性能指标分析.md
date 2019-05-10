
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
used_memory_human:218.78M   --used_memory和used_memory_human是一样的，有redis分配器分配的内存总量，以字节（byte）为单位，另一以M/G为单位显示
used_memory_rss:281231360
used_memory_rss_human:268.20M  --从操作系统上显示已经分配的内存总量
used_memory_peak:241806888
used_memory_peak_human:230.61M  --内存使用的峰值大小
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
mem_fragmentation_ratio:1.23
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
total_connections_received:7
total_commands_processed:108179189
instantaneous_ops_per_sec:1890
total_net_input_bytes:19500797164
total_net_output_bytes:135699207
instantaneous_input_kbps:325.74
instantaneous_output_kbps:0.06
rejected_connections:0
sync_full:0
sync_partial_ok:0
sync_partial_err:0
expired_keys:0
expired_stale_perc:0.00
expired_time_cap_reached_count:0
evicted_keys:0
keyspace_hits:1755547
keyspace_misses:4541
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
