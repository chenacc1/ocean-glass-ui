# Neo-Glass UI — 玻璃拟态深色组件库

22+ 组件 · WebGL 着色器背景 · 3D 倾斜交互 · 零依赖 · 纯 HTML/CSS/JS

<p align="center">
  <img src="screenshots/dashboard-check.png" alt="Neo-Glass Dashboard" width="800">
</p>

## 立即购买

> **[点此购买 →](https://ifdian.net/a/markdownpaste)** — ¥29 个人商用许可，包含 3 个演示文件 + 5 份设计文档

---

## 核心特性

| 特性 | 说明 |
|------|------|
| **9 层新拟态阴影** | 精确的光源方向（左上→右下），2 层外层 + 7 层内层阴影 |
| **遮罩复合描边环** | `mask-composite: exclude` 技法，贴合任意 border-radius |
| **3D 透视倾斜** | 所有面板鼠标跟踪，`cubic-bezier` 弹簧缓动回弹 |
| **玻璃球悬停物理** | 11 层阴影增强 + `scale(1.15)` 弹簧缩放 |
| **水纹焦散纹理** | SVG `feTurbulence` 数据 URI，`soft-light` 混合模式 |
| **WebGL 流动波浪** | 全屏着色器背景，鼠标交互，8CD7FF 天蓝色调 |
| **零依赖** | 纯 HTML/CSS/JS，无框架锁定，打开即运行 |

---

## 组件目录

### 核心表面
| 组件 | 类名 | 说明 |
|------|------|------|
| 玻璃卡片 | `.glass-base` | 毛玻璃面板（描边环 + 光泽叠加伪元素） |
| 玻璃球 | `.glass-ball` | 3D 球体（径向高光 + 多层阴影） |

### 按钮
| 组件 | 类名 | 说明 |
|------|------|------|
| 玻璃胶囊按钮 | `.figma-btn` | 罗马风情字体，3D 透视倾斜 |
| 玻璃按钮 | `.glass-btn` | 主色调 / 危险 / 文字 / 小 / 大 变体 |

### 表单控件
| 组件 | 类名 | 说明 |
|------|------|------|
| 文本输入框 | `.glass-input` | 聚焦辉光 + 9 层内阴影 |
| 复选框 | `.glass-check` | 勾选 → 玻璃球动画过渡 |
| 开关 | `.toggle` | 42×22px，3D 倾斜 + 悬停阴影增强 |
| 滑块 | `.glass-slider` | 拖动即时响应 + 焦散填充动画 |
| 下拉选择器 | `.glass-select` | 弹性弹出 + 玻璃折射悬停 |
| 分段控制器 | `.glass-seg` | 258×84px，弹簧指示器 + 悬停放大 |
| 评分星级 | `.glass-rate` | 金色点亮 / 灰色熄灭 + 凹凸立体效果 |
| 进度条 | `.glass-progress` | 凹槽样式 + 焦散纹理 + 流动动画 |

### 数据展示
| 组件 | 类名 | 说明 |
|------|------|------|
| 表格 | `.glass-table` | 行悬停玻璃折射 + 缩放入场 |
| 列表 | `.glass-list` | 悬停镜头折射 + 边框半径展开 |
| 树形控件 | `.glass-tree` | 展开箭头旋转 + 悬停折射 |
| 分页器 | `.glass-pagination` | 玻璃卡片风格 + 悬浮提升 |

### 导航与容器
| 组件 | 类名 | 说明 |
|------|------|------|
| 导航菜单 | `.glass-nav` | 左侧蓝色激活指示 + 徽章集成 |
| 折叠面板 | `.glass-collapse` | 弹性展开 + 平滑合起 |
| 轮播 | `.glass-carousel` | 3D 倾斜 + 导航按钮 |
| 玻璃卡片 | `.glass-card` | 三栏式（头部 / 内容 / 底部）|

### 反馈与装饰
| 组件 | 类名 | 说明 |
|------|------|------|
| 悬浮按钮 | `.float-btn` | 浮动动画 + 3D 悬停 |
| 标签 | `.glass-tag` | 5 色变体 + 3D 倾斜 |
| 徽章 | `.glass-badge` | 圆点 + 计数两种样式 |
| 头像 | `.glass-avatar` | 44×44px 玻璃球 + 悬停内阴影增强 |

---

## 演示文件

| 文件 | 说明 |
|------|------|
| `neo-glass-dashboard.html` | 完整后台面板（所有 22 个组件 + 侧边栏 + WebGL 背景） |
| `neo-glass-ui-kit.html` | 组件目录（60+ 变体，按类别整理） |
| `figma-group5.html` | 原始 Figma 参考实现（含所有交互效果） |

---

## 快速入门

```html
<!-- 1. 引入字体 -->
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
<link href="https://fonts.googleapis.com/css2?family=Romanesco&display=swap" rel="stylesheet">

<!-- 2. 添加 WebGL 背景画布 -->
<canvas id="shader-bg"></canvas>

<!-- 3. 使用任意组件 -->
<div class="glass-base panel-3d-wrap">
  <div class="panel-3d">
    <!-- 你的内容 -->
  </div>
</div>
```

详细 CSS 类和 JS 交互模式参见 `SKILL-NEO-GLASS-DASHBOARD.md`。

---

## 技术规格

| 项目 | 说明 |
|------|------|
| 语言 | HTML + CSS + JavaScript（原生） |
| 依赖 | 零（仅 Google Fonts CDN） |
| 浏览器 | Chrome 90+, Edge 90+, Safari 15+, Firefox 90+ |
| WebGL | 需要 WebGL 支持（着色器背景，不可用时回退为纯色） |
| 文件大小 | 约 88KB 每个演示文件（自包含） |

---

## 购买许可

| 版本 | 价格 | 内容 |
|------|------|------|
| **个人版** | ¥29 | 3 个 HTML 演示 + 5 份设计文档 + 个人商用许可 |

**[在爱发电购买 →](https://ifdian.net/a/markdownpaste)**

---

## 项目结构

```
neo-glass-ui/
├── neo-glass-dashboard.html    # 仪表板演示（主要产品）
├── neo-glass-ui-kit.html       # 组件目录（60+ 变体）
├── figma-group5.html           # 原始 Figma 参考
├── docs/
│   ├── SKILL-NEO-GLASS-DASHBOARD.md  # 完整设计系统文档
│   ├── SKILL-NEO-GLASS-LIGHT.md      # 浅色主题变体
│   ├── SKILL-NEO-GLASS-MODAL.md      # 模态框组件规格
│   ├── SKILL-NEO-GLASS-CAUSTIC.md    # 焦散与着色器效果
│   └── SKILL-NEO-GLASS.md            # 核心设计原则
├── screenshots/                # 产品截图
└── README.md                   # 本文件
```

---

## 截图

<p align="center">
  <img src="screenshots/dashboard-check.png" alt="完整仪表板" width="400">
  <img src="screenshots/pill-btn-verify.png" alt="玻璃胶囊按钮" width="400">
</p>

---

&copy; 2026 Neo-Glass UI. 保留所有权利。
