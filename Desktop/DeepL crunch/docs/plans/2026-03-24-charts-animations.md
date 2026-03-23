# Charts & Animations Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Add a radar chart to the At a Glance section and scroll-triggered micro-animations throughout `deepl-marketing-snapshot.html`.

**Architecture:** Single HTML file — no build step, no npm. Chart.js loaded via CDN for the radar chart. Vanilla `IntersectionObserver` for scroll-triggered animations (fade-up, fade-left, staggered cascades, bar fill animations, count-up numbers). All JS in one `<script>` block at the bottom of `<body>`. Accessibility handled via `prefers-reduced-motion`.

**Tech Stack:** Chart.js 4.x (CDN), vanilla JS, CSS transitions/keyframes

**Design doc:** `docs/plans/2026-03-24-charts-animations-design.md`

---

### Task 1: Add Chart.js CDN and restructure At a Glance layout

**Files:**
- Modify: `deepl-marketing-snapshot.html`

**Step 1: Add Chart.js CDN script tag**

Inside `<head>`, after the Google Fonts `<link>`, add:

```html
<script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.4/dist/chart.umd.min.js"></script>
```

**Step 2: Add CSS for the two-column At a Glance layout**

Add to the `<style>` block, after the `.summary-grid` rule:

```css
/* ---- AT A GLANCE RADAR LAYOUT ---- */
.glance-layout {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 32px;
  align-items: start;
}

.radar-wrap {
  background: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: 12px;
  padding: 28px;
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.radar-wrap .radar-title {
  font-family: 'JetBrains Mono', monospace;
  font-size: 11px;
  letter-spacing: 2px;
  text-transform: uppercase;
  color: var(--text-muted);
}

.radar-cards {
  display: flex;
  flex-direction: column;
  gap: 14px;
}

@media (max-width: 900px) {
  .glance-layout {
    grid-template-columns: 1fr;
  }
}
```

**Step 3: Restructure the At a Glance HTML**

Find the existing `<div class="summary-grid">` block (lines ~478–509) and replace the entire contents of the `<section class="exec-summary">` (everything after `<h2>At a Glance</h2>`) with:

```html
<div class="glance-layout">
  <!-- LEFT: Radar chart -->
  <div class="radar-wrap">
    <div class="radar-title">Marketing Function Score</div>
    <canvas id="radarChart" width="400" height="400"></canvas>
  </div>

  <!-- RIGHT: Metric cards -->
  <div class="radar-cards">
    <div class="summary-card">
      <div class="metric-label">Domain Authority</div>
      <div class="metric-value green" data-count="98" data-suffix=" / 100">98 / 100</div>
      <div class="metric-context">Only google.com sits higher. Extraordinary for a single-product company.</div>
    </div>
    <div class="summary-card">
      <div class="metric-label">Organic Traffic Value</div>
      <div class="metric-value green" data-count="9.06" data-prefix="$" data-suffix="M">$9.06M</div>
      <div class="metric-context">Equivalent paid cost of organic traffic — achieved on near-zero ad spend.</div>
    </div>
    <div class="summary-card">
      <div class="metric-label">Traffic Concentration</div>
      <div class="metric-value red" data-count="67.1" data-suffix="%">67.1%</div>
      <div class="metric-context">Share of organic traffic flowing to /translator pages alone. No blog or content page ranks in the top 100.</div>
    </div>
    <div class="summary-card">
      <div class="metric-label">Paid Search Keywords</div>
      <div class="metric-value red" data-count="7">7</div>
      <div class="metric-context">Total paid keywords. $13 in spend. No safety net if organic positions shift.</div>
    </div>
    <div class="summary-card">
      <div class="metric-label">AI Mentions</div>
      <div class="metric-value amber" data-count="76.6" data-suffix="K">76.6K</div>
      <div class="metric-context">Across Google AI Overviews, AI Mode, and Gemini — but converting to ~0% referral traffic.</div>
    </div>
    <div class="summary-card">
      <div class="metric-label">Keyword Trajectory</div>
      <div class="metric-value red" data-count="10" data-prefix="−" data-suffix="%">−10%</div>
      <div class="metric-context">Decline in organic keyword count, with a −3.3% drop in traffic. Heading the wrong direction pre-IPO.</div>
    </div>
  </div>
</div>
```

**Step 4: Visual check in browser**

Open `deepl-marketing-snapshot.html` in a browser. At a Glance should now show a two-column layout — left column empty (canvas not yet initialised), right column has the 6 metric cards. No broken layout elsewhere.

**Step 5: Commit**

```bash
git add "deepl-marketing-snapshot.html"
git commit -m "feat: restructure At a Glance layout for radar chart"
```

---

### Task 2: Initialise the radar chart

**Files:**
- Modify: `deepl-marketing-snapshot.html` (add `<script>` block before `</body>`)

**Step 1: Add the script block**

Before the closing `</body>` tag (after the closing `</div>` of `.container`), add:

```html
<script>
// ============================================================
// RADAR CHART
// ============================================================
(function () {
  const ctx = document.getElementById('radarChart').getContext('2d');

  const labels = ['Search', 'Content', 'Brand', 'AI Discovery', 'Reputation', 'Social'];
  const scores = [8, 2, 4, 5, 5, 4];

  new Chart(ctx, {
    type: 'radar',
    data: {
      labels,
      datasets: [{
        data: scores,
        backgroundColor: 'rgba(96,165,250,0.10)',
        borderColor: '#60A5FA',
        borderWidth: 2,
        pointBackgroundColor: '#60A5FA',
        pointBorderColor: 'transparent',
        pointRadius: 4,
        pointHoverRadius: 6,
      }]
    },
    options: {
      animation: {
        duration: 1000,
        easing: 'easeInOutQuart',
      },
      scales: {
        r: {
          min: 0,
          max: 10,
          ticks: {
            stepSize: 2,
            display: false,
          },
          grid: {
            color: '#252A36',
          },
          angleLines: {
            color: '#252A36',
          },
          pointLabels: {
            color: '#8B8F9C',
            font: {
              family: "'DM Sans', sans-serif",
              size: 12,
            },
          },
        },
      },
      plugins: {
        legend: { display: false },
        tooltip: { enabled: false },
      },
    },
  });
})();
</script>
```

**Step 2: Visual check in browser**

Refresh the page. The radar chart should draw itself in ~1 second on load. The shape should spike high on "Search" and be flat everywhere else. The dark grid lines, blue fill, and DM Sans labels should match the page aesthetic.

**Step 3: Commit**

```bash
git add "deepl-marketing-snapshot.html"
git commit -m "feat: add animated radar chart to At a Glance section"
```

---

### Task 3: Add CSS animation classes

**Files:**
- Modify: `deepl-marketing-snapshot.html` (style block)

**Step 1: Add animation CSS**

Add to the `<style>` block, before the closing `</style>` tag:

```css
/* ============================================================
   SCROLL ANIMATIONS
   ============================================================ */

/* Base state — invisible until JS triggers */
.anim-fade-up {
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 0.5s ease-out, transform 0.5s ease-out;
}

.anim-fade-left {
  opacity: 0;
  transform: translateX(-16px);
  transition: opacity 0.5s ease-out, transform 0.5s ease-out;
}

/* Visible state added by JS */
.anim-fade-up.is-visible,
.anim-fade-left.is-visible {
  opacity: 1;
  transform: none;
}

/* Stagger delays for child elements */
.anim-stagger > *:nth-child(1) { transition-delay: 0ms; }
.anim-stagger > *:nth-child(2) { transition-delay: 60ms; }
.anim-stagger > *:nth-child(3) { transition-delay: 120ms; }
.anim-stagger > *:nth-child(4) { transition-delay: 180ms; }
.anim-stagger > *:nth-child(5) { transition-delay: 240ms; }
.anim-stagger > *:nth-child(6) { transition-delay: 300ms; }

/* Bar fill animation — JS sets --bar-target and triggers .bar-animate */
.bar-fill {
  width: 0 !important;
  transition: width 0.7s ease-out;
}

.bar-fill.bar-animate {
  width: var(--bar-target) !important;
}

/* Reduced motion — skip all transitions */
@media (prefers-reduced-motion: reduce) {
  .anim-fade-up,
  .anim-fade-left {
    opacity: 1;
    transform: none;
    transition: none;
  }
  .bar-fill {
    width: var(--bar-target) !important;
    transition: none;
  }
}
```

**Step 2: Visual check**

Refresh the page. Everything should now be **invisible** (all the cards, bars, headings are gone). That's correct — JS hasn't run yet to add `.is-visible`. If you see content missing and no JS errors in the console, the CSS is correct.

Wait — actually, the JS hasn't been added yet so `.is-visible` won't be added. To avoid a broken page before the next task, temporarily add the JS. Actually, since the JS will be added in Task 4 immediately after, this is fine as a brief intermediate state. Just verify no CSS parse errors in DevTools and move on.

**Step 3: Commit**

```bash
git add "deepl-marketing-snapshot.html"
git commit -m "feat: add animation CSS classes and bar fill transition"
```

---

### Task 4: Add IntersectionObserver scroll triggers

**Files:**
- Modify: `deepl-marketing-snapshot.html` (script block)

**Step 1: Add the animation classes to HTML elements**

Find and update these elements in the HTML (search for each class):

- `.pillar-header` → add `anim-fade-up`
- `.verdict` → add `anim-fade-left`
- `.data-grid` → add `anim-stagger`; each `.data-cell` inside → add `anim-fade-up`
- `.radar-cards` → add `anim-stagger`; each `.summary-card` inside → add `anim-fade-up`
- `.review-grid` → add `anim-stagger`; each `.review-card` inside → add `anim-fade-up`
- `.two-col` (each instance) → add `anim-stagger`; each `.finding` inside → add `anim-fade-up`
- `.callout` → add `anim-fade-up`
- `.radar-wrap` → add `anim-fade-up`

**Step 2: Add IntersectionObserver JS**

Inside the `<script>` block (after the radar chart IIFE), add:

```js
// ============================================================
// SCROLL ANIMATIONS
// ============================================================
(function () {
  // Skip if reduced motion
  if (window.matchMedia('(prefers-reduced-motion: reduce)').matches) return;

  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('is-visible');
        observer.unobserve(entry.target);
      }
    });
  }, { threshold: 0.15 });

  document.querySelectorAll('.anim-fade-up, .anim-fade-left').forEach(el => {
    observer.observe(el);
  });
})();
```

**Step 3: Visual check**

Refresh the page. Scroll down slowly. Each section's elements should fade in as they enter the viewport. Cards should cascade in with slight stagger. Verdict banners should slide in from the left. Nothing should be permanently invisible.

**Step 4: Commit**

```bash
git add "deepl-marketing-snapshot.html"
git commit -m "feat: add IntersectionObserver scroll-triggered fade animations"
```

---

### Task 5: Animate bar fills on scroll

**Files:**
- Modify: `deepl-marketing-snapshot.html`

**Step 1: Move bar widths from inline style to data attribute**

Find every `.bar-fill` element. Each has an inline `style="width: X%;"`. Change each one:

- Remove `style="width: X%;"`
- Add `data-width="X%"` and `style="--bar-target: X%;"` (CSS custom property for the transition target)

Example — before:
```html
<div class="bar-fill blue-fill" style="width: 37.25%;">37.3%</div>
```
After:
```html
<div class="bar-fill blue-fill" style="--bar-target: 37.25%;" data-width="37.25%">37.3%</div>
```

There are 8 bar fills total across the page (5 in Search Performance, 3 in Brand Positioning). Update all of them.

**Step 2: Add bar animation JS**

Inside the `<script>` block (after the scroll animations IIFE), add:

```js
// ============================================================
// BAR FILL ANIMATIONS
// ============================================================
(function () {
  const reduced = window.matchMedia('(prefers-reduced-motion: reduce)').matches;

  const bars = document.querySelectorAll('.bar-fill');

  if (reduced) {
    // Restore widths immediately for reduced motion
    bars.forEach(bar => {
      bar.style.setProperty('--bar-target', bar.dataset.width);
    });
    return;
  }

  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('bar-animate');
        observer.unobserve(entry.target);
      }
    });
  }, { threshold: 0.3 });

  bars.forEach(bar => observer.observe(bar));
})();
```

**Step 3: Visual check**

Refresh and scroll to the Search Performance section. The bar chart should start with all bars at zero width, then animate to their final values as you scroll them into view. The nearly-empty bars (0%, 0.65%, 0.82%) should make their smallness more dramatic than the static version.

**Step 4: Commit**

```bash
git add "deepl-marketing-snapshot.html"
git commit -m "feat: animate bar fills on scroll via IntersectionObserver"
```

---

### Task 6: Count-up animation for numeric values

**Files:**
- Modify: `deepl-marketing-snapshot.html` (script block only)

**Step 1: Add count-up JS**

Inside the `<script>` block (after the bar fill IIFE), add:

```js
// ============================================================
// COUNT-UP ANIMATION
// ============================================================
(function () {
  if (window.matchMedia('(prefers-reduced-motion: reduce)').matches) return;

  function animateCount(el) {
    const target = parseFloat(el.dataset.count);
    const prefix = el.dataset.prefix || '';
    const suffix = el.dataset.suffix || '';
    const duration = 800;
    const isDecimal = String(target).includes('.');
    const decimals = isDecimal ? (String(target).split('.')[1] || '').length : 0;

    const start = performance.now();

    function tick(now) {
      const elapsed = now - start;
      const progress = Math.min(elapsed / duration, 1);
      // easeOutCubic
      const eased = 1 - Math.pow(1 - progress, 3);
      const current = target * eased;
      el.textContent = prefix + current.toFixed(decimals) + suffix;
      if (progress < 1) requestAnimationFrame(tick);
    }

    requestAnimationFrame(tick);
  }

  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        animateCount(entry.target);
        observer.unobserve(entry.target);
      }
    });
  }, { threshold: 0.5 });

  // Observe all elements with data-count attribute
  document.querySelectorAll('[data-count]').forEach(el => observer.observe(el));
})();
```

**Step 2: Add `data-count` attributes to review scores**

The review score elements in Pillar 5 don't have `data-count` yet (only the At a Glance cards do from Task 1). Update each `.score` element:

```html
<!-- Before -->
<div class="score green">4.6</div>

<!-- After -->
<div class="score green" data-count="4.6">4.6</div>
```

Do this for all 5 review cards (G2: 4.6, Capterra: 4.7, Gartner: 4.7, App Store: 4.8, Trustpilot: 1.8).

Also add to `.cell-value` elements in data grids (the ones with JetBrains Mono numeric values). Examples:
- `592,867` → not a simple float, skip (leave static)
- `11.5M` → `data-count="11.5" data-suffix="M"`
- `8.0M` → `data-count="8.0" data-suffix="M"`
- `$13` → `data-count="13" data-prefix="$"`
- `29.8K` → `data-count="29.8" data-suffix="K"`
- `20K` → `data-count="20" data-suffix="K"`
- `17.6K` → `data-count="17.6" data-suffix="K"`
- `~1%` → skip (has tilde, leave static)
- `102` → `data-count="102"`
- `2.25K` → `data-count="2.25" data-suffix="K"`
- `~3,500` → skip (has tilde, leave static)
- `4` → `data-count="4"`

**Step 3: Visual check**

Scroll to the At a Glance section (or just load the page — it's near the top). The metric values should tick up from 0 to their final values when they come into view. Check: `98 / 100` should count up the `98` while keeping `/ 100` static. Check: `−10%` should count up `10` while keeping `−` and `%` static. Check: `$9.06M` should count up `9.06` while keeping `$` and `M` static.

**Step 4: Commit**

```bash
git add "deepl-marketing-snapshot.html"
git commit -m "feat: add count-up animation to numeric metric values"
```

---

### Task 7: Final visual review and cleanup

**Step 1: Full page scroll test**

Open the page and scroll from top to bottom at a moderate pace. Check:
- [ ] Radar chart draws itself on load
- [ ] At a Glance metric values count up
- [ ] Pillar headers fade up as they enter view
- [ ] Verdict banners slide in from left
- [ ] Data cells and summary cards cascade in with stagger
- [ ] Bar fills animate from 0 to target on scroll
- [ ] Review cards cascade in with stagger
- [ ] Findings fade up in pairs
- [ ] Callout boxes fade up
- [ ] No elements permanently invisible
- [ ] No console errors

**Step 2: Reduced motion test**

In DevTools > Rendering > "Emulate CSS media feature prefers-reduced-motion: reduce". Reload. All content should be immediately visible, bars should be at their correct widths, no animations should play.

**Step 3: Mobile check**

Resize browser to 375px wide. Check:
- At a Glance layout stacks vertically (radar on top, cards below)
- Radar chart is readable at small size
- Bar charts still work

**Step 4: Final commit**

```bash
git add "deepl-marketing-snapshot.html"
git commit -m "feat: complete charts and animations — radar, count-up, scroll triggers"
```
