# Sticky Markdown Note (Enhanced Fork)

一个浮在桌面、永远置顶、半透明的 Markdown 便签 / TODO 工具,专为 macOS 设计。

> 一句话:**Stickies 的浮动 + Markdown 的灵活 + Typora 的颜值 + 一堆细节体验改进**。

基于 [seongmini/sticky-markdown-note](https://github.com/seongmini/sticky-markdown-note) 的深度增强版,修复了 20+ 个 bug 和 UX 问题(详见下方"改进清单")。

---

## ✨ 核心特性

### 始终浮动 · 永不丢失
- ✅ **真·永远置顶**:所有便签窗口浮在所有应用之上,切到全屏视频/编辑器也不挡
- ✅ **半透明背景**:默认 90% 不透,后面的窗口可以看到,**透明度可自定义**
- ✅ 数据是普通 `.md` 文件,可以用 iCloud / git 同步,永不被工具绑架

### Markdown 全家桶
- ✅ GitHub Task List(`- [ ]` / `- [x]`),点击切换勾选
- ✅ 勾选自动**划掉文字 + 灰化**(嵌套子项不受影响)
- ✅ 标题 / 加粗 / 斜体 / 下划线 / 删除线 / 代码 / 引用 / 链接 / 表格 / KaTeX 数学公式
- ✅ Markdown 语法高亮(颜色区分代码 / 标题 / 引用)

### 不挡视线的工具栏
- ✅ 顶部一行格式按钮:**A** *A* A̲ A̶ `</>` `"` 用样式化字母作图标
- ✅ **响应式压缩**:窗口窄时按优先级隐藏(斜体 → 下划线 → 代码 → 引号)
- ✅ 📌 一键置顶切换、新建、列表、关闭

### 流畅的输入体验
- ✅ **在预览模式下也能直接打字**——按键自动路由到编辑器,实时渲染
- ✅ **格式按钮支持预览选区**:在预览里选中文字,点按钮即可格式化
- ✅ **Toggle 切换**:对已经加粗的文字再点 **A**,自动取消加粗
- ✅ **中文输入法**完全兼容(修复了 IME 选词时重复输入的 bug)

### 字号 / 透明度热调
- ✅ **Cmd + 滚轮** → 调字号(8-40px)
- ✅ **Cmd + Shift + 滚轮** → 调透明度(20%-100%)
- ✅ 设置**每个便签独立保存**,下次打开自动恢复

---

## 📦 安装

### 方式 1:从 Release 下载(推荐普通用户)
1. 去 [Releases 页面](https://github.com/yaofuhong0311/sticky-markdown-note/releases) 下载最新的 `.dmg`
2. 打开 dmg,把 `Sticky Markdown Note.app` 拖到"应用程序"
3. 因为是个人构建未签名,**首次打开**需要解除 Gatekeeper:
   ```bash
   xattr -dr com.apple.quarantine "/Applications/Sticky Markdown Note.app"
   ```
   或在"系统设置 → 隐私与安全性"里选"仍要打开"。

### 方式 2:从源码构建(开发者)
```bash
git clone https://github.com/yaofuhong0311/sticky-markdown-note.git
cd sticky-markdown-note
npm install
CSC_IDENTITY_AUTO_DISCOVERY=false npm run build:mac
# 产物在 dist/mac-arm64/Sticky Markdown Note.app
cp -R "dist/mac-arm64/Sticky Markdown Note.app" /Applications/
xattr -dr com.apple.quarantine "/Applications/Sticky Markdown Note.app"
```

依赖:Node.js 18+,macOS 12+(Apple Silicon 已测试,Intel 应该也能跑)

---

## ⌨️ 快捷键

| 操作 | 快捷键 |
|---|---|
| 切换 编辑器 / 预览 | **Cmd + O** |
| 切回 双视图(both) | **Cmd + P** |
| 加粗 | Cmd + B |
| 斜体 | Cmd + I |
| 删除线 | Cmd + Shift + S |
| 行内代码 | Cmd + ` |
| 引用 | Cmd + Q |
| 标题 | Cmd + H |
| **调字号** | **Cmd + 滚轮** |
| **调透明度** | **Cmd + Shift + 滚轮** |
| 新建便签 | Cmd + N |
| 打开列表 | Cmd + M |

---

## 🎨 自定义

### 透明度
在便签上 **Cmd + Shift + 上滚** 变不透,**下滚** 变透明。
每个便签独立保存,默认 90%。

### 字号
**Cmd + 上滚** 变大,**Cmd + 下滚** 变小。范围 8-40px。

### 改默认背景色
编辑 `src/styles/common.css` 顶部的 `--bg-color` 变量(rgba 值)然后重新构建。
默认是 `rgba(239, 236, 230, 0.9)`(温暖纸色 + 90% 不透)。

### 主题(深色/浅色)
便签列表窗口右上角齿轮 → 切换深色/浅色模式。

---

## 🛠 改进清单(相对原版)

这个 fork 修复 / 改进了原版 20+ 处问题:

### Bug 修复
- ✅ README 承诺的"永远置顶"在代码里实际没实现 —— 已补上 `alwaysOnTop: true` + `setAlwaysOnTop('floating')`
- ✅ 点击 checkbox 缩进会翻倍的 bug(regex 误把前导空格也算进 bullet)
- ✅ 中文 / 日文输入法选词时 Enter / 数字键被列表逻辑误处理,导致重复输入
- ✅ 跨标题 / 空行的 task list (loose list) 渲染时被 `<p>` 包裹,导致 CSS 选择器失效,勾选不划线
- ✅ 工具栏按钮在窄窗口溢出 / 重叠

### UX 改进
- ✅ 温暖纸色主题(`#efece6`)替代刺眼的纯白
- ✅ 整体半透明窗口,可自定义透明度,设置持久化
- ✅ task list 隐藏冗余的项目符号(checkbox 本身就是 marker)
- ✅ 勾选自动划线 + 灰化(嵌套子项不受影响)
- ✅ 响应式工具栏(按优先级隐藏不重要的格式按钮)
- ✅ 视觉化格式按钮(**A** *A* A̲ A̶)而不是字母 B/I/U/S
- ✅ 格式按钮支持预览区选区(不用切到编辑器)
- ✅ 格式按钮 toggle:对已格式化的文字再点会取消格式
- ✅ 跨行 / 歧义选区时拒绝执行,按钮闪红提示
- ✅ 在 only-preview 模式下打字也能直接追加(不用 Cmd+O 切换)
- ✅ Cmd+滚轮调字号 / Cmd+Shift+滚轮调透明度,设置每便签独立保存

### 视觉精修
- ✅ checkbox 像素值改成 em(随字号联动等比缩放)
- ✅ 嵌套层级用虚线左边框可视化
- ✅ markdown 元素语法高亮(标题蓝、代码绿、链接、引用)
- ✅ monospace 字体(SF Mono / JetBrains Mono / Cascadia Code)

---

## 📁 数据位置

便签文件存在:
```
~/Library/Application Support/sticky-markdown/notes/*.md
```

每个便签是一个独立的 `.md` 文件,可以用 VSCode / Obsidian / 任何编辑器打开,**永远不会被工具绑架**。

每便签的字号 / 透明度等设置存在对应的 `*-settings.json`。

---

## 🤝 致谢

原始项目:[seongmini/sticky-markdown-note](https://github.com/seongmini/sticky-markdown-note) (MIT)

本 fork 在其基础上做了深度重写,如果你喜欢简洁的原版,也可以去看原作者的。

---

## 📜 License

MIT
