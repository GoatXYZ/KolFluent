# KolFluent Design System — Complete Documentation

A design system following **Microsoft's [Fluent 2 Design System](https://fluent2.microsoft.design/)** guidance. Two modes: **KolFluent** (light) and **KolFluent Dark**. Shared structure, typography, spacing, and component patterns — differentiated by color palette, shadow intensity, and surface material treatment.

> **Source of truth**: All design tokens, color values, type ramp, elevation levels, motion curves, spacing scale, and material effects (Acrylic, Mica, Reveal Highlight) in this document are derived from Microsoft's official Fluent 2 Design System documentation and the `webLightTheme` / `webDarkTheme` token sets from [`@fluentui/react-components`](https://react.fluentui.dev/). Token names map 1:1 to the Fluent UI React v9 theme API.

> **Origin**: Implemented as a Fluent 2 showcase ("Flowstate" product landing page) from a multi-direction design exploration. Codenames: **Fluent Light** (`data-theme="light"`) and **Fluent Dark** (`data-theme="dark"`). Built as a self-contained HTML implementation using pure CSS custom properties and vanilla JavaScript.

---

## 1. Design Principles

- **Layered surfaces.** Content hierarchy established through elevation (shadow2 through shadow64) and translucent materials (Acrylic blur, Mica gradients), not border weight or color alone.
- **Brand as accent, neutral as foundation.** A single brand blue ramp provides interactive color. The vast majority of the UI is neutral greys, letting content dominate.
- **Systematized motion.** Eight duration tokens and eight easing curves guarantee consistent, physically plausible transitions across every interactive state.
- **Reveal and respond.** Fluent Reveal Highlight — a radial gradient that tracks the cursor — gives every card a tangible, physical quality. Active press uses `scale(0.98)`.
- **Adaptive theming.** A single `data-theme` attribute swaps the entire palette. Shadows double their alpha in dark mode. Acrylic material adjusts its tint. No structural changes, just token reassignment.

---

## 2. Typography

### Font Stacks

| Role | Family | Fallbacks |
|------|--------|-----------|
| **Base** (body, buttons, headings, all UI text) | `Segoe UI Variable` | `Segoe UI`, `system-ui`, `-apple-system`, `BlinkMacSystemFont`, `sans-serif` |
| **Monospace** (code, technical labels) | `Consolas` | `Courier New`, `Courier`, `monospace` |

> **Fluent 2 reference**: Fluent 2 uses a [single typeface family](https://fluent2.microsoft.design/typography) (`Segoe UI Variable`) for all hierarchical roles. Hierarchy is conveyed by size, weight, and line height alone — matching Microsoft's type ramp from `fontSizeBase100` (10px) through `fontSizeHero1000` (68px). `Segoe UI Variable` is a system font on Windows. On macOS/Linux, the stack falls through to `system-ui` / `-apple-system`. No external font import is needed.

### Type Scale — Fluent 2 Type Ramp

| Token | Size | Semantic Name | Line Height | Usage |
|-------|------|---------------|-------------|-------|
| `--fontSizeBase100` | `10px` | Caption 2 | `14px` | Footer copyright, pricing badge, stat change indicators |
| `--fontSizeBase200` | `12px` | Caption 1 | `16px` | Announcement bar, overlines, footer links, card labels |
| `--fontSizeBase300` | `14px` | Body 1 | `20px` | Body base, buttons, nav links, descriptions, FAQ answers |
| `--fontSizeBase400` | `16px` | Subtitle 2 | `22px` | Navbar logo, hero description, card titles, FAQ questions |
| `--fontSizeBase500` | `20px` | Subtitle 1 | `26px` | (Available in ramp) |
| `--fontSizeBase600` | `24px` | Title 3 | `32px` | Section titles (min clamp), dash-card values |
| `--fontSizeHero700` | `28px` | Title 2 | `36px` | Section titles (max clamp), metric numbers (min clamp) |
| `--fontSizeHero800` | `32px` | Title 1 | `40px` | Hero h1 (min clamp), pricing price |
| `--fontSizeHero900` | `40px` | Large Title | `52px` | CTA title (max clamp), metric numbers (max clamp) |
| `--fontSizeHero1000` | `68px` | Display | `92px` | Hero h1 (max clamp) |

### Font Weights

| Token | Value | Usage |
|-------|-------|-------|
| `--fontWeightRegular` | `400` | Body text, nav links, pricing period text |
| `--fontWeightMedium` | `500` | Hero badge, social proof label, card labels, stat change |
| `--fontWeightSemibold` | `600` | Buttons, headings, navbar logo, section titles, pricing price, author names |
| `--fontWeightBold` | `700` | (Available in ramp, reserved for emphasis) |

### Base Styles

```css
html {
  scroll-behavior: smooth;
}

body {
  font-family: var(--fontFamilyBase);
  font-size: var(--fontSizeBase300);      /* 14px */
  line-height: var(--lineHeightBase300);  /* 20px */
  color: var(--colorNeutralForeground1);
  background-color: var(--colorNeutralBackground2);
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  transition: background-color var(--durationSlower) var(--curveEasyEase),
              color var(--durationSlower) var(--curveEasyEase);
}

img { display: block; max-width: 100%; }
a { color: var(--colorBrandForegroundLink); text-decoration: none; }
a:hover { color: var(--colorBrandForegroundLinkHover); text-decoration: underline; }
```

---

## 3. Color Tokens

### Dual Palette

> **Fluent 2 reference**: These tokens follow Microsoft's Fluent 2 color token naming and values as defined in the [Fluent 2 Design System — Color](https://fluent2.microsoft.design/color) documentation. Light values correspond to `webLightTheme` and dark values to `webDarkTheme` from `@fluentui/tokens`.

#### Brand Colors

| Token | KolFluent (Light) | KolFluent Dark | Notes |
|-------|-------------------|----------------|-------|
| `--colorBrandBackground` | `#0f6cbd` | `#115ea3` | Primary interactive fill; darker in dark mode |
| `--colorBrandBackgroundHover` | `#115ea3` | `#0f6cbd` | Light/dark swap — dark hover is brighter than rest |
| `--colorBrandBackgroundPressed` | `#0c3b5e` | `#0f548c` | Active/pressed state |
| `--colorBrandBackgroundSelected` | `#115ea3` | — | Selection indicator |
| `--colorBrandBackground2` | `#ebf3fc` | `#0a2e4a` | Tinted surface; tint in light, deep shade in dark |
| `--colorBrandBackground2Hover` | `#b4d6fa` | — | Light-only hover on tinted surfaces |
| `--colorBrandForeground1` | `#0f6cbd` | `#479ef5` | Primary text/icon on neutral bg; much brighter in dark |
| `--colorBrandForeground2` | `#115ea3` | `#62abf5` | Secondary brand text |
| `--colorBrandForegroundLink` | `#115ea3` | `#479ef5` | Link color |
| `--colorBrandForegroundLinkHover` | `#0f548c` | `#77bcf8` | Link hover |
| `--colorBrandStroke1` | `#0f6cbd` | `#479ef5` | Brand-colored borders (featured pricing card) |

#### Neutral Backgrounds

| Token | KolFluent (Light) | KolFluent Dark | Notes |
|-------|-------------------|----------------|-------|
| `--colorNeutralBackground1` | `#ffffff` | `#292929` | Primary card/surface bg |
| `--colorNeutralBackground1Hover` | `#f5f5f5` | `#3d3d3d` | Card hover bg |
| `--colorNeutralBackground1Pressed` | `#e0e0e0` | — | Pressed state |
| `--colorNeutralBackground2` | `#fafafa` | `#1f1f1f` | Page background (body) |
| `--colorNeutralBackground3` | `#f5f5f5` | `#141414` | Titlebar, nav rail bg |
| `--colorNeutralBackground4` | `#f0f0f0` | `#0f0f0f` | Surface skeleton bars, chips |
| `--colorNeutralBackground5` | `#ebebeb` | `#0a0a0a` | Surface indicator dots |
| `--colorNeutralBackground6` | `#e0e0e0` | `#333333` | Deepest neutral fill |

#### Neutral Foregrounds

| Token | KolFluent (Light) | KolFluent Dark | Notes |
|-------|-------------------|----------------|-------|
| `--colorNeutralForeground1` | `#242424` | `#ffffff` | Primary text |
| `--colorNeutralForeground2` | `#424242` | `#d6d6d6` | Secondary text, subtle button text |
| `--colorNeutralForeground3` | `#616161` | `#adadad` | Tertiary text, descriptions |
| `--colorNeutralForeground4` | `#707070` | `#999999` | Quaternary, social proof logos, footer text |
| `--colorNeutralForegroundDisabled` | `#bdbdbd` | `#5c5c5c` | Disabled state |
| `--colorNeutralForegroundOnBrand` | `#ffffff` | `#ffffff` | Text on brand bg (same in both themes) |

#### Neutral Strokes

| Token | KolFluent (Light) | KolFluent Dark | Notes |
|-------|-------------------|----------------|-------|
| `--colorNeutralStroke1` | `#d1d1d1` | `#666666` | Primary border, card hover border |
| `--colorNeutralStroke2` | `#e0e0e0` | `#525252` | Card resting border, navbar border |
| `--colorNeutralStroke3` | `#f0f0f0` | `#3d3d3d` | Footer divider |
| `--colorNeutralStrokeAccessible` | `#616161` | `#adadad` | WCAG AA-accessible stroke |

#### Subtle

| Token | KolFluent (Light) | KolFluent Dark | Notes |
|-------|-------------------|----------------|-------|
| `--colorSubtleBackground` | `transparent` | `transparent` | Theme toggle resting bg |
| `--colorSubtleBackgroundHover` | `#f5f5f5` | `#383838` | Nav link hover, outline button hover |
| `--colorSubtleBackgroundPressed` | `#e0e0e0` | `#2e2e2e` | Pressed subtle elements |

#### Compound Brand

| Token | KolFluent (Light) | KolFluent Dark | Notes |
|-------|-------------------|----------------|-------|
| `--colorCompoundBrandBackground` | `#0f6cbd` | `#479ef5` | Compound brand fill |
| `--colorCompoundBrandBackgroundHover` | `#115ea3` | `#62abf5` | Compound brand hover |
| `--colorCompoundBrandStroke` | `#0f6cbd` | `#479ef5` | Compound brand border |

#### Status

| Token | KolFluent (Light) | KolFluent Dark | Notes |
|-------|-------------------|----------------|-------|
| `--colorStatusSuccessBackground1` | `#f1faf1` | — | Success tint bg (pricing checkmarks) |
| `--colorStatusSuccessForeground1` | `#0e700e` | — | Success text (stat change indicators) |
| `--colorStatusWarningBackground1` | `#fff9f5` | — | Warning tint bg |
| `--colorStatusWarningForeground1` | `#bc4b09` | — | Warning text |

> Status tokens are not overridden in the dark theme. They inherit light values since their usage contexts (pricing check marks, stat changes) appear within cards that maintain sufficient contrast.

---

## 4. Shadows

> **Fluent 2 reference**: The 6-step elevation system follows Microsoft's [Fluent 2 Elevation](https://fluent2.microsoft.design/elevation) guidance. Each shadow is a two-layer composite (directional key light + ambient fill) matching the `shadow2`–`shadow64` tokens from `@fluentui/tokens`.

### Elevation System — 6-Step

| Token | KolFluent (Light) | KolFluent Dark |
|-------|-------------------|----------------|
| `--shadow2` | `0px 1px 2px rgba(0,0,0,0.14), 0px 0px 2px rgba(0,0,0,0.12)` | `0px 1px 2px rgba(0,0,0,0.48), 0px 0px 2px rgba(0,0,0,0.24)` |
| `--shadow4` | `0px 2px 4px rgba(0,0,0,0.14), 0px 0px 2px rgba(0,0,0,0.12)` | `0px 2px 4px rgba(0,0,0,0.48), 0px 0px 2px rgba(0,0,0,0.24)` |
| `--shadow8` | `0px 4px 8px rgba(0,0,0,0.14), 0px 0px 2px rgba(0,0,0,0.12)` | `0px 4px 8px rgba(0,0,0,0.48), 0px 0px 2px rgba(0,0,0,0.24)` |
| `--shadow16` | `0px 8px 16px rgba(0,0,0,0.14), 0px 0px 2px rgba(0,0,0,0.12)` | `0px 8px 16px rgba(0,0,0,0.48), 0px 0px 2px rgba(0,0,0,0.24)` |
| `--shadow28` | `0px 14px 28px rgba(0,0,0,0.14), 0px 0px 8px rgba(0,0,0,0.12)` | `0px 14px 28px rgba(0,0,0,0.48), 0px 0px 8px rgba(0,0,0,0.24)` |
| `--shadow64` | `0px 32px 64px rgba(0,0,0,0.14), 0px 0px 8px rgba(0,0,0,0.12)` | `0px 32px 64px rgba(0,0,0,0.48), 0px 0px 8px rgba(0,0,0,0.24)` |

Dark mode uses ~3.4x higher alpha on the directional layer (0.48 vs 0.14) and 2x on the ambient layer (0.24 vs 0.12) because dark surfaces need stronger shadows to register visually. Each shadow is a two-layer composite: a directional key light and an ambient fill.

### Shadow Usage

| Shadow | Usage |
|--------|-------|
| `shadow2` | Card resting state |
| `shadow4` | Navbar on scroll |
| `shadow8` | Card hover, mobile nav dropdown, hero surface 1 |
| `shadow16` | Hero surface 2 |
| `shadow28` | Dashboard frame |
| `shadow64` | (Available for dialogs/overlays) |

---

## 5. Radius & Spacing

### Radius Scale

| Token | Value | Usage |
|-------|-------|-------|
| `--borderRadiusNone` | `0` | Reset |
| `--borderRadiusSmall` | `2px` | Chart bar top corners |
| `--borderRadiusMedium` | `4px` | Buttons, nav links, theme toggle, nav-rail items, chips, titlebar search |
| `--borderRadiusLarge` | `6px` | Feature icon containers, dashboard inner cards |
| `--borderRadiusXLarge` | `8px` | Cards (`fluent-card`), hero surfaces, dashboard frame |
| `--borderRadiusCircular` | `10000px` | Hero badge (pill), testimonial avatar, pricing badge, titlebar dots |

### Spacing Scale

| Token | Value | Usage |
|-------|-------|-------|
| `--spacingXXS` | `2px` | (Reserved) |
| `--spacingXS` | `4px` | Navbar link gap, nav rail item gap |
| `--spacingSNudge` | `6px` | Pricing feature list item padding |
| `--spacingS` | `8px` | Button icon gap, announcement padding, hero badge gap, section margins |
| `--spacingMNudge` | `10px` | (Reserved) |
| `--spacingM` | `12px` | Navbar-right gap, footer heading margins, testimonial author gap |
| `--spacingL` | `16px` | Feature/metrics/pricing grid gap, hero heading margin, footer legal gap, FAQ question padding |
| `--spacingXL` | `20px` | Social proof label margin, pricing desc padding/margin, testimonial quote margin |
| `--spacingXXL` | `24px` | Card padding, container side-padding, hero badge margin-bottom |
| `--spacingXXXL` | `32px` | Hero description margin, footer grid gap, CTA description margin |

### Stroke Widths

| Token | Value | Usage |
|-------|-------|-------|
| `--strokeWidthThin` | `1px` | All borders (cards, navbar, buttons, inputs) |
| `--strokeWidthThick` | `2px` | (Available for emphasis borders) |

### Content Widths

| Element | Width |
|---------|-------|
| Container max-width | `1200px` |
| Container padding | `24px` desktop, `16px` mobile |
| Dashboard frame max-width | `960px` |
| FAQ list max-width | `720px` |
| Section description max-width | `560px` |
| Hero content max-width | `600px` |
| Hero description max-width | `500px` |
| Pricing card max-width (mobile) | `400px` |

---

## 6. Theme-Specific Behaviors

These are the structural differences between light and dark that go beyond simple color token swaps.

> **Dark mode mechanism**: The `data-theme` attribute on the `<html>` element is toggled by JavaScript. The quick-start blocks in Section 15 offer a `prefers-color-scheme` media query as an alternative approach.

### Navigation Bar — Acrylic Material

| Property | KolFluent (Light) | KolFluent Dark |
|----------|-------------------|----------------|
| Background | `rgba(255,255,255,0.72)` | `rgba(41,41,41,0.72)` |
| Backdrop filter | `saturate(180%) blur(20px)` | `saturate(180%) blur(20px)` |
| Effect | Translucent white Acrylic | Translucent dark Acrylic |

### Card Reveal Highlight

| Property | KolFluent (Light) | KolFluent Dark |
|----------|-------------------|----------------|
| Gradient color | `rgba(0,0,0,0.04)` | `rgba(255,255,255,0.06)` |
| Effect | Dark radial gradient on white surface | Light radial gradient on dark surface |
| Radius | `250px` circle, mouse-tracking | `250px` circle, mouse-tracking |

### Hero Background — Mica-Inspired

| Property | KolFluent (Light) | KolFluent Dark |
|----------|-------------------|----------------|
| Primary gradient | `rgba(15,108,189,0.07)` at 65% 10% | `rgba(71,158,245,0.08)` at 65% 10% |
| Secondary gradient | `rgba(15,108,189,0.04)` at 25% 90% | `rgba(71,158,245,0.04)` at 25% 90% |
| Tint source | Brand resting `#0f6cbd` | Brand foreground `#479ef5` |

### CTA Section Button Inversion

| Property | KolFluent (Light) | KolFluent Dark |
|----------|-------------------|----------------|
| Button bg | `white` | `white` |
| Button text | `--colorBrandBackground` | `--colorBrandBackground` |
| Button hover bg | `rgba(255,255,255,0.9)` | `rgba(255,255,255,0.9)` |

### Theme Toggle Icon

| Theme | Visible Icon | Hidden Icon |
|-------|-------------|-------------|
| Light | Sun (&#9788;) | Moon |
| Dark | Moon (&#9790;) | Sun |

---

## 7. Components

### 7.1 Button

3 variants, 2 sizes. Active press: `transform: scale(0.98)`.

**Shared Properties** — All buttons: `display: inline-flex`, `align-items: center`, `justify-content: center`, `gap: var(--spacingS)`, `font-family: var(--fontFamilyBase)`, `font-size: var(--fontSizeBase300)`, `font-weight: var(--fontWeightSemibold)`, `border-radius: var(--borderRadiusMedium)`, `border: var(--strokeWidthThin) solid transparent`, `cursor: pointer`, `transition: background-color/border-color/color/box-shadow var(--durationFast) var(--curveEasyEase)`.

**Sizes**

| Size | Min Height | Padding | Font Size | Radius |
|------|-----------|---------|-----------|--------|
| `default` | `32px` | `5px 12px` | `14px` | Medium (4px) |
| `lg` | `40px` | `8px 16px` | `14px` | Medium (4px) |

**Variants**

| Variant | Background | Text | Border | Hover |
|---------|-----------|------|--------|-------|
| `primary` | `--colorBrandBackground` | `--colorNeutralForegroundOnBrand` | `--colorBrandBackground` | `--colorBrandBackgroundHover` bg/border |
| `outline` | `transparent` | `--colorNeutralForeground1` | `--colorNeutralStroke1` | `--colorSubtleBackgroundHover` bg |
| `subtle` | `--colorSubtleBackground` (transparent) | `--colorNeutralForeground2` | `transparent` | `--colorSubtleBackgroundHover` bg, `--colorNeutralForeground1` text |

```css
.fluent-btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: var(--spacingS);
  padding: 5px 12px;
  min-height: 32px;
  font-family: var(--fontFamilyBase);
  font-size: var(--fontSizeBase300);
  font-weight: var(--fontWeightSemibold);
  line-height: var(--lineHeightBase300);
  border-radius: var(--borderRadiusMedium);
  border: var(--strokeWidthThin) solid transparent;
  cursor: pointer;
  transition: background-color var(--durationFast) var(--curveEasyEase),
              border-color var(--durationFast) var(--curveEasyEase),
              color var(--durationFast) var(--curveEasyEase),
              box-shadow var(--durationFast) var(--curveEasyEase);
  text-decoration: none;
}

.fluent-btn:active { transform: scale(0.98); }

.fluent-btn-primary {
  background-color: var(--colorBrandBackground);
  color: var(--colorNeutralForegroundOnBrand);
  border-color: var(--colorBrandBackground);
}
.fluent-btn-primary:hover {
  background-color: var(--colorBrandBackgroundHover);
  border-color: var(--colorBrandBackgroundHover);
}
.fluent-btn-primary:active {
  background-color: var(--colorBrandBackgroundPressed);
  border-color: var(--colorBrandBackgroundPressed);
}

.fluent-btn-outline {
  background-color: transparent;
  color: var(--colorNeutralForeground1);
  border-color: var(--colorNeutralStroke1);
}
.fluent-btn-outline:hover {
  background-color: var(--colorSubtleBackgroundHover);
}

.fluent-btn-subtle {
  background-color: var(--colorSubtleBackground);
  color: var(--colorNeutralForeground2);
  border-color: transparent;
}
.fluent-btn-subtle:hover {
  background-color: var(--colorSubtleBackgroundHover);
  color: var(--colorNeutralForeground1);
}

.fluent-btn-lg {
  padding: 8px 16px;
  min-height: 40px;
  font-size: var(--fontSizeBase300);
  border-radius: var(--borderRadiusMedium);
}
```

### 7.2 Card (with Fluent Reveal Highlight)

Compound component with a `::before` pseudo-element that creates a mouse-tracking radial gradient.

| Property | Style |
|----------|-------|
| Background | `--colorNeutralBackground1` |
| Border | `var(--strokeWidthThin) solid var(--colorNeutralStroke2)` |
| Radius | `--borderRadiusXLarge` (8px) |
| Shadow (resting) | `--shadow2` |
| Shadow (hover) | `--shadow8` |
| Border (hover) | `--colorNeutralStroke1` |
| Padding | `--spacingXXL` (24px) |
| Overflow | `hidden` |
| Transition | `box-shadow/border-color var(--durationNormal) var(--curveEasyEase)` |

**Reveal Highlight** — The `::before` pseudo-element covers the card with `inset: -1px`, renders a `radial-gradient(circle 250px at var(--reveal-x) var(--reveal-y))`, and fades in on hover. JavaScript sets `--reveal-x` and `--reveal-y` via `mousemove`:

```css
.fluent-card::before {
  content: '';
  position: absolute;
  inset: -1px;
  border-radius: inherit;
  background: radial-gradient(
    circle 250px at var(--reveal-x, 50%) var(--reveal-y, 50%),
    rgba(0,0,0,0.04),
    transparent
  );
  opacity: 0;
  transition: opacity var(--durationNormal) var(--curveEasyEase);
  pointer-events: none;
  z-index: 0;
}

[data-theme="dark"] .fluent-card::before {
  background: radial-gradient(
    circle 250px at var(--reveal-x, 50%) var(--reveal-y, 50%),
    rgba(255,255,255,0.06),
    transparent
  );
}

.fluent-card:hover::before { opacity: 1; }
```

```js
document.querySelectorAll('.reveal-card').forEach(card => {
  card.addEventListener('mousemove', (e) => {
    const rect = card.getBoundingClientRect();
    card.style.setProperty('--reveal-x', (e.clientX - rect.left) + 'px');
    card.style.setProperty('--reveal-y', (e.clientY - rect.top) + 'px');
  });
});
```

### 7.3 Announcement Bar

| Property | Style |
|----------|-------|
| Background | `--colorBrandBackground` |
| Text color | `--colorNeutralForegroundOnBrand` |
| Padding | `var(--spacingS) var(--spacingXXL)` |
| Font size | `--fontSizeBase200` (12px) |
| Line height | `--lineHeightBase200` (16px) |
| Text align | `center` |
| Link style | Inherited color, `--fontWeightSemibold`, `underline`, `text-underline-offset: 2px` |
| Link hover | `opacity: 0.85` |

### 7.4 Navbar — Acrylic Material

| Property | Style |
|----------|-------|
| Position | `sticky`, `top: 0`, `z-index: 1000` |
| Height | `48px` |
| Light background | `rgba(255,255,255,0.72)` + `backdrop-filter: saturate(180%) blur(20px)` |
| Dark background | `rgba(41,41,41,0.72)` + `backdrop-filter: saturate(180%) blur(20px)` |
| Border | `var(--strokeWidthThin) solid var(--colorNeutralStroke2)` |
| On-scroll shadow | `.scrolled` class adds `--shadow4` |
| Max-width | `1200px`, centered |
| Padding | `0 var(--spacingXXL)` |

**Logo**: `--fontSizeBase400`, `--fontWeightSemibold`, `--colorNeutralForeground1`, `gap: var(--spacingS)`, SVG icon `20x20`.

**Nav Links**: `padding: 6px 10px`, `--fontSizeBase300`, `--fontWeightRegular`, `--colorNeutralForeground2`, `--borderRadiusMedium`. Gap between links: `var(--spacingXS)`.

**Link States**

| State | Text | Background |
|-------|------|-----------|
| Default | `--colorNeutralForeground2` | `transparent` |
| Hover | `--colorNeutralForeground1` | `--colorSubtleBackgroundHover` |

### 7.5 Hero Section — Mica-Inspired

| Property | Style |
|----------|-------|
| Padding | `100px 0 80px` |
| Background | Mica-style radial gradients over `--colorNeutralBackground2` (see Section 6) |
| Layout | Flex, `55% content / 40% visual`, `gap: 64px` |
| Badge | Pill (`--borderRadiusCircular`), `--colorBrandBackground2` bg, `--colorBrandForeground1` text, `--fontSizeBase200`, `--fontWeightMedium` |
| H1 | `font-size: clamp(var(--fontSizeHero800), 5vw, var(--fontSizeHero1000))`, `--fontWeightSemibold`, `line-height: 1.1`, `letter-spacing: -0.02em` |
| Brand text span | `--colorBrandForeground1` |
| Description | `--fontSizeBase400`, `--colorNeutralForeground2`, `max-width: 500px` |
| Actions | Flex, `gap: var(--spacingM)`, primary + outline buttons in `lg` size |

### 7.6 Floating Surfaces (Hero Visual)

Three animated card-like surfaces positioned absolutely within the hero visual area.

| Surface | Size | Position | Shadow | Animation |
|---------|------|----------|--------|-----------|
| Surface 1 | `280x180` | `top: 20px, left: 0` | `shadow8` | `heroFloat1` — 6s, Y: -10px |
| Surface 2 | `220x140` | `top: 80px, left: 180px` | `shadow16` | `heroFloat2` — 7s, Y: -14px + rotate ±0.5deg |
| Surface 3 | `200x120` | `top: 180px, left: 40px` | `shadow4` | `heroFloat3` — 8s, Y: -8px |

All surfaces share: `--colorNeutralBackground1` bg, `--strokeWidthThin solid --colorNeutralStroke2` border, `--borderRadiusXLarge` radius. Inner content uses skeleton bars, indicator dots, and chips to simulate UI elements.

```css
@keyframes heroFloat1 {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-10px); }
}

@keyframes heroFloat2 {
  0%, 100% { transform: translateY(0) rotate(0.5deg); }
  50% { transform: translateY(-14px) rotate(-0.5deg); }
}

@keyframes heroFloat3 {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-8px); }
}
```

### 7.7 Social Proof

| Property | Style |
|----------|-------|
| Background | `--colorNeutralBackground2` |
| Padding | `56px 0` |
| Label | `--fontSizeBase200`, `--fontWeightMedium`, `--colorNeutralForeground4`, `uppercase`, `letter-spacing: 0.08em` |
| Logo text | `--fontSizeBase400`, `--fontWeightSemibold`, `--colorNeutralForeground4` |
| Logo gap | `40px`, flex wrap |

### 7.8 Section Header (Reusable Pattern)

Used by Features, Dashboard, Testimonials, Pricing, and FAQ sections.

| Element | Style |
|---------|-------|
| Overline | `--fontSizeBase200`, `--fontWeightSemibold`, `--colorBrandForeground1`, `uppercase`, `letter-spacing: 0.06em`, `margin-bottom: var(--spacingS)` |
| Title | `font-size: clamp(var(--fontSizeBase600), 3vw, var(--fontSizeHero700))`, `--fontWeightSemibold`, `--lineHeightHero700`, `margin-bottom: var(--spacingS)` |
| Description | `--fontSizeBase400`, `--lineHeightBase400`, `--colorNeutralForeground3`, `max-width: 560px`, `margin-bottom: 48px` |

### 7.9 Feature Card

Extends `fluent-card` with feature-specific content.

| Element | Style |
|---------|-------|
| Icon container | `40x40`, `--borderRadiusLarge`, `--colorBrandBackground2` bg, `--colorBrandForeground1` color, `margin-bottom: var(--spacingL)` |
| Icon SVG | `18px` in `20x20` viewBox, `stroke-width: 1.5`, `currentColor` |
| Title | `--fontSizeBase400`, `--fontWeightSemibold`, `--lineHeightBase400`, `margin-bottom: var(--spacingS)` |
| Description | `--fontSizeBase300`, `--lineHeightBase300`, `--colorNeutralForeground3` |
| Grid | `3 columns`, `gap: var(--spacingL)` |

### 7.10 Dashboard Preview

Full app mockup component.

| Element | Style |
|---------|-------|
| Frame | `--colorNeutralBackground1` bg, `--colorNeutralStroke1` border, `--borderRadiusXLarge`, `--shadow28`, `max-width: 960px` |
| Titlebar | `--colorNeutralBackground3` bg, `padding: 10px 16px`, 3x `10px` dots, search bar (26px height, `--borderRadiusMedium`), avatar circle (24px, brand bg) |
| Nav Rail | `48px` wide, `--colorNeutralBackground3` bg, `32x32` items, active: `--colorBrandBackground2` bg / `--colorBrandForeground1` text |
| Main Grid | `2 columns`, `gap: 12px`, `padding: 20px` |
| Dash Card | `--borderRadiusLarge`, `padding: 16px`, label (`--fontSizeBase200`, `--colorNeutralForeground3`), value (`--fontSizeBase600`, `--fontWeightSemibold`), change (`--fontSizeBase100`, `--colorStatusSuccessForeground1`) |
| Chart Bars | `--borderRadiusSmall` top, `--colorBrandBackground2` default, `--colorBrandBackground` active, flex-equal width |

### 7.11 Metric Card

Extends `fluent-card`. Center-aligned.

| Element | Style |
|---------|-------|
| Padding | `var(--spacingXXXL) var(--spacingXXL)` |
| Number | `font-size: clamp(var(--fontSizeHero700), 3vw, var(--fontSizeHero900))`, `--fontWeightSemibold`, `line-height: 1.2`, `--colorBrandForeground1` |
| Label | `--fontSizeBase300`, `--colorNeutralForeground3` |
| Grid | `4 columns`, `gap: var(--spacingL)` |

### 7.12 Testimonial Card

Extends `fluent-card`. Flex column.

| Element | Style |
|---------|-------|
| Quote | `--fontSizeBase300`, `line-height: 1.65`, `--colorNeutralForeground2`, `flex: 1` |
| Quote `::before` | `\201C` curly quote, `48px`, `--colorBrandForeground1`, `opacity: 0.3` |
| Author row | Flex, `gap: var(--spacingM)` |
| Avatar | `36x36`, `--borderRadiusCircular`, `--colorBrandBackground` bg, `white` text, `--fontSizeBase200`, `--fontWeightSemibold` |
| Name | `--fontSizeBase300`, `--fontWeightSemibold`, `--colorNeutralForeground1` |
| Title | `--fontSizeBase200`, `--colorNeutralForeground4` |
| Grid | `3 columns`, `gap: var(--spacingL)`, `margin-top: 48px` |

### 7.13 Pricing Card

Extends `fluent-card`. Flex column.

| Element | Style |
|---------|-------|
| Plan name | `--fontSizeBase300`, `--fontWeightSemibold`, `--colorNeutralForeground2` |
| Price | `--fontSizeHero800`, `--fontWeightSemibold`, `--colorNeutralForeground1`, `--lineHeightHero800` |
| Price period | `--fontSizeBase300`, `--fontWeightRegular`, `--colorNeutralForeground3` |
| Description | `--fontSizeBase200`, `--colorNeutralForeground4`, bottom border `--colorNeutralStroke2` |
| Feature list | No bullets, `padding: 6px 0`, `--fontSizeBase300`, `--colorNeutralForeground2`, `gap: var(--spacingS)` |
| Feature check | `16x16` circle, `--colorStatusSuccessBackground1` bg, `1px solid rgba(14,112,14,0.15)` |
| Button | Full width, outline or primary variant |
| Grid | `3 columns`, `gap: var(--spacingL)`, `margin-top: 48px`, `align-items: start` |

**Featured Variant**: `--colorBrandStroke1` border, absolute-positioned badge:

```css
.pricing-card.featured .pricing-badge {
  position: absolute;
  top: -1px;
  left: 50%;
  transform: translateX(-50%) translateY(-50%);
  background: var(--colorBrandBackground);
  color: var(--colorNeutralForegroundOnBrand);
  font-size: var(--fontSizeBase100);
  font-weight: var(--fontWeightSemibold);
  padding: 2px 12px;
  border-radius: var(--borderRadiusCircular);
  text-transform: uppercase;
  letter-spacing: 0.04em;
}
```

### 7.14 FAQ Accordion

| Element | Style |
|---------|-------|
| Item border | `var(--strokeWidthThin) solid var(--colorNeutralStroke2)` (bottom) |
| Question button | Full width, `--fontSizeBase400`, `--fontWeightSemibold`, `space-between` flex, `padding: var(--spacingL) 0` |
| Question hover | `--colorBrandForeground1` text |
| Chevron | `20x20`, `--colorNeutralForeground3`, `font-size: 12px` |
| Chevron (open) | `transform: rotate(180deg)`, `var(--durationNormal) var(--curveDecelerateMid)` |
| Answer | `max-height: 0` → `200px`, `overflow: hidden`, `var(--durationSlow) var(--curveDecelerateMid)` |
| Answer text | `--fontSizeBase300`, `line-height: 1.65`, `--colorNeutralForeground3`, `padding-bottom: var(--spacingL)` |
| Behavior | Exclusive open (one at a time), `aria-expanded` toggled |

```js
document.querySelectorAll('.faq-question').forEach(btn => {
  btn.addEventListener('click', () => {
    const item = btn.parentElement;
    const isOpen = item.classList.contains('open');

    // Close all
    document.querySelectorAll('.faq-item.open').forEach(el => {
      el.classList.remove('open');
      el.querySelector('.faq-question').setAttribute('aria-expanded', 'false');
    });

    // Toggle clicked
    if (!isOpen) {
      item.classList.add('open');
      btn.setAttribute('aria-expanded', 'true');
    }
  });
});
```

### 7.15 CTA Section

| Property | Style |
|----------|-------|
| Background | `--colorBrandBackground` |
| Padding | `100px 0` |
| Overlay | `::before` with two white radial gradients (`rgba(255,255,255,0.08)` and `0.05`) |
| Title | `font-size: clamp(var(--fontSizeBase600), 3.5vw, var(--fontSizeHero900))`, `--fontWeightSemibold`, `--colorNeutralForegroundOnBrand` |
| Description | `--fontSizeBase400`, `rgba(255,255,255,0.8)` |
| Button | Inverted: `white` bg, `--colorBrandBackground` text, hover `rgba(255,255,255,0.9)` |

### 7.16 Footer

| Element | Style |
|---------|-------|
| Background | `--colorNeutralBackground1` |
| Border top | `var(--strokeWidthThin) solid var(--colorNeutralStroke2)` |
| Padding | `48px 0 32px` |
| Grid | `1.5fr repeat(4, 1fr)`, `gap: var(--spacingXXXL)` |
| Brand | `--fontSizeBase400`, `--fontWeightSemibold`, `--colorNeutralForeground1` |
| Brand description | `--fontSizeBase200`, `--colorNeutralForeground4`, `line-height: 1.5` |
| Column heading | `--fontSizeBase200`, `--fontWeightSemibold`, `--colorNeutralForeground3`, `uppercase`, `letter-spacing: 0.06em` |
| Column links | `--fontSizeBase200`, `--colorNeutralForeground3`, hover `--colorNeutralForeground1` |
| Bottom bar | `--colorNeutralStroke3` top border, flex `space-between` |
| Copyright | `--fontSizeBase100`, `--colorNeutralForeground4` |
| Legal links | `--fontSizeBase100`, `--colorNeutralForeground4`, `gap: var(--spacingL)` |

### 7.17 Theme Toggle

| Property | Style |
|----------|-------|
| Size | `32x32` |
| Radius | `--borderRadiusMedium` |
| Background | `--colorSubtleBackground` (transparent) |
| Text color | `--colorNeutralForeground2` |
| Icon size | `16px` |
| Hover | `--colorSubtleBackgroundHover` bg |
| Transition | `var(--durationFaster) var(--curveEasyEase)` |

Icon switching via CSS:

```css
.theme-toggle .icon-moon { display: none; }
[data-theme="dark"] .theme-toggle .icon-sun { display: none; }
[data-theme="dark"] .theme-toggle .icon-moon { display: block; }
```

```js
const toggle = document.getElementById('themeToggle');
const html = document.documentElement;

toggle.addEventListener('click', () => {
  const next = html.getAttribute('data-theme') === 'light' ? 'dark' : 'light';
  html.setAttribute('data-theme', next);
});
```

---

## 8. Layout

### App Shell

```
+------------------------------------------+
| Announcement Bar (brand bg, 12px text)   |
+------------------------------------------+
| Navbar (sticky, 48px, Acrylic material)  |
+------------------------------------------+
|  +------------------------------------+  |
|  | max-w-1200px, px-24px              |  |
|  |                                    |  |
|  |  Hero                              |  |
|  |  Social Proof                      |  |
|  |  Features                          |  |
|  |  Dashboard Preview                 |  |
|  |  Metrics                           |  |
|  |  Testimonials                      |  |
|  |  Pricing                           |  |
|  |  FAQ                               |  |
|  |  CTA                               |  |
|  |                                    |  |
|  +------------------------------------+  |
+------------------------------------------+
| Footer (multi-column grid, legal bar)    |
+------------------------------------------+
```

### Hero Layout

```
+-------------------------------------------+
| Content (55%)          | Visual (40%)      |
|                        |                   |
| [Badge pill]           | [Surface 1  ]     |
| Heading (Display)      |    [Surface 2]    |
| Description            | [Surface 3]       |
| [Primary] [Outline]    |                   |
|                        |                   |
+-------------------------------------------+
gap: 64px
@media (max-width: 1024px): stacks vertically, center-aligned
```

### Section Page Pattern

```
+--------------------------------------+
| Overline (12px, brand, uppercase)    |
| Section Title (clamp 24–28px)        |
| Description (16px, max-w 560px)      |
|                                      |
| Grid content (3 / 2 / 1 columns)    |
+--------------------------------------+
padding: 80px 0 (desktop), 56px 0 (tablet/mobile)
```

### Dashboard Frame

```
+----------------------------------------------+
| Titlebar: [● ● ●] [⌕ Search workflows...] [◉]|
+------+---------------------------------------+
| Rail | Main Grid (2 cols)                     |
| 48px | [Card: Active workflows] [Card: Tasks] |
|      | [Chart: Full-width bar chart         ] |
+------+---------------------------------------+
max-width: 960px, shadow28
@media (max-width: 768px): rail becomes horizontal top bar, grid → 1 column
```

---

## 9. Navigation

### Structure

```
+--------------------------------------------------------+
| Logo+Icon         Nav Links           [Toggle] [CTA]   |
+--------------------------------------------------------+
```

### Navbar Specs

| Property | Style |
|----------|-------|
| Height | `48px` |
| Position | `sticky top-0 z-1000` |
| Border | `border-bottom: var(--strokeWidthThin) solid var(--colorNeutralStroke2)` |
| Light bg | `rgba(255,255,255,0.72)` + `saturate(180%) blur(20px)` |
| Dark bg | `rgba(41,41,41,0.72)` + `saturate(180%) blur(20px)` |
| Max width | `1200px`, `padding: 0 var(--spacingXXL)` |

### Brand Lockup

```css
font-size: var(--fontSizeBase400);   /* 16px */
font-weight: var(--fontWeightSemibold);
color: var(--colorNeutralForeground1);
gap: var(--spacingS);
/* SVG icon: 20x20, four rounded rects at decreasing opacity */
```

### Nav Link States

| State | Text | Background |
|-------|------|-----------|
| Default | `--colorNeutralForeground2` | `transparent` |
| Hover | `--colorNeutralForeground1` | `--colorSubtleBackgroundHover` |

Links: `padding: 6px 10px`, `border-radius: var(--borderRadiusMedium)`, `font-size: var(--fontSizeBase300)`, `font-weight: var(--fontWeightRegular)`, `transition: var(--durationFaster) var(--curveEasyEase)`.

### CTA Button

Primary button in navbar right area. Default size (32px).

### Theme Toggle

Ghost icon button, `32x32`, sun/moon swap. See Section 7.17.

### Mobile Toggle

Hamburger: 3x `18x2px` bars, `--colorNeutralForeground2`, transitions for rotation. Shows at `768px` breakpoint. Opens dropdown: `--colorNeutralBackground1` bg, `--shadow8`, `padding: var(--spacingS) var(--spacingXXL)`.

---

## 10. Utility Classes

### `fluent-card`

Card container with Reveal Highlight and elevation hover.

```css
.fluent-card {
  position: relative;
  background: var(--colorNeutralBackground1);
  border: var(--strokeWidthThin) solid var(--colorNeutralStroke2);
  border-radius: var(--borderRadiusXLarge);
  box-shadow: var(--shadow2);
  padding: var(--spacingXXL);
  transition: box-shadow var(--durationNormal) var(--curveEasyEase),
              border-color var(--durationNormal) var(--curveEasyEase),
              background-color var(--durationSlower) var(--curveEasyEase);
  overflow: hidden;
}

.fluent-card:hover {
  box-shadow: var(--shadow8);
  border-color: var(--colorNeutralStroke1);
}
```

### `section-overline`

Brand-colored uppercase micro-label for section headers.

```css
.section-overline {
  font-size: var(--fontSizeBase200);
  font-weight: var(--fontWeightSemibold);
  color: var(--colorBrandForeground1);
  text-transform: uppercase;
  letter-spacing: 0.06em;
  margin-bottom: var(--spacingS);
}
```

### `section-title`

Responsive clamped section heading.

```css
.section-title {
  font-size: clamp(var(--fontSizeBase600), 3vw, var(--fontSizeHero700));
  font-weight: var(--fontWeightSemibold);
  line-height: var(--lineHeightHero700);
  color: var(--colorNeutralForeground1);
  margin-bottom: var(--spacingS);
}
```

### `section-description`

Muted body text for section intros.

```css
.section-description {
  font-size: var(--fontSizeBase400);
  line-height: var(--lineHeightBase400);
  color: var(--colorNeutralForeground3);
  margin-bottom: 48px;
  max-width: 560px;
}
```

### `reveal`

Scroll-reveal entrance animation (fade-up).

```css
.reveal {
  opacity: 0;
  transform: translateY(20px);
  transition: opacity var(--durationSlower) var(--curveDecelerateMid),
              transform var(--durationSlower) var(--curveDecelerateMid);
}

.reveal.visible {
  opacity: 1;
  transform: translateY(0);
}
```

Triggered by IntersectionObserver:

```js
const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.classList.add('visible');
    }
  });
}, { threshold: 0.1, rootMargin: '0px 0px -40px 0px' });

document.querySelectorAll('.reveal').forEach(el => observer.observe(el));
```

### `reveal-card`

Mouse-tracking Reveal Highlight effect. Applies via `mousemove` handler setting `--reveal-x` and `--reveal-y` CSS properties. See Section 7.2 for implementation.

---

## 11. Accessibility

- **Skip link**: Not present in prototype — recommend adding `<a href="#main-content">Skip to main content</a>` with `sr-only` + focus-visible styling for production.
- **Theme toggle**: `aria-label="Toggle theme"`.
- **Mobile toggle**: `aria-label="Menu"`.
- **FAQ accordion**: `aria-expanded` toggled on each question button. Exclusive open behavior (one at a time).
- **Hero visual**: `aria-hidden="true"` on the decorative floating surfaces.
- **Accessible strokes**: `--colorNeutralStrokeAccessible` provides WCAG AA-compliant stroke colors in both themes (`#616161` light, `#adadad` dark).
- **Color contrast**: Fluent 2 tokens are designed for WCAG AA compliance. Primary text (`--colorNeutralForeground1`) meets AA against the page background in both themes.
- **Reduced motion**: Recommend adding for production:

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
  .reveal { opacity: 1; transform: none; }
}
```

---

## 12. Icons

**Library**: Inline SVGs (no external icon library). Icons use consistent `20x20` viewBox with `stroke-width: 1.5` and `currentColor`.

| Context | Size | Stroke Width | Type |
|---------|------|-------------|------|
| Feature card icons | `18px` in `20x20` viewBox | `1.5` | Stroke-based SVG |
| Navbar logo | `20x20` | — | Filled rects at decreasing opacity |
| Theme toggle | `16px` | — | Unicode characters (&#9788; / &#9790;) |
| FAQ chevron | `20x20` container | — | Unicode `▼` at `12px` |
| Mobile hamburger | `18x2px` bars | — | CSS bars |
| Nav rail items | `14px` | — | Unicode shapes (&#9632; &#9650; &#9679; &#9670;) |

> For production, recommend adopting `@fluentui/react-icons` for the React ecosystem or `lucide-react` for a lighter alternative.

---

## 13. Motion System

> **Fluent 2 reference**: Duration and easing tokens follow Microsoft's [Fluent 2 Motion](https://fluent2.microsoft.design/motion) guidance. The decelerate/accelerate curve pairs map to Fluent 2's entrance/exit motion model.

### Duration Tokens — 8-Step

| Token | Value | Usage |
|-------|-------|-------|
| `--durationUltraFast` | `50ms` | (Reserved) |
| `--durationFaster` | `100ms` | Nav link hover, theme toggle hover, footer link hover |
| `--durationFast` | `150ms` | Button transitions (bg, border, color, shadow) |
| `--durationNormal` | `200ms` | Card reveal highlight, chevron rotation, navbar scroll shadow |
| `--durationGentle` | `250ms` | (Reserved) |
| `--durationSlow` | `300ms` | FAQ answer expand/collapse, chart bar height |
| `--durationSlower` | `400ms` | Theme transitions (body bg, all surfaces, borders), scroll-reveal entrance |
| `--durationUltraSlow` | `500ms` | (Reserved) |

### Easing Curves — 8 Curves

| Token | Value | Usage |
|-------|-------|-------|
| `--curveDecelerateMax` | `cubic-bezier(0.1, 0.9, 0.2, 1)` | (Reserved for dramatic entrances) |
| `--curveDecelerateMid` | `cubic-bezier(0, 0, 0, 1)` | Scroll-reveal entrance, FAQ accordion, chevron rotation |
| `--curveDecelerateMin` | `cubic-bezier(0.33, 0, 0.1, 1)` | (Reserved) |
| `--curveAccelerateMax` | `cubic-bezier(1, 0, 1, 1)` | (Reserved for dramatic exits) |
| `--curveAccelerateMid` | `cubic-bezier(0.7, 0, 1, 0.5)` | (Reserved) |
| `--curveAccelerateMin` | `cubic-bezier(0.8, 0, 0.78, 1)` | (Reserved) |
| `--curveEasyEase` | `cubic-bezier(0.33, 0, 0.67, 1)` | Most UI transitions (buttons, cards, theme, navbar, surfaces) |
| `--curveEasyEaseMax` | `cubic-bezier(0.8, 0, 0.2, 1)` | Hero floating surface animations |

### Curve Usage Guide

| Transition Type | Recommended Curve | Duration |
|----------------|-------------------|----------|
| Hover states (buttons, links) | `--curveEasyEase` | `--durationFast` or `--durationFaster` |
| Card elevation / reveal | `--curveEasyEase` | `--durationNormal` |
| Content entrance (scroll reveal) | `--curveDecelerateMid` | `--durationSlower` |
| Expand/collapse (accordion) | `--curveDecelerateMid` | `--durationSlow` |
| Theme switching (global) | `--curveEasyEase` | `--durationSlower` |
| Ambient loops (hero floats) | `--curveEasyEase` | `6–8s infinite` |

---

## 14. Tooling Reference

### Standalone (No Build Tools)

KolFluent is implemented as a single HTML file with embedded `<style>` and `<script>`. No build pipeline required.

| Concern | Approach |
|---------|----------|
| Theming | Native CSS custom properties, `data-theme` attribute |
| Animations | CSS `@keyframes` + `transition` properties |
| Scroll reveal | `IntersectionObserver` API |
| Reveal highlight | `mousemove` event + CSS custom properties |
| Theme toggle | Vanilla JS toggling `data-theme` attribute |
| FAQ accordion | Vanilla JS class toggling + `aria-expanded` |

### Production (Framework)

For a production implementation, the design system maps directly to:

| Tool | Role |
|------|------|
| **Fluent UI React v9** (`@fluentui/react-components`) | Component library with built-in tokens via `FluentProvider` + `webLightTheme` / `webDarkTheme` |
| **@fluentui/tokens** | Standalone token package if not using Fluent UI React |
| **@fluentui/react-icons** | Icon library with Fluent design language |
| **React 19** | UI framework |
| **TypeScript** | Type safety across tokens and component props |
| **Vite** | Dev server and bundler |

### Token Mapping to Fluent UI React v9

The CSS custom property names used in KolFluent match the Fluent UI React v9 theme token names exactly (camelCase → CSS kebab-case). For example:

| KolFluent CSS Property | Fluent UI React v9 Token |
|----------------------|-------------------------|
| `--colorBrandBackground` | `tokens.colorBrandBackground` |
| `--colorNeutralForeground1` | `tokens.colorNeutralForeground1` |
| `--fontSizeBase300` | `tokens.fontSizeBase300` |
| `--shadow8` | `tokens.shadow8` |

---

## 15. Quick-Start Token Block

Drop this into a new project's CSS to bootstrap either theme.

### KolFluent (Light)

```css
:root {
  /* Brand */
  --colorBrandBackground: #0f6cbd;
  --colorBrandBackgroundHover: #115ea3;
  --colorBrandBackgroundPressed: #0c3b5e;
  --colorBrandBackgroundSelected: #115ea3;
  --colorBrandBackground2: #ebf3fc;
  --colorBrandBackground2Hover: #b4d6fa;
  --colorBrandForeground1: #0f6cbd;
  --colorBrandForeground2: #115ea3;
  --colorBrandForegroundLink: #115ea3;
  --colorBrandForegroundLinkHover: #0f548c;
  --colorBrandStroke1: #0f6cbd;

  /* Neutral Backgrounds */
  --colorNeutralBackground1: #ffffff;
  --colorNeutralBackground1Hover: #f5f5f5;
  --colorNeutralBackground1Pressed: #e0e0e0;
  --colorNeutralBackground2: #fafafa;
  --colorNeutralBackground3: #f5f5f5;
  --colorNeutralBackground4: #f0f0f0;
  --colorNeutralBackground5: #ebebeb;
  --colorNeutralBackground6: #e0e0e0;

  /* Neutral Foregrounds */
  --colorNeutralForeground1: #242424;
  --colorNeutralForeground2: #424242;
  --colorNeutralForeground3: #616161;
  --colorNeutralForeground4: #707070;
  --colorNeutralForegroundDisabled: #bdbdbd;
  --colorNeutralForegroundOnBrand: #ffffff;

  /* Neutral Strokes */
  --colorNeutralStroke1: #d1d1d1;
  --colorNeutralStroke2: #e0e0e0;
  --colorNeutralStroke3: #f0f0f0;
  --colorNeutralStrokeAccessible: #616161;

  /* Subtle */
  --colorSubtleBackground: transparent;
  --colorSubtleBackgroundHover: #f5f5f5;
  --colorSubtleBackgroundPressed: #e0e0e0;

  /* Compound Brand */
  --colorCompoundBrandBackground: #0f6cbd;
  --colorCompoundBrandBackgroundHover: #115ea3;
  --colorCompoundBrandStroke: #0f6cbd;

  /* Status */
  --colorStatusSuccessBackground1: #f1faf1;
  --colorStatusSuccessForeground1: #0e700e;
  --colorStatusWarningBackground1: #fff9f5;
  --colorStatusWarningForeground1: #bc4b09;

  /* Font Family */
  --fontFamilyBase: 'Segoe UI Variable', 'Segoe UI', system-ui, -apple-system, BlinkMacSystemFont, sans-serif;
  --fontFamilyMonospace: Consolas, 'Courier New', Courier, monospace;

  /* Font Sizes — Fluent 2 Type Ramp */
  --fontSizeBase100: 10px;
  --fontSizeBase200: 12px;
  --fontSizeBase300: 14px;
  --fontSizeBase400: 16px;
  --fontSizeBase500: 20px;
  --fontSizeBase600: 24px;
  --fontSizeHero700: 28px;
  --fontSizeHero800: 32px;
  --fontSizeHero900: 40px;
  --fontSizeHero1000: 68px;

  /* Font Weights */
  --fontWeightRegular: 400;
  --fontWeightMedium: 500;
  --fontWeightSemibold: 600;
  --fontWeightBold: 700;

  /* Line Heights */
  --lineHeightBase100: 14px;
  --lineHeightBase200: 16px;
  --lineHeightBase300: 20px;
  --lineHeightBase400: 22px;
  --lineHeightBase500: 26px;
  --lineHeightBase600: 32px;
  --lineHeightHero700: 36px;
  --lineHeightHero800: 40px;
  --lineHeightHero900: 52px;
  --lineHeightHero1000: 92px;

  /* Border Radius */
  --borderRadiusNone: 0;
  --borderRadiusSmall: 2px;
  --borderRadiusMedium: 4px;
  --borderRadiusLarge: 6px;
  --borderRadiusXLarge: 8px;
  --borderRadiusCircular: 10000px;

  /* Spacing */
  --spacingXXS: 2px;
  --spacingXS: 4px;
  --spacingSNudge: 6px;
  --spacingS: 8px;
  --spacingMNudge: 10px;
  --spacingM: 12px;
  --spacingL: 16px;
  --spacingXL: 20px;
  --spacingXXL: 24px;
  --spacingXXXL: 32px;

  /* Stroke Widths */
  --strokeWidthThin: 1px;
  --strokeWidthThick: 2px;

  /* Shadows */
  --shadow2: 0px 1px 2px rgba(0,0,0,0.14), 0px 0px 2px rgba(0,0,0,0.12);
  --shadow4: 0px 2px 4px rgba(0,0,0,0.14), 0px 0px 2px rgba(0,0,0,0.12);
  --shadow8: 0px 4px 8px rgba(0,0,0,0.14), 0px 0px 2px rgba(0,0,0,0.12);
  --shadow16: 0px 8px 16px rgba(0,0,0,0.14), 0px 0px 2px rgba(0,0,0,0.12);
  --shadow28: 0px 14px 28px rgba(0,0,0,0.14), 0px 0px 8px rgba(0,0,0,0.12);
  --shadow64: 0px 32px 64px rgba(0,0,0,0.14), 0px 0px 8px rgba(0,0,0,0.12);

  /* Motion — Duration */
  --durationUltraFast: 50ms;
  --durationFaster: 100ms;
  --durationFast: 150ms;
  --durationNormal: 200ms;
  --durationGentle: 250ms;
  --durationSlow: 300ms;
  --durationSlower: 400ms;
  --durationUltraSlow: 500ms;

  /* Motion — Easing Curves */
  --curveDecelerateMax: cubic-bezier(0.1, 0.9, 0.2, 1);
  --curveDecelerateMid: cubic-bezier(0, 0, 0, 1);
  --curveDecelerateMin: cubic-bezier(0.33, 0, 0.1, 1);
  --curveAccelerateMax: cubic-bezier(1, 0, 1, 1);
  --curveAccelerateMid: cubic-bezier(0.7, 0, 1, 0.5);
  --curveAccelerateMin: cubic-bezier(0.8, 0, 0.78, 1);
  --curveEasyEase: cubic-bezier(0.33, 0, 0.67, 1);
  --curveEasyEaseMax: cubic-bezier(0.8, 0, 0.2, 1);
}
```

### KolFluent Dark

```css
:root {
  color-scheme: dark;

  /* Font Family */
  --fontFamilyBase: 'Segoe UI Variable', 'Segoe UI', system-ui, -apple-system, BlinkMacSystemFont, sans-serif;
  --fontFamilyMonospace: Consolas, 'Courier New', Courier, monospace;

  /* Brand */
  --colorBrandBackground: #115ea3;
  --colorBrandBackgroundHover: #0f6cbd;
  --colorBrandBackgroundPressed: #0f548c;
  --colorBrandBackground2: #0a2e4a;
  --colorBrandForeground1: #479ef5;
  --colorBrandForeground2: #62abf5;
  --colorBrandForegroundLink: #479ef5;
  --colorBrandForegroundLinkHover: #77bcf8;
  --colorBrandStroke1: #479ef5;

  /* Neutral Backgrounds */
  --colorNeutralBackground1: #292929;
  --colorNeutralBackground1Hover: #3d3d3d;
  --colorNeutralBackground2: #1f1f1f;
  --colorNeutralBackground3: #141414;
  --colorNeutralBackground4: #0f0f0f;
  --colorNeutralBackground5: #0a0a0a;
  --colorNeutralBackground6: #333333;

  /* Neutral Foregrounds */
  --colorNeutralForeground1: #ffffff;
  --colorNeutralForeground2: #d6d6d6;
  --colorNeutralForeground3: #adadad;
  --colorNeutralForeground4: #999999;
  --colorNeutralForegroundDisabled: #5c5c5c;
  --colorNeutralForegroundOnBrand: #ffffff;

  /* Neutral Strokes */
  --colorNeutralStroke1: #666666;
  --colorNeutralStroke2: #525252;
  --colorNeutralStroke3: #3d3d3d;
  --colorNeutralStrokeAccessible: #adadad;

  /* Subtle */
  --colorSubtleBackground: transparent;
  --colorSubtleBackgroundHover: #383838;
  --colorSubtleBackgroundPressed: #2e2e2e;

  /* Compound Brand */
  --colorCompoundBrandBackground: #479ef5;
  --colorCompoundBrandBackgroundHover: #62abf5;
  --colorCompoundBrandStroke: #479ef5;

  /* Status (inherited from light — override here for production) */
  --colorStatusSuccessBackground1: #f1faf1;
  --colorStatusSuccessForeground1: #0e700e;
  --colorStatusWarningBackground1: #fff9f5;
  --colorStatusWarningForeground1: #bc4b09;

  /* Font Sizes — Fluent 2 Type Ramp */
  --fontSizeBase100: 10px;
  --fontSizeBase200: 12px;
  --fontSizeBase300: 14px;
  --fontSizeBase400: 16px;
  --fontSizeBase500: 20px;
  --fontSizeBase600: 24px;
  --fontSizeHero700: 28px;
  --fontSizeHero800: 32px;
  --fontSizeHero900: 40px;
  --fontSizeHero1000: 68px;

  /* Font Weights */
  --fontWeightRegular: 400;
  --fontWeightMedium: 500;
  --fontWeightSemibold: 600;
  --fontWeightBold: 700;

  /* Line Heights */
  --lineHeightBase100: 14px;
  --lineHeightBase200: 16px;
  --lineHeightBase300: 20px;
  --lineHeightBase400: 22px;
  --lineHeightBase500: 26px;
  --lineHeightBase600: 32px;
  --lineHeightHero700: 36px;
  --lineHeightHero800: 40px;
  --lineHeightHero900: 52px;
  --lineHeightHero1000: 92px;

  /* Border Radius */
  --borderRadiusNone: 0;
  --borderRadiusSmall: 2px;
  --borderRadiusMedium: 4px;
  --borderRadiusLarge: 6px;
  --borderRadiusXLarge: 8px;
  --borderRadiusCircular: 10000px;

  /* Spacing */
  --spacingXXS: 2px;
  --spacingXS: 4px;
  --spacingSNudge: 6px;
  --spacingS: 8px;
  --spacingMNudge: 10px;
  --spacingM: 12px;
  --spacingL: 16px;
  --spacingXL: 20px;
  --spacingXXL: 24px;
  --spacingXXXL: 32px;

  /* Stroke Widths */
  --strokeWidthThin: 1px;
  --strokeWidthThick: 2px;

  /* Shadows */
  --shadow2: 0px 1px 2px rgba(0,0,0,0.48), 0px 0px 2px rgba(0,0,0,0.24);
  --shadow4: 0px 2px 4px rgba(0,0,0,0.48), 0px 0px 2px rgba(0,0,0,0.24);
  --shadow8: 0px 4px 8px rgba(0,0,0,0.48), 0px 0px 2px rgba(0,0,0,0.24);
  --shadow16: 0px 8px 16px rgba(0,0,0,0.48), 0px 0px 2px rgba(0,0,0,0.24);
  --shadow28: 0px 14px 28px rgba(0,0,0,0.48), 0px 0px 8px rgba(0,0,0,0.24);
  --shadow64: 0px 32px 64px rgba(0,0,0,0.48), 0px 0px 8px rgba(0,0,0,0.24);

  /* Motion — Duration */
  --durationUltraFast: 50ms;
  --durationFaster: 100ms;
  --durationFast: 150ms;
  --durationNormal: 200ms;
  --durationGentle: 250ms;
  --durationSlow: 300ms;
  --durationSlower: 400ms;
  --durationUltraSlow: 500ms;

  /* Motion — Easing Curves */
  --curveDecelerateMax: cubic-bezier(0.1, 0.9, 0.2, 1);
  --curveDecelerateMid: cubic-bezier(0, 0, 0, 1);
  --curveDecelerateMin: cubic-bezier(0.33, 0, 0.1, 1);
  --curveAccelerateMax: cubic-bezier(1, 0, 1, 1);
  --curveAccelerateMid: cubic-bezier(0.7, 0, 1, 0.5);
  --curveAccelerateMin: cubic-bezier(0.8, 0, 0.78, 1);
  --curveEasyEase: cubic-bezier(0.33, 0, 0.67, 1);
  --curveEasyEaseMax: cubic-bezier(0.8, 0, 0.2, 1);
}
```

### Both Themes via `prefers-color-scheme`

> **Note**: The source implementation uses `[data-theme="dark"]` on the `<html>` element, toggled by JavaScript. This `prefers-color-scheme` approach is provided as an alternative for projects that prefer automatic OS-level theme switching.

```css
:root {
  /* Font Family */
  --fontFamilyBase: 'Segoe UI Variable', 'Segoe UI', system-ui, -apple-system, BlinkMacSystemFont, sans-serif;
  --fontFamilyMonospace: Consolas, 'Courier New', Courier, monospace;

  /* Font Sizes */
  --fontSizeBase100: 10px;
  --fontSizeBase200: 12px;
  --fontSizeBase300: 14px;
  --fontSizeBase400: 16px;
  --fontSizeBase500: 20px;
  --fontSizeBase600: 24px;
  --fontSizeHero700: 28px;
  --fontSizeHero800: 32px;
  --fontSizeHero900: 40px;
  --fontSizeHero1000: 68px;

  /* Font Weights */
  --fontWeightRegular: 400;
  --fontWeightMedium: 500;
  --fontWeightSemibold: 600;
  --fontWeightBold: 700;

  /* Line Heights */
  --lineHeightBase100: 14px;
  --lineHeightBase200: 16px;
  --lineHeightBase300: 20px;
  --lineHeightBase400: 22px;
  --lineHeightBase500: 26px;
  --lineHeightBase600: 32px;
  --lineHeightHero700: 36px;
  --lineHeightHero800: 40px;
  --lineHeightHero900: 52px;
  --lineHeightHero1000: 92px;

  /* Border Radius */
  --borderRadiusNone: 0;
  --borderRadiusSmall: 2px;
  --borderRadiusMedium: 4px;
  --borderRadiusLarge: 6px;
  --borderRadiusXLarge: 8px;
  --borderRadiusCircular: 10000px;

  /* Spacing */
  --spacingXXS: 2px;
  --spacingXS: 4px;
  --spacingSNudge: 6px;
  --spacingS: 8px;
  --spacingMNudge: 10px;
  --spacingM: 12px;
  --spacingL: 16px;
  --spacingXL: 20px;
  --spacingXXL: 24px;
  --spacingXXXL: 32px;

  /* Stroke Widths */
  --strokeWidthThin: 1px;
  --strokeWidthThick: 2px;

  /* Motion — Duration */
  --durationUltraFast: 50ms;
  --durationFaster: 100ms;
  --durationFast: 150ms;
  --durationNormal: 200ms;
  --durationGentle: 250ms;
  --durationSlow: 300ms;
  --durationSlower: 400ms;
  --durationUltraSlow: 500ms;

  /* Motion — Easing Curves */
  --curveDecelerateMax: cubic-bezier(0.1, 0.9, 0.2, 1);
  --curveDecelerateMid: cubic-bezier(0, 0, 0, 1);
  --curveDecelerateMin: cubic-bezier(0.33, 0, 0.1, 1);
  --curveAccelerateMax: cubic-bezier(1, 0, 1, 1);
  --curveAccelerateMid: cubic-bezier(0.7, 0, 1, 0.5);
  --curveAccelerateMin: cubic-bezier(0.8, 0, 0.78, 1);
  --curveEasyEase: cubic-bezier(0.33, 0, 0.67, 1);
  --curveEasyEaseMax: cubic-bezier(0.8, 0, 0.2, 1);

  /* Light (default) */
  --colorBrandBackground: #0f6cbd;
  --colorBrandBackgroundHover: #115ea3;
  --colorBrandBackgroundPressed: #0c3b5e;
  --colorBrandBackgroundSelected: #115ea3;
  --colorBrandBackground2: #ebf3fc;
  --colorBrandBackground2Hover: #b4d6fa;
  --colorBrandForeground1: #0f6cbd;
  --colorBrandForeground2: #115ea3;
  --colorBrandForegroundLink: #115ea3;
  --colorBrandForegroundLinkHover: #0f548c;
  --colorBrandStroke1: #0f6cbd;

  --colorNeutralBackground1: #ffffff;
  --colorNeutralBackground1Hover: #f5f5f5;
  --colorNeutralBackground1Pressed: #e0e0e0;
  --colorNeutralBackground2: #fafafa;
  --colorNeutralBackground3: #f5f5f5;
  --colorNeutralBackground4: #f0f0f0;
  --colorNeutralBackground5: #ebebeb;
  --colorNeutralBackground6: #e0e0e0;

  --colorNeutralForeground1: #242424;
  --colorNeutralForeground2: #424242;
  --colorNeutralForeground3: #616161;
  --colorNeutralForeground4: #707070;
  --colorNeutralForegroundDisabled: #bdbdbd;
  --colorNeutralForegroundOnBrand: #ffffff;

  --colorNeutralStroke1: #d1d1d1;
  --colorNeutralStroke2: #e0e0e0;
  --colorNeutralStroke3: #f0f0f0;
  --colorNeutralStrokeAccessible: #616161;

  --colorSubtleBackground: transparent;
  --colorSubtleBackgroundHover: #f5f5f5;
  --colorSubtleBackgroundPressed: #e0e0e0;

  --colorCompoundBrandBackground: #0f6cbd;
  --colorCompoundBrandBackgroundHover: #115ea3;
  --colorCompoundBrandStroke: #0f6cbd;

  --colorStatusSuccessBackground1: #f1faf1;
  --colorStatusSuccessForeground1: #0e700e;
  --colorStatusWarningBackground1: #fff9f5;
  --colorStatusWarningForeground1: #bc4b09;

  --shadow2: 0px 1px 2px rgba(0,0,0,0.14), 0px 0px 2px rgba(0,0,0,0.12);
  --shadow4: 0px 2px 4px rgba(0,0,0,0.14), 0px 0px 2px rgba(0,0,0,0.12);
  --shadow8: 0px 4px 8px rgba(0,0,0,0.14), 0px 0px 2px rgba(0,0,0,0.12);
  --shadow16: 0px 8px 16px rgba(0,0,0,0.14), 0px 0px 2px rgba(0,0,0,0.12);
  --shadow28: 0px 14px 28px rgba(0,0,0,0.14), 0px 0px 8px rgba(0,0,0,0.12);
  --shadow64: 0px 32px 64px rgba(0,0,0,0.14), 0px 0px 8px rgba(0,0,0,0.12);
}

@media (prefers-color-scheme: dark) {
  :root {
    color-scheme: dark;

    --colorBrandBackground: #115ea3;
    --colorBrandBackgroundHover: #0f6cbd;
    --colorBrandBackgroundPressed: #0f548c;
    --colorBrandBackground2: #0a2e4a;
    --colorBrandForeground1: #479ef5;
    --colorBrandForeground2: #62abf5;
    --colorBrandForegroundLink: #479ef5;
    --colorBrandForegroundLinkHover: #77bcf8;
    --colorBrandStroke1: #479ef5;

    --colorNeutralBackground1: #292929;
    --colorNeutralBackground1Hover: #3d3d3d;
    --colorNeutralBackground2: #1f1f1f;
    --colorNeutralBackground3: #141414;
    --colorNeutralBackground4: #0f0f0f;
    --colorNeutralBackground5: #0a0a0a;
    --colorNeutralBackground6: #333333;

    --colorNeutralForeground1: #ffffff;
    --colorNeutralForeground2: #d6d6d6;
    --colorNeutralForeground3: #adadad;
    --colorNeutralForeground4: #999999;
    --colorNeutralForegroundDisabled: #5c5c5c;

    --colorNeutralStroke1: #666666;
    --colorNeutralStroke2: #525252;
    --colorNeutralStroke3: #3d3d3d;
    --colorNeutralStrokeAccessible: #adadad;

    --colorSubtleBackgroundHover: #383838;
    --colorSubtleBackgroundPressed: #2e2e2e;

    --colorCompoundBrandBackground: #479ef5;
    --colorCompoundBrandBackgroundHover: #62abf5;
    --colorCompoundBrandStroke: #479ef5;

    --shadow2: 0px 1px 2px rgba(0,0,0,0.48), 0px 0px 2px rgba(0,0,0,0.24);
    --shadow4: 0px 2px 4px rgba(0,0,0,0.48), 0px 0px 2px rgba(0,0,0,0.24);
    --shadow8: 0px 4px 8px rgba(0,0,0,0.48), 0px 0px 2px rgba(0,0,0,0.24);
    --shadow16: 0px 8px 16px rgba(0,0,0,0.48), 0px 0px 2px rgba(0,0,0,0.24);
    --shadow28: 0px 14px 28px rgba(0,0,0,0.48), 0px 0px 8px rgba(0,0,0,0.24);
    --shadow64: 0px 32px 64px rgba(0,0,0,0.48), 0px 0px 8px rgba(0,0,0,0.24);
  }
}
```

---

## 16. Responsive Breakpoints

| Breakpoint | Changes |
|-----------|---------|
| `≤ 1024px` | Hero stacks vertically (center-aligned). Features grid: 3 → 2 columns. Testimonials: 3 → 2 columns. Footer grid: 5 → 3 columns (brand spans full width). |
| `≤ 768px` | Nav links hidden, mobile hamburger toggle shown. Hero padding: 100px → 72px top. Section padding: 80px → 56px. Features: 2 → 1 column. Metrics: 4 → 2 columns. Pricing: 3 → 1 column (max-width 400px, centered). Testimonials: 2 → 1 column. Dashboard: nav rail becomes horizontal top bar, main grid → 1 column. Footer: 3 → 2 columns. |
| `≤ 480px` | Container padding: 24px → 16px. Hero h1 capped at `--fontSizeHero700` (28px). Hero surfaces shrink proportionally. Metrics: 2 → 1 column. Footer: 2 → 1 column. Footer bottom: stacks vertically, center-aligned. Social proof logo gap: 40px → 20px. |

---

## 17. Origins

KolFluent was extracted from a Fluent 2 Design System showcase — a "Flowstate" product landing page built as a self-contained HTML file during a multi-direction design exploration. The design system implements authentic Microsoft Fluent Design System 2 tokens, materials (Acrylic translucency, Mica-inspired gradients), and interaction patterns (Reveal Highlight, elevation-based depth system). It demonstrates how Fluent 2 can be used outside the Microsoft/Fluent UI React ecosystem using pure CSS custom properties and vanilla JavaScript.
