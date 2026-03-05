# MySQL 主从复制 (Master-Slave)

此配置使用 Bitnami MySQL 镜像提供简单的主从复制（Master-Slave）配置。

## 服务

- **mysql-master**: 主 MySQL 实例。
  - 端口: 13306 (宿主机) -> 3306 (容器)
  - Root 密码: `root_password`
  - 复制用户: `repl_user`
  - 复制密码: `repl_password`
- **mysql-slave**: 从 MySQL 实例。
  - 端口: 13307 (宿主机) -> 3306 (容器)
  - 从 `mysql-master` 复制数据。

## 配置

此配置使用以下环境变量进行复制：

- `MYSQL_REPLICATION_MODE`: `master` 或 `slave`
- `MYSQL_REPLICATION_USER`: `repl_user`
- `MYSQL_REPLICATION_PASSWORD`: `repl_password`
- `MYSQL_MASTER_HOST`: `mysql-master` (用于从节点)
- `MYSQL_MASTER_ROOT_PASSWORD`: `root_password` (用于从节点初始化连接)

## 使用方法

1. 启动集群：
    ```bash
    docker-compose up -d
    ```

2. 验证复制：

    在主节点上创建表：
    ```bash
    docker exec -it mysql-master mysql -u root -proot_password -D my_database -e "CREATE TABLE test (id INT AUTO_INCREMENT PRIMARY KEY, name VARCHAR(50)); INSERT INTO test (name) VALUES ('Replication Works');"
    ```

    在从节点上检查数据：
    ```bash
    docker exec -it mysql-slave mysql -u root -proot_password -D my_database -e "SELECT * FROM test;"
    ```
