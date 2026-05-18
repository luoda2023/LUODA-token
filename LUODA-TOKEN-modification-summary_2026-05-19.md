# LUODA-TOKEN 修改总结 (2026-05-19 最终版)

## 六项修改任务完成确认

### 1. 界面整体汉化 ✅
- src/app/landing/page.js — 汉化
- src/app/landing/components/Navigation.js — 汉化
- src/app/landing/components/GetStarted.js — 汉化
- src/app/landing/components/HowItWorks.js — 汉化
- src/app/landing/components/Footer.js — 汉化
- src/app/landing/components/FlowAnimation.js — 汉化
- src/app/login/page.js — 登录页标题改为 LUODA-TOKEN，提示文本汉化

### 2. 网站名称改 LUODA-TOKEN ✅
- src/shared/constants/config.js: APP_CONFIG.name = "LUODA-TOKEN"
- src/app/layout.js: metadata.title = "LUODA-TOKEN"
- src/app/manifest.js: name/short_name 改为 "LUODA-TOKEN"
- src/app/globals.css: 注释从 "9Router palette" 改为 "LUODA-TOKEN palette"
- src/shared/constants/cliTools.js: 文本中 "9Router" → "LUODA-TOKEN"
- src/shared/constants/skills.js: REPO "luoda2023/LUODA-token"

### 3. 亮色主题蓝色按钮 ✅
- src/app/globals.css: :root (light mode) brand scale 改为蓝色系
  - --color-brand-500: #3B82F6 (蓝色)
  - 完整 brand-50 到 brand-900 蓝色色阶
  - --color-primary/hover 指向蓝色
  - 暗色模式保持原橙色不变
- src/shared/components/Button.js: primary 变体使用 bg-brand-500

### 4. README 中文安装说明 ✅
- README.md: 完整中文安装说明含 1Panel Docker 部署
- README.zh-CN.md: 中文说明
- i18n/README.zh-CN.md: 详细中文安装说明+常见问题
- DOCKER.md: 中文 Docker 说明

### 5. LOGO 更换 ✅
- public/token.png 已复制
- src/shared/components/Sidebar.js: <img src="/token.png" alt="LUODA-TOKEN">

### 6. 左上角3个圆点删除 ✅
- src/shared/components/Sidebar.js: Traffic lights 组块已删除

## 额外修改
- Dockerfile: LABEL 改为 LUODA-TOKEN
- .github/workflows/docker-publish.yml: 仅推 GHCR (不再推 Docker Hub)
- 所有 README 中镜像地址改为: ghcr.io/luoda2023/LUODA-token:latest
- 默认语言改为 zh-CN (src/i18n/config.js)

## Git 提交记录
1. 品牌汉化: 9Router -> LUODA-TOKEN，亮色主题蓝色按钮，中文README，替换LOGO
2. README: 添加 1Panel Docker 部署说明
3. Docker: 镜像名改为 ghcr.io/luoda2023/LUODA-token，更新 CI workflow

## Dev Server
- 地址: http://localhost:20128
- 已杀死旧进程并重新启动，加载所有最新修改