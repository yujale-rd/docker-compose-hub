# 使用 Repmgr 和 Pgpool 的 PostgreSQL 高可用集群

此配置使用 `bitnami/postgresql-repmgr` 实现具有复制管理功能的高可用性 (HA)，并使用 `bitnami/pgpool` 进行负载均衡和连接池管理。

## 架构

- **pg-master**: 主 PostgreSQL 节点。
  - 端口: 15432 (宿主机) -> 5432 (容器)
  - 使用 Repmgr 进行集群管理。
- **pg-slave**: 备用 PostgreSQL 节点。
  - 端口: 15433 (宿主机) -> 5432 (容器)
  - 从 `pg-master` 复制数据。
- **pgpool**: 连接池和负载均衡器。
  - 端口: 15434 (宿主机) -> 5432 (容器)
  - 应用程序入口点。
  - 在主节点和从节点之间平衡读取查询。
  - 将写入查询定向到主节点。

## 配置

### 凭据

- **PostgreSQL 用户**: `postgres`
- **PostgreSQL 密码**: `postgrespassword`
- **数据库**: `ha`
- **Repmgr 用户**: `repmgr`
- **Repmgr 密码**: `repmgrpassword`
- **Pgpool 管理员用户**: `admin`
- **Pgpool 管理员密码**: `adminpassword`

## 使用方法

1. 启动集群：
    ```bash
    docker-compose up -d
    ```

2. 通过 Pgpool 检查状态：
    连接到 Pgpool 并检查节点：
    ```bash
    PGPASSWORD=postgrespassword psql -h localhost -p 15434 -U postgres -d ha -c "SHOW POOL_NODES"
    ```
    *注意：您可能需要在本地安装 `postgresql-client` 或使用 `docker exec`。*

    使用 Docker Exec：
    ```bash
    docker exec -it pgpool psql -U postgres -d ha -c "SHOW POOL_NODES"
    ```

3. 验证读写分离：
    创建表（写入 -> Master）：
    ```bash
    docker exec -it pgpool psql -U postgres -d ha -c "CREATE TABLE test (id serial PRIMARY KEY, name VARCHAR(50)); INSERT INTO test (name) VALUES ('HA Cluster');"
    ```

    读取数据（读取 -> 负载均衡）：
    ```bash
    docker exec -it pgpool psql -U postgres -d ha -c "SELECT * FROM test;"
    ```
