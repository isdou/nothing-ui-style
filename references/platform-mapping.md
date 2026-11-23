# Glyph UI Style — 多平台映射指南 (Platform Mapping)

> 本映射指南参考并吸收自 [**dominikmartn/nothing-design-skill**](https://github.com/dominikmartn/nothing-design-skill)（MIT License），并统一对齐 `glyph-ui-style` 的 7 级灰阶与动效规范。

---

## 1. HTML / CSS / Web

直接引入 [`references/tokens.css`](./tokens.css)，并加载本地 `assets/fonts/` 或 Google Fonts：

```html
<link rel="preconnect" href="https://fonts.googleapis.com" />
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
<link
  href="https://fonts.googleapis.com/css2?family=Doto:ROND,wght@100,900&family=Space+Grotesk:wght@300;400;500;600&family=Space+Mono:wght@400;700&display=swap"
  rel="stylesheet"
/>
```

通过 `<html data-theme="dark">` 或 `<html data-theme="light">` 切换双主题。

---

## 2. Tailwind CSS（v4 `@theme` 映射）

在全局 CSS 中声明 Tailwind v4 主题变量，即可直接使用 `bg-glyph-s1`、`text-glyph-fg`、`border-glyph-s3`、`font-dot`、`font-mono`：

```css
@import "tailwindcss";

@theme {
  --color-glyph-bg: var(--glyph-bg);
  --color-glyph-s1: var(--glyph-s1);
  --color-glyph-s2: var(--glyph-s2);
  --color-glyph-s3: var(--glyph-s3);
  --color-glyph-mute: var(--glyph-mute);
  --color-glyph-grey: var(--glyph-grey);
  --color-glyph-fg: var(--glyph-fg);
  --color-glyph-ink: var(--glyph-ink);
  --color-glyph-accent: var(--glyph-accent);
  --color-glyph-success: var(--glyph-success);
  --color-glyph-warning: var(--glyph-warning);

  --font-dot: "Doto", monospace;
  --font-ui: "Space Grotesk", -apple-system, "PingFang SC", sans-serif;
  --font-mono: "Space Mono", ui-monospace, monospace;

  --ease-glide: cubic-bezier(0.25, 1, 0.5, 1);
}
```

---

## 3. SwiftUI（iOS / macOS）

将 `assets/fonts/` 中的 `.ttf` / `.otf` 字体加入项目并在 `Info.plist` 的 `UIAppFonts` 中注册，使用 `@Environment(\.colorScheme)` 适配深浅双色：

```swift
import SwiftUI

enum GlyphColor {
    static func bg(_ scheme: ColorScheme) -> Color   { scheme == .dark ? Color(hex: 0x000000) : Color(hex: 0xE9E9E9) }
    static func s1(_ scheme: ColorScheme) -> Color   { scheme == .dark ? Color(hex: 0x0E0E0E) : Color(hex: 0xFFFFFF) }
    static func s2(_ scheme: ColorScheme) -> Color   { scheme == .dark ? Color(hex: 0x1A1A1A) : Color(hex: 0xF1F1F1) }
    static func s3(_ scheme: ColorScheme) -> Color   { scheme == .dark ? Color(hex: 0x2A2A2A) : Color(hex: 0xD9D9D9) }
    static func mute(_ scheme: ColorScheme) -> Color { scheme == .dark ? Color(hex: 0x4A4A4A) : Color(hex: 0xB8B8B8) }
    static func grey(_ scheme: ColorScheme) -> Color { scheme == .dark ? Color(hex: 0x8C8C8C) : Color(hex: 0x6E6E6E) }
    static func fg(_ scheme: ColorScheme) -> Color   { scheme == .dark ? Color(hex: 0xF2F2F2) : Color(hex: 0x0B0B0B) }
    static func ink(_ scheme: ColorScheme) -> Color  { scheme == .dark ? Color(hex: 0x000000) : Color(hex: 0xFFFFFF) }

    static let accent  = Color(hex: 0xD71921) // One live red
    static let success = Color(hex: 0x4A9E5C)
    static let warning = Color(hex: 0xD4A843)
}

extension Font {
    static func glyphDot(_ size: CGFloat) -> Font  { .custom("Doto", size: max(size, 26)) }
    static func glyphUI(_ size: CGFloat) -> Font   { .custom("SpaceGrotesk-Regular", size: size) }
    static func glyphMono(_ size: CGFloat) -> Font { .custom("SpaceMono-Regular", size: size) }
}

extension Animation {
    /// Glide: ease-out-quart, zero overshoot
    static let glyphGlide = Animation.timingCurve(0.25, 1.0, 0.5, 1.0, duration: 0.35)
}

private extension Color {
    init(hex: UInt32) {
        self.init(
            red: Double((hex >> 16) & 0xFF) / 255.0,
            green: Double((hex >> 8) & 0xFF) / 255.0,
            blue: Double(hex & 0xFF) / 255.0
        )
    }
}
```
