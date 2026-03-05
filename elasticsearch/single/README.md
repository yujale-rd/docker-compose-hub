# Elasticsearch 单节点部署

## 前置要求 (Prerequisites)

- **OS Configuration**: 宿主机必须设置 `vm.max_map_count >= 262144`
  - **Linux**: `sysctl -w vm.max_map_count=262144` (永久生效需写入 `/etc/sysctl.conf`)
  - **macOS**: 通常无需配置，Docker Desktop 4.x+ 已默认处理

## 快速开始

1. **Permissions (权限设置)**:
   ```bash
   mkdir -p data plugins logs
   chmod 777 data plugins logs
   ```

2. **Start (启动)**:
   ```bash
   docker-compose up -d
   ```

3. **Verify (验证)**:
   ```bash
   curl localhost:9200
   ```

## 默认配置

- **Version (版本)**: 7.17.21
- **Port (端口)**: `9200` (HTTP), `9300` (Transport)
- **JVM Heap**: 1G (`-Xms1g -Xmx1g`)
- **Resources (资源限制)**: 2.5G 内存 (Limit)
- **Mode (模式)**: Single Node (单节点)
- **Security (安全)**: Disabled (开发环境禁用 X-Pack 安全验证)

## 数据目录

- **Data**: `./data` -> `/usr/share/elasticsearch/data`
- **Plugins**: `./plugins` -> `/usr/share/elasticsearch/plugins`
- **Logs**: `./logs` -> `/usr/share/elasticsearch/logs`
