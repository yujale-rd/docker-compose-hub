# Redis Single Instance

## 快速开始

```bash
docker-compose up -d
```

## 默认配置

- **端口**: `6379`
- **密码**: `redis104802`
- **持久化**: 开启 AOF (`appendonly yes`)
- **资源限制**: 512M 内存
- **配置文件**: 可选。默认使用命令行参数启动。如果需要自定义配置，请在 `config` 目录下创建 `redis.conf` 并修改 docker-compose `command` 为 `redis-server /usr/local/etc/redis/redis.conf`
