# Elasticsearch 8.x 集群 (3 节点)

此配置运行一个包含 3 个节点的 Elasticsearch 8.0 集群和 Kibana。

## 服务概览

- **es01**: 主节点 (Master + Data)。
  - 角色: `master, data, ingest`
  - 端口: 9200 (HTTP)
  - 资源: Heap 1G, Limit 2.5G 内存
- **es02, es03**: 数据节点 (Data Only)。
  - 角色: `data, ingest`
  - 资源: Heap 512M, Limit 1G 内存
- **kibana**: 仪表板 (Port 5601)。

## 快速开始

1. **系统配置 (Prerequisites)**:
   宿主机必须配置足够的虚拟内存映射数。

   - **Linux**:
     ```bash
     sysctl -w vm.max_map_count=262144
     ```
   - **macOS / Docker Desktop**:
     默认已配置。

2. **启动 (Start)**:

   ```bash
   docker-compose up -d
   ```

   _注意：首次启动可能需要几分钟。_

3. **验证 (Verify)**:

   - **集群健康**:
     ```bash
     curl http://localhost:9200/_cat/health?v
     ```
     状态应为 `green` 或 `yellow` (如果副本数未满足)。
   - **节点列表**:
     ```bash
     curl http://localhost:9200/_cat/nodes?v
     ```
     应显示 3 个节点。

4. **访问 Kibana**:
   打开浏览器访问 [http://localhost:5601](http://localhost:5601)。

## 故障排查

- **节点无法加入集群**: 检查 `es02` 和 `es03` 日志，确认是否能解析并连接到 `es01`。
- **内存溢出 (OOM)**: 如果容器频繁重启 (Exit Code 137)，请尝试增加 Docker 分配的内存或减少 `ES_JAVA_OPTS`。
- **Kibana 连接失败**: Kibana 需要等待 ES 集群变为 `Yellow` 或 `Green` 状态才能完全启动。
