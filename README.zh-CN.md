# LUODA-TOKEN

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

编辑 `.env`，修改以下关键配置：

```ini
JWT_SECRET=替换为你的随机密钥
INITIAL_PASSWORD=设置你的初始登录密码
```

### 4. 启动开发服务

```bash
npm run dev
```

浏览器访问 `http://localhost:20128` 进入管理面板。

## 生产部署

```bash
npm run build
npm start
```

启动后默认监听 `http://localhost:20128`，可通过 `.env` 中的 `PORT` 修改端口。

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
- 🔄 **多提供商** — 支持 OpenAI、Anthropic、Google、DeepSeek 等
- 🛡️ **MITM 代理** — 拦截 CLI 工具流量并智能路由
- 🎛️ **模型组合** — 支持回退机制的模型编排
- 🔌 **CLI 工具集成** — 一键配置 Cursor、Codex、Cline 等开发工具

## 项目结构

```
LUODA-token/
├── src/
│   ├── app/              # Next.js App Router 页面
│   ├── shared/           # 共享组件、常量、工具函数
│   ├── lib/              # 后端业务逻辑
│   └── mitm/             # MITM 代理模块
├── public/               # 静态资源
├── .env.example           # 环境变量模板
└── package.json
```

## 许可证

MIT License