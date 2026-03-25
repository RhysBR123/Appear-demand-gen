# Search & Visibility Page Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Build `search-visibility.html` — a Branch Road service page with two visually contrasting sections: traditional search (dark background) and AI & answer engines (light `#EAFFFD` background).

**Architecture:** Single self-contained HTML file built from `demand-generation.html` as a template. Two service sections instead of four. Key difference from other pages: Section 3 uses the light background variant (`--bg-light`, `--text-dark`, `--accent-dark`) requiring CSS overrides for text, pills, and the service visual card. All other CSS, nav, hero, CTA, and JS are identical to the template.

**Tech Stack:** HTML5, CSS (custom properties), vanilla JS. Google Fonts (Outfit).

**Reference files:**
- `demand-generation.html` — base template (copy in full)
- `explainer-video-production.html` lines ~455–470 — `.process-wrapper` shows the light section CSS pattern to follow

---

### Task 1: Scaffold from template

**Files:**
- Create: `search-visibility.html`

**Step 1: Copy demand-generation.html as starting point**

```bash
cp demand-generation.html search-visibility.html
```

**Step 2: Update head meta tags**

Change only these values:

```html
<title>Search & Visibility for B2B Tech | Branch Road Media</title>
<meta name="description" content="SEO, website optimisation, AI search, LLM citations, and answer engine optimisation for B2B tech companies. Be found where buyers are looking.">
```

Update OG/Twitter titles and descriptions to match. Keep all TODO placeholders.

**Step 3: Update nav active link**

```html
<li><a href="/demand-generation">Demand Gen</a></li>
<li><a href="/search-visibility" aria-current="page">Search</a></li>
```

**Step 4: Commit**

```bash
git add search-visibility.html
git commit -m "feat: scaffold search-visibility page from demand-generation template"
```

---

### Task 2: Update hero section

**Files:**
- Modify: `search-visibility.html`

**Step 1: Replace hero copy**

Find `.hero-copy` and replace its contents:

```html
<div class="hero-copy">
  <span class="eyebrow">Search &amp; Visibility</span>
  <h1>Be found where <em>buyers are looking</em></h1>
  <p class="hero-sub">Search hasn't disappeared — it's multiplied. Buyers find answers in Google, in AI overviews, in Perplexity and ChatGPT. Being visible now means showing up across all of them.</p>
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
    <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><circle cx="11" cy="11" r="8"/><path d="m21 21-4.35-4.35"/></svg>
  </div>
  <h3>Visibility checker</h3>
  <p>See where your brand shows up in AI-generated answers — and where it doesn't.</p>
  <span class="hero-card-placeholder-badge">Coming soon</span>
</div>
```

**Step 3: Commit**

```bash
git add search-visibility.html
git commit -m "feat: update hero for search-visibility page"
```

---

### Task 3: Add light section CSS

**Files:**
- Modify: `search-visibility.html`

**Step 1: Add light section overrides inside `<style>`, after the existing service section CSS**

This is the key CSS that makes the AI section visually distinct. Add:

```css
/* ─── LIGHT SECTION (AI & Answer Engines) ─── */
.section-light {
  background: var(--bg-light);
  color: var(--text-dark);
}
.section-light .section-label {
  color: var(--accent-dark);
}
.section-light h2 {
  color: var(--text-dark);
}
.section-light h2 em {
  color: var(--accent-dark);
}
.section-light .service-copy p {
  color: var(--text-dark-secondary);
}
.section-light .output-pill {
  border-color: var(--border-dark);
  background: rgba(0,0,0,0.04);
  color: rgba(31,31,31,0.65);
}
.section-light .output-pill:hover {
  border-color: rgba(0,201,181,0.4);
  color: var(--accent-dark);
  background: rgba(0,201,181,0.08);
}
.section-light .service-visual {
  background: var(--bg-light-card);
  border-color: var(--border-dark);
}
.section-light .service-visual-label {
  color: var(--accent-dark);
}
.section-light .service-visual-title {
  color: var(--text-dark);
}
.section-light .service-visual-body {
  color: var(--text-dark-secondary);
}
.section-light .service-visual-tag {
  background: rgba(0,201,181,0.1);
  border-color: rgba(0,201,181,0.25);
  color: var(--accent-dark);
}
```

**Step 2: Commit**

```bash
git add search-visibility.html
git commit -m "feat: add light section CSS for AI search section"
```

---

### Task 4: Replace service sections HTML

**Files:**
- Modify: `search-visibility.html`

**Step 1: Delete all four existing service sections**

Remove everything from `<!-- ── SECTION 2 -->` through to the closing `</section>` of the last service section (before the CTA). Leave hero and CTA intact.

**Step 2: Add Section 2 — Traditional search (dark)**

```html
  <!-- ── SECTION 2: Traditional search ── -->
  <section class="block" id="what-we-make">
    <div class="container">
      <div class="service-section">
        <div class="service-copy reveal">
          <p class="section-label">SEO &amp; website optimisation</p>
          <h2>Built to rank, <em>built to convert</em></h2>
          <p>SEO without website optimisation is just traffic that bounces. We combine search strategy with on-site performance — so the buyers who find you actually stay.</p>
          <div class="output-pills">
            <span class="output-pill">Technical SEO</span>
            <span class="output-pill">On-page optimisation</span>
            <span class="output-pill">SEO content strategy</span>
            <span class="output-pill">Core Web Vitals</span>
            <span class="output-pill">Conversion rate optimisation</span>
            <span class="output-pill">Site architecture</span>
          </div>
        </div>
        <div class="service-visual reveal reveal-delay-1">
          <span class="service-visual-label">Example output</span>
          <p class="service-visual-title">SEO &amp; content audit</p>
          <p class="service-visual-body">A full read of where you rank, what's working, and what's holding you back. The starting point for any search strategy worth having.</p>
          <div class="service-visual-tags">
            <span class="service-visual-tag">Technical audit</span>
            <span class="service-visual-tag">Content gaps</span>
            <span class="service-visual-tag">Quick wins</span>
          </div>
        </div>
      </div>
    </div>
  </section>
```

**Step 3: Add Section 3 — AI & answer engines (light)**

Note the `section-light` class on the `<section>` — this triggers all the light background overrides from Task 3.

```html
  <!-- ── SECTION 3: AI & answer engines (light background) ── -->
  <section class="block section-light">
    <div class="container">
      <div class="service-section" style="direction: rtl;">
        <div class="service-copy reveal" style="direction: ltr;">
          <p class="section-label">AI search &amp; answer engines</p>
          <h2>Visible in <em>the new search</em></h2>
          <p>AI overviews, LLM-generated answers, and answer engines are now where many buyers start their research. We help you show up there — with the right citations, the right structure, and the right content.</p>
          <div class="output-pills">
            <span class="output-pill">AI search optimisation</span>
            <span class="output-pill">LLM citations</span>
            <span class="output-pill">Answer engine optimisation</span>
            <span class="output-pill">Structured data</span>
            <span class="output-pill">Topical authority</span>
            <span class="output-pill">Featured snippets</span>
          </div>
        </div>
        <div class="service-visual reveal reveal-delay-1" style="direction: ltr;">
          <span class="service-visual-label">Example output</span>
          <p class="service-visual-title">AI visibility audit</p>
          <p class="service-visual-body">Where your brand appears (or doesn't) in AI-generated answers, and what to do about it. Most B2B brands have no idea how they're represented in LLM outputs.</p>
          <div class="service-visual-tags">
            <span class="service-visual-tag">LLM audit</span>
            <span class="service-visual-tag">Citation gaps</span>
            <span class="service-visual-tag">Structured data</span>
          </div>
        </div>
      </div>
    </div>
  </section>
```

**Step 4: Commit**

```bash
git add search-visibility.html
git commit -m "feat: add traditional search and AI sections to search-visibility page"
```

---

### Task 5: Update CTA section

**Files:**
- Modify: `search-visibility.html`

**Step 1: Replace CTA content**

```html
<div class="cta">
  <h2>Ready to show up where <em>your buyers are looking?</em></h2>
  <p>Tell us where you're starting from. We'll show you where you're missing.</p>
  <div class="cta-actions">
    <a href="mailto:hello@branchroad.media" class="btn-primary">Start a conversation</a>
    <a href="/" class="btn-secondary">See all services</a>
  </div>
</div>
```

**Step 2: Commit**

```bash
git add search-visibility.html
git commit -m "feat: update CTA for search-visibility page"
```

---

### Task 6: Visual review checklist

Open `search-visibility.html` in a browser and verify:

- [ ] Nav is fixed; "Search" link has active underline state
- [ ] Hero headline reads "Be found where buyers are looking" with "buyers are looking" in accent colour
- [ ] Placeholder card shows visibility checker copy with "Coming soon" badge
- [ ] Section 2 (Traditional search) renders on dark `#1F1F1F` background with white text
- [ ] Section 3 (AI & answer engines) renders on light `#EAFFFD` background with dark text
- [ ] Section 3 output pills have dark text and dark borders (not white-on-dark)
- [ ] Section 3 service visual card has white background with dark text
- [ ] Section 3 service visual tags use `--accent-dark` (teal) not `--accent` (bright cyan)
- [ ] CTA section renders correctly after the light section
- [ ] Scroll reveal animations fire on both sections
- [ ] Mobile nav opens/closes at <640px
- [ ] No demand-generation copy remains anywhere on the page

**Step 1: Fix any issues found, then commit**

```bash
git add search-visibility.html
git commit -m "feat: search-visibility page complete — visual review passed"
```

---

## Done

The page is complete when all 6 tasks are committed and the visual review checklist passes. Pay particular attention to the light/dark contrast between sections — that's the key design feature of this page.
