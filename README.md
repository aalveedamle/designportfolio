# aalveedamle.com

The source for my portfolio — case studies in designing trust into high-stakes systems: AI/risk, banking, and civic tech.

**→ [aalveedamle.com](https://aalveedamle.com)**

<br>

## Why it looks like this

No framework, no bundler, no package manager. Every page is a single self-contained `.html` file with its CSS in a `<style>` block and its JS at the bottom. You can open any file directly in a browser and it works.

That's a deliberate constraint, not laziness. A portfolio is six or seven pages that change a few times a year. A build step would add a dependency graph to maintain, a thing to break at deploy time, and nothing a visitor would ever notice. The cost of duplicating the nav across files is lower than the cost of a toolchain.

## Structure

| File | |
|---|---|
| `index.html` | Landing page — hero, case study grid, testimonials, contact |
| `work.html` | Case study index |
| `aalvee_about_v3.html` | About |
| `aalvee_case_*.html` | One file per case study (GenIAus, Genie, Peepal, ResolveNow, RAP, Yulu) |
| `aalvee_strategy_*.html` | UX strategy write-ups |
| `yulu-prototype.html` | Standalone interactive prototype embedded in the Yulu case study |
| `yulu-wireframes.html` | Annotated wireframe set for the Yulu case study |

## Design system

Tokens live in a `:root` block with a `[data-theme="light"]` override, duplicated identically across pages.

- Dark by default; theme choice persists in `localStorage`
- Accent: `#E9F056` lime (dark) / `#ff5c34` coral (light)
- Type: SF Pro Display for headings, SF Pro Text for body
- Layout: `.wrap` at 1200px, `.wrap-narrow` at 820–980px
- Breakpoints: 720px (mobile nav) and 900px (grid collapse)

`yulu-prototype.html` intentionally ignores all of the above and uses IBM Plex and Yulu's blue — it's the product's UI, not site chrome.

## Motion

Three behaviours, inlined on every page: a theme toggle, an `IntersectionObserver` reveal-on-scroll, and a 15-node cursor trail. The homepage additionally uses GSAP for the hero dot field — 160 SVG circles with parallax on `mousemove`.

All of it is disabled under `prefers-reduced-motion`, and the cursor trail is skipped entirely on coarse-pointer devices.

## Running it

```bash
open index.html
```

That's it. For a local server:

```bash
python3 -m http.server 8000
```

## Deploying

Pushing to `main` triggers a Cloudflare Workers build, which publishes to aalveedamle.com. Static assets are served from the repo root via the `ASSETS` binding in `wrangler.toml`.

---

Design and code by [Aalvee Damle](https://www.linkedin.com/in/aalvee-damle/).
