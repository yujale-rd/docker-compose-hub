# Nginx 单实例部署

此配置运行一个单节点的 Nginx 实例。

## 快速开始

1. **创建目录 (Prepare)**:
   ```bash
   mkdir -p html conf.d logs certs
   ```
   *注意：如果已有默认配置文件，可以直接使用。本仓库已包含示例 `index.html` 和 `default.conf`。*

2. **启动 (Start)**:
   ```bash
   docker-compose up -d
   ```

3. **访问 (Access)**:
   - http://localhost

## 目录说明

- `html`: 静态文件目录，挂载到 `/usr/share/nginx/html`
- `conf.d`: 配置文件目录，挂载到 `/etc/nginx/conf.d`
- `logs`: 日志目录，挂载到 `/var/log/nginx`
- `certs`: SSL 证书目录，挂载到 `/etc/nginx/certs`

## 默认配置

- **HTTP 端口**: `80`
- **HTTPS 端口**: `443`
- **时区**: `Asia/Shanghai`
- **资源限制**: 512M 内存 (Limit)

## 故障排查

- **配置文件错误**: 如果 Nginx 无法启动，检查 `logs/error.log` 或使用 `docker logs nginx-single` 查看是否有配置语法错误。
- **端口冲突**: 确保 80 或 443 端口未被占用。
