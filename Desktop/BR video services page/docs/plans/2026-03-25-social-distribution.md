# Social & Distribution Page Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Build `social-distribution.html` — a Branch Road service page with three service sections: organic social, paid social & PPC, and campaign tracking & performance reporting.

**Architecture:** Single self-contained HTML file built from `demand-generation.html` as a template. Three service sections, all on dark background (no light section variant). Alternating layout: Section 2 copy-left/visual-right, Section 3 flipped, Section 4 copy-left/visual-right. All CSS, nav, hero, CTA, scroll-reveal animations, and responsive breakpoints identical to the template.

**Tech Stack:** HTML5, CSS (custom properties), vanilla JS. Google Fonts (Outfit).

**Reference file:** `demand-generation.html` — copy in full, then update content only.

---

### Task 1: Scaffold from template

**Files:**
- Create: `social-distribution.html`

**Step 1: Copy demand-generation.html as starting point**

```bash
cp demand-generation.html social-distribution.html
```

**Step 2: Update head meta tags**

Change only these values:

```html
<title>Social & Distribution for B2B Tech | Branch Road Media</title>
<meta name="description" content="Organic social, paid social, PPC, and campaign tracking for B2B tech companies. Organic and paid that pull in the same direction.">
```

Update OG/Twitter titles and descriptions to match. Keep all TODO placeholders.

**Step 3: Update nav active link**

```html
<li><a href="/demand-generation">Demand Gen</a></li>
<li><a href="/social-distribution" aria-current="page">Social</a></li>
```

**Step 4: Commit**

```bash
git add social-distribution.html
git commit -m "feat: scaffold social-distribution page from demand-generation template"
```

---

### Task 2: Update hero section

**Files:**
- Modify: `social-distribution.html`

**Step 1: Replace hero copy**

Find `.hero-copy` and replace its contents:

```html
<div class="hero-copy">
  <span class="eyebrow">Social &amp; Distribution</span>
  <h1>Social and paid that <em>pull in the same direction</em></h1>
  <p class="hero-sub">Most B2B social generates likes from competitors and reports that explain what happened. We connect organic and paid to a single narrative, track what matters, and tell you what to do next.</p>
  <div style="display:flex;gap:12px;flex-wrap:wrap;">
    <a href="#contact" class="btn-primary">Start a conversation</a>
    <a href="#what-we-make" class="btn-secondary">See what we do</a>
  </div>
</div>
```

**Step 2: Replace hero placeholder card**

```html
<div class="hero-card-placeholder">
  <div class="hero-card-placeholder-icon">
    <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><path d="M18 20V10M12 20V4M6 20v-6"/></svg>
  </div>
  <h3>Campaign planner</h3>
  <p>Map your organic and paid activity to a single narrative and timeline.</p>
  <span class="hero-card-placeholder-badge">Coming soon</span>
</div>
```

**Step 3: Commit**

```bash
git add social-distribution.html
git commit -m "feat: update hero for social-distribution page"
```

---

### Task 3: Add Section 2 — Organic social

**Files:**
- Modify: `social-distribution.html`

**Step 1: Delete all four existing service sections**

Remove everything from `<!-- ── SECTION 2 -->` through to the closing `</section>` of the last service section (before the CTA). Leave hero and CTA intact.

**Step 2: Add Section 2**

```html
  <!-- ── SECTION 2: Organic social ── -->
  <section class="block" id="what-we-make">
    <div class="container">
      <div class="service-section">
        <div class="service-copy reveal">
          <p class="section-label">Organic social</p>
          <h2>A presence <em>worth following</em></h2>
          <p>Organic social that exists to fill a calendar doesn't build pipeline. We build a presence around a clear point of view — content that reaches the right people and gives them a reason to engage.</p>
          <div class="output-pills">
            <span class="output-pill">Content strategy</span>
            <span class="output-pill">LinkedIn presence</span>
            <span class="output-pill">Executive social</span>
            <span class="output-pill">Community management</span>
            <span class="output-pill">Social copywriting</span>
            <span class="output-pill">Content calendar</span>
          </div>
        </div>
        <div class="service-visual reveal reveal-delay-1">
          <span class="service-visual-label">Example output</span>
          <p class="service-visual-title">LinkedIn content programme</p>
          <p class="service-visual-body">A consistent, POV-driven presence built around your narrative, not just company updates. Content that earns attention from buyers, not just peers.</p>
          <div class="service-visual-tags">
            <span class="service-visual-tag">POV-driven</span>
            <span class="service-visual-tag">Executive-led</span>
            <span class="service-visual-tag">Pipeline-focused</span>
          </div>
        </div>
      </div>
    </div>
  </section>
```

**Step 3: Commit**

```bash
git add social-distribution.html
git commit -m "feat: add organic social section to social-distribution page"
```

---

### Task 4: Add Section 3 — Paid social & PPC

**Files:**
- Modify: `social-distribution.html`

**Step 1: Add after the organic social closing `</section>`**

```html
  <!-- ── SECTION 3: Paid social & PPC ── -->
  <section class="block">
    <div class="container">
      <div class="service-section" style="direction: rtl;">
        <div class="service-copy reveal" style="direction: ltr;">
          <p class="section-label">Paid social &amp; PPC</p>
          <h2>Spend that <em>earns its place</em></h2>
          <p>Paid without a narrative is just noise with a budget. We run campaigns built around the same story as your organic — targeted at the right audience, at the right stage, with creative that doesn't look like an ad.</p>
          <div class="output-pills">
            <span class="output-pill">LinkedIn ads</span>
            <span class="output-pill">Paid social</span>
            <span class="output-pill">PPC</span>
            <span class="output-pill">Audience targeting</span>
            <span class="output-pill">Ad creative</span>
            <span class="output-pill">A/B testing</span>
            <span class="output-pill">Retargeting</span>
          </div>
        </div>
        <div class="service-visual reveal reveal-delay-1" style="direction: ltr;">
          <span class="service-visual-label">Example output</span>
          <p class="service-visual-title">Demand gen campaign</p>
          <p class="service-visual-body">A paid programme tied directly to your content narrative, not running parallel to it. Same message, right audience, right stage.</p>
          <div class="service-visual-tags">
            <span class="service-visual-tag">Narrative-aligned</span>
            <span class="service-visual-tag">Stage-targeted</span>
            <span class="service-visual-tag">Creative-led</span>
          </div>
        </div>
      </div>
    </div>
  </section>
```

**Step 2: Commit**

```bash
git add social-distribution.html
git commit -m "feat: add paid social section to social-distribution page"
```

---

### Task 5: Add Section 4 — Campaign tracking & performance reporting

**Files:**
- Modify: `social-distribution.html`

**Step 1: Add after the paid social closing `</section>`**

```html
  <!-- ── SECTION 4: Campaign tracking & performance reporting ── -->
  <section class="block">
    <div class="container">
      <div class="service-section">
        <div class="service-copy reveal">
          <p class="section-label">Campaign tracking &amp; performance reporting</p>
          <h2>Measurement that tells you <em>what to do next</em></h2>
          <p>Most reporting tells you what happened. We build tracking frameworks that tell you why — and what to change. Attribution that connects spend to pipeline, not just clicks.</p>
          <div class="output-pills">
            <span class="output-pill">Campaign tracking</span>
            <span class="output-pill">UTM framework</span>
            <span class="output-pill">Attribution modelling</span>
            <span class="output-pill">Dashboard setup</span>
            <span class="output-pill">Performance reporting</span>
            <span class="output-pill">Channel analysis</span>
          </div>
        </div>
        <div class="service-visual reveal reveal-delay-1">
          <span class="service-visual-label">Example output</span>
          <p class="service-visual-title">Performance dashboard</p>
          <p class="service-visual-body">A live view of what's working across organic and paid, built to inform decisions not justify spend. Connected to pipeline, not just impressions.</p>
          <div class="service-visual-tags">
            <span class="service-visual-tag">Pipeline-connected</span>
            <span class="service-visual-tag">Cross-channel</span>
            <span class="service-visual-tag">Decision-ready</span>
          </div>
        </div>
      </div>
    </div>
  </section>
```

**Step 2: Commit**

```bash
git add social-distribution.html
git commit -m "feat: add tracking and reporting section to social-distribution page"
```

---

### Task 6: Update CTA section

**Files:**
- Modify: `social-distribution.html`

**Step 1: Replace CTA content**

```html
<div class="cta">
  <h2>Ready to make your distribution <em>work harder?</em></h2>
  <p>Tell us what you're running. We'll show you what's missing.</p>
  <div class="cta-actions">
    <a href="mailto:hello@branchroad.media" class="btn-primary">Start a conversation</a>
    <a href="/" class="btn-secondary">See all services</a>
  </div>
</div>
```

**Step 2: Commit**

```bash
git add social-distribution.html
git commit -m "feat: update CTA for social-distribution page"
```

---

### Task 7: Visual review checklist

Open `social-distribution.html` in a browser and verify:

- [ ] Nav is fixed; "Social" link has active underline state
- [ ] Hero headline reads "Social and paid that pull in the same direction" with "pull in the same direction" in accent colour
- [ ] Placeholder card shows campaign planner copy with "Coming soon" badge
- [ ] Three service sections render in order: Organic social → Paid social & PPC → Tracking & reporting
- [ ] Section 2 and 4: copy left, visual right
- [ ] Section 3: copy right, visual left (flipped)
- [ ] All sections on dark background — no light section
- [ ] Output pills wrap correctly on narrow screens
- [ ] Scroll reveal animations fire as sections enter viewport
- [ ] CTA renders correctly after Section 4
- [ ] Mobile nav opens/closes at <640px
- [ ] No demand-generation copy remains anywhere on the page

**Step 1: Fix any issues found, then commit**

```bash
git add social-distribution.html
git commit -m "feat: social-distribution page complete — visual review passed"
```

---

## Done

The page is complete when all 7 tasks are committed and the visual review checklist passes.
