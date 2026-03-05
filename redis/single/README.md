# Redis 单实例部署

## 快速开始

```bash
docker-compose up -d
```

## 默认配置

- **Port (端口)**: `6379`
- **Password (密码)**: `redis104802`
- **Persistence (持久化)**: 开启 AOF (`appendonly yes`)
- **Resources (资源限制)**: 512M 内存 (Limit)
- **Config (配置文件)**: 默认使用命令行参数启动。如果需要自定义配置，请在 `config` 目录下创建 `redis.conf` 并修改 docker-compose `command` 为 `redis-server /usr/local/etc/redis/redis.conf`

## 连接示例

```bash
redis-cli -h localhost -p 6379 -a redis104802
```
