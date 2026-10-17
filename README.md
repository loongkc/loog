# Loog · 私人日记

<div align="center">

![License](https://img.shields.io/badge/license-MIT-green?style=flat-square)
![Version](https://img.shields.io/badge/version-1.0.0-blue?style=flat-square)
![Single File](https://img.shields.io/badge/single--file-yes-blue?style=flat-square)
![Zero Backend](https://img.shields.io/badge/backend-none-lightgrey?style=flat-square)
![Encryption](https://img.shields.io/badge/encryption-AES--256--GCM-blue?style=flat-square)
![Vanilla JS](https://img.shields.io/badge/vanilla-JS-f7df1e?style=flat-square&logo=javascript&logoColor=black)
![Tailwind CSS](https://img.shields.io/badge/Tailwind-3.4-38bdf8?style=flat-square&logo=tailwindcss&logoColor=white)

[![Stars](https://img.shields.io/github/stars/loongkc/loog?style=flat-square)](https://github.com/loongkc/loog/stargazers)
[![Forks](https://img.shields.io/github/forks/loongkc/loog?style=flat-square)](https://github.com/loongkc/loog/network/members)
[![Issues](https://img.shields.io/github/issues/loongkc/loog?style=flat-square)](https://github.com/loongkc/loog/issues)
[![Last Commit](https://img.shields.io/github/last-commit/loongkc/loog?style=flat-square)](https://github.com/loongkc/loog/commits)

</div>

> 一个纯前端、零服务器、单文件部署的私人日记应用。所有数据只存在你的浏览器里。

Loog 是一个离线优先的日记工具：没有账号、没有云端、没有后端接口。你写下的每一个字都保存在本地 `localStorage` 中，通过 `.loog` 加密备份可以把整本日记带走。界面以暖纸、鼠尾草、陶土为基调，配合手写字体和纸纹背景，尽量接近真实手帐的翻阅手感。

[在线演示](https://loongkc.github.io/loog/) · [报告问题](https://github.com/loongkc/loog/issues) · [功能建议](https://github.com/loongkc/loog/issues)

---

## ✨ 核心特性

### 书写体验
- **书写台**：标题、日期、天气、心境、标签、正文，一应俱全
- **工具栏**：加粗、斜体、下划线、荧光笔、清除格式、表情、涂鸦贴纸
- **荧光笔**：使用 `styleWithCSS` 生成 `<span style="background-color: rgb(236,223,180)">`，净化器只保留 hex/rgb/rgba 格式的背景色，外部粘贴的花哨样式会被剥离
- **专注模式**：按 Esc 退出，隐藏除正文外的所有界面元素
- **草稿自动保存**：每 280ms 防抖保存，刷新/关闭页面不丢失

### 每日一句 · 好句有感
- **多来源**：在线一言 API（文学 / 诗词 / 原创 / 哲学四类）→ 语句库回退 → 内置语录兜底
- **打字机效果**：换句时逐字打出，出处延迟淡入
- **好句有感**：点击 ♡ 把当前句作为独立字段附加到日记，只读、可删除、不进入正文、不计入字数

### 日记本
- **左侧大日期布局**：每张卡片左侧是日期数字与「X月 / 周X」，右侧是标题、摘要与标签
- **按月分隔条**：自动插入「YYYY 年 M 月」分隔条，翻阅手感更接近真实手帐
- **搜索与筛选**：标题、正文、标签、日期全文检索，标签 chip 一键筛选

### 统计
- **书写热力图**：年视图紧凑网格 + 月视图带字数标注，今天描边高亮
- **心情分布**：环形饼图
- **天气图谱**：横向柱状图
- **书写时段**：24 小时柱状分布
- **字数趋势**：按月累计折线图

### 数据安全
- **本地分块存储**：元数据头 / 内容块 / 校验尾三段式，轻度混淆防误读
- **白名单净化**：正文渲染前经 DOMParser 净化，只保留安全标签
- **沙箱 iframe**：阅读视图放在无脚本权限的 iframe 中，CSP 限制 `default-src 'none'`
- **粘贴转纯文本**：编辑区粘贴一律转为纯文本，杜绝外部样式注入

### 备份与迁移
- **完整导出**：AES-256-GCM 加密的 `.loog` 文件
- **增量更新**：把当前库的差量合并进已有 `.loog`，原文件旧日记不丢失
- **按日期范围导入**：可选全部 / 近一年 / 近一月 / 近一周
- **释放本地空间**：合并后可把较早的日记从浏览器移除，腾出存储
- **纯文本导出**：`.txt` 格式，方便迁移到其他工具

### 其他
- **时光胶囊**：随机翻开一段过去的心情
- **待办清单**：描边圆点勾选，完成态淡化划线
- **时光机**：7 天内任意版本回溯
- **回收站**：删除的日记保留 30 天
- **数据体检**：逐篇校验「头 / 内容 / 校验尾」，损坏条目可尝试修复
- **多皮肤**：暖纸 / 雾蓝 / 鼠尾草 / 夜读 / 自定义配色

---

## 🚀 快速开始

### 方式一：直接下载使用

1. 下载 `index.html`
2. 用现代浏览器打开（推荐 Chrome / Edge / Firefox 最新版）
3. 开始书写

> ⚠️ **重要提示**：`.loog` 加密备份依赖 Web Crypto API，该 API 要求页面运行在 **https** 或 **localhost** 下。直接用 `file://` 打开时，部分浏览器会禁用 `crypto.subtle`，导致导出/导入加密档失败。日常书写和本地存储不受影响。

### 方式二：GitHub Pages（推荐）

```bash
# 1. Fork 本仓库
# 2. 在仓库 Settings → Pages 中选择 main 分支
# 3. 访问 https://your-username.github.io/loog/
```

### 方式三：任意静态托管

把 `index.html` 上传到 Netlify / Vercel / Cloudflare Pages 即可，无需构建步骤。

### 方式四：本地开发

```bash
# 克隆仓库
git clone https://github.com/loongkc/loog.git
cd loog

# 用任意静态服务器启动（Web Crypto 需要 localhost）
python3 -m http.server 8080
# 或
npx serve .
```

访问 `http://localhost:8080` 即可。

---

## 🔐 数据存储与安全

### localStorage 布局

| Key | 内容 |
|-----|------|
| `loog:idx` | 日记 id 索引 |
| `loog:e:<id>:h` | 元数据头（标题、日期、天气、心境、标签、字数、附加好句） |
| `loog:e:<id>:c` | 正文内容块 |
| `loog:e:<id>:f` | 校验尾（cyrb53 哈希 + 长度） |
| `loog:ops` | 编辑操作日志（保留 7 天，用于版本回溯和损坏修复） |
| `loog:trash` | 回收站（保留 30 天） |
| `loog:draft` | 当前草稿 |
| `loog:todos` | 待办清单 |
| `loog:stickers` | 涂鸦贴纸 |
| `loog:set` | 皮肤设置（含自定义配色） |
| `loog:hitokoto` | 每日一句缓存（6 小时） |

### 安全边界（请务必理解）

- **localStorage 不是加密**。它采用「分块 + 校验 + 轻度混淆」，只能防止误读和一般性的直接查看，**任何能打开这台设备浏览器的人仍可能读到内容**。
- 需要保密请使用设备锁屏，并**只通过 `.loog` 带密码导出备份**。
- **`.loog` 是真加密**，机密性来自 AES-256-GCM + PBKDF2（25 万次迭代）；自定义魔数、乱序分块、S-box 混淆与双层哈希让文件结构无法被通用工具识别，并能发现篡改。
- **密码一旦遗忘无法找回**。请使用 8 位以上强密码，并妥善保管。

### `.loog` 格式说明

```
0..7      魔数  4C 4F 4F 47 7E A5 19 01
8         版本
9         标志位
10..25    随机盐(16)
26..37    AES-GCM IV(12)
38..41    分块数 n
42..45    密文总长
46..53    第一层签名：cyrb53(头[0..46) + 正文)
54..85    第二层签名：SHA-256(头[0..54) + 正文)
86..      正文：n 个乱序分块 [序号 u32][长度 u16][S-box + 动态偏移混淆后的密文字节]
```

加密流程：PBKDF2-SHA256(25 万次, 随机盐) 派生 AES-256-GCM 密钥（头部前 38 字节作为 AAD 绑定）。

---

## 🧭 项目结构

```
loog/
├── index.html          # 单文件应用（HTML + CSS + JS 全部内联）
└── README.md
```

整个应用只有 `index.html` 一个文件，包含：

- `<style>` 皮肤系统（CSS 变量 + 4 套预设 + 自定义）
- `<script id="loog-format">` 独立的 `.loog` 加密容器实现（无 DOM 依赖，可单独测试）
- 主应用脚本（存储层、路由、渲染、事件委托）

---

## 💻 浏览器兼容性

| 浏览器 | 最低版本 | 备注 |
|--------|----------|------|
| Chrome / Edge | 90+ | 推荐 |
| Firefox | 88+ | 推荐 |
| Safari | 14+ | 需 https 或 localhost |
| iOS Safari | 14+ | 需 https |

依赖的关键 API：
- Web Crypto API（`.loog` 加密）
- DOMParser（HTML 净化）
- AbortController（请求超时）
- CSS 自定义属性（皮肤系统）
- `contenteditable` + `execCommand`（富文本编辑）

---

## 🛠️ 开发说明

### 设计原则

1. **零依赖**：除 Tailwind CDN 和 Google Fonts 外无第三方库
2. **离线优先**：所有数据本地存储，网络只用于每日一句
3. **单文件**：所有代码内联，方便分发和部署
4. **防御性**：所有用户输入经净化；阅读视图沙箱隔离；粘贴转纯文本

### 本地调试

```bash
# 启动本地服务器
python3 -m http.server 8080

# 打开开发者工具
# Application → Local Storage → http://localhost:8080
# 可以看到所有 loog:* 键
```

### 清空测试数据

```js
// 在控制台执行（保留 seed）
Object.keys(localStorage)
  .filter(k => k.startsWith('loog:') && k !== 'loog:seed')
  .forEach(k => localStorage.removeItem(k));
location.reload();
```

### 贡献指南

欢迎提交 Issue 和 PR。提交前请确认：

- 改动不引入新的第三方依赖
- 新增功能有对应的错误处理和边界情况
- 涉及数据存储的改动保持向后兼容（或提供迁移逻辑）
- 敏感操作（删除、导出、导入）有二次确认

---

## ❓ 常见问题

**Q：为什么导出 `.loog` 提示"当前环境不支持 Web Crypto"？**

A：Web Crypto API 要求页面运行在 https 或 localhost 下。直接双击 `file://` 打开时，Chrome / Edge / Safari 会禁用该 API。请通过 GitHub Pages、Netlify 等静态托管访问，或本地启动一个 http 服务器。

**Q：忘记 `.loog` 密码怎么办？**

A：无法找回。AES-256-GCM + PBKDF2 的设计就是为了让密码成为唯一入口。建议把密码存在密码管理器里。

**Q：数据存在哪里？会上传到服务器吗？**

A：只存在你的浏览器 `localStorage` 里。除了每日一句会从 `v1.hitokoto.cn` 获取句子外，应用不会发起任何网络请求。没有任何后端服务器。

**Q：换了浏览器 / 设备，日记还能看到吗？**

A：不能直接看到。请先用 `.loog` 导出备份，在新设备上导入。

**Q：浏览器提示存储空间不足怎么办？**

A：localStorage 上限通常是 5MB。可以：
1. 「设置 → 备份与迁移 → 增量更新已有文件」把差量合并进备份
2. 「设置 → 数据体检 → 释放本地空间」把较早的日记从浏览器移除
3. 需要时再从 `.loog` 按日期范围重新导入

**Q：每日一句加载失败怎么办？**

A：应用会自动回退到语句库或内置语录。如果长期失败，可在「设置 → 每日一句来源」切换到"语句库"或"内置语录"。

**Q：支持 Markdown 吗？**

A：不支持。Loog 使用 `contenteditable` 富文本编辑，支持加粗、斜体、下划线、荧光笔，但不会存储 Markdown 语法。

---

## 🗺️ 路线图

- [ ] 多句收集（目前一篇日记只附加一句好句）
- [ ] 荧光笔多色选择
- [ ] 日记内搜索高亮
- [ ] PWA 离线支持
- [ ] 导出为静态 HTML 书册
- [ ] 时间线视图

---

## 📄 许可证

[MIT License](LICENSE)

---

## 🙏 致谢

- 每日一句数据来自 [一言 Hitokoto](https://hitokoto.cn/) 与 [hitokoto-osc/sentences-bundle](https://github.com/hitokoto-osc/sentences-bundle)
- 界面灵感来自纸质手帐
- 字体来自 Google Fonts：Noto Sans SC、Noto Serif SC、Ma Shan Zheng
- CSS 工具类来自 [Tailwind CSS](https://tailwindcss.com/)

---

<p align="center">
  <sub>世界很吵，但纸页永远安静。</sub>
</p>
