# Docker Compose Hub

这是一个常用中间件的 Docker Compose 配置集合，方便快速启动开发或测试环境。

## 目录结构

### Elasticsearch
- **单节点 (7.x)**: [elasticsearch/v7/single](elasticsearch/v7/single/README.md) - Elasticsearch 7.17 单机版
- **集群 (7.x)**: [elasticsearch/v7/cluster](elasticsearch/v7/cluster/README.md) - Elasticsearch 7.17 三节点集群
- **单节点 (8.x)**: [elasticsearch/v8/single](elasticsearch/v8/single/README.md) - Elasticsearch 8.0 单机版
- **集群 (8.x)**: [elasticsearch/v8/cluster](elasticsearch/v8/cluster/README.md) - Elasticsearch 8.0 三节点集群

### Redis
- **单实例**: [redis/single](redis/single/README.md) - Redis 单机版 (带密码)
- **主从集群**: [redis/master-slave](redis/master-slave/README.md) - Redis 一主两从集群 (带密码)

### MySQL
- **单实例**: [mysql/single](mysql/single/docker-compose.yml) - MySQL 8.0 单机版
- **主从复制**: [mysql/master-slave](mysql/master-slave/README.md) - MySQL 一主一从复制

### PostgreSQL
- **单实例**: [postgresql/single](postgresql/single/README.md) - PostgreSQL 15 单机版
- **高可用集群**: [postgresql/master-slave](postgresql/master-slave/README.md) - 基于 Repmgr 和 Pgpool 的高可用集群

### Kafka
- **单实例**: [kafka/single](kafka/single/README.md) - Kafka KRaft 模式 (无 Zookeeper)

## 使用方法

进入相应的目录，运行以下命令启动服务：

```bash
docker-compose up -d
```

停止服务：

```bash
docker-compose down
```
