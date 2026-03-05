# PostgreSQL HA Cluster with Repmgr and Pgpool

This setup uses `bitnami/postgresql-repmgr` for High Availability (HA) with replication management, and `bitnami/pgpool` for load balancing and connection pooling.

## Architecture

- **pg-master**: The primary PostgreSQL node.
  - Port: 15432 (Host) -> 5432 (Container)
  - Uses Repmgr for cluster management.
- **pg-slave**: The standby PostgreSQL node.
  - Port: 15433 (Host) -> 5432 (Container)
  - Replicates from `pg-master`.
- **pgpool**: The connection pooler and load balancer.
  - Port: 15434 (Host) -> 5432 (Container)
  - Application entry point.
  - Balances read queries between master and slave.
  - Directs write queries to the master.

## Configuration

### Credentials

- **PostgreSQL User**: `postgres`
- **PostgreSQL Password**: `postgrespassword`
- **Database**: `ha`
- **Repmgr User**: `repmgr`
- **Repmgr Password**: `repmgrpassword`
- **Pgpool Admin User**: `admin`
- **Pgpool Admin Password**: `adminpassword`

## Usage

1. Start the cluster:
    ```bash
    docker-compose up -d
    ```

2. Check status via Pgpool:
    Connect to Pgpool and check the nodes:
    ```bash
    PGPASSWORD=postgrespassword psql -h localhost -p 15434 -U postgres -d ha -c "SHOW POOL_NODES"
    ```
    *Note: You might need to install `postgresql-client` locally or use `docker exec`.*

    Using Docker Exec:
    ```bash
    docker exec -it pgpool psql -U postgres -d ha -c "SHOW POOL_NODES"
    ```

3. Verify Read/Write Splitting:
    Create a table (Write -> Master):
    ```bash
    docker exec -it pgpool psql -U postgres -d ha -c "CREATE TABLE test (id serial PRIMARY KEY, name VARCHAR(50)); INSERT INTO test (name) VALUES ('HA Cluster');"
    ```

    Read data (Read -> Load Balanced):
    ```bash
    docker exec -it pgpool psql -U postgres -d ha -c "SELECT * FROM test;"
    ```
