# Frontend Slides Xver

> **CodeBuddy Skill** — 数据驱动、图表丰富的 HTML 演示文稿技能

## 概述

`frontend-slides-xver` 是一个专门用于创建**单文件 HTML 演示文稿**的 CodeBuddy 技能。

**特点：**
- 📊 **数据丰富** — 大量使用图表、KPI、指标和数据可视化
- 🏢 **McKinsey 风格** — "结论先行"结构，每页都有底线标题
- 📈 **图表驱动** — 基于 Chart.js 的交互式可视化
- 💼 **适合高管** — 专为商业报告、董事会议、数据叙事设计

## 快速开始

### 1. 在 CodeBuddy 中使用

直接告诉 CodeBuddy 你的需求：

```
"帮我创建一个 Q2 业务回顾的演示文稿，包含营收趋势图和 KPI 仪表盘"
```

CodeBuddy 会自动加载此技能并生成专业的 HTML 演示文稿。

### 2. 手动使用

```bash
git clone https://github.com/poopoo5194379/frontend-slides-xver.git
```

参考 `examples/xver-reference.html` 了解完整实现。

## 文件结构

```
frontend-slides-xver/
├── SKILL.md                      # 技能定义文件
├── README.md                     # 本文件
├── STYLE_PRESETS_XVER.md         # 风格预设目录
├── animation-patterns.md         # 动画模式
├── chart-template.md             # 图表模板
├── chart-renderer-runtime.md     # 图表渲染运行时
├── editor-runtime-xver.md        # 编辑器运行时
├── viewport-base.css             # 基础 CSS
├── examples/
│   └── xver-reference.html       # 参考实现
├── docs/
│   └── preset-previews/          # 风格预览图
└── scripts/
    ├── extract-pptx.py           # PPTX 提取工具
    └── extract-pdf.py            # PDF 提取工具
```

## 依赖

- **Chart.js v4.x** — CDN 引入，无需安装
- 纯 HTML/CSS/JS，无其他外部依赖

## License

MIT