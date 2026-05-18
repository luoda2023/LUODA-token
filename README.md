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