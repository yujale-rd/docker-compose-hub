# Elasticsearch 8.0 单节点

此配置运行 Elasticsearch 8.0 单节点和 Kibana。

## 服务

- **elasticsearch**: Elasticsearch 节点。
  - 端口: 9200 (HTTP), 9300 (Transport)
  - 内存: 512MB (Xms/Xmx)
  - 安全性: 已禁用 (为了简化配置)
- **kibana**: Kibana 仪表板。
  - 端口: 5601

## 先决条件

确保您的 Docker 主机具有足够的虚拟内存映射计数：

```bash
sysctl -w vm.max_map_count=262144
```

## 使用方法

1. 启动服务：

   ```bash
   docker-compose up -d
   ```

2. 访问 Kibana：
   在浏览器中打开 [http://localhost:5601](http://localhost:5601)。

3. 验证 Elasticsearch：
   ```bash
   curl http://localhost:9200
   ```
