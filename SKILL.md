---
name: glyph-ui-style
description: >
  使用源自 Glyph / Nothing OS 的「极简黑白点阵 + 唯一红点」工业美学设计语言（Glyph UI Style）创建 Web、Dashboard、桌面应用或 SwiftUI 界面。当用户需要：
  (1) 使用 Nothing OS 风格、Glyph 风格、点阵 LED 风格、极简黑白红工业风创建 UI 页面或组件；
  (2) 构建高对比度深色/浅色 Bento 仪表盘、硬件控制台、音乐播放器、系统监控面板、极客工具或 AI 产品界面；
  (3) 复用 glyph-rice 与 nothing-design-skill 的融合视觉语言（Doto 点阵数字 + Space Grotesk + Space Mono 大写标签 + 7 级灰度阶梯 + #D71921 唯一红点 + 三层信息层级 + 环形点阵进度/分段灯带/展开胶囊开关 + SwiftUI/Tailwind/CSS 多平台映射）；
  (4) 提问"glyph 风格"、"Nothing OS 风格"、"nothing design"、"点阵风 UI"、"黑白红极客风"时，务必使用此 skill。
---

# Glyph UI Style — Nothing OS 工业点阵设计系统指南

本 Skill 融合提炼自两个开源项目：
- [**Nebelung-cloud/glyph-rice**](https://github.com/Nebelung-cloud/glyph-rice)：核心 7 级黑白灰阶、LED 点阵/灯带/展开胶囊开关等实装硬件原语、Glide 无过冲动效与本地开源字体资产。
- [**dominikmartn/nothing-design-skill**](https://github.com/dominikmartn/nothing-design-skill)（MIT License）：三层信息层级法则、间距语义与容器轻量化梯队、数据状态色规范、极客态反馈模式及多平台（Web / Tailwind / SwiftUI）映射。

> **核心视觉信条**：**Black, white dots, one red.**（纯黑基底、白色点阵、全屏仅一处红点；减法优先，让结构与数据本身成为装饰。）

---

## 1. 核心设计哲学与构图法则 (Philosophy & Craft Rules)

1. **减法优先（Subtract, don't add）**：每个像素都必须有理由存在，结构、网格与数据本身就是装饰。
2. **三层信息层级铁律（The Three-Layer Rule）**：每块屏幕严格控制为 **3 个视觉层级**：
   - **Primary（主焦点）**：用户第一眼看到的唯一核心（巨型数字、核心标题或主状态）。用 `Doto` 或大号 `Space Grotesk`，配充足呼吸留白（`48px–96px`）。
   - **Secondary（支撑层）**：上下文数据或短副标。用 `Space Grotesk` 正文体，紧密贴合主焦点（`8px–16px`）。
   - **Tertiary（元信息）**：时间、路径、标签、导航。用 `Space Mono` **全大写** + `--glyph-grey`，退至边缘或底角，绝不与主焦点抢戏。
   - *眯眼测试（Squint Test）*：眯起眼睛看页面，如果两个元素在抢夺视线，必须缩小、淡化或移开其中一个。
3. **「唯一红点」铁律（One Live Red）**：`#D71921` 在同一视野内**最多只出现 1 处**，专用于标识「当前正在运行的活体状态」（播放键、录制点、实时指针、核心 CTA）或「紧急告警」。如果页面没有紧急或活体焦点，可以完全不用红。常规选中态一律使用黑白反色（`--glyph-fg` 底 + `--glyph-ink` 字）。
4. **单点破局与不对称平衡**：全屏在字体、字距、节奏、对齐上高度一致，只在**恰好 1 处**打破规律（一个超大点阵数字、一个圆形组件、一处红点或一大片留白）；优先采用不对称构图（左大右小、上重下轻、边缘锚定），用留白而非堆元素来平衡视觉重量。
5. **容器轻量化梯队**：按从轻到重顺序选择分组方式——**① 纯间距分组 > ② 单根 `1px` 分割线 > ③ 细边框轮廓 > ④ 表面背景卡片**。不要给最重要的核心元素套多余的盒框。
6. **零过冲机械阻尼（Glide Motion）**：动效感官是「精密机械咔哒声（click/tick）」而非粘腻流体，统一使用 `cubic-bezier(0.25, 1, 0.5, 1)`，**严禁弹跳（bounce）或过冲（spring overshoot）**。

---

## 2. 色彩系统与 Design Tokens

完整可直接引入的 CSS 变量见 [references/tokens.css](./references/tokens.css)，多平台映射（Web / Tailwind / SwiftUI）见 [references/platform-mapping.md](./references/platform-mapping.md)。

### 2.1 七级灰度阶梯 + 唯一强调色

| Token | 语义角色 | Dark 模式（OLED 仪器面板） | Light 模式（印刷技术手册） | 使用说明 |
|---|---|---|---|---|
| `--glyph-bg` | 最底层画布 | `#000000` | `#E9E9E9` | 页面背景、点阵底布 |
| `--glyph-s1` | 一级表面 | `#0E0E0E` | `#FFFFFF` | 顶栏、侧栏、大面板、弹窗底 |
| `--glyph-s2` | 二级表面 | `#1A1A1A` | `#F1F1F1` | Bento 卡片、磁贴、未激活控件底 |
| `--glyph-s3` | 线条/熄灭态 | `#2A2A2A` | `#D9D9D9` | `1px` 边框、分割线、熄灭的 LED 点阵/灯带 |
| `--glyph-mute` | 弱化/禁用态 | `#4A4A4A` | `#B8B8B8` | 禁用态、滚动条滑块、未激活开关圆点 |
| `--glyph-grey` | 次级文本/标签 | `#8C8C8C` | `#6E6E6E` | 大写元标签、辅助说明、未选中导航字 |
| `--glyph-fg` | 主文本/高亮激活 | `#F2F2F2` | `#0B0B0B` | 主文字、点亮的 LED、激活态反色底 |
| `--glyph-ink` | 反色文字 | `#000000` | `#FFFFFF` | 写在 `--glyph-fg` 激活块上的反色文字/图标 |
| `--glyph-accent` | 唯一活体强调色 | `#D71921` | `#D71921` | **全屏最多 1 处**；深浅主题保持不变 |

### 2.2 数据语义状态色（仅限数据值豁免）
在仪表盘、监控与报表场景下，编码数据状态时可使用以下克制状态色（不受“全屏仅一处彩”限制），但**仅作用于数值/进度条本身，严禁给标签或整行刷彩色背景**：

| Token | 色值 | 语义 |
|---|---|---|
| `--glyph-success` | `#4A9E5C` | 健康、已连接、达标 |
| `--glyph-warning` | `#D4A843` | 注意、待处理、轻度超阈 |
| `--glyph-red` | `#D71921` | 告警、超限、错误 |
| `--glyph-interactive` | `#5B9BF6` (Dark) / `#007AFF` (Light) | 纯文字可点击链接 / 选择器值（不用于按钮） |

---

## 3. 三字体排印与字号预算 (Typography)

本地 OFL 开源字体已内置于 [assets/fonts/](./assets/fonts/)，Web 原型也可通过 Google Fonts 加载（开工前必须显式声明字体加载方式）。

| 角色 | 字体族 | 关键样式规范 | 适用场景 |
|---|---|---|---|
| **点阵展示体 (`--font-dot`)** | `Doto` | `font-variation-settings: "ROND" 100, "wght" 900;`<br>`line-height: 0.85; font-variant-numeric: tabular-nums;`<br>**硬规则：字号严禁小于 `26px`**（推荐 `36px+`） | 时钟、KPI 大数字、百分比、温度、1–3 词 Hero 标 |
| **界面正文字体 (`--font-ui`)** | `Space Grotesk` | Hero 欢迎语：`weight: 300, letter-spacing: -0.02em`<br>正文/卡片：`weight: 400–500, 14px–16px` | 中文回退 `PingFang SC / Noto Sans SC / sans-serif` |
| **机械元标签 (`--font-mono`)** | `Space Mono` | `text-transform: uppercase; letter-spacing: 0.14em;`<br>`font-size: 11px–14px; color: var(--glyph-grey);` | 卡片顶标、状态栏、按钮文案、表格数字、单位、时间戳 |

> **单屏字体预算**：单屏尽量不超过 **3 个字号**（大 / 中 / 小）和 **2 个字重**。想拉大区分度时，优先拉大**间距**或调整**灰度**，而不是无节制增加新字号。

---

## 4. 间距语义、圆角与图标规范 (Layout, Geometry & Icons)

- **8px 基准间距即语义**：
  - `4px–8px`（Tight）：强绑定关系（图标 + 文字、数字 + 单位）
  - `16px–20px`（Medium）：同组异项（Bento 卡片间距、表单项、列表项）
  - `32px–48px`（Wide）：新区块分隔（大模块间距）
  - `64px–96px`（Vast）：语境切换（Hero 区与主体内容区之间）
- **双轨圆角体系（按场景二选一，单项目保持统一）**：
  - **Bento 硬件桌面风（Glyph 默认）**：交互控件全胶囊 `999px`；主面板/Bento 卡片 `24px–28px`；内部列表选中项 `14px`。
  - **精密仪器/技术面板风（Compact Technical）**：按钮胶囊 `999px` 或技术直角 `4px–8px`；紧凑卡片 `12px–16px`；数据条直角块 `0px`。
- **图标规范**：仅使用 `1.5px` 细单线无填充图标（推荐 Lucide thin / Phosphor thin，圆头圆角，继承文字颜色），**禁止实心填充图标、多色图标或用 Emoji 当 UI 图标**。
- **点阵画布背景**：`radial-gradient(circle, var(--glyph-s3) 1px, transparent 1px)`，`background-size: 12px–16px`。

---

## 5. 动效规范 (Motion)

- **唯一主曲线（Glide）**：`cubic-bezier(0.25, 1, 0.5, 1)`（ease-out-quart，无回弹）。
- **时长规范**：微状态/Hover 变亮 `140ms–200ms`；开关/面板过渡 `350ms`；点阵波浪逐颗延迟 `8ms`。
- **机械离散闪烁**：时钟冒号、录制点采用 `steps(1)` 在 `opacity: 1` 与 `0.2` 之间切换（`1s` 周期）。

---

## 6. 标志性组件与状态反馈模式 (Components & State Patterns)

### 6.1 六大 Glyph 硬件原语
1. **Bento 读数卡**：左上 `Space Mono` 大写顶标 + `Doto` 核心大数字 + 底部状态条/元信息。
2. **Seg 分段灯带**：12 段等宽胶囊或直角块（`2px–4px` 间隙），未点亮 `--glyph-s3`，点亮 `--glyph-fg`（超阈告警段切 `--glyph-red`）；务必配数字读数（条表比例，数表精度）。
3. **Ring 环形点阵进度**：`24–44` 颗 `5px–6px` 圆点沿圆周排布，从 12 点钟顺时针按 `index * 8ms` 波浪点亮。
4. **展开式胶囊开关（Expanding Pill Toggle）**：关闭态左侧小灰圆 + 右侧灰字；开启态滑块以 `350ms Glide` 拉满整颗胶囊变 `--glyph-fg`，文字左移并反色为 `--glyph-ink`。
5. **唯一红点动作钮**：正圆 `#D71921` 底 + `#FFFFFF` 图标，承担全屏唯一活体焦点。
6. **黑白点阵滤镜（Halftone Mask）**：图片/封面去色转高对比黑白后叠加点阵网格或 Canvas 采样点阵。

### 6.2 数据密集页的视觉形式多样化
单屏出现 3 个以上数据区块时，避免全部长成一模一样的卡片——主区块用重形式（Hero 数字），次区块换形式（分段灯带 / 环形点阵 / 折线图），辅助区用轻形式（纯文字 Stat 行、紧凑行内条）。

### 6.3 极客态交互模式（拒绝庸俗 Web 模板）
- **加载态**：不用骨架屏（Skeleton）→ 用 `[LOADING...]` 括号等宽文字或分段硬件进度条。
- **操作反馈**：不用悬浮 Toast 弹窗 → 在触发按钮旁就地显示内联状态：`[SAVED]`、`[COPIED]`、`[ERROR: ...]`。
- **表格与列表**：不用斑马纹（Zebra Striping）→ 用 `1px solid var(--glyph-s3)` 细分割线，文字左对齐、数字用 `Space Mono` 右对齐，选中行左侧加 `2px solid var(--glyph-accent)` 竖线。
- **空状态**：大留白居中，一句克制说明，禁止可爱卡通插画或哭脸。

---

## 7. 交付前自检红线 (Anti-Patterns)

- [ ] **已声明字体加载**：确认已引入本地字体或 Google Fonts（`Doto`、`Space Grotesk`、`Space Mono`）。
- [ ] **严控红色数量**：全屏 `#D71921` 作为 UI 强调色是否 `<= 1` 处？常规选中态是否使用了黑白反色？
- [ ] **禁止小号 `Doto`**：所有 `Doto` 文本是否都 `>= 26px`？
- [ ] **符合三层层级与留白**：眯眼能否一眼分辨 Primary / Secondary / Tertiary？是否去掉了冗余次级解释文案？
- [ ] **无禁用视觉杂质**：无渐变、无厚重投影、无毛玻璃、无斑马纹、无骨架屏、无 Toast 弹窗、无弹跳动效、无实心/多色图标。

---

## 8. 资源索引
- CSS Design Tokens & 组件基础样式：[references/tokens.css](./references/tokens.css)
- 多平台代码映射（HTML/CSS · Tailwind · SwiftUI）：[references/platform-mapping.md](./references/platform-mapping.md)
- 交互式离线组件演示：[demo.html](./demo.html)
- 内嵌 OFL 开源字体：[assets/fonts/](./assets/fonts/)
