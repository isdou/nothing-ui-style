---
name: glyph-ui-style
description: >
  使用源自 Glyph / Nothing OS 的「极简黑白点阵 + 唯一红点」工业美学设计语言（Glyph UI Style）创建 Web、Dashboard、桌面应用或组件界面。当用户需要：
  (1) 使用 Nothing OS 风格、Glyph 风格、点阵 LED 风格、极简黑白红工业风创建 UI 页面或组件；
  (2) 构建高对比度深色/浅色 Bento 仪表盘、硬件控制台、音乐播放器、系统监控面板、极客工具或 AI 产品界面；
  (3) 复用 glyph-rice 的视觉语言（Doto 点阵数字 + Space Grotesk + Space Mono 大写标签 + 7 级灰度阶梯 + #D71921 唯一红点 + 环形点阵进度/分段灯带/展开胶囊开关）；
  (4) 提问"glyph 风格"、"Nothing OS 风格"、"点阵风 UI"、"黑白红极客风"、"glyph-rice 风格"时，务必使用此 skill。
---

# Glyph UI Style — Nothing OS 工业点阵设计系统指南

本 Skill 提炼自开源项目 `glyph-rice`（Nothing OS 灵感设计系统），将其完整的视觉语法、色彩阶梯、排印规范、点阵组件原语与无过冲动效体系转化为跨平台 UI 设计规范，适用于 **HTML/CSS、React、Vue 3、Tailwind CSS、SwiftUI / 桌面端** 等各类前端界面开发。

> **核心视觉信条**：**Black, white dots, one red.**（纯黑基底、白色点阵、全屏仅一处红点。）

---

## 1. 核心设计哲学 (Design Philosophy)

1. **极致克制的单色层级**：不用花哨渐变、厚重投影或廉价毛玻璃；仅依靠严谨的 7 级黑白灰阶（`bg → s1 → s2 → s3 → mute → grey → fg`）与 `1px` 细线建立清晰的空间深度。
2. **「唯一红点」铁律（One Live Red）**：品牌强调色 Nothing Red（`#D71921`）是整个界面的最高视觉权重。**同一视野内最多只允许出现 1 处红色**，且仅用于标识「当前正在运行的活体状态」（如播放键、录制指示灯、实时指针、核心 CTA）或「不可忽视的告警」。常规选中态、激活态一律用高对比反色（深色模式下白底黑字 `#F2F2F2 / #000000`，浅色模式下黑底白字 `#0B0B0B / #FFFFFF`）。
3. **硬件点阵与矩阵隐喻**：将数字、波形、进度、封面与背景抽象为可逐颗点亮的 LED 点阵（Dot Matrix）与分段灯带（Segmented Bar），赋予数字界面精密硬件的触感。
4. **胶囊与大圆角几何**：交互控件（按钮、输入框、开关、Tab、侧栏项）统一为全胶囊（`999px`），容器与 Bento 卡片统一为大圆角（`24px–28px`），内部嵌套保持同心圆角或清晰留白。
5. **零过冲机械阻尼（Glide Motion）**：所有过渡使用 `ease-out-quart`（`cubic-bezier(0.25, 1, 0.5, 1)`），快启慢收、干脆利落，**禁止弹跳（bounce）或弹性过冲（overshoot）**。

---

## 2. 色彩系统与 Design Tokens

完整可直接引入的 CSS 变量见 [tokens.css](./references/tokens.css)。

### 2.1 七级灰度阶梯 + 强调色

| Token | 语义角色 | Dark 模式（默认主风格） | Light 模式 | 使用说明 |
|---|---|---|---|---|
| `--glyph-bg` | 最底层画布 | `#000000` | `#E9E9E9` | 页面背景、点阵底布 |
| `--glyph-s1` | 一级表面 | `#0E0E0E` | `#FFFFFF` | 顶栏、侧栏、大面板、弹窗底 |
| `--glyph-s2` | 二级表面 | `#1A1A1A` | `#F1F1F1` | Bento 卡片、磁贴、未激活按钮/开关底 |
| `--glyph-s3` | 三级线条/熄灭态 | `#2A2A2A` | `#D9D9D9` | `1px` 边框、分割线、未点亮的 LED 点阵/灯带 |
| `--glyph-mute` | 弱化/禁用态 | `#4A4A4A` | `#B8B8B8` | 禁用图标、滚动条滑块、未激活开关圆点 |
| `--glyph-grey` | 次级文本/标签 | `#8C8C8C` | `#6E6E6E` | 大写元标签、辅助说明、未选中导航字 |
| `--glyph-fg` | 主文本/高亮激活 | `#F2F2F2` | `#0B0B0B` | 主文字、点亮的 LED、激活态按钮/开关填充底 |
| `--glyph-ink` | 反色文字 | `#000000` | `#FFFFFF` | 写在 `--glyph-fg` 激活块上的反色文字/图标 |
| `--glyph-accent` | 唯一活体强调色 | `#D71921` | `#D71921` | **全屏最多 1 处**；深浅主题保持不变 |
| `--glyph-red` | 警戒/危险色 | `#D71921` | `#D71921` | 错误提示、低电量、危险操作 |
| `--glyph-scrim` | 遮罩层 | `rgba(0, 0, 0, 0.74)` | `rgba(233, 233, 233, 0.80)` | 模态弹窗背景遮罩 |

### 2.2 衍生配色模式（可选）
若业务需要非纯黑白的衍生主题，保持上述 7 级明度结构不变，仅替换对应角色色（详见 [tokens.css](./references/tokens.css)）：
- **Nothing（默认）**：纯黑 + 白点 + `#D71921`
- **多色主题预设**：支持映射到 Catppuccin、Rosé Pine、Gruvbox、Nord、Dracula、Tokyo Night 等暗/亮双色板，保持“7 级灰阶 + 单一强调色”的秩序不变。

---

## 3. 三字体排印系统 (Typography)

Glyph UI 严格划分三种字体职责，**禁止混用角色**（本地 OFL 字体资产已内置于 [assets/fonts/](./assets/fonts/)，也可通过 Google Fonts 加载）：

| 角色 | 字体族 | 关键样式规范 | 适用场景 |
|---|---|---|---|
| **点阵展示体 (`--font-dot`)** | `Doto` | `font-variation-settings: "ROND" 100, "wght" 900;`<br>`line-height: 0.85; font-variant-numeric: tabular-nums;`<br>**硬规则：字号严禁小于 `26px`** | 时钟、KPI 大数字、百分比、温度、极短英文标题（1–3 词） |
| **界面正文字体 (`--font-ui`)** | `Space Grotesk` | 问候语/Hero 大字：`weight: 300, letter-spacing: -0.02em, line-height: 1.1`<br>正文/卡片内容：`weight: 400–500, 14px–16px` | 中文可回退至 `PingFang SC / Noto Sans SC / sans-serif`；承担全部阅读内容 |
| **机械元标签 (`--font-mono`)** | `Space Mono` | `text-transform: uppercase;`<br>`letter-spacing: 0.14em;`<br>`font-size: 11px–14px; color: var(--glyph-grey);` | 卡片左上角小标、状态栏、时间戳、快捷键提示、路径、单位 |

> **中文混排建议**：中文环境下，数字与英文短标坚持用 `Doto` 与 `Space Mono`，中文标题和正文使用无衬线黑体（`Space Grotesk, "PingFang SC", "Hiragino Sans GB", "Noto Sans SC", sans-serif`），保持字重克制与充足留白。

---

## 4. 布局、圆角与间距规范 (Layout & Geometry)

- **Bento 网格系统**：优先采用 Bento 卡片矩阵布局（例如 3 列网格，单格基准 `220px × 220px`，支持 `1×1`、`2×1`、`3×1` 跨列），卡片间距固定 `gap: 16px–20px`，页面外边距 `24px–40px`。
- **圆角层级**：
  - 交互控件（按钮、输入框、Tab、侧栏胶囊项、开关）：`border-radius: 999px`（横向拼接按钮组内部接缝设为 `0`）。
  - 主面板 / Bento 卡片 / 模态框：`border-radius: 24px` 或 `28px`。
  - 卡片内次级选中项 / 小列表行：`border-radius: 14px`。
- **边框与阴影**：
  - 默认以表面色差（`bg → s1 → s2`）区分层级，需要轮廓时使用 `1px solid var(--glyph-s3)`。
  - 聚焦态边框：`1px solid var(--glyph-fg)`。
  - 仅在浮层使用极弱阴影：暗色 `0 0 0 1px var(--glyph-s3), 0 12px 32px rgba(0, 0, 0, 0.45)`；亮色 `0 8px 28px rgba(0, 0, 0, 0.12)`。
- **背景点阵**：画布背景可叠加低对比度点阵网格（`radial-gradient(circle, var(--glyph-s3) 1px, transparent 1px)`，`background-size: 12px 12px` 或 `16px 16px`）。

---

## 5. 动效规范 (Motion)

- **唯一主曲线（Glide）**：`--ease-glide: cubic-bezier(0.25, 1, 0.5, 1)`（ease-out-quart，无回弹）。
- **标准时长**：
  - 面板/开关/布局位移动画：`350ms`（`--duration-base`）
  - 颜色/微状态切换：`120ms–200ms`（`--duration-fast`）
  - 点阵波浪点亮：逐颗延迟 `8ms`（`transition-delay: calc(var(--i) * 8ms)`）
- **机械离散闪烁**：时钟冒号、录制红点等不做平滑呼吸渐变，采用 `500ms` 周期在 `opacity: 1` 与 `opacity: 0.2` 之间干脆切换（`steps(1)`）。

---

## 6. 六大标志性组件模式 (Signature Components)

在构建 Glyph 风格页面时，优先组合以下 6 种最具辨识度的硬件感组件：

### 6.1 Bento 卡片（带大写 Mono 顶标 + Doto 核心读数）
```html
<section class="glyph-card">
  <span class="glyph-label">CPU LOAD</span>
  <div class="glyph-num">42%</div>
  <div class="glyph-seg" role="progressbar" aria-valuenow="42">
    <!-- 12 段胶囊灯带，前 5 段加 .is-on -->
  </div>
</section>
```

### 6.2 Seg 分段灯带（Segmented Bar）
- 默认 `12` 段圆头胶囊（`border-radius: 999px`），段间距 `4px`，支持横向与纵向（纵向自下而上点亮）。
- 熄灭段用 `var(--glyph-s3)`，点亮段用 `var(--glyph-fg)`；仅在超阈值告警时末端或整条切换为 `var(--glyph-red)`。

### 6.3 Ring 环形点阵进度（Dot Ring）
- 由 `24–44` 颗 `5px–6px` 圆点沿圆周均匀排布，从 12 点钟方向顺时针点亮。
- 数值变化时按 `index * 8ms` 阶梯波浪点亮，中心可放置 `Doto` 大数字或图标。

### 6.4 展开式胶囊开关（Expanding Pill Toggle）
- 外壳高度 `48px–64px`，`border-radius: 999px`，背景 `var(--glyph-s2)`。
- **关闭态**：左侧一个正圆灰块（`var(--glyph-mute)`，内嵌深色小圆点），文字在右侧（`var(--glyph-grey)`）。
- **开启态**：内部滑块以 `350ms var(--ease-glide)` 展开铺满整个胶囊变为 `var(--glyph-fg)`，文字左移并反色为 `var(--glyph-ink)`，原小圆点停靠在最右侧作为指示点。

### 6.5 唯一红点主动作钮（One Live Red Action）
- 正圆（如 `48px–52px`）或高权重状态指示点，背景 `var(--glyph-accent)`（`#D71921`），前景图标 `#FFFFFF`。
- 典型用途：播放/暂停键、开始录制、主启动按钮、实时在线红点。

### 6.6 黑白点阵滤镜（Halftone / Dot-Matrix Mask）
- 专辑封面、头图或视觉装饰球先去色转黑白（`filter: grayscale(1) contrast(1.15)`），再叠加 CSS 点阵遮罩或 Canvas/SVG 采样点阵（步进 `5px–6px`，圆点半径约 `0.3 * pitch`），形成硬件 LED 屏质感。

---

## 7. 设计红线与自检清单 (Anti-Patterns)

交付任何 Glyph 风格 UI 前，必须逐条核对以下红线：

- [ ] **禁止滥用红色**：检查全屏 `#D71921` 出现次数，是否严格控制在「最多 1 处核心活体焦点」（告警场景除外）？普通选中态必须用黑白反色而非红色。
- [ ] **禁止小字号使用 `Doto`**：所有 `Doto` 文本是否都 `>= 26px`？小于 `26px` 会糊成噪点，必须改用 `Space Mono` 或 `Space Grotesk`。
- [ ] **禁止冗余次级文案**：遵守极简克制原则，避免在卡片里塞满解释性副标题和冗余描述，让数字、点阵与空间层级自己说话。
- [ ] **禁止彩虹渐变与廉价毛玻璃**：不使用高饱和多色渐变背景、荧光外发光（neon glow）或泛白的高模糊毛玻璃。
- [ ] **禁止弹性过冲动画**：所有动效均使用 `cubic-bezier(0.25, 1, 0.5, 1)`，无 `bounce` / `spring` 过冲。
- [ ] **保证对比度与可读性**：激活态白底配纯黑字（`--glyph-fg` 配 `--glyph-ink`），浅色模式自动反转灰阶而非简单反相。

---

## 8. 资源索引
- 完整 CSS Design Tokens & 组件基础样式：[references/tokens.css](./references/tokens.css)
- 本地开源字体文件（OFL 协议）：[assets/fonts/](./assets/fonts/)（含 `Doto[ROND,wght].ttf`、`SpaceGrotesk-*.otf`、`SpaceMono-*.ttf`）
