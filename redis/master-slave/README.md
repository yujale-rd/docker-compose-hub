# Redis 主从复制 (1主 2从) 带密码认证

此配置使用 Docker Compose 提供一个包含 1 个主节点和 2 个从节点的 Redis 集群，并启用了密码认证。

## 配置

- **密码**: `redis104802`
- **环境变量**:
  - `REDIS_MASTER_PASSWORD`
  - `REDIS_MASTER_AUTH_PASSWORD`
  - `REDIS_MASTER_PORT`
  - `REDIS_SLAVE*_PORT`
  - `REDIS_*_APPENDONLY`
  - `REDIS_*_BIND`
  - `REDIS_*_LOGLEVEL`

## 服务

- **redis-master**: 主 Redis 实例。
  - 端口: 16379 (宿主机) -> 6379 (容器)
  - 日志级别: debug
- **redis-slave-1**: 第一个从实例。
  - 端口: 16380 (宿主机) -> 6379 (容器)
  - 日志级别: debug
- **redis-slave-2**: 第二个从实例。
  - 端口: 16381 (宿主机) -> 6379 (容器)
  - 日志级别: debug

## 使用方法

1. 启动集群：

   ```bash
   docker-compose up -d
   ```

2. 检查状态：

   ```bash
   docker-compose ps
   ```

3. 验证复制：
   连接到主节点（需要密码）并设置一个值：

   ```bash
   docker exec -it redis-master redis-cli -a redis104802 set mykey "Hello World"
   ```

   连接到从节点（需要密码）并获取该值：

   ```bash
   docker exec -it redis-slave-1 redis-cli -a redis104802 get mykey
   ```
