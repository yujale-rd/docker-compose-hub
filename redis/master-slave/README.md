# Redis 主从复制 (1主 2从)

此配置运行一个包含 1 个主节点和 2 个从节点的 Redis 集群，启用了密码认证。

## 服务概览

- **redis-master**: 主节点 (Port 16379 -> 6379)。
  - 资源: Limit 1G, Reservation 512M
- **redis-slave-1**: 从节点 1 (Port 16380 -> 6379)。
  - 资源: Limit 512M, Reservation 256M
- **redis-slave-2**: 从节点 2 (Port 16381 -> 6379)。
  - 资源: Limit 512M, Reservation 256M
- **统一密码**: `redis104802`

## 快速开始

1. **启动 (Start)**:
   ```bash
   docker-compose up -d
   ```

2. **验证复制 (Verify Replication)**:
   
   - **在主节点写入**:
     ```bash
     docker exec -it redis-master redis-cli -a redis104802 set testkey "hello-redis"
     ```
   
   - **在从节点读取**:
     ```bash
     docker exec -it redis-slave-1 redis-cli -a redis104802 get testkey
     # 应输出 "hello-redis"
     ```

3. **查看集群状态**:
   ```bash
   docker exec -it redis-master redis-cli -a redis104802 info replication
   ```
   应显示 `connected_slaves:2`。

## 默认配置

- **环境变量**: 通过 `REDIS_REPLICATION_MODE` 和 `REDIS_MASTER_HOST` 自动配置复制关系。
- **持久化**: 默认开启 AOF。

## 故障排查

- **从节点未同步**: 检查主从节点之间的网络连通性，以及密码配置是否一致。
- **连接超时**: 确保宿主机端口 (16379-16381) 未被占用。
