# PostgreSQL 单实例部署

此配置运行一个单节点的 PostgreSQL 15 实例。

## 快速开始

1. **创建目录 (Prepare)**:
   ```bash
   mkdir -p data init
   ```

2. **启动 (Start)**:
   ```bash
   docker-compose up -d
   ```

3. **验证 (Verify)**:
   使用 `psql` 连接：
   ```bash
   # 连接到 PostgreSQL
   psql -h localhost -p 5432 -U admin -d devdb
   ```
   *(如果未安装 psql，可以使用 `docker exec -it postgres-single psql -U admin -d devdb`)*

## 默认配置

- **端口**: `5432`
- **账号**: `admin`
- **密码**: `M4Ze68DrApRCix`
- **数据库**: `devdb`
- **资源限制**: 1.5G 内存 (Limit)

## 自定义配置

- **初始化脚本**: 将 `.sql` 或 `.sh` 文件放入 `./init` 目录，首次启动时会自动执行。
- **数据持久化**: 数据存储在 `./data` 目录。

## 故障排查

- **连接失败**: 检查防火墙设置，确保 5432 端口开放。
- **权限问题**: 如果挂载的 `./data` 目录权限不正确，PG 可能无法启动。尝试 `chmod 777 data`。
