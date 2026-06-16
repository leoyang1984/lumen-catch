# Lumen Catch

> Catch a thought the moment it sparks — straight into your vault.

一个**极小的 Obsidian 移动端捕获器**。唯一职责：在念头闪现的那一秒，把它又快又稳地接住、送进 vault 的 inbox，然后立刻消失。

它**不是**桌面 Lumen 的移动版，而是与桌面共享同一个 vault、代码完全独立的捕获器。它只 catch。

## 它怎么工作（捕获与加工解耦）

捕获被劈成两段：

1. **同步段（瞬间、不碰 AI）：** 用时间戳在 inbox 建笔记，原文逐字写进 `> [!quote] 原文` 引用块 → 立即关闭输入框，给一个一闪而过的「已记录」→ **你此刻已经可以走人。**
2. **异步段（后台、可失败）：** AI 在后台把原文整理成标题 + 正文回填那条笔记，并改名。**AI 失败也不影响已落地的原文**（笔记会被打上 `catch-ai-failed`，原文一字不丢）。

> 捕获那一秒在架构上就不经过 AI —— 想往里加摩擦都加不进去。

## 安装与使用

1. 用 [BRAT](https://github.com/TfTHacker/obsidian42-brat) 安装本插件（移动端可装，`isDesktopOnly: false`）。
2. **把命令钉到移动端工具栏**（主推入口）：Obsidian 设置 → 移动端专用 → Manage toolbar options → 添加 **⚡ 智能记录**。它位置固定、可形成肌肉记忆，比在命令菜单里翻找快得多。
3. 点工具栏图标 → Modal 弹出、键盘已弹、光标在闪 → 打字 → 点「智能记录」（或 `Cmd/Ctrl + Enter`）→ 完成。

## 设置

只有两件捕获真正必需的事：

| 设置 | 说明 |
|---|---|
| 保存路径 | 捕获笔记落地的文件夹（默认 `Inbox`，不存在自动创建） |
| 主模型 | AI 提供方 + API Key + 模型。**留空 API Key 即纯捕获**，不调 AI、无需开关 |

没有 AI 开关、没有预览/历史/标签等任何多余开关 —— 它们对应的功能本就不该存在。

## 与桌面 Lumen 的衔接

Catch 写入的 frontmatter 带 `type: lumen-note` + `status: unprocessed`，与桌面 Lumen 同一套 vault 语法。手机上接住的念头，桌面侧的落位流程可凭此直接认领归位。

## 开发

```bash
npm install
npm run dev     # 监听构建，输出到 test-vault/.obsidian/plugins/lumen-catch
npm run build   # 生产构建 + 类型检查
```

技术约束：运行时为 Capacitor（**无 Node**），禁用一切 Node 内置模块；网络请求一律走 Obsidian 的 `requestUrl`（绕过移动端 CORS），不用 `fetch`。
