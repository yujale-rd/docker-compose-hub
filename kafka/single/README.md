# Kafka 单实例 (KRaft 模式)

此配置使用 Bitnami Kafka 镜像运行单实例 Kafka，采用 KRaft 模式（无需 Zookeeper）。

## 快速开始

1. **启动 (Start)**:
   ```bash
   docker-compose up -d
   ```

2. **验证 (Verify)**:
   
   - **创建 Topic**:
     ```bash
     docker exec -it kafka-single kafka-topics.sh --create --topic test-topic --bootstrap-server localhost:9092
     ```
   
   - **生产消息 (Producer)**:
     ```bash
     docker exec -it kafka-single kafka-console-producer.sh --topic test-topic --bootstrap-server localhost:9092
     > Hello Kafka
     ```
   
   - **消费消息 (Consumer)**:
     ```bash
     docker exec -it kafka-single kafka-console-consumer.sh --topic test-topic --from-beginning --bootstrap-server localhost:9092
     # 应显示 "Hello Kafka"
     ```

## 默认配置

- **版本**: Bitnami Kafka 3.4
- **端口**:
  - `9093`: 外部访问 (默认绑定 IP `192.168.19.10`，需修改)
  - `9092`: 内部容器互联 (`kafka-single:9092`)
  - `8080`: Web UI (如有)
- **资源限制**: 1G 内存 (Limit), 512M Heap
- **持久化**: `./data` 目录

## 重要注意事项

**外部访问配置**:
默认配置的 `KAFKA_CFG_ADVERTISED_LISTENERS` 中包含 IP `192.168.19.10`。如果您的服务器 IP 不同，**必须**修改 `docker-compose.yml`：

```yaml
    environment:
      - KAFKA_CFG_ADVERTISED_LISTENERS=PLAINTEXT://kafka-single:9092,EXTERNAL://<YOUR_SERVER_IP>:9093
```
将 `<YOUR_SERVER_IP>` 替换为您实际的公网或局域网 IP。

## 故障排查

- **无法连接**: 检查 `ADVERTISED_LISTENERS` 配置是否与客户端访问的 IP 一致。
- **OOM**: 检查 JVM Heap 设置，默认配置为 512M。
