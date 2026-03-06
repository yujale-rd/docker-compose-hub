# MinIO 单实例部署

此配置运行一个单节点的 MinIO 对象存储服务。

## 快速开始

1. **创建目录 (Prepare)**:
   ```bash
   mkdir -p data
   ```

2. **启动 (Start)**:
   ```bash
   docker-compose up -d
   ```

3. **访问 (Access)**:
   - **Console UI**: http://localhost:9001
   - **API Endpoint**: http://localhost:9000
   - **User**: `minioadmin`
   - **Password**: `minioadmin`

## 默认配置

- **API 端口**: `9000`
- **Console 端口**: `9001`
- **Root 用户**: `minioadmin`
- **Root 密码**: `minioadmin`
- **时区**: `Asia/Shanghai`
- **资源限制**: 2G 内存 (Limit)

## 故障排查

- **数据持久化**: 数据保存在 `./data` 目录。
- **端口冲突**: 确保 9000 和 9001 端口未被占用。
