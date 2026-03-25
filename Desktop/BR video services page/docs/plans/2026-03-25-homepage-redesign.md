# Homepage Redesign — "Terminal Pulse" Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Redesign `index.html` to the approved "Terminal Pulse" design — typewriter hero, horizontal ticker, scan-line conviction reveals, expandable service rows, dark social proof, and diagonal CTA split — while preserving all content, colours, font, and nav.

**Architecture:** Single self-contained HTML file. All CSS lives in the `<style>` block, all JS at the bottom in `<script>`. No build step, no dependencies beyond the existing Google Fonts link. Each task modifies a discrete section of the file.

**Tech Stack:** Vanilla HTML5, CSS custom properties, Intersection Observer API, requestAnimationFrame for ticker, CSS clip-path for CTA diagonal.

---

## Reference

Design doc: `docs/plans/2026-03-25-homepage-redesign-design.md`
Source file: `Desktop/BR video services page/index.html`
Colour tokens (do not change):
- `--bg-primary: #1F1F1F`
- `--accent: #01FEE5`
- `--font: 'Outfit', system-ui, -apple-system, sans-serif`

---

### Task 1: Replace hero layout with two-zone stacked structure

**Files:**
- Modify: `Desktop/BR video services page/index.html` — hero CSS + hero HTML

**Step 1: Remove the old hero-grid CSS and hero-phrase-card CSS**

In the `<style>` block, delete these rule blocks entirely:
- `.hero-grid { ... }`
- `.hero-copy { ... }`
- `.hero-kicker { ... }`
- `.hero-phrase-card { ... }`
- `.hero-phrase-card::before { ... }`
- `.hero-phrase-wrap { ... }`
- `.hero-phrase { ... }`
- `.hero-phrase.active { ... }`
- `.hero-phrase em { ... }`
- `.hero-phrase-label { ... }`
- `.hero-phrase-dots { ... }`
- `.hero-phrase-dot { ... }`
- `.hero-phrase-dot.active { ... }`

**Step 2: Add new hero CSS in their place**

```css
/* ─── HERO ─── */
.hero { padding: 140px 0 0; min-height: 60vh; display: flex; flex-direction: column; justify-content: flex-end; }
.hero-top { padding-bottom: 56px; }
.hero-headline {
  font-size: clamp(2.8rem, 6vw, 5rem);
  font-weight: 800;
  letter-spacing: -0.04em;
  line-height: 1.05;
  margin-bottom: 24px;
  min-height: 1.1em;
}
.hero-headline .cursor {
  display: inline-block;
  width: 3px;
  height: 0.85em;
  background: var(--accent);
  margin-left: 4px;
  vertical-align: middle;
  animation: blink 1s step-end infinite;
}
@keyframes blink { 0%,100% { opacity: 1; } 50% { opacity: 0; } }
.hero-headline em { color: var(--accent); font-style: normal; }
.hero-sub {
  color: var(--text-secondary);
  font-size: clamp(1rem, 1.6vw, 1.1rem);
  line-height: 1.65;
  max-width: 54ch;
  margin-bottom: 32px;
  opacity: 0;
  transition: opacity 0.6s ease;
}
.hero-sub.visible { opacity: 1; }
.hero-actions { display: flex; gap: 12px; flex-wrap: wrap; opacity: 0; transition: opacity 0.6s ease 0.2s; }
.hero-actions.visible { opacity: 1; }
```

**Step 3: Replace hero HTML inside `<section class="hero">`**

Replace everything inside `<section class="hero">` with:

```html
<section class="hero">
  <div class="container hero-top">
    <h1 class="hero-headline" id="hero-headline"><span class="cursor"></span></h1>
    <p class="hero-sub" id="hero-sub">We work with B2B tech companies that want strategy and execution in the same room — brand that positions, content that moves buyers, and distribution that reaches the right people.</p>
    <div class="hero-actions" id="hero-actions">
      <a href="mailto:hello@branchroad.media" class="btn-primary">Start a conversation</a>
      <a href="#services" class="btn-secondary">See our services</a>
    </div>
  </div>
</section>
```

**Step 4: Verify in browser**

Open `index.html` in browser. Hero should show an empty headline with a blinking cyan cursor, sub-copy and buttons invisible. No JS yet — that comes in Task 5.

**Step 5: Commit**

```bash
git add "Desktop/BR video services page/index.html"
git commit -m "feat: replace hero grid with two-zone stacked layout"
```

---

### Task 2: Add horizontal ticker below hero

**Files:**
- Modify: `Desktop/BR video services page/index.html` — add ticker CSS + ticker HTML after hero section

**Step 1: Add ticker CSS to `<style>` block**

```css
/* ─── TICKER ─── */
.ticker-wrap {
  border-top: 1px solid var(--border);
  border-bottom: 1px solid var(--border);
  overflow: hidden;
  padding: 14px 0;
  background: var(--bg-secondary);
}
.ticker-track {
  display: flex;
  gap: 0;
  white-space: nowrap;
  will-change: transform;
}
.ticker-item {
  font-size: 0.82rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  color: rgba(255,255,255,0.3);
  padding: 0 40px;
  flex-shrink: 0;
}
.ticker-item em { color: var(--accent); font-style: normal; opacity: 0.7; }
```

**Step 2: Add ticker HTML immediately after the closing `</section>` of `.hero`**

```html
<div class="ticker-wrap" aria-hidden="true">
  <div class="ticker-track" id="ticker-track">
    <span class="ticker-item">Narrative before <em>noise</em></span>
    <span class="ticker-item">Brand before <em>demand</em></span>
    <span class="ticker-item">Visibility before <em>volume</em></span>
    <span class="ticker-item">Strategy before <em>execution</em></span>
    <span class="ticker-item">Position before <em>content</em></span>
    <span class="ticker-item">Narrative before <em>noise</em></span>
    <span class="ticker-item">Brand before <em>demand</em></span>
    <span class="ticker-item">Visibility before <em>volume</em></span>
    <span class="ticker-item">Strategy before <em>execution</em></span>
    <span class="ticker-item">Position before <em>content</em></span>
  </div>
</div>
```

(Items duplicated so the loop looks seamless.)

**Step 3: Verify**

Reload — a strip of muted uppercase phrases should appear below the hero. No animation yet (JS in Task 5).

**Step 4: Commit**

```bash
git add "Desktop/BR video services page/index.html"
git commit -m "feat: add horizontal ticker strip below hero"
```

---

### Task 3: Redesign conviction section with scan-line reveal

**Files:**
- Modify: `Desktop/BR video services page/index.html` — conviction CSS + HTML

**Step 1: Replace conviction CSS**

Remove the existing `.conviction` and `.conviction-statement` blocks and replace with:

```css
/* ─── CONVICTION ─── */
.conviction {
  padding: clamp(80px, 12vw, 140px) 0;
  border-top: 1px solid var(--border);
}
.conviction-statement {
  font-size: clamp(2rem, 5vw, 4rem);
  font-weight: 700;
  letter-spacing: -0.03em;
  line-height: 1.1;
  color: var(--text-primary);
  padding: clamp(28px, 4vw, 48px) 0;
  position: relative;
  overflow: hidden;
  opacity: 0;
}
.conviction-statement.accent {
  color: var(--accent);
  font-size: clamp(2.4rem, 6vw, 4.8rem);
}
.conviction-statement .scanline {
  position: absolute;
  top: 0; left: -100%; bottom: 0;
  width: 100%;
  background: linear-gradient(90deg, transparent 0%, var(--accent) 50%, transparent 100%);
  opacity: 0.15;
  pointer-events: none;
}
.conviction-statement.scan-done { opacity: 1; }
.conviction-statement.scanning .scanline {
  animation: scan 0.5s ease-out forwards;
}
@keyframes scan {
  from { left: -100%; }
  to { left: 100%; }
}
```

**Step 2: Replace conviction HTML**

```html
<section class="conviction">
  <div class="container">
    <p class="conviction-statement" data-conviction><span class="scanline"></span>Most B2B marketing talks to itself.</p>
    <p class="conviction-statement" data-conviction><span class="scanline"></span>The best demand generation starts with brand. The best brand pays off in pipeline.</p>
    <p class="conviction-statement accent" data-conviction><span class="scanline"></span>We build both.</p>
  </div>
</section>
```

**Step 3: Verify**

Reload — conviction statements should be invisible (opacity 0). JS wiring in Task 5 will trigger the scan animation.

**Step 4: Commit**

```bash
git add "Desktop/BR video services page/index.html"
git commit -m "feat: redesign conviction section with scan-line reveal structure"
```

---

### Task 4: Replace services card grid with expandable stacked list

**Files:**
- Modify: `Desktop/BR video services page/index.html` — services CSS + HTML

**Step 1: Remove old services CSS**

Delete `.services-grid`, `.service-card`, `.service-card:hover`, `.service-card-name`, `.service-card-hook`, `.service-card-arrow`, `.service-card:hover .service-card-arrow`, `.service-card.service-card--cta`, `.service-card.service-card--cta .service-card-name`.

**Step 2: Add new services CSS**

```css
/* ─── SERVICES LIST ─── */
.services { padding: var(--section-padding) 0; border-top: 1px solid var(--border); }
.services-list { list-style: none; }
.service-row {
  display: grid;
  grid-template-columns: 64px 1fr auto;
  align-items: center;
  gap: 24px;
  padding: 24px 0;
  border-bottom: 1px solid var(--border);
  text-decoration: none;
  color: inherit;
  overflow: hidden;
  transition: padding 0.3s ease;
  cursor: pointer;
}
.service-row:first-child { border-top: 1px solid var(--border); }
.service-num {
  font-size: 2.2rem;
  font-weight: 800;
  color: var(--text-muted);
  letter-spacing: -0.04em;
  transition: color 0.25s ease;
  line-height: 1;
}
.service-name {
  font-size: clamp(1.1rem, 2vw, 1.5rem);
  font-weight: 700;
  letter-spacing: -0.02em;
  color: var(--text-primary);
  transition: color 0.25s ease;
}
.service-right {
  display: flex;
  align-items: center;
  gap: 20px;
  text-align: right;
}
.service-hook {
  font-size: 0.9rem;
  color: var(--text-secondary);
  max-width: 28ch;
  opacity: 0;
  transform: translateX(12px);
  transition: opacity 0.25s ease, transform 0.25s ease;
}
.service-arrow {
  color: var(--accent);
  font-size: 1.4rem;
  opacity: 0;
  transition: opacity 0.25s ease, transform 0.25s ease;
}
.service-row:hover {
  padding-top: 36px;
  padding-bottom: 36px;
}
.service-row:hover .service-num { color: var(--accent); }
.service-row:hover .service-hook { opacity: 1; transform: translateX(0); }
.service-row:hover .service-arrow { opacity: 1; }
.service-cta-row {
  padding: 32px 0;
  border-bottom: 1px solid rgba(1,254,229,0.2);
}
.service-cta-row .service-num { color: rgba(1,254,229,0.3); }
.service-cta-row .service-name { color: var(--accent); }
```

**Step 3: Replace services HTML**

```html
<section class="services" id="services">
  <div class="container">
    <p class="section-label">What we do</p>
    <ul class="services-list">
      <li><a href="/brand-positioning" class="service-row">
        <span class="service-num">01</span>
        <span class="service-name">Brand &amp; Positioning</span>
        <span class="service-right">
          <span class="service-hook">Built to move buyers, not just look good</span>
          <span class="service-arrow">→</span>
        </span>
      </a></li>
      <li><a href="/demand-generation" class="service-row">
        <span class="service-num">02</span>
        <span class="service-name">Demand Generation</span>
        <span class="service-right">
          <span class="service-hook">Content that earns attention and acts on it</span>
          <span class="service-arrow">→</span>
        </span>
      </a></li>
      <li><a href="/video-services" class="service-row">
        <span class="service-num">03</span>
        <span class="service-name">Video Production</span>
        <span class="service-right">
          <span class="service-hook">Video that buyers actually trust</span>
          <span class="service-arrow">→</span>
        </span>
      </a></li>
      <li><a href="/search-visibility" class="service-row">
        <span class="service-num">04</span>
        <span class="service-name">Search &amp; Visibility</span>
        <span class="service-right">
          <span class="service-hook">Be found where buyers are looking</span>
          <span class="service-arrow">→</span>
        </span>
      </a></li>
      <li><a href="/social-distribution" class="service-row">
        <span class="service-num">05</span>
        <span class="service-name">Social &amp; Distribution</span>
        <span class="service-right">
          <span class="service-hook">Organic and paid pulling in the same direction</span>
          <span class="service-arrow">→</span>
        </span>
      </a></li>
      <li><a href="mailto:hello@branchroad.media" class="service-row service-cta-row">
        <span class="service-num">→</span>
        <span class="service-name">Work with us</span>
        <span class="service-right">
          <span class="service-hook">Tell us where you are. We'll show you what we'd build.</span>
          <span class="service-arrow">→</span>
        </span>
      </a></li>
    </ul>
  </div>
</section>
```

**Step 4: Verify**

Reload — services should render as a numbered list. Hover each row to confirm padding expands, number turns cyan, hook and arrow appear.

**Step 5: Commit**

```bash
git add "Desktop/BR video services page/index.html"
git commit -m "feat: replace services grid with expandable numbered list"
```

---

### Task 5: Redesign social proof section (dark, pill logos, border testimonials)

**Files:**
- Modify: `Desktop/BR video services page/index.html` — social proof CSS + HTML

**Step 1: Replace social proof CSS**

Remove `.social-proof`, `.social-proof .section-label`, `.logo-strip`, `.logo-slot`, `.logo-slot span`, `.testimonials`, `.testimonial`, `.testimonial-mark`, `.testimonial-quote`, `.testimonial-attr`, `.testimonial-attr span`.

Add:

```css
/* ─── SOCIAL PROOF ─── */
.social-proof {
  padding: var(--section-padding) 0;
  border-top: 1px solid var(--border);
}
.logo-strip {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: clamp(12px, 3vw, 32px);
  flex-wrap: wrap;
  margin-bottom: 56px;
}
.logo-pill {
  padding: 8px 20px;
  border: 1px solid var(--border);
  border-radius: 999px;
  font-size: 0.72rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  color: var(--text-muted);
}
.testimonials {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 24px;
}
.testimonial {
  background: var(--bg-card);
  border: 1px solid var(--border);
  border-left: 3px solid var(--accent);
  border-radius: var(--radius-md);
  padding: 32px;
}
.testimonial-quote {
  font-size: 1.02rem;
  line-height: 1.65;
  color: var(--text-primary);
  margin-bottom: 20px;
}
.testimonial-attr {
  font-size: 0.82rem;
  color: var(--text-secondary);
  font-weight: 600;
}
.testimonial-attr span { color: var(--accent); }
```

**Step 2: Replace social proof HTML**

```html
<section class="social-proof">
  <div class="container">
    <p class="section-label">Trusted by</p>
    <div class="logo-strip">
      <span class="logo-pill">[Client]</span>
      <span class="logo-pill">[Client]</span>
      <span class="logo-pill">[Client]</span>
      <span class="logo-pill">[Client]</span>
      <span class="logo-pill">[Client]</span>
    </div>
    <div class="testimonials">
      <div class="testimonial reveal">
        <p class="testimonial-quote">[Testimonial quote — replace with real customer quote. Keep it short, specific, and outcome-focused. One or two sentences max.]</p>
        <p class="testimonial-attr">[Name] &mdash; <span>[Title, Company]</span></p>
      </div>
      <div class="testimonial reveal reveal-delay-1">
        <p class="testimonial-quote">[Testimonial quote — replace with real customer quote. Keep it short, specific, and outcome-focused. One or two sentences max.]</p>
        <p class="testimonial-attr">[Name] &mdash; <span>[Title, Company]</span></p>
      </div>
    </div>
  </div>
</section>
```

**Step 3: Verify**

Reload — social proof section should now be dark, logos as pill badges, testimonials with cyan left border.

**Step 4: Commit**

```bash
git add "Desktop/BR video services page/index.html"
git commit -m "feat: redesign social proof to dark theme with pill logos and border testimonials"
```

---

### Task 6: Redesign CTA section with diagonal clip-path split

**Files:**
- Modify: `Desktop/BR video services page/index.html` — CTA CSS + HTML

**Step 1: Replace CTA CSS**

Remove `.cta-section`, `.cta`, `.cta h2`, `.cta h2 em`, `.cta p`, `.cta-actions`.

Add:

```css
/* ─── CTA ─── */
.cta-section {
  padding: var(--section-padding) 0 clamp(48px, 8vw, 96px);
  border-top: 1px solid var(--border);
}
.cta {
  position: relative;
  border-radius: var(--radius-lg);
  overflow: hidden;
  padding: clamp(56px, 9vw, 96px) clamp(32px, 6vw, 72px);
  text-align: center;
  background: var(--bg-card);
  border: 1px solid var(--border);
}
.cta::before {
  content: '';
  position: absolute;
  inset: 0;
  background: rgba(1,254,229,0.09);
  clip-path: polygon(60% 0%, 100% 0%, 100% 100%, 35% 100%);
  pointer-events: none;
}
.cta-content { position: relative; z-index: 1; }
.cta h2 {
  font-size: clamp(2.2rem, 4.5vw, 3.4rem);
  letter-spacing: -0.03em;
  line-height: 1.05;
  margin-bottom: 14px;
}
.cta h2 em { color: var(--accent); font-style: normal; }
.cta p {
  color: rgba(255,255,255,0.65);
  max-width: 48ch;
  margin: 0 auto 32px;
  font-size: 1.02rem;
}
.cta-actions { display: flex; align-items: center; justify-content: center; gap: 12px; flex-wrap: wrap; }
```

**Step 2: Replace CTA HTML**

```html
<section class="cta-section">
  <div class="container">
    <div class="cta">
      <div class="cta-content">
        <h2>Ready to build something <em>worth noticing?</em></h2>
        <p>Tell us where you are. We'll tell you what we'd build.</p>
        <div class="cta-actions">
          <a href="mailto:hello@branchroad.media" class="btn-primary">Start a conversation</a>
          <a href="#services" class="btn-secondary">See our services</a>
        </div>
      </div>
    </div>
  </div>
</section>
```

**Step 3: Verify**

Reload — CTA block should have a diagonal cyan wash in the bottom-right quadrant.

**Step 4: Commit**

```bash
git add "Desktop/BR video services page/index.html"
git commit -m "feat: add diagonal clip-path accent to CTA section"
```

---

### Task 7: Wire up all JavaScript (typewriter, ticker, scan-line, remove old JS)

**Files:**
- Modify: `Desktop/BR video services page/index.html` — `<script>` block

**Step 1: Replace the entire `<script>` block** with:

```html
<script>
  // ─── Typewriter hero ───
  const headline = document.getElementById('hero-headline');
  const sub = document.getElementById('hero-sub');
  const actions = document.getElementById('hero-actions');
  const fullText = 'B2B marketing that earns its place';
  const cursor = headline.querySelector('.cursor');
  let i = 0;

  function type() {
    if (i < fullText.length) {
      cursor.insertAdjacentText('beforebegin', fullText[i]);
      i++;
      setTimeout(type, i === 1 ? 80 : 40 + Math.random() * 40);
    } else {
      sub.classList.add('visible');
      actions.classList.add('visible');
    }
  }
  setTimeout(type, 400);

  // ─── Ticker ───
  const track = document.getElementById('ticker-track');
  if (track) {
    let x = 0;
    const speed = 0.5; // px per frame
    function animateTicker() {
      x -= speed;
      const halfWidth = track.scrollWidth / 2;
      if (Math.abs(x) >= halfWidth) x = 0;
      track.style.transform = `translateX(${x}px)`;
      requestAnimationFrame(animateTicker);
    }
    requestAnimationFrame(animateTicker);
  }

  // ─── Conviction scan-line ───
  const convictionObs = new IntersectionObserver(entries => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        const el = entry.target;
        el.classList.add('scanning');
        el.addEventListener('animationend', () => {
          el.classList.add('scan-done');
          el.classList.remove('scanning');
        }, { once: true });
        convictionObs.unobserve(el);
      }
    });
  }, { threshold: 0.3 });
  document.querySelectorAll('[data-conviction]').forEach(el => convictionObs.observe(el));

  // ─── Mobile nav ───
  const btn = document.getElementById('mobile-menu-btn');
  const links = document.getElementById('nav-links');
  if (btn && links) {
    btn.addEventListener('click', () => {
      const open = links.classList.toggle('open');
      btn.setAttribute('aria-expanded', String(open));
    });
  }

  // ─── Smooth scroll ───
  document.querySelectorAll('a[href^="#"]').forEach(a => {
    a.addEventListener('click', e => {
      const target = document.querySelector(a.getAttribute('href'));
      if (target) { e.preventDefault(); target.scrollIntoView({ behavior: 'smooth', block: 'start' }); }
    });
  });

  // ─── Scroll reveal (testimonials) ───
  const revealObs = new IntersectionObserver(entries => {
    entries.forEach(e => { if (e.isIntersecting) { e.target.classList.add('visible'); revealObs.unobserve(e.target); } });
  }, { threshold: 0.1 });
  document.querySelectorAll('.reveal').forEach(el => revealObs.observe(el));
</script>
```

**Step 2: Remove unused CSS**

Remove `.reveal`, `.reveal.visible`, `.reveal-delay-1`, `.reveal-delay-2`, `.reveal-delay-3` from `<style>` (keep `.reveal` and `.reveal.visible` since testimonials still use them — actually keep all reveal classes).

**Step 3: Full verification checklist**

Open `index.html` in browser and check:
- [ ] Headline types in character by character on load
- [ ] Cyan cursor blinks throughout
- [ ] Sub-copy and buttons fade in after typing completes
- [ ] Ticker scrolls continuously, loops seamlessly
- [ ] Scrolling down: conviction statements flash scan line then appear
- [ ] Hovering service rows: padding grows, number goes cyan, hook and arrow appear
- [ ] Social proof section is dark, logos are pill badges, testimonials have cyan left border
- [ ] CTA has diagonal cyan wash bottom-right
- [ ] Mobile: hamburger menu opens/closes nav
- [ ] No console errors

**Step 4: Commit**

```bash
git add "Desktop/BR video services page/index.html"
git commit -m "feat: wire typewriter, ticker, scan-line, and remove legacy JS"
```

---

### Task 8: Responsive cleanup

**Files:**
- Modify: `Desktop/BR video services page/index.html` — responsive CSS in `<style>`

**Step 1: Replace the `@media` blocks** at the bottom of `<style>` with:

```css
@media (max-width: 960px) {
  .testimonials { grid-template-columns: 1fr; }
}
@media (max-width: 640px) {
  .hero-headline { font-size: 2.4rem; }
  .service-row { grid-template-columns: 48px 1fr; }
  .service-right { display: none; }
  .service-row:hover .service-hook,
  .service-row:hover .service-arrow { opacity: 0; }
  .conviction-statement { font-size: 1.8rem; }
  .nav-links {
    display: none;
    flex-direction: column;
    position: absolute;
    top: 74px; left: 0; right: 0;
    background: rgba(20,20,20,0.97);
    border-bottom: 1px solid var(--border);
    padding: 20px clamp(20px, 4vw, 40px);
    gap: 18px;
  }
  .nav-links.open { display: flex; }
  .mobile-menu-btn { display: block; }
}
```

**Step 2: Verify at mobile width**

In browser DevTools, set viewport to 375px wide and check:
- [ ] Service rows show number + name only (no hook column)
- [ ] Conviction statements readable at smaller size
- [ ] Hero headline doesn't overflow
- [ ] Nav hamburger menu works

**Step 3: Commit**

```bash
git add "Desktop/BR video services page/index.html"
git commit -m "feat: update responsive breakpoints for new layout"
```
