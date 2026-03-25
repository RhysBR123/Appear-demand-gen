# Search & Visibility Page Design
**Date:** 2026-03-25
**File to create:** `search-visibility.html`

## Overview
A service page for Branch Road's Search & Visibility offering. Follows the same design language as the other service pages but with a split-contrast layout — traditional search section on the standard dark background, AI & answer engines section on the light `#EAFFFD` background. Two service sections, not four.

## Core Tensions (woven into copy, not stated explicitly)
1. Companies are still optimising for a search landscape that no longer exists
2. Visibility has fractured — buyers now find answers in ChatGPT, Perplexity, and AI overviews, not just search results, and most B2B brands aren't showing up there

## Hero
- **Eyebrow:** Search & Visibility
- **Headline:** Be found where buyers are looking
- **Sub-copy:** Search hasn't disappeared — it's multiplied. Buyers find answers in Google, in AI overviews, in Perplexity and ChatGPT. Being visible now means showing up across all of them.
- **Right side:** Placeholder interactive card

---

## Section Structure

### Section 2 — Traditional search (dark background)
Groups: SEO + website optimisation
- **Headline:** Built to rank, built to convert
- **Copy:** SEO without website optimisation is just traffic that bounces. We combine search strategy with on-site performance — so the buyers who find you actually stay.
- **Output pills:** Technical SEO · On-page optimisation · SEO content strategy · Core Web Vitals · Conversion rate optimisation · Site architecture
- **Example card title:** SEO & content audit
- **Example card body:** A full read of where you rank, what's working, and what's holding you back. The starting point for any search strategy worth having.
- **Example card tags:** Technical audit · Content gaps · Quick wins

### Section 3 — AI & answer engines (light #EAFFFD background)
Groups: AI search, LLM citations, answer engine optimisation
- **Background:** `var(--bg-light)` (#EAFFFD) — same treatment as process section in video pages
- **Text colour:** `var(--text-dark)` for headings/body, `var(--accent-dark)` for labels/accent
- **Headline:** Visible in the new search
- **Copy:** AI overviews, LLM-generated answers, and answer engines are now where many buyers start their research. We help you show up there — with the right citations, the right structure, and the right content.
- **Output pills:** AI search optimisation · LLM citations · Answer engine optimisation · Structured data · Topical authority · Featured snippets
- **Example card title:** AI visibility audit
- **Example card body:** Where your brand appears (or doesn't) in AI-generated answers, and what to do about it. Most B2B brands have no idea how they're represented in LLM outputs.
- **Example card tags:** LLM audit · Citation gaps · Structured data

### Section 4 — CTA
- **Headline:** Ready to show up where your buyers are looking?
- **Sub-copy:** Tell us where you're starting from. We'll show you where you're missing.
- Contact link + back to services link

---

## Design Notes
- The light section needs its own CSS overrides: dark text, `--accent-dark` for labels, white card backgrounds, dark borders — same pattern as `.process-wrapper` in `explainer-video-production.html`
- Output pills in the light section need dark text variants
- Service visual card in light section uses `--bg-light-card` (white) background with `--border-dark`
- All other CSS (nav, hero, buttons, scroll reveal, responsive) identical to `demand-generation.html`
