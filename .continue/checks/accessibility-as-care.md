---
name: Accessibility as Care
description: The site should work for everyone — not just developers on MacBook Pros, but the people you love who don't have a framework for what's happening.
---

# Accessibility as Care

## Context

The audience for this site is not just San Francisco developers. It's also the sister in Green Bay, the parents in Michigan, the people who are finding themselves growing through a world they didn't sign up for. The site should meet them where they are — on whatever device, with whatever needs, in whatever state of attention.

This isn't about passing an audit. It's about care. The `prefers-reduced-motion` media query exists because some people get nauseated by scroll animations. The `loading="lazy"` attributes exist because some people are on slow connections. The `:focus-visible` outlines exist because some people navigate with a keyboard. Each of these is a small act of noticing that someone exists and making room for them.

## What to Check

### 1. Reduced Motion Is Respected

The site uses scroll-triggered fade-up animations and a pulsing scroll hint. All of these must be disabled when `prefers-reduced-motion: reduce` is set. The current implementation (lines 460-483 of `index.html`) sets `animation-duration: 0.01ms`, `transition-duration: 0.01ms`, and forces `opacity: 1` / `transform: none` on all animated elements. Don't add new animations without also disabling them in this media query.

GOOD:
```css
@media (prefers-reduced-motion: reduce) {
  .new-animated-element {
    opacity: 1;
    transform: none;
    animation: none;
  }
}
```

BAD: Adding a new CSS animation without a reduced-motion override.

### 2. Images Have Descriptive Alt Text

Every `<img>` must have an `alt` attribute that describes the artistic style and composition — not just "image" or empty string. These images carry meaning in the essay's argument. A screen reader user should understand what role the image plays. (See also: visual cohesion check, rule #5.)

### 3. Keyboard Navigation Works Everywhere

Every interactive element (links in the essay, the CTA, footer links) must be reachable via Tab and visually indicated with `:focus-visible` styles. The focus outlines use lavender (`--lavender`) to match the site palette. Don't add interactive elements without focus styles.

### 4. Font Sizes Are Readable

The base font size is 18px on desktop, 16px on tablet. Body text is `1.15rem` with `line-height: 1.85`. These are intentionally generous for readability. Don't shrink body text below 1rem or reduce line-height below 1.6. The essay is meant to be read slowly — give the words room.

### 5. Color Contrast Is Sufficient

Body text uses `--ink-light` (#4a4843) on `--cream` (#F8F6F1). This meets WCAG AA contrast requirements. The lavender accent (`--lavender`, #7B6FA0) is used for emphasis on large text (pull quotes, headings) where contrast requirements are lower. Don't use lavender for small body text — it's too light.

### 6. The Supporters Page Is Also Accessible

The supporters layout (`_layouts/supporters.html`) must maintain the same accessibility standards: readable font sizes, focus styles on all links, sufficient contrast, and reduced-motion support.

## Key Files to Check

- `index.html` — Animations, focus styles, font sizes, alt text, color usage
- `404.html` — Focus styles on the back link
- `_layouts/supporters.html` — Focus styles, font sizes, column layout readability

## Exclusions

- Image file optimization (compression, format) — that's a performance concern, not accessibility
- Browser-specific rendering bugs — test but don't over-engineer
