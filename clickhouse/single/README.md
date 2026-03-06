# ClickHouse 单实例部署

此配置运行一个单节点的 ClickHouse 实例。

## 快速开始

1. **创建目录 (Prepare)**:
   ```bash
   mkdir -p data logs
   ```

2. **启动 (Start)**:
   ```bash
   docker-compose up -d
   ```

3. **验证 (Verify)**:
   ```bash
   # 使用 clickhouse-client (需本地安装) 或 HTTP 接口
   echo 'SELECT 1' | curl 'http://localhost:8123/?user=admin&password=adminpassword' -d @-
   ```

## 默认配置

- **HTTP 端口**: `8123`
- **Native 端口**: `9000`
- **账号**: `admin`
- **密码**: `adminpassword`
- **时区**: `Asia/Shanghai`
- **资源限制**: 4G 内存 (Limit)

## 故障排查

- **Ulimits**: ClickHouse 需要较高的文件描述符限制，配置中已设置 `nofile: 262144`。
- **权限问题**: 数据目录权限需正确。
