# Brand & Positioning Page Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Build `brand-positioning.html` — a Branch Road service page for Brand & Positioning with three service-area sections (Journey audit, Brand narrative & messaging, GTM), each with a bold headline, copy, output pills, and an example card.

**Architecture:** Single self-contained HTML file, identical structure and CSS to `demand-generation.html`. Three service sections instead of four. Same nav, hero placeholder card, output pills, service visual cards, CTA, scroll-reveal animations, and responsive breakpoints. No framework, no build step.

**Tech Stack:** HTML5, CSS (custom properties), vanilla JS. Google Fonts (Outfit).

**Reference file:** `demand-generation.html` — copy all CSS verbatim, only change content and the number of sections.

---

### Task 1: Scaffold the file — head, CSS, nav HTML

**Files:**
- Create: `brand-positioning.html`

**Step 1: Copy `demand-generation.html` in full as the starting point**

```bash
cp demand-generation.html brand-positioning.html
```

**Step 2: Update head meta tags**

Change these values only — leave all other head content identical:

- `<title>` → `Brand & Positioning for B2B Tech | Branch Road Media`
- `<meta name="description">` → `Brand strategy, narrative, messaging, and GTM for B2B tech companies. Positioning built to move buyers, not just look good.`
- `<link rel="canonical">` → keep TODO placeholder
- OG/Twitter meta titles → `Brand & Positioning for B2B Tech | Branch Road Media`
- OG/Twitter meta descriptions → `Brand strategy and positioning that earns its place in market. Journey audit, narrative, messaging frameworks, and GTM activation for B2B tech.`

**Step 3: Update nav active link**

Change:
```html
<li><a href="/demand-generation" aria-current="page">Demand Gen</a></li>
```
To:
```html
<li><a href="/demand-generation">Demand Gen</a></li>
<li><a href="/brand-positioning" aria-current="page">Brand</a></li>
```

**Step 4: Commit**

```bash
git add brand-positioning.html
git commit -m "feat: scaffold brand-positioning page from demand-generation template"
```

---

### Task 2: Update hero section

**Files:**
- Modify: `brand-positioning.html`

**Step 1: Replace hero HTML content**

Find the `<section class="hero">` block and replace the `.hero-copy` contents:

```html
<div class="hero-copy">
  <span class="eyebrow">Brand &amp; Positioning</span>
  <h1>Brand &amp; positioning <em>built to move</em></h1>
  <p class="hero-sub">Most brand investment misses — not because the work is bad, but because it starts in the wrong place. We begin with who you're talking to, what you're up against, and where you're trying to go.</p>
  <div style="display:flex;gap:12px;flex-wrap:wrap;">
    <a href="#contact" class="btn-primary">Start a conversation</a>
    <a href="#what-we-make" class="btn-secondary">See how we work</a>
  </div>
</div>
```

**Step 2: Replace hero placeholder card content**

Find `.hero-card-placeholder` and update:

```html
<div class="hero-card-placeholder">
  <div class="hero-card-placeholder-icon">
    <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="3"/><path d="M12 2v3M12 19v3M4.22 4.22l2.12 2.12M17.66 17.66l2.12 2.12M2 12h3M19 12h3M4.22 19.78l2.12-2.12M17.66 6.34l2.12-2.12"/></svg>
  </div>
  <h3>Positioning diagnostic</h3>
  <p>An interactive tool to map your current position and surface the gaps.</p>
  <span class="hero-card-placeholder-badge">Coming soon</span>
</div>
```

**Step 3: Commit**

```bash
git add brand-positioning.html
git commit -m "feat: update hero for brand-positioning page"
```

---

### Task 3: Replace service sections — Journey audit

**Files:**
- Modify: `brand-positioning.html`

**Step 1: Delete all four existing service sections**

Remove everything between `<!-- ── SECTION 2 -->` and the closing `</section>` of the Customer advocacy section (section 5 in demand-generation.html). Leave the hero and CTA intact.

**Step 2: Add Section 2 — Journey audit**

```html
  <!-- ── SECTION 2: Journey audit ── -->
  <section class="block" id="what-we-make">
    <div class="container">
      <div class="service-section">
        <div class="service-copy reveal">
          <p class="section-label">Journey audit</p>
          <h2>Know where you stand <em>before you move</em></h2>
          <p>Most brand work starts with a blank page. We start with a thorough read of where you are — your current positioning, your audience, your competitors, and the gaps between them. So the narrative we build is grounded in reality, not assumption.</p>
          <div class="output-pills">
            <span class="output-pill">Positioning audit</span>
            <span class="output-pill">Audience mapping</span>
            <span class="output-pill">Competitor analysis</span>
            <span class="output-pill">Message gap assessment</span>
            <span class="output-pill">Stakeholder interviews</span>
          </div>
        </div>
        <div class="service-visual reveal reveal-delay-1">
          <span class="service-visual-label">Example output</span>
          <p class="service-visual-title">Positioning audit</p>
          <p class="service-visual-body">A structured read of where your brand sits relative to competitors — what's working, what's not, and where the white space is. The foundation everything else is built on.</p>
          <div class="service-visual-tags">
            <span class="service-visual-tag">Research-led</span>
            <span class="service-visual-tag">Competitor mapped</span>
            <span class="service-visual-tag">Gap analysis</span>
          </div>
        </div>
      </div>
    </div>
  </section>
```

**Step 3: Commit**

```bash
git add brand-positioning.html
git commit -m "feat: add journey audit section to brand-positioning page"
```

---

### Task 4: Add Section 3 — Brand narrative & messaging

**Files:**
- Modify: `brand-positioning.html`

**Step 1: Add after the Journey audit closing `</section>`**

```html
  <!-- ── SECTION 3: Brand narrative & messaging ── -->
  <section class="block">
    <div class="container">
      <div class="service-section" style="direction: rtl;">
        <div class="service-copy reveal" style="direction: ltr;">
          <p class="section-label">Brand narrative &amp; messaging</p>
          <h2>A story that earns its <em>place in market</em></h2>
          <p>We build brand narratives around a clear, defensible position — not a list of features dressed up as values. Copy that speaks to the right level, in the right voice, with a point of view buyers actually remember.</p>
          <div class="output-pills">
            <span class="output-pill">Brand narrative</span>
            <span class="output-pill">Messaging framework</span>
            <span class="output-pill">Value proposition</span>
            <span class="output-pill">Tone of voice</span>
            <span class="output-pill">Website copy</span>
            <span class="output-pill">Campaign messaging</span>
          </div>
        </div>
        <div class="service-visual reveal reveal-delay-1" style="direction: ltr;">
          <span class="service-visual-label">Example output</span>
          <p class="service-visual-title">Messaging framework</p>
          <p class="service-visual-body">A single document that aligns sales, marketing, and leadership on what you say, how you say it, and who you're saying it to. Built to be used in decks, on websites, and in the room.</p>
          <div class="service-visual-tags">
            <span class="service-visual-tag">Sales-aligned</span>
            <span class="service-visual-tag">Audience-specific</span>
            <span class="service-visual-tag">Campaign-ready</span>
          </div>
        </div>
      </div>
    </div>
  </section>
```

**Step 2: Commit**

```bash
git add brand-positioning.html
git commit -m "feat: add brand narrative section to brand-positioning page"
```

---

### Task 5: Add Section 4 — GTM

**Files:**
- Modify: `brand-positioning.html`

**Step 1: Add after the Brand narrative closing `</section>`**

```html
  <!-- ── SECTION 4: GTM ── -->
  <section class="block">
    <div class="container">
      <div class="service-section">
        <div class="service-copy reveal">
          <p class="section-label">Go-to-market</p>
          <h2>Built to be used, <em>not just approved</em></h2>
          <p>Brand work that stays in a deck doesn't move the needle. We wire positioning into your go-to-market — so your sales team, your content, and your campaigns all pull in the same direction from day one.</p>
          <div class="output-pills">
            <span class="output-pill">GTM playbook</span>
            <span class="output-pill">Sales messaging</span>
            <span class="output-pill">Launch content</span>
            <span class="output-pill">Campaign framework</span>
            <span class="output-pill">Channel strategy</span>
          </div>
        </div>
        <div class="service-visual reveal reveal-delay-1">
          <span class="service-visual-label">Example output</span>
          <p class="service-visual-title">GTM playbook</p>
          <p class="service-visual-body">The bridge between brand narrative and execution. What to say in each channel, to each audience, at each stage — so launch day has a spine, not just a deadline.</p>
          <div class="service-visual-tags">
            <span class="service-visual-tag">Channel-specific</span>
            <span class="service-visual-tag">Stage-mapped</span>
            <span class="service-visual-tag">Launch-ready</span>
          </div>
        </div>
      </div>
    </div>
  </section>
```

**Step 2: Commit**

```bash
git add brand-positioning.html
git commit -m "feat: add GTM section to brand-positioning page"
```

---

### Task 6: Update CTA section

**Files:**
- Modify: `brand-positioning.html`

**Step 1: Replace CTA content**

Find the `<section class="cta-section"` block and update the inner `.cta` div:

```html
<div class="cta">
  <h2>Ready to build a brand that <em>knows what it's for?</em></h2>
  <p>Tell us where you are. We'll start with what we'd need to understand before writing a word.</p>
  <div class="cta-actions">
    <a href="mailto:hello@branchroad.media" class="btn-primary">Start a conversation</a>
    <a href="/" class="btn-secondary">See all services</a>
  </div>
</div>
```

**Step 2: Commit**

```bash
git add brand-positioning.html
git commit -m "feat: update CTA for brand-positioning page"
```

---

### Task 7: Visual review checklist

Open `brand-positioning.html` in a browser and verify:

- [ ] Nav is fixed; "Brand" link has active underline state
- [ ] Hero headline reads "Brand & positioning built to move" with "built to move" in accent colour
- [ ] Placeholder card shows positioning diagnostic copy and "Coming soon" badge
- [ ] Three service sections render in order: Journey audit → Brand narrative → GTM
- [ ] Sections 2 and 4 have copy left / visual right; Section 3 flips (copy right / visual left)
- [ ] Output pills wrap correctly on narrow screens
- [ ] Scroll reveal animations fire as sections enter viewport
- [ ] CTA renders with gradient and correct headline
- [ ] Mobile nav opens/closes at <640px
- [ ] No demand-generation copy remains anywhere on the page

**Step 1: Fix any issues found, then commit**

```bash
git add brand-positioning.html
git commit -m "feat: brand-positioning page complete — visual review passed"
```

---

## Done

The page is complete when all 7 tasks are committed and the visual review checklist passes.
