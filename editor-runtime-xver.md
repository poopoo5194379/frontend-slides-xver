# Editor Runtime — Frontend Slides Xver

## Overview

The Editor Runtime enables **in-browser editing** of HTML presentations. Users can modify text, rearrange slides, adjust charts, and export the final result.

---

## Core Editing Features

### 1. Inline Text Editing

```javascript
document.querySelectorAll('.slide [data-editable]').forEach(el => {
  el.addEventListener('dblclick', (e) => {
    e.target.contentEditable = true;
    e.target.focus();
    const range = document.createRange();
    range.selectNodeContents(e.target);
    const sel = window.getSelection();
    sel.removeAllRanges();
    sel.addRange(range);
  });
  
  el.addEventListener('blur', () => { el.contentEditable = false; });
  
  el.addEventListener('keydown', (e) => {
    if (e.key === 'Enter' && !e.shiftKey) {
      e.preventDefault(); e.target.blur();
    }
  });
});
```

### 2. Slide Reordering

```javascript
const slideList = document.getElementById('slide-list');
let draggedItem = null;

slideList.addEventListener('dragstart', (e) => {
  draggedItem = e.target.closest('.slide-list-item');
  e.target.classList.add('dragging');
});

slideList.addEventListener('dragover', (e) => {
  e.preventDefault();
  const afterElement = getDragAfterElement(slideList, e.clientY);
  const item = document.querySelector('.dragging');
  if (afterElement) slideList.insertBefore(item, afterElement);
  else slideList.appendChild(item);
});

slideList.addEventListener('drop', () => {
  document.querySelector('.dragging')?.classList.remove('dragging');
  syncSlideOrder();
});
```

### 3. Object-Level Layout Editing

```javascript
let selectedElement = null;
let isDragging = false;
let dragStartX, dragStartY, elemStartX, elemStartY;

document.querySelectorAll('.slide .draggable').forEach(el => {
  el.addEventListener('mousedown', (e) => {
    if (e.target === el || e.target.closest('.drag-handle')) {
      selectElement(el);
      isDragging = true;
      dragStartX = e.clientX;
      dragStartY = e.clientY;
      const rect = el.getBoundingClientRect();
      elemStartX = rect.left;
      elemStartY = rect.top;
      e.preventDefault();
    }
  });
});

document.addEventListener('mousemove', (e) => {
  if (!isDragging || !selectedElement) return;
  const dx = e.clientX - dragStartX;
  const dy = e.clientY - dragStartY;
  selectedElement.style.left = (elemStartX + dx) + 'px';
  selectedElement.style.top = (elemStartY + dy) + 'px';
});

document.addEventListener('mouseup', () => { isDragging = false; });
```

### 4. Properties Panel

```html
<div id="properties-panel" class="properties-panel" style="display: none;">
  <h3>Properties</h3>
  <label>Width: <input type="text" id="prop-width" /></label>
  <label>Height: <input type="text" id="prop-height" /></label>
  <label>Font Size: <input type="text" id="prop-font-size" /></label>
  <label>Color: <input type="color" id="prop-color" /></label>
  <label>Background: <input type="color" id="prop-bg" /></label>
  <label>Opacity: <input type="range" id="prop-opacity" min="0" max="100" /></label>
</div>
```

---

## Export Features

### Export as HTML
```javascript
function exportHTML() {
  const html = document.documentElement.outerHTML;
  const blob = new Blob(['<!DOCTYPE html>\n' + html], { type: 'text/html' });
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url;
  a.download = 'presentation.html';
  a.click();
  URL.revokeObjectURL(url);
}
```

### Save to Local Storage
```javascript
function saveToLocal() {
  const html = document.documentElement.outerHTML;
  localStorage.setItem('presentation-backup', html);
  localStorage.setItem('presentation-timestamp', new Date().toISOString());
}

function loadFromLocal() {
  const html = localStorage.getItem('presentation-backup');
  if (html) { document.open(); document.write(html); document.close(); }
}
```

---

## Editor Toolbar

```html
<div class="editor-toolbar">
  <button onclick="addSlide()">+ Slide</button>
  <button onclick="duplicateSlide()">📋</button>
  <button onclick="deleteSlide()">🗑</button>
  <span class="separator"></span>
  <button onclick="exportHTML()">💾 Export</button>
  <button onclick="saveToLocal()">📥 Save</button>
  <button onclick="toggleEditMode()">✏️ Edit</button>
  <span class="separator"></span>
  <select onchange="changePreset(this.value)">
    <option value="">Style Preset...</option>
    <option value="professional-blue">Professional Blue</option>
    <option value="dark-executive">Dark Executive</option>
    <option value="modern-minimal">Modern Minimal</option>
    <option value="warm-corporate">Warm Corporate</option>
    <option value="tech-innovate">Tech Innovate</option>
    <option value="nature-sustainable">Nature Sustainable</option>
  </select>
</div>
```

```css
.editor-toolbar {
  position: fixed; top: 0; left: 0; right: 0; z-index: 10000;
  background: #1e293b; color: white;
  padding: 8px 16px;
  display: flex; align-items: center; gap: 8px;
  font-size: 14px;
}
.editor-toolbar button {
  background: #334155; color: white;
  border: none; padding: 6px 12px; border-radius: 4px;
  cursor: pointer;
}
.editor-toolbar button:hover { background: #475569; }
.editor-toolbar .separator {
  width: 1px; height: 24px; background: #475569;
}
```

---

## Keyboard Shortcuts

```javascript
document.addEventListener('keydown', (e) => {
  if (e.ctrlKey && e.key === 's') { e.preventDefault(); saveToLocal(); }
  if (e.ctrlKey && e.key === 'e') { e.preventDefault(); exportHTML(); }
  if (e.key === 'Delete' && selectedElement) {
    selectedElement.remove();
    selectedElement = null;
    document.getElementById('properties-panel').style.display = 'none';
  }
});
```
