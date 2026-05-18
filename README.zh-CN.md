# LUODA-TOKEN

统一的 AI 提供商代理管理和令牌分发平台。

## 功能特性

- 🔑 **统一 API 端点** — 一个端点管理所有 AI 提供商
- 📊 **用量监控** — 实时追踪 Token 消耗和请求日志
- 🔄 **多提供商支持** — 支持 OpenAI、Anthropic、Google、DeepSeek 等 100+ 提供商
- 🛡️ **MITM 代理** — 拦截 CLI 工具流量并智能路由
- 🎛️ **模型组合（Combos）** — 支持回退机制的模型组合
- 🌐 **媒体提供商** — 支持嵌入、图片生成、TTS、STT 等
- 🔌 **CLI 工具集成** — 一键配置 Cursor、Codex、Cline 等开发工具

## 快速安装

### 方式一：npm 全局安装（推荐）

```bash
npm install -g luoda-token
luoda-token
```

### 方式二：npx 直接运行

```bash
npx luoda-token
```

启动后访问 `http://localhost:20128` 进入管理面板。

## 系统要求

- **Node.js** >= 18.0.0
- **npm** >= 9.0.0
- **操作系统**: Windows / macOS / Linux

## 配置指南

### 1. 添加 AI 提供商

在管理面板中点击 **Providers**，选择你的 AI 提供商：

- **OAuth 登录**: 支持 Google、GitHub、Anthropic 等 OAuth 登录
- **API Key**: 直接输入 API 密钥
- **Cookie 导入**: 从浏览器导入已登录的会话

### 2. 获取 API 端点

在 **Endpoint** 页面查看你的 API 地址，格式为：

```
http://localhost:20128/v1
```

### 3. 配置 CLI 工具

在 **CLI Tools** 页面选择你的开发工具（Cursor、Codex、Cline 等），点击"Apply"自动配置。

## 使用示例

### OpenAI SDK

```python
from openai import OpenAI

client = OpenAI(
    base_url="http://localhost:20128/v1",
    api_key="your-api-key"
)

response = client.chat.completions.create(
    model="gpt-4o",
    messages=[{"role": "user", "content": "Hello!"}]
)
```

### cURL

```bash
curl http://localhost:20128/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer your-api-key" \
  -d '{
    "model": "claude-sonnet-4-20250514",
    "messages": [{"role": "user", "content": "你好"}]
  }'
```

## 常见问题

### 如何更新到最新版本？

```bash
npm install -g luoda-token@latest --prefer-online
```

### 端口被占用怎么办？

在设置页面修改端口号，或使用环境变量 `PORT=自定义端口`。

### 如何配置 HTTPS？

在 MITM 代理设置中启用 HTTPS 证书自动生成。

## 许可证

MIT License

## 贡献

欢迎提交 Issue 和 Pull Request！