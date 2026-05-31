# Style Presets — Frontend Slides Xver

## Overview

Style presets define the complete visual identity of a presentation.

---

## Preset 1: `professional-blue` (Default)

**Best for:** Corporate presentations, business reviews, financial reports

### Color Palette
```css
:root {
  --bg-primary: #f8fafc;
  --bg-slide: #ffffff;
  --text-primary: #1e293b;
  --text-secondary: #64748b;
  --color-primary: #1a56db;
  --color-primary-light: #dbeafe;
  --color-accent: #f59e0b;
  --color-success: #10b981;
  --color-danger: #ef4444;
  --border-color: #e2e8f0;
  --shadow: 0 1px 3px rgba(0,0,0,0.1);
}
```

### Typography
```css
body { font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif; }
.headline { font-size: 2rem; font-weight: 700; color: var(--text-primary); }
```

### Chart Colors
```javascript
const chartColors = ['#1a56db', '#7c3aed', '#f59e0b', '#10b981', '#ef4444', '#06b6d4', '#f97316', '#8b5cf6'];
```

---

## Preset 2: `dark-executive`

**Best for:** Executive briefings, evening presentations, tech keynotes

### Color Palette
```css
:root {
  --bg-primary: #0f172a;
  --bg-slide: #1e293b;
  --text-primary: #f1f5f9;
  --text-secondary: #94a3b8;
  --color-primary: #3b82f6;
  --color-primary-light: #1e3a5f;
  --color-accent: #f59e0b;
  --color-success: #34d399;
  --color-danger: #f87171;
  --border-color: #334155;
  --shadow: 0 4px 6px rgba(0,0,0,0.3);
}
```

### Chart Colors (Neon on Dark)
```javascript
const chartColors = ['#3b82f6', '#a78bfa', '#fbbf24', '#34d399', '#f87171', '#22d3ee', '#fb923c', '#c084fc'];
```

---

## Preset 3: `modern-minimal`

**Best for:** Startup pitches, creative presentations, design reviews

### Color Palette
```css
:root {
  --bg-primary: #ffffff;
  --bg-slide: #ffffff;
  --text-primary: #171717;
  --text-secondary: #737373;
  --color-primary: #000000;
  --color-primary-light: #f5f5f5;
  --color-accent: #404040;
  --color-success: #15803d;
  --color-danger: #dc2626;
  --border-color: #e5e5e5;
  --shadow: none;
}
```

### Chart Colors (Monochrome)
```javascript
const chartColors = ['#000000', '#404040', '#737373', '#a3a3a3', '#d4d4d4', '#525252', '#8a8a8a', '#b0b0b0'];
```

---

## Preset 4: `warm-corporate`

**Best for:** Internal communications, HR reports, team presentations

### Color Palette
```css
:root {
  --bg-primary: #fffbeb;
  --bg-slide: #ffffff;
  --text-primary: #451a03;
  --text-secondary: #92400e;
  --color-primary: #b45309;
  --color-primary-light: #fef3c7;
  --color-accent: #d97706;
  --color-success: #059669;
  --color-danger: #dc2626;
  --border-color: #fde68a;
  --shadow: 0 2px 4px rgba(180, 83, 9, 0.1);
}
```

### Chart Colors (Warm tones)
```javascript
const chartColors = ['#b45309', '#d97706', '#f59e0b', '#fbbf24', '#fcd34d', '#ea580c', '#c2410c', '#92400e'];
```

---

## Preset 5: `tech-innovate`

**Best for:** Tech demos, product launches, innovation showcases

### Color Palette
```css
:root {
  --bg-primary: #f0f9ff;
  --bg-slide: #ffffff;
  --text-primary: #0f172a;
  --text-secondary: #475569;
  --color-primary: #6366f1;
  --color-primary-light: #e0e7ff;
  --color-accent: #ec4899;
  --color-success: #10b981;
  --color-danger: #f43f5e;
  --border-color: #c7d2fe;
  --shadow: 0 4px 12px rgba(99, 102, 241, 0.15);
}
```

### Chart Colors (Vibrant)
```javascript
const chartColors = ['#6366f1', '#ec4899', '#14b8a6', '#f97316', '#8b5cf6', '#06b6d4', '#f43f5e', '#84cc16'];
```

---

## Preset 6: `nature-sustainable`

**Best for:** ESG reports, sustainability presentations, environmental topics

### Color Palette
```css
:root {
  --bg-primary: #f0fdf4;
  --bg-slide: #ffffff;
  --text-primary: #052e16;
  --text-secondary: #166534;
  --color-primary: #15803d;
  --color-primary-light: #dcfce7;
  --color-accent: #65a30d;
  --color-success: #16a34a;
  --color-danger: #b91c1c;
  --border-color: #bbf7d0;
  --shadow: 0 2px 4px rgba(21, 128, 61, 0.1);
}
```

### Chart Colors (Natural greens)
```javascript
const chartColors = ['#15803d', '#65a30d', '#0d9488', '#16a34a', '#84cc16', '#0891b2', '#4ade80', '#22c55e'];
```

---

## Applying a Preset

In your HTML, add the preset CSS variables in a `<style>` block:

```html
<style>
  :root {
    --bg-primary: #f8fafc;
    --bg-slide: #ffffff;
    --text-primary: #1e293b;
    /* ... copy full preset ... */
  }
</style>
```

Then use the CSS variables throughout:
```css
.slide { background: var(--bg-slide); color: var(--text-primary); }
.headline { color: var(--text-primary); }
.kpi-card { background: var(--bg-primary); border: 1px solid var(--border-color); }
```

## Choosing a Preset

| Scenario | Recommended Preset |
|---|---|
| Business reports / Finance | `professional-blue` |
| Executive briefings | `dark-executive` |
| Startup pitches / Creative | `modern-minimal` |
| Internal comms / Team | `warm-corporate` |
| Tech demos / Product launch | `tech-innovate` |
| ESG / Sustainability | `nature-sustainable` |
