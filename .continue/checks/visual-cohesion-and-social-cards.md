---
name: Visual Cohesion & Social Card Quality
description: Ensure all visual assets are cohesive with the site's two-register aesthetic and social cards feel epic when shared.
---

# Visual Cohesion & Social Card Quality

## Context

This site's imagery is a dialogue between two artistic registers, documented in HTML comments throughout `index.html`:

- **Nate's pieces** (`hero-*.webp`) — structure-first, architectural scaffolding with organic life breaking through. Isometric grids, brutalist geometry, branches pushing out.
- **Ty's pieces** (`ty-*.png`) — organic-first, watercolor bleeding outward with geometry crystallizing from it. Indigo/lavender washes, technical pen lines emerging from fluid forms.

These two registers alternate throughout the essay to mirror the site's thesis: structure and life aren't opposed — they amplify each other. The palette is intentional: cream (`#F8F6F1`), lavender (`#7B6FA0`), blue-ink (`#4A5A8A`), indigo (`#4f46e5`), with white/cream backgrounds that work with `mix-blend-mode: multiply`.

When someone shares a link on Twitter, LinkedIn, or Slack, the social card (`images/og.webp`) is the first impression. It must exist and feel like it belongs.

## What to Check

### 1. OG/Social Meta Tags Point to Real Assets

Every `og:image` and `twitter:image` meta tag must reference an image that actually exists in the repo. A broken social card is worse than no card at all.

GOOD:
```html
<meta property="og:image" content="https://amplified.dev/images/og.webp">
<!-- AND images/og.webp exists in the repo -->
```

BAD:
```html
<meta property="og:image" content="https://amplified.dev/images/og.webp">
<!-- BUT images/og.webp does NOT exist — social cards will be blank -->
```

### 2. Two-Register Image Curation

Images in the essay alternate between Nate's architectural register and Ty's organic register. New images must belong to one of these two voices — not a third style. The HTML comments above each image block document which register it belongs to and why.

- Nate images: geometric grids, isometric structures, scaffolding, branches growing *through* architecture
- Ty images: watercolor washes, root systems, heartwood rings, river deltas, city grids as living tissue, geometry *emerging from* organic forms
- Both use white/cream backgrounds, indigo-to-lavender color range, fine pen lines

GOOD: Adding a new Ty-register image with a comment block explaining the prompt, the emotional beat, and why it sits where it does in the essay.

BAD: Adding a stock photo, a flat vector, or a third artistic style that breaks the two-voice dialogue.

### 3. Image Dimensions and Performance

- OG image (`og.webp`): must be 1200x630, rendered from the hero section composition (hero image + site title + heading on cream background with noise texture). It is a standalone rendered card, not a raw copy of a hero image.
- Page images: 1024x1024 source is fine — they render at 300-500px via CSS layout classes
- All non-hero images must use `loading="lazy"` to avoid loading 8 images on first paint
- No image should exceed ~300KB — the current largest is `ty-heartwood.png` at 295KB

### 4. Page Images Are Never Deleted or Replaced Without Intent

The curated image set (`hero-7.webp`, `hero-5.webp`, `hero-8.webp`, `hero.webp`, `ty-roots.png`, `ty-heartwood.png`, `ty-delta.png`, `ty-city.png`) is fixed. These are original artworks, not interchangeable assets. Do not delete, rename, or swap them. The only image that can be regenerated freely is `og.webp` — it's a rendered social card, not original art.

GOOD: Updating `og.webp` with a new render that better matches the current site design.

BAD: Deleting `ty-heartwood.png` because "it's not referenced" after a refactor — it's an original artwork and part of the curated set.

### 5. Alt Text Describes Art Direction, Not Just Content

Alt text should describe the artistic style and composition, not just "an image." This is an art-directed editorial site, not a docs page.

GOOD:
```html
<img src="images/ty-roots.png"
     alt="Watercolor roots spreading underground, geometry crystallizing where color is densest" />
```

BAD:
```html
<img src="images/ty-roots.png" alt="decorative image" />
```

### 6. Every Page Belongs to the Same World

The site is more than `index.html`. The 404 page (`404.html`), the supporters page (`_layouts/supporters.html` + `supporters.md`), and any future pages must share the same cream background, noise texture, serif/sans typography, and lavender accent color. A visitor who hits a 404 or clicks through to supporters should never feel like they left the site.

GOOD: `404.html` uses the same `--cream`, `--serif`, `--lavender` variables, noise texture overlay, and on-brand copy ("This page *moved up*").

BAD: A 404 page using the default Jekyll theme with white background and system fonts.

### 7. Focus Styles Use the Site Palette

Every interactive element (links, buttons) must have `:focus-visible` styles using the lavender accent — not the browser default blue outline. This is both accessibility and aesthetic: keyboard users should feel like the site was designed for them too.

GOOD:
```css
.closing a:focus-visible {
  outline: 1.5px solid var(--lavender);
  outline-offset: 3px;
  border-radius: 2px;
}
```

BAD:
```css
/* No focus styles at all, or browser default blue ring */
```

## Key Files to Check

- `index.html` — Meta tags, `<img>` elements, focus styles, and the HTML comments documenting image curation intent
- `404.html` — Must match site aesthetic
- `_layouts/supporters.html` — Must match site aesthetic
- `images/` — All visual assets; currently `hero-7.webp`, `hero-5.webp`, `hero-8.webp`, `hero.webp`, `ty-roots.png`, `ty-heartwood.png`, `ty-delta.png`, `ty-city.png`, `og.webp`

## Exclusions

- `manifesto.md` — Text-only content rendered by Jekyll's default layout (legacy)
- CSS-only changes that don't add or swap images
