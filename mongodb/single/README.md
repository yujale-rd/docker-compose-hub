# MongoDB 单实例部署

此配置运行一个单节点的 MongoDB 6.0 实例。

## 快速开始

1. **创建目录 (Prepare)**:
   ```bash
   mkdir -p data config
   ```

2. **启动 (Start)**:
   ```bash
   docker-compose up -d
   ```

3. **验证 (Verify)**:
   使用 `mongosh` 连接：
   ```bash
   # 连接到 MongoDB
   mongosh --host localhost --port 27017 -u root -p rootroot --authenticationDatabase admin
   ```

## 默认配置

- **端口**: `27017`
- **Root 账号**: `root`
- **Root 密码**: `rootroot`
- **时区**: `Asia/Shanghai`
- **资源限制**: 2G 内存 (Limit)

## 故障排查

- **连接失败 (Connection Refused)**: 确保容器已完全启动（健康检查状态为 healthy）。
- **权限问题**: 如果挂载的目录权限不正确，MongoDB 可能无法启动。
