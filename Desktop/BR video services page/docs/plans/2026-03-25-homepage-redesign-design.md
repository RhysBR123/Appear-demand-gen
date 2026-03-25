# Homepage Redesign — "Terminal Pulse" Design

**Date:** 2026-03-25
**File:** `Desktop/BR video services page/index.html`
**Status:** Approved

## Overview

Redesign the Branch Road homepage to be more innovative across three dimensions simultaneously: visual/motion, structural/UX, and tone. The existing colour scheme (`#1F1F1F` bg, `#01FEE5` accent, Outfit font) and all content are preserved.

---

## Hero

**Structure:** Two-zone stacked layout replacing the current side-by-side grid.

**Top zone (~60vh):**
- Headline (`B2B marketing that earns its place`) types itself in on load, one character at a time, with a blinking cyan cursor
- Cursor stays and blinks after typing completes
- Sub-copy and two CTA buttons fade in after typing animation finishes
- Kicker label removed — headline carries the weight alone

**Bottom zone:**
- Full-width infinite horizontal ticker (marquee-style) of the five "How we think" phrases: `Narrative before noise · Brand before demand · Visibility before volume · Strategy before execution · Position before content ·`
- Continuous left-scroll, slightly muted colour (`rgba(255,255,255,0.3)`)
- Replaces the phrase card + dots — cleaner, always in motion

---

## Conviction Section

- Three full-width stacked statements, large type, no borders
- Scroll-triggered "scan line" reveal: a horizontal cyan line sweeps left-to-right (~0.4s) as each statement enters the viewport; text materialises behind it
- `We build both.` statement is slightly larger and rendered in cyan
- Whitespace-only separation between statements

---

## Services

Full-width stacked numbered list replacing the card grid.

**Each row contains:**
- Large muted number (`01`–`05`) left-aligned
- Service name bold, center-left
- Short hook right-aligned, hidden by default
- Thin bottom border

**On hover:**
- Row expands to ~2× height
- Hook slides in from right
- Number turns cyan
- Arrow (`→`) appears right-aligned
- No background fill change — motion and colour shift only

---

## Social Proof

- Section stays dark (removes the jarring light-section contrast break)
- Logo placeholders render as slim bordered pill badges
- Testimonials drop the `"` quotation mark; use a left cyan border accent instead

---

## CTA

- `clip-path` diagonal split: top-left dark, bottom-right deep cyan wash (`rgba(1,254,229,0.12)`)
- Headline and buttons centred over the split
- Bold geometric finish without being garish

---

## What Doesn't Change

- Colour tokens (all CSS custom properties preserved)
- Font (Outfit from Google Fonts)
- Navigation structure and links
- All copy and content
- Responsive behaviour (mobile breakpoints adapted to new layout)
- Accessibility (skip link, aria labels, mobile menu)
