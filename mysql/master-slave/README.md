# MySQL Master-Slave Replication

This setup uses Bitnami MySQL images to provide a simple Primary-Replica (Master-Slave) replication configuration.

## Services

- **mysql-master**: The primary MySQL instance.
  - Port: 13306 (Host) -> 3306 (Container)
  - Root Password: `root_password`
  - Replication User: `repl_user`
  - Replication Password: `repl_password`
- **mysql-slave**: The replica MySQL instance.
  - Port: 13307 (Host) -> 3306 (Container)
  - Replicates from `mysql-master`.

## Configuration

The setup uses the following environment variables for replication:

- `MYSQL_REPLICATION_MODE`: `master` or `slave`
- `MYSQL_REPLICATION_USER`: `repl_user`
- `MYSQL_REPLICATION_PASSWORD`: `repl_password`
- `MYSQL_MASTER_HOST`: `mysql-master` (for slave)
- `MYSQL_MASTER_ROOT_PASSWORD`: `root_password` (for slave to connect initially)

## Usage

1. Start the cluster:
    ```bash
    docker-compose up -d
    ```

2. Verify Replication:

    Create a table on the master:
    ```bash
    docker exec -it mysql-master mysql -u root -proot_password -D my_database -e "CREATE TABLE test (id INT AUTO_INCREMENT PRIMARY KEY, name VARCHAR(50)); INSERT INTO test (name) VALUES ('Replication Works');"
    ```

    Check the data on the slave:
    ```bash
    docker exec -it mysql-slave mysql -u root -proot_password -D my_database -e "SELECT * FROM test;"
    ```
