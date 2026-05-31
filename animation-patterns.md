# Animation Patterns — Frontend Slides Xver

## Overview

Animations enhance presentations by drawing attention to key elements and creating smooth transitions between slides. All animations use **pure CSS + vanilla JavaScript** (no external animation libraries).

---

## Pattern 1: Fade Up (Slide Enter)

**Use:** When a slide becomes active, elements fade up from below.

```css
.slide .animate-fade-up {
  opacity: 0;
  transform: translateY(30px);
  transition: opacity 0.6s ease-out, transform 0.6s ease-out;
}

.slide.active .animate-fade-up {
  opacity: 1;
  transform: translateY(0);
}
```

```html
<div class="animate-fade-up" style="transition-delay: 0.1s">First element</div>
<div class="animate-fade-up" style="transition-delay: 0.2s">Second element</div>
<div class="animate-fade-up" style="transition-delay: 0.3s">Third element</div>
```

---

## Pattern 2: Staggered Reveal

**Use:** List items or cards appear one after another.

```css
.stagger-item {
  opacity: 0;
  transform: translateX(-20px);
  transition: opacity 0.4s ease-out, transform 0.4s ease-out;
}

.slide.active .stagger-item {
  opacity: 1;
  transform: translateX(0);
}

.stagger-item:nth-child(1) { transition-delay: 0.1s; }
.stagger-item:nth-child(2) { transition-delay: 0.2s; }
.stagger-item:nth-child(3) { transition-delay: 0.3s; }
.stagger-item:nth-child(4) { transition-delay: 0.4s; }
.stagger-item:nth-child(5) { transition-delay: 0.5s; }
```

---

## Pattern 3: Count Up (Number Animation)

**Use:** KPI values animate from 0 to the target number.

```javascript
function animateCountUp(element, target, duration = 1500) {
  const start = 0;
  const startTime = performance.now();
  
  function update(currentTime) {
    const elapsed = currentTime - startTime;
    const progress = Math.min(elapsed / duration, 1);
    const eased = 1 - Math.pow(1 - progress, 3);
    const current = start + (target - start) * eased;
    element.textContent = Math.floor(current).toLocaleString();
    if (progress < 1) requestAnimationFrame(update);
  }
  
  requestAnimationFrame(update);
}
```

---

## Pattern 4: Chart Draw Animation

**Use:** Charts draw progressively when their slide becomes active.

```javascript
function createAnimatedChart(canvasId, config, delay = 300) {
  const canvas = document.getElementById(canvasId);
  const ctx = canvas.getContext('2d');
  
  const zeroData = config.data.datasets.map(ds => ({
    ...ds,
    data: ds.data.map(() => 0)
  }));
  
  const chart = new Chart(ctx, {
    ...config,
    data: { ...config.data, datasets: zeroData }
  });
  
  setTimeout(() => {
    chart.data = config.data;
    chart.update('active');
  }, delay);
  
  return chart;
}
```

---

## Pattern 5: Highlight Pulse

**Use:** Key metrics or callouts pulse to draw attention.

```css
@keyframes highlightPulse {
  0%, 100% { box-shadow: 0 0 0 0 rgba(26, 86, 219, 0.4); }
  50% { box-shadow: 0 0 0 8px rgba(26, 86, 219, 0); }
}

.pulse-highlight {
  animation: highlightPulse 2s ease-in-out infinite;
}
```

---

## Pattern 6: Slide Transition (Full Page)

**Use:** Smooth transitions between slides.

```css
.slide {
  position: absolute;
  width: 100%;
  height: 100vh;
  opacity: 0;
  transform: scale(0.95);
  transition: opacity 0.5s ease, transform 0.5s ease;
  pointer-events: none;
}

.slide.active {
  opacity: 1;
  transform: scale(1);
  pointer-events: all;
}
```

---

## Pattern 7: Progress Bar

**Use:** Show presentation progress at the bottom.

```html
<div class="progress-bar">
  <div class="progress-fill" id="progressFill"></div>
</div>
```

```css
.progress-bar {
  position: fixed;
  bottom: 0; left: 0;
  width: 100%; height: 4px;
  background: var(--border-color);
  z-index: 1000;
}

.progress-fill {
  height: 100%;
  background: var(--color-primary);
  transition: width 0.3s ease;
}
```

---

## Navigation System

```javascript
let currentSlide = 0;
const slides = document.querySelectorAll('.slide');
const totalSlides = slides.length;

function goToSlide(index) {
  slides[currentSlide].classList.remove('active');
  currentSlide = (index + totalSlides) % totalSlides;
  slides[currentSlide].classList.add('active');
  updateProgress(currentSlide, totalSlides);
}

function nextSlide() { goToSlide(currentSlide + 1); }
function prevSlide() { goToSlide(currentSlide - 1); }

// Keyboard navigation
document.addEventListener('keydown', (e) => {
  if (e.key === 'ArrowRight' || e.key === 'ArrowDown' || e.key === ' ') {
    e.preventDefault(); nextSlide();
  } else if (e.key === 'ArrowLeft' || e.key === 'ArrowUp') {
    e.preventDefault(); prevSlide();
  }
});

// Click navigation
document.addEventListener('click', (e) => {
  e.clientX > window.innerWidth / 2 ? nextSlide() : prevSlide();
});

// Touch support
let touchStartX = 0;
document.addEventListener('touchstart', (e) => {
  touchStartX = e.touches[0].clientX;
});
document.addEventListener('touchend', (e) => {
  const diff = touchStartX - e.changedTouches[0].clientX;
  if (Math.abs(diff) > 50) diff > 0 ? nextSlide() : prevSlide();
});

goToSlide(0);
```

---

## Best Practices

1. **Keep animations subtle** — Don't distract from content
2. **Duration 300-600ms** — Fast enough, slow enough to be visible
3. **Use easing** — `ease-out` for entering, `ease-in-out` for continuous
4. **Stagger delays** — 100-200ms between items
5. **One animation per element**
6. **Respect `prefers-reduced-motion`**:
```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}
```
