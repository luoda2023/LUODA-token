# Docker

Run LUODA-TOKEN in a container. Multi-platform `linux/amd64` + `linux/arm64`.

---

## 构建 Docker 镜像

```bash
# 在项目根目录构建
cd LUODA-token
docker build -t luoda-token .

# 运行
docker run -d \
  -p 20128:20128 \
  -v ./data:/app/data \
  -e DATA_DIR=/app/data \
  -e JWT_SECRET=替换为随机密钥 \
  -e INITIAL_PASSWORD=设置登录密码 \
  --name luoda-token \
  luoda-token:latest

# 访问
# http://localhost:20128
```

## 推送到 GitHub Container Registry

推送 git tag `v*` → GitHub Actions 自动构建并推送到 `ghcr.io/luoda2023/LUODA-token`。

```bash
git tag v0.1.0 && git push origin v0.1.0
```

镜像地址：`ghcr.io/luoda2023/LUODA-token:latest`

## 1Panel 部署

在 1Panel 的 **容器** → **编排** 中创建，使用 `ghcr.io/luoda2023/LUODA-token:latest` 镜像：

```yaml
version: "3.8"
services:
  luoda-token:
    image: ghcr.io/luoda2023/LUODA-token:latest
    container_name: luoda-token
    restart: always
    ports:
      - "20128:20128"
    volumes:
      - ./data:/app/data
    environment:
      - DATA_DIR=/app/data
      - JWT_SECRET=请替换为随机密钥
      - INITIAL_PASSWORD=请设置你的登录密码
      - PORT=20128
```

## 环境变量

| 变量 | 说明 | 默认值 |
|------|------|--------|
| `JWT_SECRET` | JWT 签名密钥 | 必填 |
| `INITIAL_PASSWORD` | 初始登录密码 | 必填 |
| `PORT` | 服务端口 | `20128` |
| `DATA_DIR` | 数据存储目录 | `/app/data` |

## 容器管理

```bash
docker logs -f luoda-token     # 查看日志
docker restart luoda-token     # 重启
docker stop luoda-token        # 停止
docker rm -f luoda-token       # 删除

# 更新到最新版
docker pull ghcr.io/luoda2023/LUODA-token:latest
docker rm -f luoda-token
# 重新执行 docker run 命令
```