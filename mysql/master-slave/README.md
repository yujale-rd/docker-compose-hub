# MySQL 主从复制 (Master-Slave)

此配置使用 Bitnami MySQL 镜像提供简单的主从复制（Master-Slave）配置。

## 服务概览

- **mysql-master**: 主节点 (Port 13306 -> 3306)。
  - 资源: Limit 2G, Reservation 1G
  - Root 密码: `root_password`
  - 复制用户: `repl_user` / `repl_password`
- **mysql-slave**: 从节点 (Port 13307 -> 3306)。
  - 资源: Limit 1G, Reservation 512M
  - 连接到 `mysql-master`。

## 快速开始

1. **启动 (Start)**:
   ```bash
   docker-compose up -d
   ```

2. **验证复制 (Verify Replication)**:
   
   - **在主节点创建数据**:
     ```bash
     docker exec -it mysql-master mysql -u root -proot_password -D my_database -e "CREATE TABLE test (id INT AUTO_INCREMENT PRIMARY KEY, name VARCHAR(50)); INSERT INTO test (name) VALUES ('Replication Works');"
     ```
   
   - **在从节点查询数据**:
     ```bash
     docker exec -it mysql-slave mysql -u root -proot_password -D my_database -e "SELECT * FROM test;"
     # 应显示刚才插入的数据
     ```

## 默认配置

- **环境变量**:
  - `MYSQL_REPLICATION_MODE`: `master` 或 `slave`
  - `MYSQL_REPLICATION_USER`: `repl_user`
  - `MYSQL_REPLICATION_PASSWORD`: `repl_password`
  - `MYSQL_MASTER_HOST`: `mysql-master` (用于从节点)
  - `MYSQL_MASTER_ROOT_PASSWORD`: `root_password` (用于从节点初始化连接)

## 故障排查

- **复制失败**: 检查主从节点之间的网络连通性，以及复制用户/密码是否正确。
- **连接超时**: 确保宿主机端口 (13306, 13307) 未被占用。
- **数据不一致**: 确保主从节点的 `server_id` 不重复（Bitnami 镜像会自动处理）。
