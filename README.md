# Lumen Catch

> Catch a thought the moment it sparks — straight into your vault.

一个**极小的 Obsidian 移动端捕获器**。唯一职责：在念头闪现的那一秒，把它又快又稳地接住、送进 vault 的 inbox，然后立刻消失。它只 catch。

## 它怎么工作（捕获与加工解耦）

捕获被劈成两段：

1. **同步段（瞬间、不碰 AI）：** 用时间戳在 inbox 建笔记，原文逐字写进 `> [!quote] 原文` 引用块 → 立即关闭输入框，给一个一闪而过的「已记录」→ **你此刻已经可以走人。**
2. **异步段（后台、可失败）：** AI 在后台把原文整理成标题 + 正文回填那条笔记，并改名。**AI 失败也不影响已落地的原文**（笔记会被打上 `catch-ai-failed`，原文一字不丢）。

> 捕获那一秒在架构上就不经过 AI —— 想往里加摩擦都加不进去。

## 安装与使用

1. 用 [BRAT](https://github.com/TfTHacker/obsidian42-brat) 安装：添加 `leoyang1984/lumen-catch` 即可（移动端可装，`isDesktopOnly: false`，最低 Obsidian 1.4.0）。
2. **把命令钉到移动端工具栏**（主推入口）：Obsidian 设置 → 移动端专用 → Manage toolbar options → 添加 **⚡ 智能记录**。它位置固定、可形成肌肉记忆，比在命令菜单里翻找快得多。
3. 点工具栏图标 → Modal 弹出、键盘已弹、光标在闪 → 打字 → 点「智能记录」→ 完成。

## 通过 URL / iOS 快捷指令触发（进阶）

插件注册了 URL 协议，可从 Obsidian 外面触发捕获：

- `obsidian://lumen-catch?text=你的念头` —— 直接把文字送进捕获管线（原文落地 + AI 后台整理），**连 Modal 都不弹**。
- `obsidian://lumen-catch` —— 不带 `text`，等同打开 ⚡智能记录 的 Modal。

配 iOS「快捷指令」即可做到 **敲两下手机背面 → 说一句话 → 入库**：

1. 「快捷指令」App 新建一个，依次加三个动作：
   - **询问输入**（文本）
   - **URL 编码**（编码上一步的结果，处理空格/中文/标点）
   - **打开 URL**：`obsidian://lumen-catch?text=` 后面接上 URL 编码结果
2. 把它绑到 主屏图标 / 操作按钮 / 轻点背面（Back Tap）/ 锁屏小组件。
3. 触发 → 系统输入框弹起（可直接按🎤听写）→ 说完/打完 → 自动入库。

> 触发后会切到 Obsidian（URL 唤起的固有代价），记完手动划走即可。这也正是「用系统听写零代码实现语音捕获」的路子。

## 设置

只有两件捕获真正必需的事：

| 设置 | 说明 |
|---|---|
| 保存路径 | 捕获笔记落地的文件夹（默认 `Inbox`，不存在自动创建） |
| 主模型 | AI 提供方 + API Key + 模型。**留空 API Key 即纯捕获**，不调 AI、无需开关 |

没有 AI 开关、没有预览/历史/标签等任何多余开关 —— 它们对应的功能本就不该存在。

## 与桌面 Lumen 的衔接

Catch 写入的 frontmatter 带 `type: lumen-note` + `status: unprocessed`，与桌面 Lumen 同一套 vault 语法。手机上接住的念头，桌面侧的落位流程可凭此直接认领归位。

## 许可证

[MIT](LICENSE)
