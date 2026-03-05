# Kafka 单实例 (KRaft 模式)

## 快速开始

```bash
docker-compose up -d
```

## 默认配置

- **Version (版本)**: Bitnami Kafka 3.4
- **Mode (模式)**: KRaft (无需 Zookeeper)
- **Port (端口)**:
  - `9093`: **External (外部访问)**，绑定 IP `192.168.19.10`
  - `9092`: **Internal (内部访问)**，容器互联使用 `kafka-single:9092`
  - `8080`: **UI (管理界面)**
- **Resources (资源限制)**: 1.5G 内存 (Limit), 1G JVM Heap
- **Persistence (数据持久化)**: `./data` 目录

## 访问说明

- **Kafka UI**: 访问 `http://192.168.19.10:8080`
- **External Client (外部客户端)**: 连接地址 `192.168.19.10:9093`
- **Internal Client (容器互联)**: 连接地址 `kafka-single:9092`

## 注意事项

若服务器 IP 发生变化，请修改 `docker-compose.yml` 中的 `KAFKA_CFG_ADVERTISED_LISTENERS` 配置。
