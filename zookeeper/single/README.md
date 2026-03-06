# Zookeeper 单实例部署

此配置运行一个单节点的 Zookeeper 3.8 实例。

## 快速开始

1. **创建目录 (Prepare)**:
   ```bash
   mkdir -p data datalog
   ```

2. **启动 (Start)**:
   ```bash
   docker-compose up -d
   ```

3. **验证 (Verify)**:
   ```bash
   echo ruok | nc localhost 2181
   # 输出: imok
   ```

## 默认配置

- **客户端端口**: `2181`
- **ZOO_MY_ID**: `1`
- **时区**: `Asia/Shanghai`
- **资源限制**: 1G 内存 (Limit)

## 故障排查

- **连接失败**: 确保容器已完全启动。
- **权限问题**: 如果挂载的目录权限不正确，Zookeeper 可能无法启动。
