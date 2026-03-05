# PostgreSQL Single Instance

## 快速开始

```bash
docker-compose up -d
```

## 默认配置

- **端口**: `5432`
- **账号**: `admin`
- **密码**: `M4Ze68DrApRCix`
- **数据库**: `devdb`
- **资源限制**: 1G 内存
- **数据持久化**: `./data` 目录
- **初始化脚本**: 将 `.sql` 或 `.sh` 文件放入 `./init` 目录，首次启动时会自动执行
