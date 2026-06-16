# 更新日志

本项目版本号遵循 [语义化版本](https://semver.org/lang/zh-CN/)。

## 0.1.2 — 2026-06-16

- 默认 AI 提供方改为 DeepSeek、默认模型改为 `deepseek-v4-flash`（又快又便宜；旧的 `deepseek-chat`/`deepseek-reasoner` id 将于 2026-07-24 弃用）。仅影响全新安装，已配置的实例不受影响。

## 0.1.1 — 2026-06-16

移动端体验修复。

- 捕获 Modal 在手机上改为顶到屏幕上方（原先垂直居中会被弹起的键盘盖住），确保「智能记录」按钮始终露在键盘上方、可见可点。
- 键盘弹起时收窄输入框最小高度，给按钮让位。

## 0.1.0 — 2026-06-16

首个版本。一个极小的 Obsidian 移动端捕获器：在念头闪现的那一秒接住它、送进 vault 的 inbox，然后立刻消失。

**功能**
- ⚡ 智能记录：命令 + ribbon 双入口；Modal 弹出即聚焦、键盘已弹、点完即走。
- 两段式捕获：同步段把原文逐字落进 inbox 的 `> [!quote] 原文` 块（绝不经过 AI）；异步段后台调 AI 回填标题/正文并改名。
- 失败兜底：未填 API Key / 断网 / AI 报错 / 返回非法 JSON 时，原文一字不丢；失败的笔记被打上 `catch-ai-failed`，用户无感。
- frontmatter 带 `type: lumen-note` + `status`，与桌面 Lumen 共享同一套 vault 语法，便于后续在桌面侧落位归档。
- 设置只有保存路径 + 主模型；无 AI 开关、无预览/历史等多余开关。

**兼容**
- 移动端可装（`isDesktopOnly: false`），最低 Obsidian 1.4.0。
- 全程走 `requestUrl`，不依赖任何 Node 内置模块。
