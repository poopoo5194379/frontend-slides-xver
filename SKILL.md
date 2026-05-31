---
name: frontend-slides-xver
description: Use when the user wants a data-rich, chart-heavy HTML presentation with McKinsey-style "conclusion-first" structure
---

# Frontend Slides Xver — Data-Rich HTML Presentation Skill

## Overview

**frontend-slides-xver** is a specialized skill for creating **single-file HTML presentations** that are:

- **Data-rich** — Heavy use of charts, KPIs, metrics, and data visualizations
- **McKinsey-style** — "Conclusion first" structure with bottom-line headlines
- **Chart-heavy** — Interactive Chart.js visualizations with multiple chart types
- **Executive-ready** — Designed for business reports, board presentations, and data storytelling

## When to Use This Skill

Trigger this skill when the user wants to:
- Create a business presentation with charts and data
- Build an executive briefing or board deck
- Generate a data analysis report as slides
- Make an industry insight presentation
- Create an annual review or quarterly report
- Produce a presentation with KPI dashboards
- Build any data-driven HTML slideshow

## Core Principles

### 1. Conclusion-First Structure
Every slide starts with a **bottom-line headline** — a single sentence that tells the audience the key takeaway. Supporting data and charts follow below.

### 2. Data-Driven Narrative
Slides tell a story through data:
- **KPI cards** for key metrics
- **Charts** for trends, comparisons, distributions
- **Tables** for detailed data
- **Callouts** for important insights

### 3. Visual Hierarchy
- Headline → Biggest, boldest
- Key metric → Large, prominent
- Supporting chart → Clear, well-labeled
- Detail text → Smaller, secondary

## Chart Types Available

Use Chart.js (v4.x CDN) for all charts:

| Chart Type | Best For | Chart.js Config |
|---|---|---|
| **Bar** | Comparisons, rankings | `type: 'bar'` |
| **Horizontal Bar** | Long labels, rankings | `type: 'bar'`, `indexAxis: 'y'` |
| **Line** | Trends, time series | `type: 'line'` |
| **Doughnut** | Proportions, market share | `type: 'doughnut'` |
| **Pie** | Simple proportions | `type: 'pie'` |
| **Radar** | Multi-dimensional comparison | `type: 'radar'` |
| **Polar Area** | Relative proportions | `type: 'polarArea'` |
| **Scatter** | Correlation | `type: 'scatter'` |
| **Bubble** | 3-variable comparison | `type: 'bubble'` |
| **Stacked Bar** | Composition + comparison | `type: 'bar'`, stacked |
| **Mixed** | Multi-metric overlay | Multiple datasets |

## Style Presets

See `STYLE_PRESETS_XVER.md` for the full preset catalog. Quick reference:

### Preset: `professional-blue` (Default)
- Primary: `#1a56db` (Blue)
- Background: `#f8fafc`
- Text: `#1e293b`
- Accent: `#f59e0b` (Amber for highlights)

### Preset: `dark-executive`
- Background: `#0f172a` (Dark navy)
- Text: `#f1f5f9`
- Primary: `#3b82f6`

### Preset: `modern-minimal`
- Background: `#ffffff`
- Text: `#171717`
- Primary: `#000000`

### Preset: `warm-corporate`
- Primary: `#b45309` (Amber-brown)
- Background: `#fffbeb`

## Slide Layout Templates

### Template 1: Title Slide
```html
<section class="slide title-slide">
  <div class="title-content">
    <h1>Presentation Title</h1>
    <p class="subtitle">Subtitle or date</p>
    <p class="author">Author / Department</p>
  </div>
</section>
```

### Template 2: KPI Dashboard Slide
```html
<section class="slide">
  <h2 class="headline">Key Takeaway Here</h2>
  <div class="kpi-grid">
    <div class="kpi-card">
      <span class="kpi-value">¥1.2B</span>
      <span class="kpi-label">Revenue</span>
      <span class="kpi-change positive">↑ 23%</span>
    </div>
  </div>
</section>
```

### Template 3: Chart + Insight Slide
```html
<section class="slide">
  <h2 class="headline">Conclusion Here</h2>
  <div class="split-layout">
    <div class="chart-container">
      <canvas id="chart1"></canvas>
    </div>
    <div class="insights">
      <h3>Key Findings</h3>
      <ul>
        <li>Finding 1</li>
        <li>Finding 2</li>
      </ul>
    </div>
  </div>
</section>
```

### Template 4: Two-Chart Comparison
```html
<section class="slide">
  <h2 class="headline">Conclusion Here</h2>
  <div class="chart-grid-2">
    <div class="chart-container">
      <h3>Control</h3>
      <canvas id="chartA"></canvas>
    </div>
    <div class="chart-container">
      <h3>Experiment</h3>
      <canvas id="chartB"></canvas>
    </div>
  </div>
</section>
```

### Template 5: End Slide
```html
<section class="slide end-slide">
  <div class="end-content">
    <h1>Thank You</h1>
    <p>Q&A</p>
  </div>
</section>
```

## CSS Framework

Use `viewport-base.css` as the base CSS. Key classes:

### Layout Classes
- `.slide` — Full viewport slide (100vw × 100vh)
- `.split-layout` — 50/50 horizontal split
- `.split-layout-60-40` — 60/40 split
- `.split-layout-40-60` — 40/60 split
- `.chart-grid-2` — Two equal charts side by side
- `.chart-grid-3` — Three charts in a row
- `.chart-grid-4` — Four charts (2×2)
- `.kpi-grid` — KPI cards in a row (auto-wrap)
- `.kpi-grid-4` — Exactly 4 KPI cards

### Component Classes
- `.headline` — Bottom-line conclusion text
- `.kpi-card` — Individual KPI metric card
- `.kpi-value` — Large number in KPI card
- `.kpi-label` — Description under value
- `.kpi-change` — Up/down indicator
- `.chart-container` — Chart wrapper with responsive sizing
- `.data-table` — Styled data table
- `.insights` — Bullet-point insights panel
- `.callout` — Highlighted callout box

### Color Utility Classes
- `.positive` / `.negative` / `.neutral` — Color indicators

## Dependencies

- **Chart.js v4.x** — CDN: `https://cdn.jsdelivr.net/npm/chart.js`
- No other external dependencies (pure HTML/CSS/JS)

## Files Included

- `SKILL.md` — This file (skill definition)
- `README.md` — Quick start guide
- `STYLE_PRESETS_XVER.md` — Complete style preset catalog
- `animation-patterns.md` — Animation patterns and code
- `chart-template.md` — Chart templates and recipes
- `chart-renderer-runtime.md` — Chart rendering runtime docs
- `editor-runtime-xver.md` — Editor runtime documentation
- `viewport-base.css` — Base CSS for all presentations
- `examples/xver-reference.html` — Reference implementation example
- `scripts/extract-pptx.py` — PPTX extraction utility
- `scripts/extract-pdf.py` — PDF extraction utility
