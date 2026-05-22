# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is a personal portfolio website for Aalvee Damle (Senior Product Designer). It is a collection of standalone, self-contained HTML files — no build system, bundler, package manager, or framework. Open any file directly in a browser to view it.

## File Map

| File | Purpose |
|---|---|
| `aalvee_homepage_v14.html` | Main landing page — hero, case study grid, testimonials, contact |
| `aalvee_about_v3.html` | About page |
| `case study page.html` | Case studies index |
| `aalvee_case_geniaus_v2.html` | Geniaus case study (GenAI copilot for auditors, EY) |
| `aalvee_case_genie_v1.html` | Genie case study (wealth platform, US bank) |
| `aalvee_case_peepal_v2.html` | Peepal case study (AgriTech for World Bank) |

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

### JavaScript Behaviors (shared pattern)

All pages use the same three JS modules, inlined at the bottom of each file:

1. **Theme toggle** — reads/writes `localStorage` key `aalvee-theme`; toggles `data-theme` attribute on `<html>`
2. **Reveal-on-scroll** — `IntersectionObserver` adds `.in` class to `.reveal` elements; falls back to adding `.in` immediately if `IntersectionObserver` is unavailable
3. **Cursor trail** — 15 DOM divs lerped behind the cursor (factor 0.3); disabled on touch/coarse-pointer devices and when `prefers-reduced-motion` is set

The homepage additionally loads **GSAP 3.12.5 via CDN** for the hero dot field (160 SVG `<circle>` elements with parallax on `mousemove`). No other page uses GSAP.

The About page loads **Google Fonts "Caveat"** for handwritten annotation styling.

### Placeholder URLs

The homepage contains unfilled placeholder strings that need real URLs:
- `GENIAUS_CASE_URL_HERE`
- `GENIE_CASE_URL_HERE`
- `PEEPAL_CASE_URL_HERE`
- `UX_STRATEGIES_URL_HERE`
- `ABOUT_URL_HERE`

Search for these before publishing.

## Conventions

- `prefers-reduced-motion` is respected: all animations and the cursor trail are disabled via a single media query block near the bottom of each `<style>` section.
- Responsive breakpoints are `720px` (mobile nav, padding) and `900px` (two-column grids).
- Section padding uses `clamp()` for fluid spacing.
- The `.reveal` / `.in` animation pattern is the standard way to add scroll-triggered entrance animations.
