# RabbitMQ 单实例部署

此配置运行一个单节点的 RabbitMQ 实例（包含 Management 插件）。

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
   - **Management UI**: http://localhost:15672
   - **User**: `admin`
   - **Password**: `adminpassword`

## 默认配置

- **AMQP 端口**: `5672`
- **Management 端口**: `15672`
- **账号**: `admin`
- **密码**: `adminpassword`
- **资源限制**: 1G 内存 (Limit)

## 故障排查

- **Erlang Cookie 问题**: 如果集群模式下遇到 cookie 不一致问题，需确保 `.erlang.cookie` 权限正确（通常为 400）。
- **数据持久化**: 数据保存在 `./data` 目录。
