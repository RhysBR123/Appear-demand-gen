# DeepL Snapshot — Charts & Animations Design

**Date:** 2026-03-24
**File:** `deepl-marketing-snapshot.html`
**Approach:** Chart.js (CDN) + vanilla IntersectionObserver

---

## Goals

1. Add a radar chart to the At a Glance section giving the reader an immediate "overall standing" at a single glance
2. Add polished, credibility-signalling micro-animations throughout the page
3. Keep the page a single self-contained HTML file

---

## At a Glance — Radar Chart

### Layout

Two-column layout within the `exec-summary` section:
- **Left column:** Radar chart (Chart.js), draws itself on page load (~1s animation)
- **Right column:** The 6 existing metric cards (with count-up animations added)

### Radar Axes & Scores (out of 10)

| Pillar | Score | Rationale |
|---|---|---|
| Search | 8 | Extraordinary authority + $9M traffic value, but −10% keyword decline |
| Content | 2 | Zero blog/content pages ranking; invisible in search |
| Brand | 4 | Market sees a translation tool, not a Language AI platform |
| AI Discoverability | 5 | 76.6K mentions, ~1% traffic conversion |
| Reputation | 5 | Product scores 4.6–4.8 vs Trustpilot 1.8/5 |
| Social | 4 | LinkedIn strong (450K+), everything else low-scale |

### Chart.js Config

- Load via CDN `<script>` tag (no npm)
- Dark theme: background fill `rgba(96,165,250,0.08)`, border `#60A5FA`, grid lines `--border` colour
- `animation.duration: 1000`, `easing: 'easeInOutQuart'`
- Tooltips disabled (data is self-explanatory)
- Point labels styled in `DM Sans` to match the page font

---

## Page-wide Animations

All powered by `IntersectionObserver` with `threshold: 0.15`. Elements start invisible (`opacity: 0`) and animate to final state when entering the viewport.

### CSS classes added

| Class | Animation | Duration |
|---|---|---|
| `.anim-fade-up` | opacity 0→1, translateY 20px→0 | 0.5s ease-out |
| `.anim-fade-left` | opacity 0→1, translateX −16px→0 | 0.5s ease-out |
| `.anim-stagger` | applied to parent; children get sequential `animation-delay` in 60ms increments | — |

### Elements animated

| Element | Animation | Notes |
|---|---|---|
| `.pillar-header` | fade-up | — |
| `.verdict` | fade-left | Matches the left-border design language |
| `.summary-card` | fade-up + stagger | Cards cascade in 60ms apart |
| `.data-cell` | fade-up + stagger | — |
| `.review-card` | fade-up + stagger | — |
| `.finding` | fade-up + stagger | Two-column pairs |
| `.callout` | fade-up | — |
| `.bar-fill` | width 0 → target on scroll | 0.7s ease-out; target stored in `data-width` attribute |

### Count-up animation

Applied to: `.metric-value`, `.cell-value`, `.score` (review cards)

- Parse the numeric portion of the text content (handling prefixes like `$`, `−`, suffixes like `M`, `K`, `%`, `/ 100`)
- Animate from 0 to final value over 800ms using `requestAnimationFrame`
- Non-numeric text values are left static

### Not animated

- Prose paragraphs, table rows, the page header, finding body text — keeps the "serious analytical document" feel

---

## Implementation Notes

- Bar fill widths must be moved from inline `style="width: X%"` to `data-width="X%"` before JS runs, so bars start at 0 and animate in
- `prefers-reduced-motion` media query: if set, skip all JS animations and restore static widths immediately
- Chart.js loaded from `https://cdn.jsdelivr.net/npm/chart.js` (latest stable)
- All JS in a single `<script>` block at the bottom of `<body>`, after the Chart.js CDN tag
