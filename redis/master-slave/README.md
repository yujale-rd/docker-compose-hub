# Redis Master-Slave (1 Master, 2 Slaves) with Password

This setup provides a Redis cluster with 1 Master and 2 Slaves using Docker Compose, secured with a password.

## Configuration

- **Password**: `redis104802`
- **Environment Variables**:
  - `REDIS_MASTER_PASSWORD`
  - `REDIS_MASTER_AUTH_PASSWORD`
  - `REDIS_MASTER_PORT`
  - `REDIS_SLAVE*_PORT`
  - `REDIS_*_APPENDONLY`
  - `REDIS_*_BIND`
  - `REDIS_*_LOGLEVEL`

## Services

- **redis-master**: The master Redis instance.
  - Port: 16379 (Host) -> 6379 (Container)
  - Log Level: debug
- **redis-slave-1**: The first slave instance.
  - Port: 16380 (Host) -> 6379 (Container)
  - Log Level: debug
- **redis-slave-2**: The second slave instance.
  - Port: 16381 (Host) -> 6379 (Container)
  - Log Level: debug

## Usage

1. Start the cluster:

   ```bash
   docker-compose up -d
   ```

2. Check the status:

   ```bash
   docker-compose ps
   ```

3. Verify replication:
   Connect to the master (requires password) and set a value:

   ```bash
   docker exec -it redis-master redis-cli -a redis104802 set mykey "Hello World"
   ```

   Connect to a slave (requires password) and get the value:

   ```bash
   docker exec -it redis-slave-1 redis-cli -a redis104802 get mykey
   ```
