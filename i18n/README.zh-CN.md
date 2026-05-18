# LUODA-TOKEN 安装说明

统一的 AI 提供商代理管理面板，基于 Next.js 构建。

## 环境要求

- **Node.js** >= 18.0.0
- **npm** >= 9.0.0（或 yarn / pnpm / bun）

## 快速开始

### 1. 克隆项目

```bash
git clone https://github.com/luoda2023/LUODA-token.git
cd LUODA-token
```

### 2. 安装依赖

```bash
npm install
```

### 3. 配置环境变量

```bash
cp .env.example .env
```

编辑 `.env` 文件，修改以下关键配置：

```ini
# 必填项
JWT_SECRET=替换为你的随机密钥（建议使用 openssl rand -hex 32 生成）
INITIAL_PASSWORD=设置你的初始登录密码

# 可选配置
PORT=20128                  # 服务端口，默认 20128
NODE_ENV=production         # 生产模式
```

### 4. 启动服务

**开发模式：**

```bash
npm run dev
```

**生产模式：**

```bash
npm run build
npm start
```

浏览器访问 `http://localhost:20128`，使用设置的 `INITIAL_PASSWORD` 登录。

## Docker 部署（1Panel）

### 1Panel 面板部署（推荐）

1. 登录 1Panel 面板，进入 **容器** → **编排**
2. 点击 **创建编排**，粘贴以下 `docker-compose.yml`：

```yaml
version: "3.8"
services:
  luoda-token:
    image: decolua/9router:latest
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

3. 确认并部署，等待容器启动
4. 访问 `http://你的服务器IP:20128`

### 1Panel 终端部署

在 1Panel 的 **终端** 中直接执行：

```bash
# 创建数据目录
mkdir -p /opt/luoda-token/data

# 启动容器
docker run -d \
  --name luoda-token \
  --restart always \
  -p 20128:20128 \
  -v /opt/luoda-token/data:/app/data \
  -e DATA_DIR=/app/data \
  -e JWT_SECRET=请替换为随机密钥 \
  -e INITIAL_PASSWORD=请设置你的登录密码 \
  decolua/9router:latest
```

### 配置反向代理（可选）

在 1Panel 中进入 **网站** → **创建网站** → **反向代理**：

- **域名**：填入你的域名
- **代理地址**：`http://127.0.0.1:20128`
- 开启 SSL 后即可通过 `https://你的域名` 访问

### 常用管理命令

在 1Panel 容器界面可直接操作，或通过终端执行：

```bash
docker logs -f luoda-token     # 查看日志
docker restart luoda-token     # 重启容器
docker stop luoda-token        # 停止容器
docker rm -f luoda-token       # 删除容器

# 更新镜像到最新版本
docker pull decolua/9router:latest
docker rm -f luoda-token
# 重新执行上面的 docker run 命令
```

## 主要功能

- 🔑 **统一端点** — 一个 API 地址接入所有 AI 提供商
- 📊 **用量追踪** — 实时监控 Token 消耗与请求日志
- 🔄 **多提供商** — 支持 OpenAI、Anthropic、Google、DeepSeek 等 100+ 提供商
- 🛡️ **MITM 代理** — 拦截 CLI 工具流量并智能路由
- 🎛️ **模型组合** — 支持回退机制的模型编排
- 🔌 **CLI 工具集成** — 一键配置 Cursor、Codex、Cline 等开发工具
- 🌐 **媒体提供商** — 支持嵌入、图片生成、TTS、STT 等

## 登录管理面板

1. 首次启动后，访问 `http://localhost:20128`
2. 输入 `.env` 中设置的 `INITIAL_PASSWORD`
3. 进入仪表盘后可添加 AI 提供商、配置 CLI 工具等

## 添加 AI 提供商

在管理面板左侧导航点击 **Providers** → **Add Provider**：

- **OAuth 登录**：Google、GitHub、Anthropic 等
- **API Key**：直接输入密钥
- **Cookie 导入**：从浏览器导入已登录会话

## 获取 API 端点

配置完成后，在 **Endpoint** 页面查看你的统一 API 地址：

```
http://localhost:20128/v1
```

所有支持 OpenAI 兼容接口的 SDK 和工具都可以直接使用此端点。

## 配置 CLI 工具

在 **CLI Tools** 页面选择你的开发工具（Cursor、Codex、Cline 等），点击 **Apply** 一键完成配置。

## 常见问题

### 端口被占用？

编辑 `.env` 文件，修改 `PORT=自定义端口`，然后重启服务。

### 如何更新？

```bash
git pull
npm install
npm run build
npm start
```

### 忘记密码？

编辑 `.env` 中的 `INITIAL_PASSWORD`，然后重启服务。注意：这只会重置密码，不会影响已配置的提供商数据。

### 1Panel 中如何查看日志？

在 1Panel → **容器** 中找到 `luoda-token`，点击 **日志** 即可。

### 1Panel 中如何修改环境变量？

在 1Panel → **容器** 中找到 `luoda-token`，先停止 → 编辑 → 修改环境变量 → 重新启动。

## 环境变量参考

| 变量 | 说明 | 默认值 |
|------|------|--------|
| `JWT_SECRET` | JWT 签名密钥 | 必填 |
| `INITIAL_PASSWORD` | 初始登录密码 | 必填 |
| `PORT` | 服务端口 | `20128` |
| `NODE_ENV` | 运行环境 | `production` |
| `DATA_DIR` | 数据存储目录 | `~/.9router` |
| `ENABLE_REQUEST_LOGS` | 启用请求日志 | `false` |

## 许可证

MIT License