# 🏭 KolFluent

**Microsoft Fluent 2 design system reference implementation.**

A self-contained HTML/CSS showcase of Fluent 2 design tokens — typography, color palettes, elevation, motion, and material effects. Dual-theme (light/dark) with zero framework dependencies.

🔗 **[Live Demo](https://goatxyz.github.io/KolFluent/)**

---

## ✨ Features

### 🎨 Design Tokens

- 🔤 **Type ramp** — 10 px–68 px across 5 font weights (Segoe UI Variable)
- 🌈 **Color palette** — Full semantic color system with automatic light/dark swapping
- 📐 **Spacing** — Consistent spacing scale from tokens
- 🏔️ **Elevation** — 8 shadow levels (shadow2–shadow64)

### ✨ Material Effects

- 🌫️ **Acrylic** — Frosted glass blur with noise texture
- 🪟 **Mica** — Subtle gradient backgrounds
- 💡 **Reveal Highlight** — Cursor-tracking radial gradient on hover

### 🌗 Theming

- 🔀 **Dual theme** — Light and dark mode via `data-theme` attribute
- 🎯 **Token swap** — No structural changes, just CSS variable reassignment
- 📏 **Spec-accurate** — Validated against Microsoft's official Fluent 2 documentation

### ⚡ Motion

- ⏱️ **8 duration tokens** — From ultra-fast to extra-slow
- 🔄 **8 easing curves** — Matched to Fluent 2 motion spec

---

## 🏗️ Architecture

```
KolFluent/
├── index.html            # Main showcase page (103 KB)
├── 6.html                # Secondary page (73 KB)
└── KolFluent.md          # Comprehensive design documentation (88 KB)
                            Typography, colors, spacing, elevation,
                            motion, components, material effects
```

### 🧠 Key Design Decisions

- **Zero dependencies** — Pure HTML/CSS/vanilla JS, no build step required
- **CSS custom properties** — All tokens as CSS variables for easy adoption
- **Self-documenting** — The showcase page *is* the documentation

---

## 🚀 Getting Started

Open `index.html` in a browser. That's it.

To serve locally:

```bash
python3 -m http.server 8080
# or
npx serve .
```

---

## 📦 Tech Stack

| Layer        | Technology                     |
| ------------ | ------------------------------ |
| 🎨 Tokens   | Microsoft Fluent 2 (hardcoded) |
| 🔷 Language  | HTML / CSS / Vanilla JS        |
| 🔤 Fonts     | Segoe UI Variable, Consolas    |

---

## 📄 License

Proprietary — [Kolene Corporation](https://kolene.com). Internal use only.

---

<p align="center">
  🏭 <a href="https://kolene.com">Kolene Corporation</a> — Internal Tool
</p>
