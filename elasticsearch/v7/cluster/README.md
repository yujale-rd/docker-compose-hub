# Elasticsearch 7.x 集群 (3 节点)

此配置运行一个包含 3 个节点的 Elasticsearch 7.17 集群和 Kibana。

## 服务

- **es01**: 主节点 (Master + Data)。
  - 角色: `master, data, ingest`
  - 端口: 9200 (HTTP)
  - 资源:
    - Heap: 1G (Xms/Xmx)
    - Limit: 2.5G 内存, 2.0 CPU
- **es02, es03**: 数据节点 (Data Only)。
  - 角色: `data, ingest` (非 Master)
  - 资源:
    - Heap: 512M (Xms/Xmx)
    - Limit: 1G 内存, 1.0 CPU
- **kibana**: Kibana 仪表板。
  - 端口: 5601
  - 连接到 `es01` (从而连接到集群)。

## 先决条件

确保您的 Docker 主机具有足够的虚拟内存映射计数：

```bash
sysctl -w vm.max_map_count=262144
```

## 使用方法

1. 启动集群：

   ```bash
   docker-compose up -d
   ```

2. 访问 Kibana：
   在浏览器中打开 [http://localhost:5601](http://localhost:5601)。

3. 验证集群健康状态：
   ```bash
   curl http://localhost:9200/_cat/nodes?v
   curl http://localhost:9200/_cluster/health?pretty
   ```
