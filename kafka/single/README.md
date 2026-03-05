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
- **自动创建 Topic**: `true` (当 Producer 发送不存在的 Topic 时自动创建)
- **最大消息大小**: 100MB (已调大)
- **资源限制**: 1G 内存 (JVM Heap 512M)
- **数据持久化**: `./data` 目录

## 访问说明

- **端口**: `9093`
- **UI 端口**: `8080` (Web 管理界面)
- **监听地址**: `<YOUR_SERVER_IP>:9093` (外部直连，需替换为公网 IP)
- **内部地址**: `kafka-single:9092` (容器内互联)

## 注意事项

若服务器 IP 发生变化，请修改 `docker-compose.yml` 中的 `KAFKA_CFG_ADVERTISED_LISTENERS` 配置。
