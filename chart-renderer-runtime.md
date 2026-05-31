# Chart Renderer Runtime — Frontend Slides Xver

## Overview

The Chart Renderer Runtime provides JavaScript infrastructure for creating and managing Chart.js charts within HTML presentations.

---

## Core Runtime

```javascript
const ChartRenderer = {
  charts: {},
  
  init(canvasId, config, options = {}) {
    const canvas = document.getElementById(canvasId);
    if (!canvas) { console.warn(`Canvas #${canvasId} not found`); return null; }
    
    const ctx = canvas.getContext('2d');
    const defaultOptions = {
      responsive: true,
      maintainAspectRatio: false,
      animation: { duration: 1000, easing: 'easeOutQuart' },
      ...options
    };
    
    const chart = new Chart(ctx, {
      ...config,
      options: { ...config.options, ...defaultOptions }
    });
    
    this.charts[canvasId] = chart;
    return chart;
  },
  
  update(canvasId, newData, animate = true) {
    const chart = this.charts[canvasId];
    if (!chart) return;
    chart.data = newData;
    chart.update(animate ? 'default' : 'none');
  },
  
  destroy(canvasId) {
    const chart = this.charts[canvasId];
    if (chart) { chart.destroy(); delete this.charts[canvasId]; }
  },
  
  destroyAll() {
    Object.keys(this.charts).forEach(id => this.destroy(id));
  },
  
  resizeAll() {
    Object.values(this.charts).forEach(chart => {
      if (chart && chart.resize) chart.resize();
    });
  },
  
  animateOnSlide(canvasId, targetData, delay = 300) {
    const chart = this.charts[canvasId];
    if (!chart) return;
    
    const zeroData = JSON.parse(JSON.stringify(targetData));
    zeroData.datasets = zeroData.datasets.map(ds => ({
      ...ds,
      data: ds.data.map(() => 0)
    }));
    chart.data = zeroData;
    chart.update('none');
    
    setTimeout(() => {
      chart.data = targetData;
      chart.update('active');
    }, delay);
  }
};

// Debounced resize handler
let resizeTimeout;
window.addEventListener('resize', () => {
  clearTimeout(resizeTimeout);
  resizeTimeout = setTimeout(() => ChartRenderer.resizeAll(), 250);
});
```

---

## Integration with Slide Navigation

```javascript
const slideCharts = {
  0: [],
  1: [
    { id: 'revenueChart', type: 'line', data: revenueData },
    { id: 'userChart', type: 'bar', data: userData }
  ],
  2: [{ id: 'marketShare', type: 'doughnut', data: shareData }],
  3: []
};

function onSlideEnter(slideIndex) {
  const charts = slideCharts[slideIndex] || [];
  charts.forEach(chart => {
    if (ChartRenderer.charts[chart.id]) {
      ChartRenderer.animateOnSlide(chart.id, chart.data);
    } else {
      ChartRenderer.init(chart.id, chart.config);
    }
  });
}
```

---

## KPI Counter Runtime

```javascript
const KPICounter = {
  counters: [],
  
  register(elementId, targetValue, options = {}) {
    this.counters.push({
      element: document.getElementById(elementId),
      target: targetValue,
      prefix: options.prefix || '',
      suffix: options.suffix || '',
      decimals: options.decimals || 0,
      duration: options.duration || 1500,
      animated: false
    });
  },
  
  animateAll() {
    this.counters.forEach(counter => {
      if (counter.animated) return;
      this.animateCounter(counter);
      counter.animated = true;
    });
  },
  
  animateCounter(counter) {
    const { element, target, prefix, suffix, decimals, duration } = counter;
    if (!element) return;
    
    const startTime = performance.now();
    
    function update(currentTime) {
      const elapsed = currentTime - startTime;
      const progress = Math.min(elapsed / duration, 1);
      const eased = 1 - Math.pow(1 - progress, 3);
      const current = target * eased;
      
      element.textContent = prefix + current.toFixed(decimals) + suffix;
      
      if (progress < 1) requestAnimationFrame(update);
    }
    
    requestAnimationFrame(update);
  },
  
  reset() {
    this.counters.forEach(c => { c.animated = false; });
  }
};
```

---

## Performance Considerations

1. **Lazy initialization** — Only create charts when their slide becomes active
2. **Destroy off-screen charts** — Free memory by destroying distant charts
3. **Use `maintainAspectRatio: false`** — Let container control chart size
4. **Debounce resize** — Avoid excessive redraws
5. **Limit chart count per slide** — Max 4 charts for performance
