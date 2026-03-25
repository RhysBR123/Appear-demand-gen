# Branch Road Homepage Design
**Date:** 2026-03-25
**File to create:** `homepage.html`

## Overview
The Branch Road homepage. Visually bold and conceptually sharp — the page demonstrates Branch Road's capabilities through its own design and copy. Five sections: Hero → Conviction statements → Services grid → Social proof → CTA.

## Positioning
- **Overarching claim:** Strategy and execution for B2B companies that are serious about growth
- **Hero headline:** B2B marketing that earns its place
- **Tone:** Confident, editorial, provocative — not generic agency copy

---

## Section Structure

### Section 1 — Hero
- **Headline:** B2B marketing that earns its place
- **Sub-copy:** We work with B2B tech companies that want strategy and execution in the same room — brand that positions, content that moves buyers, and distribution that reaches the right people.
- **Right side:** Animated typographic card. Key phrases cycle through one at a time with a smooth fade/slide transition:
  - "Narrative before noise"
  - "Brand before demand"
  - "Visibility before volume"
  - "Strategy before execution"
  - "Position before content"
  - Each phrase fades out, next fades in. Dark card background, large white type, accent colour on key word. Loops continuously.
- **Hero CTAs:** "Start a conversation" (primary) · "See our services" (secondary, scrolls to services grid)

### Section 2 — Conviction statements
- No section label. No sub-copy. Statements stand alone.
- Three beats, presented stacked, full-width, large type (clamp ~2rem to ~3.5rem):
  1. "Most B2B marketing talks to itself."
  2. "The best demand generation starts with brand. The best brand pays off in pipeline."
  3. "We build both."
- Generous vertical spacing between statements
- Each statement animates in on scroll (fade up)
- Statement 3 ("We build both.") is accent coloured — the payoff

### Section 3 — Services grid
- **Section label:** What we do
- **Layout:** 3 columns × 2 rows grid (responsive: 2 col on tablet, 1 col on mobile)
- **Six cards:**

| Service | Hook | Link |
|---|---|---|
| Brand & Positioning | Built to move buyers, not just look good | /brand-positioning |
| Demand Generation | Content that earns attention and acts on it | /demand-generation |
| Video Production | Video that buyers actually trust | /video-services |
| Search & Visibility | Be found where buyers are looking | /search-visibility |
| Social & Distribution | Organic and paid pulling in the same direction | /social-distribution |
| (sixth slot) | Work with us | /contact |

- Each card: service name (bold), hook (muted), arrow icon (→) bottom-right, hover state lifts card and shows accent border
- Cards link to respective service pages

### Section 4 — Social proof
- **Logo strip:** 5–6 client logo placeholder slots. Greyscale, opacity 0.5. Row, centered, with subtle dividers.
- **Testimonials:** 1–2 large pull-quotes below the logo strip
  - Large opening quotation mark in accent colour
  - Quote text in large type (~1.2rem)
  - Attribution: Name, Title, Company — small, muted
  - Placeholder text to be replaced before publishing
- Background: light section (`--bg-light` / `#EAFFFD`) — visually distinct from the dark sections above

### Section 5 — CTA
- **Headline:** Ready to build something worth noticing?
- **Sub-copy:** Tell us where you are. We'll tell you what we'd build.
- **Buttons:** "Start a conversation" (primary, mailto) · "See our services" (secondary, scrolls to services)

---

## Hero Animation — Technical Notes
- CSS keyframe animation or JS interval (JS preferred for control)
- Phrases array defined in JS
- Each phrase displays for ~2.5 seconds, crossfades over ~0.4s
- Accent word (last word of each phrase) wrapped in `<em>` and coloured with `--accent`
- Card has fixed min-height so layout doesn't shift during transitions

## Design Language
- Identical CSS variables, fonts, and nav to all service pages
- Conviction statements section: dark background, full-width, generous padding
- Social proof section: light `--bg-light` background with dark text (same pattern as search-visibility.html light section)
- Services grid cards: dark background (`--bg-card`), hover lift + accent border
- All other patterns (buttons, pills, scroll reveal) consistent with existing pages
