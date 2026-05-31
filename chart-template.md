# Chart Templates — Frontend Slides Xver

## Overview

Ready-to-use Chart.js chart templates for common presentation scenarios.

---

## Template 1: Revenue Trend (Line Chart)

**Best for:** Showing revenue/user growth over time

```javascript
new Chart(document.getElementById('revenueTrend'), {
  type: 'line',
  data: {
    labels: ['Q1', 'Q2', 'Q3', 'Q4'],
    datasets: [{
      label: 'Revenue',
      data: [120, 150, 180, 210],
      borderColor: 'var(--color-primary)',
      backgroundColor: 'var(--color-primary-light)',
      fill: true,
      tension: 0.4,
      pointRadius: 5,
      pointBackgroundColor: 'var(--color-primary)'
    }]
  },
  options: {
    responsive: true,
    maintainAspectRatio: false,
    plugins: { legend: { display: false } },
    scales: {
      y: { 
        beginAtZero: false, 
        grid: { color: 'var(--border-color)' },
        ticks: { callback: v => '¥' + (v/100).toFixed(0) + 'M' }
      },
      x: { grid: { display: false } }
    }
  }
});
```

---

## Template 2: Product Comparison (Horizontal Bar)

**Best for:** Comparing products, categories, or competitors

```javascript
new Chart(document.getElementById('productCompare'), {
  type: 'bar',
  data: {
    labels: ['Product A', 'Product B', 'Product C', 'Product D', 'Product E'],
    datasets: [{
      label: 'Revenue (¥M)',
      data: [450, 320, 280, 150, 100],
      backgroundColor: ['#1a56db', '#7c3aed', '#f59e0b', '#10b981', '#ef4444'],
      borderRadius: 4,
      borderWidth: 0
    }]
  },
  options: {
    indexAxis: 'y',
    responsive: true,
    maintainAspectRatio: false,
    plugins: { legend: { display: false } },
    scales: {
      x: { 
        beginAtZero: true, 
        grid: { color: 'var(--border-color)' },
        ticks: { callback: v => '¥' + v + 'M' }
      },
      y: { grid: { display: false } }
    }
  }
});
```

---

## Template 3: Market Share (Doughnut)

**Best for:** Market share, portfolio allocation, category breakdown

```javascript
new Chart(document.getElementById('marketShare'), {
  type: 'doughnut',
  data: {
    labels: ['Product A', 'Product B', 'Product C', 'Others'],
    datasets: [{
      data: [45, 30, 15, 10],
      backgroundColor: ['#1a56db', '#7c3aed', '#f59e0b', '#e2e8f0'],
      borderWidth: 2,
      borderColor: '#ffffff'
    }]
  },
  options: {
    responsive: true,
    maintainAspectRatio: false,
    plugins: {
      legend: { 
        position: 'bottom',
        labels: { padding: 20, usePointStyle: true }
      },
      tooltip: {
        callbacks: {
          label: ctx => ctx.label + ': ' + ctx.parsed + '%'
        }
      }
    }
  }
});
```

---

## Template 4: YoY Comparison (Grouped Bar)

**Best for:** Year-over-year, quarter-over-quarter comparison

```javascript
new Chart(document.getElementById('yoyCompare'), {
  type: 'bar',
  data: {
    labels: ['Q1', 'Q2', 'Q3', 'Q4'],
    datasets: [
      {
        label: '2024',
        data: [100, 120, 140, 160],
        backgroundColor: 'rgba(26, 86, 219, 0.7)',
        borderRadius: 4
      },
      {
        label: '2025',
        data: [120, 150, 180, 210],
        backgroundColor: 'rgba(16, 185, 129, 0.7)',
        borderRadius: 4
      }
    ]
  },
  options: {
    responsive: true,
    maintainAspectRatio: false,
    plugins: { legend: { position: 'top' } },
    scales: {
      y: { beginAtZero: true, grid: { color: 'var(--border-color)' } },
      x: { grid: { display: false } }
    }
  }
});
```

---

## Template 5: KPI Trend (Multi-Line with Dual Axis)

**Best for:** Tracking multiple KPIs over time

```javascript
new Chart(document.getElementById('kpiTrend'), {
  type: 'line',
  data: {
    labels: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun'],
    datasets: [
      {
        label: 'Revenue',
        data: [100, 115, 130, 145, 160, 180],
        borderColor: '#1a56db',
        tension: 0.4,
        yAxisID: 'y'
      },
      {
        label: 'Users (K)',
        data: [50, 55, 62, 70, 80, 95],
        borderColor: '#10b981',
        tension: 0.4,
        yAxisID: 'y1'
      }
    ]
  },
  options: {
    responsive: true,
    maintainAspectRatio: false,
    plugins: { legend: { position: 'top' } },
    scales: {
      y: { 
        type: 'linear', position: 'left',
        title: { display: true, text: 'Revenue (¥M)' },
        grid: { color: 'var(--border-color)' }
      },
      y1: {
        type: 'linear', position: 'right',
        title: { display: true, text: 'Users (K)' },
        grid: { display: false }
      },
      x: { grid: { display: false } }
    }
  }
});
```

---

## Template 6: Stacked Area (Composition Trend)

**Best for:** Showing how components contribute to total over time

```javascript
new Chart(document.getElementById('stackedArea'), {
  type: 'line',
  data: {
    labels: ['Q1', 'Q2', 'Q3', 'Q4'],
    datasets: [
      {
        label: 'Product A',
        data: [50, 60, 70, 80],
        backgroundColor: 'rgba(26, 86, 219, 0.5)',
        borderColor: '#1a56db',
        fill: true, tension: 0.4
      },
      {
        label: 'Product B',
        data: [30, 35, 40, 45],
        backgroundColor: 'rgba(124, 58, 237, 0.5)',
        borderColor: '#7c3aed',
        fill: true, tension: 0.4
      },
      {
        label: 'Product C',
        data: [20, 25, 30, 35],
        backgroundColor: 'rgba(245, 158, 11, 0.5)',
        borderColor: '#f59e0b',
        fill: true, tension: 0.4
      }
    ]
  },
  options: {
    responsive: true,
    maintainAspectRatio: false,
    plugins: { legend: { position: 'top' } },
    scales: {
      y: { stacked: true, beginAtZero: true, grid: { color: 'var(--border-color)' } },
      x: { grid: { display: false } }
    }
  }
});
```

---

## Template 7: Radar (Multi-Dimensional)

**Best for:** Capability assessment, competitive analysis

```javascript
new Chart(document.getElementById('radarChart'), {
  type: 'radar',
  data: {
    labels: ['Market', 'Technology', 'Team', 'Funding', 'Product', 'Growth'],
    datasets: [
      {
        label: 'Our Company',
        data: [85, 90, 75, 60, 88, 82],
        borderColor: '#1a56db',
        backgroundColor: 'rgba(26, 86, 219, 0.2)',
        borderWidth: 2
      },
      {
        label: 'Competitor',
        data: [70, 65, 80, 85, 72, 65],
        borderColor: '#ef4444',
        backgroundColor: 'rgba(239, 68, 68, 0.1)',
        borderWidth: 2
      }
    ]
  },
  options: {
    responsive: true,
    maintainAspectRatio: false,
    plugins: { legend: { position: 'bottom' } },
    scales: { r: { beginAtZero: true, max: 100, ticks: { stepSize: 20 } } }
  }
});
```

---

## Color Palettes for Charts

```javascript
// Professional (default)
const professional = ['#1a56db', '#7c3aed', '#f59e0b', '#10b981', '#ef4444', '#06b6d4', '#f97316', '#8b5cf6'];

// Dark theme
const dark = ['#3b82f6', '#a78bfa', '#fbbf24', '#34d399', '#f87171', '#22d3ee', '#fb923c', '#c084fc'];

// Warm
const warm = ['#b45309', '#d97706', '#f59e0b', '#fbbf24', '#fcd34d', '#ea580c', '#c2410c', '#92400e'];

// Nature
const nature = ['#15803d', '#65a30d', '#0d9488', '#16a34a', '#84cc16', '#0891b2', '#4ade80', '#22c55e'];

// Pastel
const pastel = ['#93c5fd', '#c4b5fd', '#fde68a', '#a7f3d0', '#fecaca', '#67e8f9', '#fed7aa', '#ddd6fe'];
```
