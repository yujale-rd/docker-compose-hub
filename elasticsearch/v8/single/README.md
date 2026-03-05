# Elasticsearch 8.0 单节点部署

此配置运行一个单节点的 Elasticsearch 8.0 实例。

## 快速开始

1. **权限设置 (Permissions)**:
   宿主机数据目录需要正确的权限，否则 ES 可能无法写入。
   ```bash
   mkdir -p data plugins logs
   chmod 777 data plugins logs
   ```

2. **系统配置 (System Config)**:
   Elasticsearch 需要较大的虚拟内存映射数。
   - **Linux**:
     ```bash
     sysctl -w vm.max_map_count=262144
     ```
     要永久生效，请将 `vm.max_map_count=262144` 添加到 `/etc/sysctl.conf`。
   - **macOS / Docker Desktop**:
     通常无需配置，Docker Desktop 已经默认处理。

3. **启动 (Start)**:
   ```bash
   docker-compose up -d
   ```

4. **验证 (Verify)**:
   检查服务是否正常运行：
   ```bash
   curl localhost:9200
   ```

## 默认配置

- **版本**: 8.8.2
- **端口**: `9200` (HTTP), `9300` (Transport)
- **JVM Heap**: 512M (`-Xms512m -Xmx512m`)
- **资源限制**: 1G 内存 (Limit)
- **模式**: Single Node (单节点)
- **安全**: Disabled (开发环境禁用 X-Pack 安全验证)

## 故障排查

- **容器无法启动**: 检查 `logs` 目录下的日志，通常是因为内存不足或 `vm.max_map_count` 未设置。
- **连接拒绝**: 确保防火墙未阻止 9200 端口，且容器已完全启动（ES 启动可能需要 30秒+）。
