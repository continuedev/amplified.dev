---
name: Visual Cohesion & Social Card Quality
description: Ensure all visual assets — especially OG/social cards — are cohesive with the site's design identity and feel epic when shared.
---

# Visual Cohesion & Social Card Quality

## Context

This site has a strong, intentional aesthetic: cream backgrounds (`#F8F6F1`), watercolor-meets-architectural illustrations, lavender/blue-ink tones, and elegant serif/sans typography (Cormorant Garamond + DM Sans). When someone shares a link on Twitter, LinkedIn, or Slack, the social card is the first impression. It needs to feel like it belongs to the same world as the site — not like an afterthought or a generic placeholder. The OG image (`images/og.webp`) is referenced in `index.html` meta tags and must actually exist and look intentional.

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

### 2. Visual Consistency With Site Palette

Any new images added to the site should feel like they belong to the existing visual language:

- Watercolor/architectural illustration style with organic elements (branches, botanicals) growing through geometric structures
- Color palette: cream, lavender (`#7B6FA0`), blue-ink (`#4A5A8A`), ink (`#1a1917`)
- Light, airy backgrounds that work with `mix-blend-mode: multiply` on the cream body
- No stock photos, no flat vector illustrations, no neon colors — these break the editorial, gallery-like tone

GOOD: A watercolor illustration of branches growing through isometric grid structures in purple/blue tones on a white/cream background.

BAD: A bright gradient banner with bold sans-serif text and a tech-startup look.

### 3. Image Dimensions for Social Sharing

OG images should work well when cropped to common social card aspect ratios:

- Ideal OG image: 1200x630 (1.91:1 ratio) for `summary_large_image` Twitter cards and LinkedIn previews
- If using a square source image (like the hero illustrations), the focal point should be centered so it survives center-cropping
- The image should be legible and visually striking at small sizes (social cards render ~500px wide in feeds)

### 4. Hero Images Match the Essay Tone

Images interspersed throughout the essay in `index.html` should:

- Alternate layouts naturally (`.layout-right`, `.layout-left`, `.layout-center`, `.layout-full`, `.image-pair`)
- Not repeat the same image twice in close proximity
- Progress in visual intensity — lighter/simpler near the top, more complex further down
- Have meaningful `alt` text that describes both the artistic style and composition

GOOD:
```html
<img src="images/hero-9.webp" alt="Architectural watercolor — tree growing through isometric structure" />
```

BAD:
```html
<img src="images/hero-9.webp" alt="image" />
```

## Key Files to Check

- `index.html` — All `og:image`, `twitter:image` meta tags and inline `<img>` elements
- `images/` — All visual assets, especially `og.webp`

## Exclusions

- `supporters.md` — No visual content
- `manifesto.md` — Text-only content
- Changes that only modify CSS without adding/changing images
