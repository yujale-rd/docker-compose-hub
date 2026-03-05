# Kafka Single Instance (KRaft)

## 快速开始

```bash
docker-compose up -d
```

## 默认配置

- **版本**: Bitnami Kafka 3.4
- **模式**: KRaft (无需 Zookeeper)
- **端口**: `9093`
- **UI 端口**: `8080` (Web 管理界面)
- **监听地址**: `192.168.19.10:9093` (外部直连)
- **内部地址**: `kafka-single:9092` (容器内互联)
- **资源限制**: 1G 内存 (JVM Heap 512M)
- **数据持久化**: `./data` 目录

## 注意事项

此配置仅适用于单机开发。容器内部 `hostname` 为 `kafka-single`，宿主机访问使用 `localhost`。
如果需要在局域网内其他机器访问，请修改 `KAFKA_CFG_ADVERTISED_LISTENERS` 中的 `localhost` 为服务器 IP。
