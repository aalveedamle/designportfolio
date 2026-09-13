# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is a personal portfolio website for Aalvee Damle (Senior Product Designer). It is a collection of standalone, self-contained HTML files — no build system, bundler, package manager, or framework. Open any file directly in a browser to view it.

## File Map

| File | Purpose |
|---|---|
| `index.html` | Main landing page — hero, case study grid, testimonials, contact |
| `work.html` | Work index — the case-study card list linked from every nav |
| `aalvee_about_v3.html` | About page |
| `aalvee_case_geniaus_v2.html` | Geniaus case study (GenAI copilot for auditors, EY) |
| `aalvee_case_genie_v1.html` | Genie case study (wealth platform, US bank) |
| `aalvee_case_peepal_v2.html` | Peepal case study (AgriTech for World Bank) |
| `aalvee_case_resolvenow_v1.html` | ResolveNow case study (citizen complaint platform, Indian municipalities) |
| `aalvee_case_rap_v1.html` | RAP case study (AI digital twin for risk analytics, EY) — plays `RAP.mp4` |
| `aalvee_case_yulu_v1.html` | Yulu case study (AI-native micro-mobility) — embeds the two files below |
| `yulu-prototype.html` | Standalone interactive prototype for the Yulu case study (self-contained, own design system) |
| `yulu-wireframes.html` | Standalone annotated wireframe set for the Yulu case study |
| `aalvee_ux_strategies_v1.html`, `aalvee_strategy_0*.html` | UX strategy index and write-ups |
| `404.html` | Served by Cloudflare for any URL that doesn't exist (`not_found_handling = "404-page"`) |
| `case study page.html` | Stale — nothing links to it |

## Architecture

**Each file is fully self-contained**: CSS lives in a `<style>` block, JavaScript in `<script>` blocks, all in the same `.html` file. There are no shared partials or imports — nav, footer, and the design token `:root` block are duplicated across every page.

### Design System (CSS custom properties)

All pages share an identical token set defined in `:root` and a `[data-theme="light"]` override block:

- **Default theme**: Dark (`data-theme="dark"` on `<html>`)
- **Dark accent**: `#E9F056` (lime)
- **Light accent**: `#ff5c34` (coral)
- **Typography**: Apple system stack — `"SF Pro Display"` for headings, `"SF Pro Text"` for body
- **Easing**: `--ease: cubic-bezier(0.28,0.16,0.22,1)` / `--ease-out: cubic-bezier(0.16,1,0.3,1)`
- **Layouts**: `.wrap` (max 1200px) and `.wrap-narrow` (max 820–980px, varies by page)

When editing tokens, **update every file** — there is no single source of truth for the design system.

`work.html` and `index.html` each carry a `.cs-card` per case study, and every case study's "next case study" strip links to the next one in a loop (geniaus → genie → peepal → resolvenow → rap → yulu → geniaus). **Adding a case study means touching four places**: the new file, both card lists, and the previous case study's next-strip.

`case study page.html` is stale — nothing links to it. Leave it alone or delete it; don't add to it.

The Yulu case study embeds `yulu-prototype.html` in an iframe. That file deliberately uses its own product design system (IBM Plex, Yulu blue) rather than the portfolio tokens — it is the product's UI, not site chrome.

### Images and media

- **Never inline images as base64 `data:` URIs.** That is what made the Genie and GenIAus pages 2–2.5MB: the photos couldn't be cached, lazy-loaded, or decoded off the main thread. Case-study images live in `images/<page>/` (e.g. `images/genie/`); reference them with `loading="lazy" decoding="async"`.
- Card covers are 1200px JPEGs in `homepage card images/` (the 1920px PNGs are originals, kept off the live site).
- Video must be `.mp4` (H.264). Chrome and Edge refuse `video/quicktime`, so `.mov` files don't play.

### Deployment

Cloudflare serves the whole repo root as static assets (`wrangler.toml`). **`.assetsignore` keeps non-site files off aalveedamle.com** — tooling, `*.md`, `wrangler.toml`, raw source media. Add any new file that isn't part of the website there, or it becomes publicly downloadable.

### JavaScript Behaviors (shared pattern)

Inlined on every page:

1. **Theme** — a tiny inline script right after `<meta charset>` applies the saved `localStorage` `aalvee-theme` before first paint (so light-mode visitors don't get a dark flash); the toggle button at the bottom reads/writes the same key.
2. **Reveal-on-scroll** — `IntersectionObserver` adds `.in` to `.reveal` elements; falls back to adding `.in` immediately if `IntersectionObserver` is unavailable.
3. **Cursor dot** — one 24px decorative follower with time-based easing that stops its `requestAnimationFrame` loop once it catches up. **The native cursor stays visible — don't reintroduce `cursor: none`**; with it, any main-thread hitch made the "cursor" itself lag. Hidden on touch, coarse pointers, ≤768px, and `prefers-reduced-motion`.
4. **Nav** — hide on scroll-down / show on scroll-up, colour flip over `[data-nav-invert]` sections. Case studies also build a table-of-contents sidebar. Both do their scroll work at most once per frame via `requestAnimationFrame`; keep new scroll handlers the same way (no layout reads per scroll event).
5. **Clock** — US Eastern time; the `EST`/`EDT` label comes from `Intl`, so it follows daylight saving.

The homepage hero grid is drawn on a single `<canvas>` (the "Hero grid background" script) that reproduces a perspective diamond grid with a hover tint. It replaced 2,704 `<div>`s on a 3D-transformed plane, which was the heaviest thing on the site to paint and hit-test — don't go back to DOM cells. No page uses GSAP.

The About page loads **Google Fonts "Caveat"** for handwritten annotation styling.

## Conventions

- `prefers-reduced-motion` is respected: animations and the cursor dot are disabled via media query blocks near the bottom of each `<style>` section.
- Responsive breakpoints are `720px` (mobile nav, padding) and `900px` (two-column grids).
- Section padding uses `clamp()` for fluid spacing.
- The `.reveal` / `.in` animation pattern is the standard way to add scroll-triggered entrance animations. **Gotcha:** `.reveal.in { transform: none }` has the same specificity as `.card:hover` and comes later, so it silently cancels hover transforms (and replaces the element's own `transition`). An element that is both `.reveal` and has a hover lift needs a `.card.reveal.in:hover { transform: … }` rule placed after `.reveal.in` — see the existing ones in `index.html`, `work.html`, and the strategy pages.
