---
name: ocean-glass-ui
description: Apply the OceanAvenu dark glass UI design system to any React + Ant Design project. Use when user asks for dark glass theme, transparent panels, or wants to match the OceanAvenu aesthetic.
---

# OceanAvenu Dark Glass UI

Apply this glass-morphism design system to React projects using Ant Design 6.

## Quick Start

### Step 1: Background Image

Place the background image as `src/OceanAvenu.jpg`. Then:

```css
html, body, #root {
  min-height: 100vh;
  background-image: url('./OceanAvenu.jpg');
  background-size: cover;
  background-position: center;
  background-attachment: fixed;
}
```

### Step 2: Ant Design Theme Tokens

In `App.tsx` ConfigProvider:

```tsx
const themeConfig = {
  algorithm: theme.darkAlgorithm,
  token: {
    colorPrimary: '#78bbff',
    borderRadius: 12,
    colorBgContainer: 'rgba(7, 8, 10, 0.12)',
    colorBgElevated: 'rgba(7, 8, 10, 0.12)',
    colorBgLayout: 'transparent',
    colorBgMask: 'rgba(0, 0, 0, 0.45)',
    colorText: 'rgba(235, 237, 240, 0.98)',
    colorTextSecondary: 'rgba(178, 185, 194, 0.92)',
    colorBorder: 'rgba(119, 128, 140, 0.25)',
    fontFamily: "'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif",
  },
};
```

### Step 3: Global CSS

Reference: `DESIGN_SYSTEM.md` for the complete CSS. Key overrides needed:

**Layout** — Make `.ant-layout` transparent. Set dark glass backgrounds on `.ant-layout-sider` and `.ant-layout-header`.

**Cards** — `background: rgba(7,8,10,0.12)`, `backdrop-filter: blur(40px)`, `border: 1px solid rgba(255,255,255,0.08)`, `border-radius: 20px`.

**Drawer/Modal** — Target `.ant-drawer-section` and `.ant-modal-content` (NOT `.ant-drawer-pure` — check actual DOM). Use `rgba(7,8,10,0.12)` for uniform glass.

**Inputs** — `.ant-input-affix-wrapper` outer frame: `border: rgba(255,255,255,0.12)`. Inner `.ant-input`: transparent bg, `border: none`.

**Tables** — Transparent background, header cells: `rgba(7,8,10,0.12)`.

**Tabs** — `.ant-tabs-ink-bar`: `rgba(120,187,255,0.35)`, `border-radius: 4px`. `.ant-tabs-tab-active`: `rgba(120,187,255,0.08)`, `border-radius: 16px`.

## Design Tokens

| Token | Value | Usage |
|-------|-------|-------|
| `--bg-base` | `#07080a` | Page background |
| Glass panels | `rgba(7,8,10,0.12)` | Cards, sidebars, drawers, modals |
| Glass inputs | `rgba(7,8,10,0.08)` | Input fields |
| Accent | `#78bbff` | Primary buttons, links, focus |
| Text primary | `rgba(255,255,255,0.92)` | Headings, body |
| Text secondary | `rgba(255,255,255,0.6)` | Labels, hints |
| Border glass | `rgba(255,255,255,0.08)` | Panel borders |
| Border input | `rgba(255,255,255,0.06)` | Input borders (subtle) |
| Radius panel | `20px` | Cards, modals |
| Radius input | `12px` | Buttons, inputs |
| Shadow | `0 4px 20px rgba(0,0,0,0.3)` | Elevated panels |

## Critical Gotchas

1. **Class names**: Always verify actual DOM class names in browser DevTools. Ant Design 6 CSS-in-JS class names may differ from docs.

2. **Use `!important`**: Ant Design CSS-in-JS injects styles at runtime with unpredictable order. Always use `!important`.

3. **`backdrop-filter` needs `-webkit-` prefix**: Always write both lines.

4. **Don't use `filter: drop-shadow()`**: It breaks `backdrop-filter`. Use `box-shadow` with `border-radius` for rounded shadows.

5. **`colorBgElevated` is key**: This token controls Drawer/Modal/Picker panel backgrounds. Setting it transparent in ConfigProvider eliminates most individual overrides.

6. **Light color cleanup**: Scan all page TSX files for hardcoded `#fafafa`, `#f5f5f5`, `#f0f0f0`, `#fff7e6`, `#f6ffed`, `#1677ff`, `#d9d9d9` and replace with dark glass equivalents.

## How to Verify Changes are Loading

If a change seems to have no effect, add an unmistakable visual marker:
```css
.ant-drawer-section { border-left: 2px solid red !important; }
```
Rebuild, serve, and check. If no red border appears, the build is not being loaded (wrong port, cache, etc). Remove the marker once confirmed.
