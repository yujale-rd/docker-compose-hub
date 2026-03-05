# Redis 单实例部署

此配置运行一个单节点的 Redis 实例，启用了密码认证和 AOF 持久化。

## 快速开始

1. **启动 (Start)**:
   ```bash
   docker-compose up -d
   ```

2. **验证 (Verify)**:
   使用 `redis-cli` 连接测试：
   ```bash
   # 连接到 Redis
   docker exec -it redis-single redis-cli -a redis104802 ping
   # 输出应为 PONG
   ```

## 默认配置

- **端口**: `6379`
- **密码**: `redis104802`
- **持久化**: AOF (`appendonly yes`)
- **资源限制**: 512M 内存 (Limit)

## 自定义配置

如果需要自定义 `redis.conf`：
1. 在当前目录下创建 `config/redis.conf` 文件。
2. 修改 `docker-compose.yml` 中的 `command`：
   ```yaml
   command: redis-server /usr/local/etc/redis/redis.conf
   ```

## 故障排查

- **连接被拒绝**: 检查密码是否正确，或者端口是否冲突。
- **数据丢失**: 确保 `./data` 目录已正确挂载，且 `appendonly` 已开启。
