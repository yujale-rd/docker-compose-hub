# MySQL 单实例部署

此配置运行一个单节点的 MySQL 8.0 实例。

## 快速开始

1. **创建目录 (Prepare)**:
   ```bash
   mkdir -p data config init logs
   ```

2. **启动 (Start)**:
   ```bash
   docker-compose up -d
   ```

3. **验证 (Verify)**:
   使用 `mysql` 客户端连接：
   ```bash
   # 连接到 MySQL
   mysql -h 127.0.0.1 -P 3306 -u root -prootroot
   ```

## 默认配置

- **端口**: `3306`
- **Root 密码**: `rootroot`
- **普通用户**: `admin` / `adminpassword`
- **字符集**: 默认 `utf8mb4`
- **时区**: `Asia/Shanghai`
- **资源限制**: 2G 内存 (Limit)

## 自定义配置

- **配置文件**: 将自定义的 `my.cnf` 放入 `./config` 目录。
- **初始化脚本**: 将 `.sql` 或 `.sh` 文件放入 `./init` 目录，首次启动时会自动执行（按字母顺序）。

## 故障排查

- **连接失败 (Connection Refused)**: 确保容器已完全启动（健康检查状态为 healthy）。
- **权限问题**: 如果挂载的目录权限不正确，MySQL 可能无法启动。尝试 `chmod 777 data logs`。
- **OOM**: 如果容器意外退出，检查 `docker logs mysql-single` 或 `dmesg` 是否有内存溢出错误。
