<div align="center">

# ● NOTHING UI STYLE

**Black, white dots, one red.**

面向 AI Coding Agent（Antigravity / Claude Code / Cursor / OpenClaw 等）的 **Nothing OS / Glyph 工业点阵风格 UI 设计 Skill**。  
将极简 7 级黑白灰阶、三层信息层级、LED 点阵矩阵、唯一活体红点（`#D71921`）、无过冲 Glide 动效与跨平台映射（Web / Tailwind / SwiftUI），封装为可直接复用的 UI 设计规范与 Design Tokens。

![Style](https://img.shields.io/badge/Style-Nothing%20OS%20%2F%20Glyph-000000?style=flat-square)
![Accent](https://img.shields.io/badge/One%20Live%20Red-%23D71921-D71921?style=flat-square)
![Theme](https://img.shields.io/badge/Theme-Dark%20%26%20Light-1A1A1A?style=flat-square)
![Demo](https://img.shields.io/badge/Live%20Demo-Open%20Preview-D71921?style=flat-square)

<br />

**[▶ 在线体验交互式组件 Demo (Live Preview)](https://isdou.github.io/nothing-ui-style/demo.html)**

<br />

<img src="assets/screenshots/desktop.png" alt="Glyph Design Reference" width="820" />

</div>

---

## ✨ 这是什么

`nothing-ui-style` 是一个面向现代前端、桌面端与移动端开发的 **UI Design Skill**。当你想用 AI 构建具有硬件精密感、极高对比度与极简工业美学的界面（Dashboard、系统监控面板、音频/硬件控制台、极客效率工具、AI 产品控制台）时，只需加载本 Skill，AI 就会严格遵循这套视觉语言输出代码。

### 核心设计原则
- **7 级单色灰阶**：摒弃花哨渐变与廉价毛玻璃，依靠精确的 7 级黑白灰（`#000000 → #0E0E0E → #1A1A1A → #2A2A2A → #4A4A4A → #8C8C8C → #F2F2F2`）与 `1px` 细线建立空间层级，完整支持 Dark / Light 双模式自动反转。
- **三层信息层级 & 容器轻量化**：每屏严格控制 Primary / Secondary / Tertiary 三层权重，优先用留白（`8px` 基准阶梯）与细线分组，避免套壳与视觉扁平。
- **「唯一红点」铁律（One Live Red）**：`#D71921` 在同一视野内**最多只出现 1 处**，专用于标识「当前正在运行的活体焦点」或紧急告警；其余选中态严格采用黑白反色。数据密集页支持克制的数据状态色（仅给数值本身上色）。
- **三字体分工体系**：
  - `Doto`（圆点点阵体，字号 `>= 26px`）：时钟、KPI 巨型数字与短词
  - `Space Grotesk`：界面正文与大号欢迎语
  - `Space Mono`（全大写 + `0.14em` 字距）：元标签、状态栏、按钮文案与硬件标识
- **Glide 机械阻尼与极客态反馈**：统一使用 `cubic-bezier(0.25, 1, 0.5, 1)`（`350ms`，**零过冲回弹**）；用 `[LOADING...]` / `[SAVED]` 替代骨架屏与花哨 Toast；表格无斑马纹；仅用 `1.5px` 单线极简图标。

---

## 🎮 Interactive Demo（交互式组件演示）

> **在线预览**：https://isdou.github.io/nothing-ui-style/demo.html

本仓库内置了一个 **零依赖、可离线运行** 的完整交互演示页 [`demo.html`](./demo.html)，直接加载仓库内嵌的 `Doto`、`Space Grotesk`、`Space Mono` 开源字体，集中展示了 6 大标志性 Glyph 组件：

| 组件 | 交互体验 |
|---|---|
| **Dark / Light 主题切换** | 顶栏胶囊一键切换 7 级灰阶与点阵画布背景 |
| **Doto 点阵时钟卡** | 圆点点阵实时时钟 + `steps(1)` 机械离散闪烁冒号 |
| **44-LED 环形点阵进度（Ring）** | 点击 `25 / 76 / 100` 胶囊，体验每颗 `8ms` 顺时针波浪点亮动画 |
| **12 段交互式分段灯带（Seg）** | 点击任意段落实时调节 `VOLUME` / `BRIGHTNESS` 并联动数字读数 |
| **媒体播放器（唯一红点）** | 全屏唯一 `#D71921` 圆形播放键 + 16×6 动态点阵频谱可视化与切歌 |
| **展开式胶囊开关（Expanding Toggle）** | 点击体验 `350ms` Glide 无过冲展开与文字反色平滑位移 |

### 本地体验 Demo
```bash
git clone https://github.com/isdou/nothing-ui-style.git
cd nothing-ui-style
open demo.html   # macOS（Linux 可用 xdg-open demo.html，Windows 直接双击打开）
```

---

## 📦 安装与使用

### Antigravity（推荐）
将仓库克隆到本地，并软链接到全局 skills 目录：
```bash
git clone https://github.com/isdou/nothing-ui-style.git ~/nothing-ui-style
ln -sfn ~/nothing-ui-style ~/.gemini/config/skills/nothing-ui-style
```

### Claude Code / Cursor / OpenClaw 等其他 Agent 平台
将本仓库目录放入对应平台的 `skills/` 目录（确保 `SKILL.md` 位于 `skills/nothing-ui-style/SKILL.md`），或在提示词中直接引用 [`SKILL.md`](./SKILL.md)、[`references/tokens.css`](./references/tokens.css) 与 [`references/platform-mapping.md`](./references/platform-mapping.md)。

### 触发方式
安装后新开对话，直接向 AI 描述需求即可自动触发，例如：
- 「用 **Glyph 风格**帮我做一个 AI 模型监控 Dashboard」
- 「按 **Nothing OS 点阵风**写一个 SwiftUI 番茄钟组件，支持深浅色切换」
- 「套用 **nothing-ui-style** 重构这个设置面板」

---

## 📁 仓库结构

```text
nothing-ui-style/
├── SKILL.md                      # Agent Skill 核心规范（设计哲学、Token、三层层级、组件原语、反模式红线）
├── index.html                    # GitHub Pages 根路径自动跳转页
├── demo.html                     # 零依赖交互式组件 Demo（双击浏览器打开）
├── references/
│   ├── tokens.css                # 可直接复用的 Dark/Light CSS Design Tokens 与基础组件样式
│   └── platform-mapping.md       # HTML/CSS、Tailwind CSS v4、SwiftUI (iOS/macOS) 映射模板
└── assets/
    ├── fonts/                    # 内嵌 OFL 开源字体（Doto / Space Grotesk / Space Mono）
    └── screenshots/              # 原版 Glyph 桌面视觉参考图
```

---

## 🙏 致敬与鸣谢 (Credits & Attribution)

本 Skill 的设计体系、组件原语、构图法则与参考素材融合并致敬自以下优秀开源项目：

1. [**Nebelung-cloud/glyph-rice**](https://github.com/Nebelung-cloud/glyph-rice) by [@Nebelung-cloud](https://github.com/Nebelung-cloud)（GPL-3.0）
   - 提供了本 Skill 的核心视觉基底：7 级黑白灰阶、LED 环形进度/分段灯带/展开胶囊开关等实装硬件原语、Glide 无过冲动效、开源字体资产及桌面视觉参考图。
2. [**dominikmartn/nothing-design-skill**](https://github.com/dominikmartn/nothing-design-skill) by [@dominikmartn](https://github.com/dominikmartn)（MIT License, Copyright (c) 2026 Dominik Martin）
   - 吸收了其极具洞察力的构图与工程法则：三层信息层级铁律（The Three-Layer Rule）、8px 间距语义与容器轻量化梯队、数据状态色规范、极客态反馈模式（`[LOADING]` / `[SAVED]` / 无斑马纹 / `1.5px` 单线图标）以及多平台（Tailwind / SwiftUI）映射思路。
3. **上游灵感与字体致谢**：
   - [**Nothing OS**](https://nothing.tech) — 原始工业美学与 Glyph 灯光交互灵感（Nothing / Nothing OS / Glyph 为 Nothing Technology Ltd. 商标，本项目为非官方粉丝衍生项目）
   - [**Doto**](https://github.com/oliverlalan/Doto) by Oliver Lalan — 点阵可变字体（OFL-1.1）
   - **Space Grotesk & Space Mono** — 正文与等宽标签字体（OFL-1.1）

## 📄 License

- 衍生自 [`Nebelung-cloud/glyph-rice`](https://github.com/Nebelung-cloud/glyph-rice) 的设计参考图与规范延续 **GPL-3.0** 协议。
- 吸收自 [`dominikmartn/nothing-design-skill`](https://github.com/dominikmartn/nothing-design-skill) 的方法论与多平台映射规范遵循原 **MIT License**。
- `assets/fonts/` 下的字体文件遵循各自开源协议 [**OFL-1.1**](./assets/fonts/OFL.txt)。
