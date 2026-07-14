# Aalvee Damle — Brand Guidelines

**Source of truth for all visual, verbal, and motion decisions across the portfolio.**
Read alongside [CLAUDE.md](CLAUDE.md), which documents the current technical implementation. This file documents *why* things should look and move the way they do, and how to extend them. When a future design decision conflicts with this document, name the conflict explicitly and resolve it here — not silently in code.

**Reference source:** [fiasco.design](https://fiasco.design), a London brand & digital agency, studied live on 2026-07 — every value below (hex codes, font names, pixel radii, timing values, class names) was read directly out of the rendered page's computed styles and DOM, not estimated. This supersedes all earlier moodboard-based directions in this file's history. Two things are Fiasco's own IP and are named for reference only, not reproduced verbatim: their exact copy/wordmark, and their two licensed commercial typefaces (noted in Section 3, with a free fallback stack so nothing here depends on an unlicensed asset).

---

## 1. What Makes Fiasco's System Work

Five mechanics carry almost the entire experience, and none of them are decorative — each one is solving a real communication problem:

1. **The nav disappears when you don't need it.** It hides on scroll-down and reappears on scroll-up, so long-form case-study pages stay uncluttered without ever losing quick access back to navigation.
2. **The nav (and the logo inside it) flips color depending on what's behind it.** Dark sections get a white nav; light sections get a black nav. The site never needs a manually-placed "light hero" vs "dark hero" nav variant — one mechanism handles every page.
3. **One accent color, used as a full-bleed event, not a decoration.** Off-black and off-white carry ~90% of the site. A single saturated yellow shows up in exactly two places: the CTA band and the mobile menu takeover. Because it's rare, it reads as a moment, not a brand color scattered everywhere.
4. **Type does two jobs with two faces.** A grotesque sans carries navigation, UI, and most body copy — the "operating" voice. A serif, always italic, carries eyebrows and single emphasized words dropped into an otherwise-sans headline — the "feeling" voice, deployed a word or two at a time, never as a whole paragraph.
5. **Interactivity is proof of craft, kept small.** Nav links split into a character each so they can roll on hover. Project tiles swap a static frame for a looping video only once you're actually looking at them. Nothing animates unless a person is present to see it.

---

## 2. Color System

### Base (carries ~90% of every page)

| Token | Hex | Role |
|---|---|---|
| `--ink` | `#1D1E19` | Off-black. Primary text, dark-page backgrounds, footer, buttons |
| `--paper` | `#F8F9F3` | Off-white. Primary page background, text-on-dark |
| `--grey` | `#D8D8D8` | Borders, dividers, disabled states |

Neither black nor white is pure — `#1D1E19` has a hair of warmth, `#F8F9F3` a hair of green. Pure `#000`/`#FFF` would read colder and cheaper; the off-shades are what make the neutral palette feel considered rather than default.

### Accent (each with a tint and a shade — used sparingly, one at a time)

| Hue | Base | Tint (lighter) | Shade (darker) | Where Fiasco uses it |
|---|---|---|---|---|
| Yellow | `#FFF714` | `#FFFB86` | `#DCD401` | The one true brand accent — full-bleed CTA band, mobile menu takeover |
| Green | `#03AC47` | `#4AD782` | `#06873A` | Stat callouts, insight-card tagging |
| Blue | `#84BDFF` | `#B5D7FF` | `#6B94C4` | Stat callouts, insight-card tagging |
| Pink | `#FCC5FE` | `#FEE0FF` | `#CB8BCD` | Stat callouts, insight-card tagging |
| Orange | `#FD6B01` | `#FF9F59` | `#BF5101` | Stat callouts, insight-card tagging |

**The rule that matters more than the hex codes:** exactly one accent is ever a *brand* color (full-bleed section, primary CTA) at a time. The other four exist only as small, content-driven flourishes — a stat's numeral, a card's tag dot — never as a second competing full-bleed moment on the same page. Fiasco's homepage uses yellow as the only full-bleed accent; green/blue/pink/orange appear only inside small stat cards and insight thumbnails, never as a section background.

### Opacity utilities (for overlays, not solid fills)

| Token | Value | Use |
|---|---|---|
| `--opacity-05` / `-10` / `-25` / `-50` | `rgba(29,30,25, .05 / .1 / .25 / .5)` | Scrims and overlays on light backgrounds |
| `--opacity-w05` / `-w10` / `-w25` / `-w50` | `rgba(248,249,243, .05 / .1 / .25 / .5)` | Scrims and overlays on dark backgrounds |

### Page-level theming (not a toggle — a per-page editorial choice)

Fiasco doesn't have one fixed dark/light mode. Individual pages commit fully to one theme: the homepage is `--paper` background / `--ink` text throughout; the Approach page is `--ink` background / `--paper` text throughout, section to section. Within a page, individual blocks can carry a `dark` modifier class to flip locally (the footer is always dark even on light pages). Decide the theme per page based on the content's emotional register — reflective/strategic pages (Approach, About) can commit to dark; scannable/proof pages (Work, case studies) default to light — rather than mechanically alternating.

---

## 3. Typography

### The pairing

| Role | Fiasco's actual face | Job | Free fallback stack for this portfolio |
|---|---|---|---|
| Display / UI / body | **Area Normal** (licensed, Displaay) | Navigation, buttons, most body copy, headline base | `-apple-system, BlinkMacSystemFont, 'Segoe UI', 'Helvetica Neue', Arial, sans-serif` |
| Editorial serif | **HAL Timezone** (licensed) | Italic-only: eyebrows, and single emphasized words dropped into sans headlines | `'New York', 'Iowan Old Style', 'Palatino Linotype', Georgia, serif` (italic) |

To reproduce Fiasco's exact type feel, license Area Normal and HAL Timezone. Until then, the fallback stack above preserves the same *role* split — a quiet grotesque for operating, a warm italic serif for feeling — which is the part that actually carries the brand, not the specific letterforms.

### The signature move: mixed-face headlines

Fiasco's headlines are not set in one face. A sentence runs in the sans, and one or two words mid-sentence drop into italic serif for emphasis:

> We believe in the power of *emotion* to drive meaningful *growth*.

This is the single most distinctive typographic habit on the site — more than the specific fonts, it's *this pattern* (sans sentence, serif word, sans sentence) that should carry over. Use it on hero statements and section headers; never on body paragraphs, where it would read as decoration rather than emphasis.

### Scale

| Use | Face | Size (desktop) | Weight | Letter-spacing |
|---|---|---|---|---|
| Hero statement | Sans + italic serif emphasis | ~47px | 400 | -0.94px (tight) |
| Body | Sans | 20px (base) | 400 | normal |
| Eyebrow label | Italic serif | ~19px | 400 italic | normal |
| Nav / UI | Sans | 16px | 400 | -0.32px |
| Footer giant wordmark | Sans | ~22vw (cropped at viewport edge) | 700 | tight |

Note the base body size: **20px, not 16px.** This is a deliberate premium-editorial signal — everything reads slightly larger and more generous than a typical SaaS site.

---

## 4. Motion System

Two tokens govern every transition on the site:

```css
--duration: .2s;
--ease: cubic-bezier(0, 0, 0, 1);
```

This curve starts at full speed and decelerates hard into the landing — nothing eases in, everything *lands*. It reads as snappy and confident rather than soft. Use it everywhere instead of a generic `ease` or `ease-in-out`.

### Nav — hide on scroll-down, show on scroll-up

The nav is `position: fixed`, height 90px. A scroll listener compares the current scroll position to the previous one each frame:

- Scrolling **down** → nav gets `translateY(-100%)` (fully hidden above the viewport)
- Scrolling **up** (any amount) → nav gets `translateY(0)`, `transition: transform var(--duration) var(--ease)`
- At the very top of the page, always shown regardless of direction

### Nav — color flip based on what's underneath

Every section that needs a dark background carries a plain `.dark` class. An `IntersectionObserver` (or equivalent scroll check) watches which section currently sits directly behind the fixed nav's vertical position and toggles a `nav--color-flip` class on the nav itself:

- Section behind nav has `.dark` → nav text/logo becomes `--paper` (white)
- Section behind nav is light → nav text/logo becomes `--ink` (black)
- Transition: `color var(--duration) var(--ease)` — no crossfade delay, matches the snap-to-position curve

This is what lets a single fixed nav sit correctly over a page that alternates between light and dark sections without ever needing a manual per-section override.

### Link hover — character lift (read directly from the site's JS bundle, not guessed)

This is implemented as a GSAP component (`LinkCharShift`), and the exact mechanic is more specific — and simpler — than a typical "roll" effect. Pulled straight from `main.js`:

```js
// Animations = { duration: { chars: .7 }, stagger: { chars: .02 },
//                ease: { anticipation: "anticipation" } }
// CustomEase.create("anticipation", "M0,0 C0.3,-0.43 0,1 1,1")

setupChars() {
  this.split = new SplitText(this.element, { type: "chars", charsClass: "char" });
}
onMouseEnter() {
  if (!this.params.canHover) return;
  this.params.canHover = false;
  if (this.hoverTL) { this.hoverTL.restart(); return; }
  this.hoverTL = gsap.timeline({
    onComplete: () => { gsap.set(this.chars, { yPercent: 0 }); this.params.canHover = true; }
  });
  this.hoverTL.to(this.chars, {
    yPercent: -76,
    duration: Animations.duration.chars,   // 0.7s
    ease: Animations.ease.anticipation,    // cubic-bezier(0.3, -0.43, 0, 1)
    stagger: Animations.stagger.chars,     // 0.02s per character
  });
}
onMouseLeave() { this.params.canHover = true; } // does NOT reverse the tween
```

The parts that actually matter and are easy to get wrong by assumption:

- **One `<span>` per character, not two.** There is no duplicate glyph sliding in from underneath — the letter itself lifts.
- **The link element has `overflow: hidden`.** As each character's `yPercent` approaches -76%, it's clipped by the link's own box, so it appears to lift up and off rather than just shifting position.
- **`yPercent: -76`, not -100.** The letter never fully exits before the reset; the number was tuned by eye, not derived from a round fraction — copy it exactly rather than rounding to -100.
- **The ease is a custom "anticipation" curve** (`cubic-bezier(0.3, -0.43, 0, 1)`) — the negative first control-point y-value means the letter dips *down* very slightly before lifting, a classic animation-principle "anticipation" wind-up. A plain ease-out reads flatter and misses this entirely.
- **The reset is instant, not animated** — `onComplete` does a hard `gsap.set(..., {yPercent:0})`, not a reverse tween. Implement this as removing the triggering class/animation rather than transitioning back to 0.
- **Leaving mid-hover does not cancel it.** `onMouseLeave` only clears a re-trigger flag; the lift plays to completion regardless of whether the pointer is still there. Don't wire this to `:hover` alone (which would reverse on mouse-out) — gate it with a JS flag so the full run always finishes.
- **Re-hovering restarts the same timeline** rather than creating a new one each time.

CSS-only implementation (no GSAP dependency): one `@keyframes` animating `transform: translateY(-76%)` with `animation-timing-function: cubic-bezier(0.3, -0.43, 0, 1)`, `animation-duration: .7s`, and a per-character `animation-delay` of `index * 0.02s`, all triggered by a JS-added class on `mouseenter` (guarded so a second `mouseenter` mid-run is ignored) and removed via `setTimeout` after the total run length — never wired to plain CSS `:hover`.

### Project cards — hover-to-video

Each project tile shows a static poster frame by default. On `mouseenter`, a `<video autoplay loop muted playsinline>` fades in over the poster and starts playing; on `mouseleave`, it fades back to the static frame (video pauses, doesn't unload, so replaying is instant). Aspect ratio locked at 16:9. This is what makes the work grid feel alive without autoplaying video for every visitor who never hovers a card.

### Sticky-hero + scroll-reveal stats

On the Approach page, the hero heading is pinned (`position: sticky` or an equivalent scroll-driven pin) while three stat cards scroll up from below and settle in front of it, slightly overlapping the now-dimmed hero text. This reads as the headline claim being immediately backed up by evidence, without needing a page break.

### Mobile menu — full-screen accent takeover

Below the nav's mobile breakpoint, "Menu" replaces the link row. Tapping it slides in a **full-viewport-height panel in the single brand accent color** (yellow) from the right edge, rounded on its leading corner, containing the same nav links stacked large, a close control, and the live clock repeated at the bottom. This is the boldest single moment in the whole system — the accent color, normally rationed to one CTA band, gets to fully take over the screen for this one interaction.

### Reduced motion

None of the above is essential to understanding the content — respect `prefers-reduced-motion: reduce` by disabling the character-roll and hover-video crossfade animations (swap instantly instead) and keeping the nav hide/show as an instant `display` change rather than a transform transition.

---

## 5. Small Details Worth Keeping

- **A live local-time clock** sits in the top-right of the nav (`01:43ᵁᴷ` — time plus a superscript timezone code), updating in real time. A small, human, "we're a real studio, here's what time it is for us" signal — recommend a version showing Aalvee's own local time zone.
- **Every link/button ends in `↘`** (south-east arrow), used consistently across CTAs, "Read more" links, even the cookie-consent buttons. One directional glyph, used everywhere, becomes a recognizable brand mark in its own right.
- **The footer ends in an oversized, deliberately cropped wordmark** — the brand name set at ~22vw, bleeding off both the left and bottom edges of the viewport so only part of it is ever visible without scrolling further. It's a signature, not a functional element.
- **CTA sections use a 40px top-corner radius against the section above**, creating a "peeling" effect where the accent-colored band appears to lift off the neutral page rather than sitting in a hard-edged rectangle.
- **Buttons are compact pills**: `border-radius: 800px` (effectively fully round), `padding: 8px 20px` — small and confident rather than large and shouty.

---

## 6. Layout & Grid

- Base font-size 20px establishes a slightly larger, more generous rhythm than typical 16px web body text — spacing scales should follow from this, not from a 16px assumption.
- Content grid reads as a 12-column system with named breakpoint suffixes (mobile-first, `-l` suffix for large/desktop overrides) — e.g. an 8-column block on desktop collapsing to full-width on mobile. Implement with standard CSS Grid `grid-template-columns: repeat(12, 1fr)` and span utilities rather than reproducing Fiasco's exact class names.
- Project grid: 2-column on desktop, single column on mobile, generous gutter, no card border — separation comes from whitespace and the image's own edge, not from a stroke or shadow.

---

## 7. Design Tokens (implementation-ready)

```css
:root {
  /* --- Base --- */
  --ink: #1D1E19;
  --paper: #F8F9F3;
  --grey: #D8D8D8;

  /* --- Accent (base / tint / shade) --- */
  --yellow: #FFF714;      --yellow-tint: #FFFB86;   --yellow-shade: #DCD401;
  --green:  #03AC47;      --green-tint:  #4AD782;   --green-shade:  #06873A;
  --blue:   #84BDFF;      --blue-tint:   #B5D7FF;   --blue-shade:   #6B94C4;
  --pink:   #FCC5FE;      --pink-tint:   #FEE0FF;   --pink-shade:   #CB8BCD;
  --orange: #FD6B01;      --orange-tint: #FF9F59;   --orange-shade: #BF5101;

  /* --- Overlay opacities --- */
  --opacity-05:  rgba(29,30,25,.05);   --opacity-w05:  rgba(248,249,243,.05);
  --opacity-10:  rgba(29,30,25,.10);   --opacity-w10:  rgba(248,249,243,.10);
  --opacity-25:  rgba(29,30,25,.25);   --opacity-w25:  rgba(248,249,243,.25);
  --opacity-50:  rgba(29,30,25,.50);   --opacity-w50:  rgba(248,249,243,.50);

  /* --- Type --- */
  --font-sans: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Helvetica Neue', Arial, sans-serif; /* Area Normal if licensed */
  --font-serif: 'New York', 'Iowan Old Style', 'Palatino Linotype', Georgia, serif; /* HAL Timezone if licensed */
  --font-size-base: 20px;

  /* --- Motion --- */
  --duration: .2s;
  --ease: cubic-bezier(0, 0, 0, 1);
  --nav-height: 90px;

  /* --- Shape --- */
  --radius-pill: 800px;
  --radius-cta: 40px;

  /* --- Theme-mapped roles (per-page, not per-toggle) --- */
  --bg: var(--paper);
  --fg: var(--ink);
  --accent: var(--yellow);
}

[data-page-theme="dark"] {
  --bg: var(--ink);
  --fg: var(--paper);
}
```

---

## 8. Adapting This for Aalvee Damle

- Keep the mechanic, adapt the identity: nav hide/show, color-flip, character-roll links, and the sticky-stat pattern are all content-agnostic and should be built exactly as specified. The accent color, wordmark, and copy voice should be Aalvee's own.
- Suggested accent: pick one saturated color to play the role Fiasco's yellow plays — a single full-bleed CTA/mobile-menu color, used nowhere else. This should be decided deliberately (see open question below), not defaulted to yellow just because that's what the reference uses.
- The mixed-face headline habit (sans sentence, italic serif emphasis word) is worth adopting as-is — it's a low-cost, high-signature typographic move independent of which two fonts are chosen.
- License Area Normal and HAL Timezone if the goal is a pixel-exact match; otherwise the fallback stack in Section 3 preserves the same role split.
- Case-study pages are the natural home for the hover-to-video project tiles (Section 4) — Aalvee's case studies already have rich visual assets that could support short looping clips per project.
