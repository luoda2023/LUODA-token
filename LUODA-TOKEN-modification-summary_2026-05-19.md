# LUODA-TOKEN 品牌汉化与界面修改 — 总结

**时间**: 2026-05-19

## 完成的6项修改

### 1. 界面完整汉化
- `src/i18n/config.js`: `DEFAULT_LOCALE` 从 `"en"` → `"zh-CN"`
- `src/app/layout.js`: `<html lang="en">` → `<html lang="zh-CN">`，metadata title/description 更新

### 2. 网站名称 9Router Proxy → LUODA-TOKEN
- `src/shared/constants/config.js`: APP_CONFIG.name → `"LUODA-TOKEN"`
- `src/app/layout.js`: metadata title/description 更新
- `src/app/manifest.js`: name/short_name 更新
- `src/app/login/page.js`: 登录页标题更新
- **Landing 页全部组件**: Navigation、FlowAnimation、Footer、GetStarted、HowItWorks、page.js 中所有可见 "9Router" 文本 → "LUODA-TOKEN"

### 3. 白亮主题按钮色 → 蓝色
- `src/app/globals.css` `:root`（亮色模式）品牌色从橙色 `#E56A4A` → 蓝色 `#3B82F6`
- 涉及：brand-50~900 全系列、shadow-warm/focus、selection、scrollbar、dot-grid-bg、border-glow、ctaGlowPulse 动画
- `.dark`（暗色模式）保持原有橙色不变

### 4. README 说明替换
- `README.md` 和 `README.zh-CN.md` 全部重写为中文安装说明

### 5. LOGO 替换
- `token.png` 从桌面复制到 `public/token.png`
- `src/shared/components/Sidebar.js`: 左上角图标从 material icon + 渐变背景 → `<img src="/token.png">`

### 6. 删除左上角3个圆点
- `src/shared/components/Sidebar.js`: 删除 Traffic lights 整个 div 块

## 未修改（保留原样）
- 后端路径引用（`dataDir.js`、`appUpdater.js`、`mitm/` 等）— 属于功能代码，非用户可见
- GitHub URL（仍指向 `decolua/9router`）— 暂未改
- 暗色主题保持橙色品牌色
- Landing 页硬编码的橙色（这是独立暗色主题页面，不受主面板主题影响）