# Demand Generation Page Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Build `demand-generation.html` — a Branch Road service page for Demand Generation with four service-area sections, each with a bold headline, copy, and a row of output-type pills.

**Architecture:** Single self-contained HTML file matching the design language of `explainer-video-production.html`. Same CSS variables, fonts, nav, and component patterns. No framework, no build step. Six sections: Hero → Narrative-led content → Thought leadership → Sales enablement → Customer advocacy → CTA.

**Tech Stack:** HTML5, CSS (custom properties), vanilla JS (scroll animations, mobile nav, FAQ accordion). Google Fonts (Outfit). No external dependencies.

---

### Task 1: Scaffold the file — head, meta, CSS variables

**Files:**
- Create: `demand-generation.html`

**Step 1: Create the file with DOCTYPE, head, meta tags, and font import**

Copy the head block from `explainer-video-production.html` and update:
- `<title>` → `Demand Generation for B2B Tech | Branch Road Media`
- `<meta name="description">` → `Narrative-led content, thought leadership, sales enablement, and customer advocacy for B2B tech companies. Content that earns attention and moves buyers.`
- Remove the JSON-LD schema blocks (not needed yet)
- Keep all OG/Twitter meta with TODO placeholders
- Keep the Google Fonts link for Outfit

**Step 2: Add the CSS :root block and base styles**

Copy the full `:root` block and base styles (`*`, `html`, `body`, `::selection`, `.container`) verbatim from `explainer-video-production.html`. The tokens are identical — do not change any values.

```css
:root {
  --bg-primary: #1F1F1F;
  --bg-secondary: #171717;
  --bg-card: #000000;
  --bg-soft: #0f0f0f;
  --bg-light: #EAFFFD;
  --bg-light-card: #FFFFFF;
  --text-primary: #FFFFFF;
  --text-secondary: rgba(255,255,255,0.6);
  --text-muted: rgba(255,255,255,0.3);
  --text-dark: #1F1F1F;
  --text-dark-secondary: rgba(31,31,31,0.55);
  --accent: #01FEE5;
  --accent-hover: #33FFE9;
  --accent-soft: rgba(1,254,229,0.1);
  --accent-glow: rgba(1,254,229,0.15);
  --accent-dark: #00C9B5;
  --border: rgba(255,255,255,0.06);
  --border-dark: rgba(31,31,31,0.08);
  --radius-lg: 24px;
  --radius-md: 16px;
  --max-width: 1200px;
  --section-padding: clamp(28px,4vw,48px);
  --font: 'Outfit', system-ui, -apple-system, sans-serif;
}
```

**Step 3: Add nav CSS**

Copy the full nav styles (`nav`, `.nav-inner`, `.nav-logo`, `.nav-logo span`, `.nav-links`, `.nav-links a`, `.nav-links a::after`, `.nav-links a:hover`, `.mobile-menu-btn`) verbatim from `explainer-video-production.html`.

**Step 4: Commit**

```bash
git add demand-generation.html
git commit -m "feat: scaffold demand-generation page with head and CSS variables"
```

---

### Task 2: Add hero section CSS + HTML

**Files:**
- Modify: `demand-generation.html`

**Step 1: Add hero CSS**

Add these styles after the nav CSS:

```css
/* ─── HERO ─── */
.hero { padding: 126px 0 56px; }
main { padding-top: clamp(8px, 2vw, 20px); }

.hero-grid {
  display: grid;
  grid-template-columns: 1.1fr 0.9fr;
  gap: 22px;
  align-items: stretch;
}
.hero-copy {
  display: flex;
  flex-direction: column;
  min-height: 100%;
}
.eyebrow {
  display: inline-flex;
  width: fit-content;
  white-space: nowrap;
  align-items: center;
  gap: 8px;
  padding: 7px 12px;
  border-radius: 999px;
  border: 1px solid rgba(1,254,229,0.25);
  background: var(--accent-soft);
  color: var(--accent);
  text-transform: uppercase;
  letter-spacing: 0.08em;
  font-size: 0.74rem;
  font-weight: 600;
  margin-bottom: 18px;
}
.eyebrow::before {
  content: '';
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: var(--accent);
  box-shadow: 0 0 14px var(--accent-glow);
}
h1 {
  font-size: clamp(2.6rem, 6.2vw, 5rem);
  line-height: 1.01;
  letter-spacing: -0.04em;
  margin-bottom: 16px;
  max-width: 14ch;
}
h1 em { color: var(--accent); font-style: normal; }
.hero-sub {
  color: var(--text-secondary);
  max-width: 60ch;
  font-size: clamp(1rem, 1.6vw, 1.08rem);
  margin-bottom: 28px;
}
.btn-primary, .btn-secondary {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  text-decoration: none;
  border-radius: 999px;
  padding: 18px 36px;
  font-size: 0.95rem;
  transition: all 0.25s;
}
.btn-primary {
  background: var(--accent);
  color: var(--bg-card);
  font-weight: 700;
}
.btn-primary:hover { background: var(--accent-hover); transform: translateY(-2px); box-shadow: 0 8px 32px var(--accent-glow); }
.btn-secondary {
  color: var(--text-primary);
  border: 2px solid rgba(255,255,255,0.12);
  font-weight: 500;
}
.btn-secondary:hover { border-color: rgba(255,255,255,0.3); background: rgba(255,255,255,0.04); transform: translateY(-2px); }

/* ─── HERO PLACEHOLDER CARD ─── */
.hero-card {
  border: 1px solid rgba(1,254,229,0.25);
  border-radius: 32px;
  background: #060606;
  overflow: hidden;
  display: flex;
  flex-direction: column;
  min-height: 320px;
}
.hero-card-placeholder {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 14px;
  padding: 40px 32px;
  text-align: center;
}
.hero-card-placeholder-icon {
  width: 56px;
  height: 56px;
  border-radius: 16px;
  background: var(--accent-soft);
  border: 1px solid rgba(1,254,229,0.2);
  display: grid;
  place-items: center;
  color: var(--accent);
  font-size: 1.4rem;
}
.hero-card-placeholder h3 {
  font-size: 1.05rem;
  letter-spacing: -0.02em;
  color: var(--text-primary);
}
.hero-card-placeholder p {
  color: var(--text-muted);
  font-size: 0.86rem;
  max-width: 26ch;
}
.hero-card-placeholder-badge {
  padding: 6px 14px;
  border-radius: 999px;
  background: rgba(1,254,229,0.06);
  border: 1px solid rgba(1,254,229,0.15);
  color: var(--accent);
  font-size: 0.74rem;
  font-weight: 600;
  letter-spacing: 0.06em;
  text-transform: uppercase;
}
```

**Step 2: Add the HTML — skip link, nav, hero**

After `</style>` add `</head><body>`:

```html
<a class="skip-link" href="#main-content">Skip to content</a>

<nav aria-label="Main navigation">
  <div class="nav-inner">
    <a href="/" class="nav-logo">Branch <span>Road</span></a>
    <ul class="nav-links" id="nav-links">
      <li><a href="/video-services">Video</a></li>
      <li><a href="/demand-generation" aria-current="page">Demand Gen</a></li>
      <li><a href="/contact">Contact</a></li>
    </ul>
    <button class="mobile-menu-btn" id="mobile-menu-btn" aria-label="Toggle menu" aria-expanded="false">
      <svg width="22" height="22" viewBox="0 0 22 22" fill="none"><rect y="3" width="22" height="2" rx="1" fill="currentColor"/><rect y="10" width="22" height="2" rx="1" fill="currentColor"/><rect y="17" width="22" height="2" rx="1" fill="currentColor"/></svg>
    </button>
  </div>
</nav>

<main id="main-content">
  <section class="hero">
    <div class="container">
      <div class="hero-grid">
        <div class="hero-copy">
          <span class="eyebrow">Demand Generation</span>
          <h1>B2B content that <em>moves buyers</em></h1>
          <p class="hero-sub">Most B2B content gets ignored. Not because there isn't enough of it — because it doesn't say anything. We make content that earns attention, takes a real position, and reaches the right people at the right level.</p>
          <div style="display:flex;gap:12px;flex-wrap:wrap;">
            <a href="#contact" class="btn-primary">Start a conversation</a>
            <a href="#what-we-make" class="btn-secondary">See what we make</a>
          </div>
        </div>
        <div class="hero-card" aria-label="Interactive tool coming soon">
          <div class="hero-card-placeholder">
            <div class="hero-card-placeholder-icon">
              <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="3" width="18" height="18" rx="3"/><path d="M9 9h6M9 12h4M9 15h5"/></svg>
            </div>
            <h3>Content strategy tool</h3>
            <p>An interactive tool to help you find the right content for your stage, audience, and goal.</p>
            <span class="hero-card-placeholder-badge">Coming soon</span>
          </div>
        </div>
      </div>
    </div>
  </section>
```

**Step 3: Commit**

```bash
git add demand-generation.html
git commit -m "feat: add hero section to demand-generation page"
```

---

### Task 3: Add service section CSS

**Files:**
- Modify: `demand-generation.html`

**Step 1: Add service section styles inside `<style>`**

Add after the hero card styles:

```css
/* ─── SERVICE SECTIONS ─── */
section.block { padding: var(--section-padding) 0; }
section.block + section.block { border-top: 1px solid var(--border); }

.section-label {
  text-transform: uppercase;
  letter-spacing: 0.08em;
  font-size: 0.76rem;
  color: var(--accent);
  font-weight: 700;
  margin-bottom: 10px;
}

.service-section {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: clamp(32px, 5vw, 80px);
  align-items: start;
}

.service-copy h2 {
  font-size: clamp(1.9rem, 3.8vw, 2.9rem);
  letter-spacing: -0.03em;
  line-height: 1.08;
  margin-bottom: 14px;
}
.service-copy h2 em { color: var(--accent); font-style: normal; }

.service-copy p {
  color: var(--text-secondary);
  font-size: clamp(0.95rem, 1.4vw, 1.05rem);
  line-height: 1.65;
  max-width: 54ch;
}

/* ─── OUTPUT PILLS ─── */
.output-pills {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  margin-top: 22px;
}
.output-pill {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  padding: 8px 14px;
  border-radius: 999px;
  border: 1px solid var(--border);
  background: rgba(255,255,255,0.02);
  color: var(--text-secondary);
  font-size: 0.82rem;
  font-weight: 500;
  transition: border-color 0.2s, color 0.2s, background 0.2s;
}
.output-pill:hover {
  border-color: rgba(1,254,229,0.3);
  color: var(--accent);
  background: var(--accent-soft);
}
.output-pill::before {
  content: '';
  width: 5px;
  height: 5px;
  border-radius: 50%;
  background: currentColor;
  opacity: 0.5;
  flex-shrink: 0;
}

/* ─── SERVICE VISUAL PANEL ─── */
.service-visual {
  background: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: var(--radius-lg);
  padding: 28px;
  display: flex;
  flex-direction: column;
  gap: 14px;
  min-height: 280px;
}
.service-visual-label {
  font-size: 0.72rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  color: var(--accent);
}
.service-visual-title {
  font-size: 1.05rem;
  font-weight: 600;
  letter-spacing: -0.01em;
  color: var(--text-primary);
}
.service-visual-body {
  color: var(--text-secondary);
  font-size: 0.88rem;
  line-height: 1.6;
  flex: 1;
}
.service-visual-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
}
.service-visual-tag {
  padding: 4px 10px;
  border-radius: 999px;
  background: rgba(1,254,229,0.07);
  border: 1px solid rgba(1,254,229,0.15);
  color: var(--accent);
  font-size: 0.75rem;
  font-weight: 500;
}
```

**Step 2: Commit**

```bash
git add demand-generation.html
git commit -m "feat: add service section and output pill CSS"
```

---

### Task 4: Add the four service sections HTML

**Files:**
- Modify: `demand-generation.html`

Add after the closing `</section>` of the hero, inside `<main>`, with id `what-we-make` on the first:

**Step 1: Add Section 2 — Narrative-led content**

```html
  <!-- ── SECTION 2: Narrative-led content ── -->
  <section class="block" id="what-we-make">
    <div class="container">
      <div class="service-section">
        <div class="service-copy">
          <p class="section-label">Narrative-led content &amp; interactive assets</p>
          <h2>Content with <em>a spine</em></h2>
          <p>Most content tries to cover everything. We make content built around a clear argument — formats that hold attention and give buyers something to do, share, or act on.</p>
          <div class="output-pills">
            <span class="output-pill">Interactive assessments</span>
            <span class="output-pill">Long-form narratives</span>
            <span class="output-pill">Research reports</span>
            <span class="output-pill">Campaign landing pages</span>
            <span class="output-pill">Content hubs</span>
          </div>
        </div>
        <div class="service-visual">
          <span class="service-visual-label">Example format</span>
          <p class="service-visual-title">The B2B Buyer Reality Report</p>
          <p class="service-visual-body">An original research report built around a single, provable argument — not a summary of ten different trends. Designed to be cited, shared, and used as a sales conversation starter.</p>
          <div class="service-visual-tags">
            <span class="service-visual-tag">Original research</span>
            <span class="service-visual-tag">PDF + microsite</span>
            <span class="service-visual-tag">Campaign-ready</span>
          </div>
        </div>
      </div>
    </div>
  </section>
```

**Step 2: Add Section 3 — Thought leadership**

```html
  <!-- ── SECTION 3: Thought leadership ── -->
  <section class="block">
    <div class="container">
      <div class="service-section" style="direction: rtl;">
        <div class="service-copy" style="direction: ltr;">
          <p class="section-label">Thought leadership</p>
          <h2>Ideas worth being <em>associated with</em></h2>
          <p>Thought leadership only works if there's an actual thought in it. We develop POV-driven content that makes your buyers want to share it with their peers.</p>
          <div class="output-pills">
            <span class="output-pill">Point of view series</span>
            <span class="output-pill">Executive briefings</span>
            <span class="output-pill">Industry research</span>
            <span class="output-pill">Bylined articles</span>
            <span class="output-pill">Newsletter content</span>
          </div>
        </div>
        <div class="service-visual" style="direction: ltr;">
          <span class="service-visual-label">Example format</span>
          <p class="service-visual-title">Why the category you're in is the wrong one</p>
          <p class="service-visual-body">A bylined executive article that challenges the dominant frame in a market — not a press release, not a product update. A real position that earns earned media and sparks sales conversations.</p>
          <div class="service-visual-tags">
            <span class="service-visual-tag">Executive POV</span>
            <span class="service-visual-tag">Bylined article</span>
            <span class="service-visual-tag">Media pitchable</span>
          </div>
        </div>
      </div>
    </div>
  </section>
```

**Step 3: Add Section 4 — Sales enablement**

```html
  <!-- ── SECTION 4: Sales enablement ── -->
  <section class="block">
    <div class="container">
      <div class="service-section">
        <div class="service-copy">
          <p class="section-label">Sales enablement</p>
          <h2>Content that works <em>in the room</em></h2>
          <p>Most sales content sits in a shared drive. We build materials that actually get used — at the right stage, with the right message, for the right buyer.</p>
          <div class="output-pills">
            <span class="output-pill">Battlecards</span>
            <span class="output-pill">One-pagers</span>
            <span class="output-pill">Pitch decks</span>
            <span class="output-pill">Case study frameworks</span>
            <span class="output-pill">Objection handling guides</span>
          </div>
        </div>
        <div class="service-visual">
          <span class="service-visual-label">Example format</span>
          <p class="service-visual-title">Late-stage objection deck</p>
          <p class="service-visual-body">A concise, story-led leave-behind that handles the three most common stall points in enterprise deals — built for reps to use in the room, not to send and hope for the best.</p>
          <div class="service-visual-tags">
            <span class="service-visual-tag">Late-stage</span>
            <span class="service-visual-tag">Rep-ready</span>
            <span class="service-visual-tag">Slide + PDF</span>
          </div>
        </div>
      </div>
    </div>
  </section>
```

**Step 4: Add Section 5 — Customer advocacy**

```html
  <!-- ── SECTION 5: Customer advocacy ── -->
  <section class="block">
    <div class="container">
      <div class="service-section" style="direction: rtl;">
        <div class="service-copy" style="direction: ltr;">
          <p class="section-label">Customer advocacy</p>
          <h2>Let your customers <em>do the talking</em></h2>
          <p>Peer trust beats brand trust. We turn customer stories into assets that work across the entire funnel — not just a PDF on the website.</p>
          <div class="output-pills">
            <span class="output-pill">Customer stories</span>
            <span class="output-pill">Video testimonials</span>
            <span class="output-pill">Case studies</span>
            <span class="output-pill">Reference programs</span>
            <span class="output-pill">ROI narratives</span>
          </div>
        </div>
        <div class="service-visual" style="direction: ltr;">
          <span class="service-visual-label">Example format</span>
          <p class="service-visual-title">The 3-minute customer story</p>
          <p class="service-visual-body">A short documentary-style video and written case study built around a single, specific result. Designed to be used at every stage — from LinkedIn to the final proposal.</p>
          <div class="service-visual-tags">
            <span class="service-visual-tag">Video + written</span>
            <span class="service-visual-tag">Full-funnel</span>
            <span class="service-visual-tag">Social-ready</span>
          </div>
        </div>
      </div>
    </div>
  </section>
```

**Step 5: Commit**

```bash
git add demand-generation.html
git commit -m "feat: add four service sections to demand-generation page"
```

---

### Task 5: Add CTA section + close main/body

**Files:**
- Modify: `demand-generation.html`

**Step 1: Add CTA CSS to `<style>`**

```css
/* ─── CTA ─── */
.cta-section {
  padding: var(--section-padding) 0 clamp(40px, 6vw, 72px);
}
.cta {
  border: 1px solid rgba(1,254,229,0.2);
  border-radius: var(--radius-lg);
  background: linear-gradient(135deg, rgba(1,254,229,0.15), rgba(1,254,229,0.05), rgba(0,0,0,0.2));
  padding: clamp(36px, 6vw, 52px);
  text-align: center;
}
.cta h2 {
  font-size: clamp(1.8rem, 3.5vw, 2.6rem);
  letter-spacing: -0.03em;
  line-height: 1.1;
  margin-bottom: 12px;
}
.cta h2 em { color: var(--accent); font-style: normal; }
.cta p {
  color: rgba(255,255,255,0.75);
  max-width: 56ch;
  margin: 0 auto 24px;
  font-size: 1.02rem;
  line-height: 1.6;
}
.cta-actions {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 12px;
  flex-wrap: wrap;
}
```

**Step 2: Add CTA HTML**

```html
  <!-- ── CTA ── -->
  <section class="cta-section" id="contact">
    <div class="container">
      <div class="cta">
        <h2>Ready to make content that <em>actually lands?</em></h2>
        <p>Tell us where you're at. We'll tell you what we'd make — and why.</p>
        <div class="cta-actions">
          <a href="mailto:hello@branchroad.media" class="btn-primary">Start a conversation</a>
          <a href="/" class="btn-secondary">See all services</a>
        </div>
      </div>
    </div>
  </section>

</main>
```

**Step 3: Commit**

```bash
git add demand-generation.html
git commit -m "feat: add CTA section to demand-generation page"
```

---

### Task 6: Add responsive CSS + mobile nav JS

**Files:**
- Modify: `demand-generation.html`

**Step 1: Add responsive breakpoints to `<style>`**

```css
/* ─── RESPONSIVE ─── */
@media (max-width: 860px) {
  .hero-grid { grid-template-columns: 1fr; }
  .hero-card { min-height: 220px; }
  .service-section { grid-template-columns: 1fr !important; direction: ltr !important; }
  .service-visual { min-height: auto; }
}
@media (max-width: 640px) {
  h1 { font-size: 2.4rem; }
  .nav-links { display: none; flex-direction: column; position: absolute; top: 74px; left: 0; right: 0; background: rgba(20,20,20,0.97); border-bottom: 1px solid var(--border); padding: 20px clamp(20px, 4vw, 40px); gap: 18px; }
  .nav-links.open { display: flex; }
  .mobile-menu-btn { display: block; }
}
```

**Step 2: Add JS before `</body>`**

```html
<script>
  // Mobile nav toggle
  const btn = document.getElementById('mobile-menu-btn');
  const links = document.getElementById('nav-links');
  if (btn && links) {
    btn.addEventListener('click', () => {
      const open = links.classList.toggle('open');
      btn.setAttribute('aria-expanded', String(open));
    });
  }

  // Smooth scroll for anchor links
  document.querySelectorAll('a[href^="#"]').forEach(a => {
    a.addEventListener('click', e => {
      const target = document.querySelector(a.getAttribute('href'));
      if (target) { e.preventDefault(); target.scrollIntoView({ behavior: 'smooth', block: 'start' }); }
    });
  });
</script>
</body>
</html>
```

**Step 3: Commit**

```bash
git add demand-generation.html
git commit -m "feat: add responsive CSS and mobile nav JS"
```

---

### Task 7: Scroll-reveal animations

**Files:**
- Modify: `demand-generation.html`

**Step 1: Add reveal CSS to `<style>`**

```css
/* ─── SCROLL REVEAL ─── */
.reveal {
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 0.5s ease, transform 0.5s ease;
}
.reveal.visible {
  opacity: 1;
  transform: translateY(0);
}
.reveal-delay-1 { transition-delay: 0.08s; }
.reveal-delay-2 { transition-delay: 0.16s; }
```

**Step 2: Add `reveal` class to each service section's `.service-copy` and `.service-visual`**

In each of the four service sections:
- Add `class="service-copy reveal"` to the copy div
- Add `class="service-visual reveal reveal-delay-1"` to the visual div

**Step 3: Add IntersectionObserver JS (before the existing `<script>` block or inside it)**

```js
// Scroll reveal
const observer = new IntersectionObserver(entries => {
  entries.forEach(e => { if (e.isIntersecting) { e.target.classList.add('visible'); observer.unobserve(e.target); } });
}, { threshold: 0.12 });
document.querySelectorAll('.reveal').forEach(el => observer.observe(el));
```

**Step 4: Commit**

```bash
git add demand-generation.html
git commit -m "feat: add scroll reveal animations"
```

---

### Task 8: Final polish — nav active state, skip link, section dividers

**Files:**
- Modify: `demand-generation.html`

**Step 1: Add skip-link CSS to `<style>`**

```css
.skip-link {
  position: absolute; left: -9999px; top: auto; width: 1px; height: 1px;
  overflow: hidden; z-index: 999; text-decoration: none;
}
.skip-link:focus {
  position: fixed; top: 10px; left: 10px; width: auto; height: auto;
  padding: 12px 24px; background: var(--accent); color: var(--bg-card);
  border-radius: 8px; font-weight: 700; font-size: 0.9rem; z-index: 999;
}
```

**Step 2: Style the active nav link**

Add to nav CSS:
```css
.nav-links a[aria-current="page"] {
  color: var(--text-primary);
}
.nav-links a[aria-current="page"]::after {
  transform: scaleX(1);
}
```

**Step 3: Visual review checklist**
Open `demand-generation.html` in a browser and verify:
- [ ] Nav is fixed, logo links to `/`
- [ ] Hero headline reads "B2B content that moves buyers" with "moves buyers" in accent colour
- [ ] Placeholder card is visible on desktop, stacks cleanly on mobile
- [ ] Each of the 4 service sections renders with copy left, visual right (alternating sections flip)
- [ ] Output pills wrap correctly on narrow screens
- [ ] CTA section renders with gradient background
- [ ] Scroll animations fire as sections enter viewport
- [ ] Mobile nav opens/closes correctly at <640px

**Step 4: Commit**

```bash
git add demand-generation.html
git commit -m "feat: final polish — skip link, active nav, visual review complete"
```

---

## Done

The page is complete when all 8 tasks are committed and the visual review checklist passes.
