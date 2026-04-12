# Art Portfolio — Zeeshan Yousuf

A single-page digital art portfolio built with HTML, CSS, Three.js, and GSAP. Hosted on GitHub Pages.

**Live site:** [smartzee797.github.io/art-portfolio](https://smartzee797.github.io/art-portfolio/)

---

## Sections

### Hero
Full-viewport landing with the artist name and a blurred mosaic grid of artwork in the background. The mosaic images are base64-inlined for instant rendering with zero network requests. Includes WebGL particle effects (Three.js) that follow the cursor and a teal-themed ambient particle field.

### About
Split layout — left side shows a 3x3 grid of featured artwork (base64-inlined), right side has a stylized portrait placeholder and artist bio. The section uses a white background with decorative vector elements for contrast.

### Creative Process
Interactive showcase of the artistic process across three artworks:
- **Hand Study** — gesture and anatomy progression
- **The Moment** — ink-to-color sci-fi illustration
- **Tau Ceti** — sketch-to-final planet scene

A vertical selector on the left lets you switch between artworks. Each shows 5 phases with arrow connectors illustrating the progression from initial concept to final piece.

### Gallery
Masonry-style grid displaying 39 artwork thumbnails in a 4-column layout. Each piece shows a number and tag overlay on hover with a teal glow effect. Uses CSS columns for natural aspect-ratio preservation. Images are lazy-loaded as the user scrolls.

### Footer
Compact single-line footer with copyright, social media icons (Instagram, Behance, X, Dribbble) as inline SVGs, and a commission availability status indicator.

---

## Design System

| Element | Value |
|---------|-------|
| Primary color | `#0D7377` (teal) |
| Accent color | `#D43F3F` (red dot) |
| Glow color | `#14B8B8` (teal glow) |
| Background | `#000000` (black) |
| Heading font | Inter (sans-serif) |
| Mono font | Space Mono (monospace) |

---

## Performance

The site is optimized for fast loading on GitHub Pages:

- **Hero background:** 12 images inlined as base64 (~48KB) — zero HTTP requests
- **About grid:** 9 images inlined as base64 at 400px (~300KB) — zero HTTP requests
- **Process selectors:** 3 thumbnails inlined as base64 — zero HTTP requests
- **Process phases:** 250px optimized JPEGs (~18KB each), active series loads eagerly
- **Gallery:** 600px thumbnails (~70KB each), lazy-loaded on scroll
- **Initial page load:** ~650KB (HTML with all base64 + CDN scripts)
- **Total assets:** ~4MB (loaded progressively)

### Image Pipeline

| Layer | Size | Quality | Usage |
|-------|------|---------|-------|
| Full-res originals | 2048px+ | Original | Not deployed (in `.gitignore`) |
| Gallery thumbnails | 600px | JPEG 70% | `art/thumb/` — lazy-loaded in gallery |
| Process phases | 250px | JPEG 50% | `phases/micro/` — shown in process section |
| About grid | 400px | JPEG 75% | Base64 inlined in HTML |
| Hero mosaic | 60px | JPEG 30% | Base64 inlined in HTML (CSS blur hides low res) |

---

## Tech Stack

- **HTML/CSS** — single-file, no build step
- **Three.js** (r134) — WebGL background particles
- **GSAP** (3.12.5) + ScrollTrigger — scroll animations
- **Google Fonts** — Inter + Space Mono
- **GitHub Pages** — static hosting

---

## Local Development

Just open `index.html` in a browser. No build tools or server required.

```bash
open index.html
```

---

## Deployment

Hosted via GitHub Pages from the `main` branch. Any push to `main` automatically triggers a rebuild.

```bash
git add -A && git commit -m "Update portfolio" && git push
```

---

## File Structure

```
art-portfolio/
  index.html          # Entire site (single file, ~650KB with base64)
  .gitignore           # Excludes full-res originals
  README.md
  art/
    thumb/             # 600px gallery thumbnails (deployed)
    *.JPG / *.PNG      # Full-res originals (gitignored)
  phases/
    micro/             # 250px process phase images (deployed)
    *.JPG              # Full-res phase originals (gitignored)
```
