# 使用 Repmgr 和 Pgpool 的 PostgreSQL 高可用集群

此配置使用 `bitnami/postgresql-repmgr` 实现具有复制管理功能的高可用性 (HA)，并使用 `bitnami/pgpool` 进行负载均衡和连接池管理。

## 架构概览

- **pg-master**: 主 PostgreSQL 节点 (Port 15432 -> 5432)。
  - 资源: Limit 2G, Reservation 1G
- **pg-slave**: 备用 PostgreSQL 节点 (Port 15433 -> 5432)。
  - 资源: Limit 1G, Reservation 512M
- **pgpool**: 负载均衡器入口 (Port 15434 -> 5432)。
  - 资源: Limit 1G, Reservation 256M
  - **读写分离**: 写入 -> Master, 读取 -> Master/Slave。

## 快速开始

1. **启动 (Start)**:
   ```bash
   docker-compose up -d
   ```
   *注意：首次启动需要时间进行集群初始化和节点同步。*

2. **检查状态 (Check Status)**:
   通过 Pgpool 查看集群节点状态：
   ```bash
   # 使用 docker exec 连接
   docker exec -it pgpool psql -U postgres -d ha -c "SHOW POOL_NODES"
   ```
   应显示所有节点状态为 `up`，其中一个角色为 `primary`。

3. **验证读写分离 (Verify HA)**:
   
   - **创建表 (Write -> Master)**:
     ```bash
     docker exec -it pgpool psql -U postgres -d ha -c "CREATE TABLE test (id serial PRIMARY KEY, name VARCHAR(50)); INSERT INTO test (name) VALUES ('HA Cluster');"
     ```

   - **读取数据 (Read -> Load Balanced)**:
     ```bash
     docker exec -it pgpool psql -U postgres -d ha -c "SELECT * FROM test;"
     ```

## 默认配置

- **PostgreSQL 用户**: `postgres` / `postgrespassword`
- **数据库**: `ha`
- **Pgpool 管理员**: `admin` / `adminpassword`

## 故障排查

- **节点显示 Down**: 检查容器日志，确认 Repmgr 是否成功配置复制。
- **脑裂 (Split Brain)**: 确保网络连通性，Pgpool 会尝试自动处理故障转移，但在极端网络分区下可能需要人工干预。
