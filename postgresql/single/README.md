# PostgreSQL 单实例部署

## 快速开始

```bash
docker-compose up -d
```

## 默认配置

- **Port (端口)**: `5432`
- **User (账号)**: `admin`
- **Password (密码)**: `M4Ze68DrApRCix`
- **Database (数据库)**: `devdb`
- **Resources (资源限制)**: 1.5G 内存 (Limit), 512M 内存 (Reservation)
- **Persistence (数据持久化)**: `./data` 目录映射到容器内的 `/var/lib/postgresql/data`
- **Init Scripts (初始化脚本)**: 将 `.sql` 或 `.sh` 文件放入 `./init` 目录，首次启动时会自动执行

## 连接示例

```bash
psql -h localhost -p 5432 -U admin -d devdb
```
