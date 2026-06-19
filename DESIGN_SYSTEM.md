# OceanAvenu Dark Glass UI

基于照片底图的暗色毛玻璃设计系统，适配 Ant Design 6。

## 设计令牌

### 背景与玻璃

```css
:root {
  --bg-base: #07080a;                          /* 纯黑基底 */
  --glass-bg: rgba(7, 8, 10, 0.12);           /* 面板玻璃（与侧边栏同透明度） */
  --glass-bg-input: rgba(7, 8, 10, 0.08);     /* 输入框玻璃（稍透） */
  --glass-bg-modal: rgba(7, 8, 10, 0.12);     /* 弹窗玻璃 */
  --glass-bg-header: rgba(7, 8, 10, 0.1);     /* 顶栏玻璃 */
  --glass-blur: blur(40px);                    /* 面板模糊度 */
  --glass-blur-strong: blur(60px);             /* 弹窗/抽屉强模糊 */
}
```

### 边框

```css
  --border-glass: rgba(255, 255, 255, 0.08);   /* 面板分割线 */
  --border-input: rgba(255, 255, 255, 0.06);   /* 输入框内边框 */
  --border-input-outer: rgba(255, 255, 255, 0.12); /* 输入框外框（搜索框等） */
```

### 文字

```css
  --text-primary: rgba(255, 255, 255, 0.92);
  --text-secondary: rgba(255, 255, 255, 0.6);
  --text-placeholder: rgba(255, 255, 255, 0.35);
```

### 强调色

```css
  --accent: rgba(120, 187, 255, 0.91);
  --accent-hex: #78bbff;
  /* 其他点缀色：绿 rgba(120,255,203,0.91)  琥珀 rgba(255,199,120,0.91) */
```

### 圆角

```css
  --radius-panel: 20px;    /* 卡片、弹窗、抽屉 */
  --radius-card: 12px;     /* 下拉菜单、标签页 */
  --radius-btn: 12px;      /* 按钮 */
  --radius-input: 12px;    /* 输入框 */
```

### 阴影

```css
  --shadow-card: 0px 4px 20px rgba(0, 0, 0, 0.3);
  /* 圆角元素用 box-shadow（非 filter:drop-shadow，会破坏 backdrop-filter） */
```

### 字体

```css
  --font: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
```

---

## 基底图设置

```css
html, body, #root {
  background-image: url('./OceanAvenu.jpg');
  background-size: cover;
  background-position: center;
  background-attachment: fixed;
}

/* 暗色罩层确保文字可读 */
#root::before {
  content: '';
  position: fixed; inset: 0;
  background: rgba(7, 8, 10, 0.15);
  z-index: 0; pointer-events: none;
}
```

---

## Ant Design 6 覆盖要点

### 主题令牌（ConfigProvider）

```tsx
<ConfigProvider theme={{
  algorithm: theme.darkAlgorithm,
  token: {
    colorPrimary: '#78bbff',
    borderRadius: 12,
    colorBgContainer: 'rgba(7, 8, 10, 0.12)',
    colorBgElevated: 'rgba(7, 8, 10, 0.12)',  /* 关键：Drawer/Modal/Picker 弹层背景 */
    colorBgLayout: 'transparent',
    colorBgMask: 'rgba(0, 0, 0, 0.45)',
    colorText: 'rgba(235, 237, 240, 0.98)',
    colorTextSecondary: 'rgba(178, 185, 194, 0.92)',
    colorBorder: 'rgba(119, 128, 140, 0.25)',
    fontFamily: "'Inter', -apple-system, ...",
  }
}}>
```

### 关键组件覆盖

```css
/* 卡片 */
.ant-card {
  background: var(--glass-bg) !important;
  backdrop-filter: var(--glass-blur) !important;
  border: 1px solid var(--border-glass) !important;
  border-radius: var(--radius-panel) !important;
  box-shadow: var(--shadow-card) !important;
}

/* 表格 */
.ant-table { background: transparent !important; }
.ant-table-thead > tr > th { background: rgba(7,8,10,0.12) !important; }

/* 弹窗 + 抽屉（统一透明度） */
.ant-modal-content,
.ant-drawer-section, .ant-drawer-pure {
  background: rgba(7,8,10,0.12) !important;
  backdrop-filter: blur(60px) !important;
}

/* 输入框：外框可见，内框消失 */
.ant-input-affix-wrapper {
  background: rgba(7,8,10,0.1) !important;
  border: 1px solid rgba(255,255,255,0.12) !important;
}
.ant-input-affix-wrapper .ant-input {
  background: transparent !important;
  border: none !important;
}

/* 标签页激活态 */
.ant-tabs-ink-bar {
  background: rgba(120,187,255,0.35) !important;
  border-radius: 4px !important;
}
.ant-tabs-tab-active {
  background: rgba(120,187,255,0.08) !important;
  border-radius: 16px !important;
}

/* 侧边栏 */
.ant-layout-sider {
  background: rgba(7,8,10,0.06) !important;
  backdrop-filter: blur(30px) !important;
  border-right: 1px solid rgba(255,255,255,0.08) !important;
  box-shadow: 4px 0 20px rgba(0,0,0,0.3);
}

/* 顶栏 */
.ant-layout-header {
  background: rgba(7,8,10,0.1) !important;
  backdrop-filter: blur(20px) !important;
  border-radius: 0 0 16px 16px;
  box-shadow: 0 4px 20px rgba(0,0,0,0.3);
}
```

---

## 经验教训

### 1. CSS 类名：看 DOM 不看文档
Ant Design 6 CSS-in-JS 生成的类名可能与文档不同。始终从浏览器 DevTools Elements 面板获取实际类名。
- 例：Drawer 实际类名是 `.ant-drawer-section`，不是文档中的 `.ant-drawer-pure`

### 2. 主题令牌 > CSS 覆盖
优先改 ConfigProvider 的 token（如 `colorBgElevated`），它直接控制 `var(--ant-color-bg-elevated)`。
CSS 覆盖作补充手段。

### 3. `!important` 是必要的
Ant Design 6 CSS-in-JS 的 `:where()` 选择器零优先级，但运行时注入顺序不确定。用 `!important` 确保覆盖。

### 4. 统一透明度
所有玻璃面板用同一个透明度值（推荐 `0.12`），输入框稍亮（`0.08-0.1`）。
不一致的透明度是风格不统一的主要原因。

### 5. `backdrop-filter` 需要 `-webkit-` 前缀
始终双写：
```css
backdrop-filter: blur(40px) !important;
-webkit-backdrop-filter: blur(40px) !important;
```

### 6. `filter: drop-shadow()` 与 `backdrop-filter` 冲突
不能用 `filter: drop-shadow()`（会破坏毛玻璃效果），只能用 `box-shadow`。
圆角阴影靠 `border-radius` 实现——`box-shadow` 会跟随圆角。

### 7. 排查改动是否生效
加一个不可能错过的视觉标记（如 `border: 2px solid red`），确认构建加载后再移除。

---

## 页面 CSS 清理清单

接手旧项目时，扫描并替换所有硬编码浅色值：
```
#fafafa #f5f5f5 #f0f0f0 #e8e8e8 → rgba(7,8,10,0.12)
#fff7e6 #fff1f0         → rgba(255,171,0,0.06)  / rgba(255,77,79,0.06)
#f6ffed                 → rgba(82,196,26,0.06)
#f0f5ff                 → rgba(68,138,255,0.06)
#1677ff                 → #78bbff
#d9d9d9 #b7eb8f #ffd591 → rgba(...,0.1-0.2)
```

Canvas 图表中：
```
#fafafa → rgba(7,8,10,0.3)
#e8e8e8 → rgba(255,255,255,0.08)
#fff    → rgba(255,255,255,0.92)
#333    → rgba(255,255,255,0.85)
```
