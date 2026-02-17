---
name: Resist Complexity
description: The site is HTML, CSS, and images. That's the point. Don't add what you don't need.
---

# Resist Complexity

## Context

This site is one HTML file, one 404 page, one Jekyll layout for supporters, a handful of images, and three discoverability files. There is no build pipeline worth speaking of — Jekyll copies the HTML unchanged, renders two markdown files, and that's it. The entire site could be served from a USB stick.

This simplicity is not a temporary state on the way to something more sophisticated. It is the architecture. The person who built this site spent years in the optimization-industrial complex and came out the other side believing that "trying to use the system to break the system only broke me further." The site embodies the opposite: do less, but mean it.

Every dependency is a future liability. Every build step is a thing that can break at 2am. Every abstraction is a layer between the words and the person reading them. The essay argues that developers should handle the signal while AI handles the volume — the site itself should be pure signal.

## What to Check

### 1. No New Build Dependencies

Don't add npm, webpack, Tailwind, PostCSS, Sass, or any other build tool. The CSS is inline in `<style>` tags. The JS is inline in `<script>` tags. This is not a problem to solve — it's a decision that was made.

GOOD: Writing CSS directly in the `<style>` block of `index.html`.

BAD: Adding a `package.json` to install a CSS framework.

### 2. No JavaScript Frameworks

The site uses vanilla JS — one IntersectionObserver for scroll animations and one `addEventListener` for grid lines. That's ~20 lines. Don't add React, Vue, Alpine, htmx, or any other framework. If something needs interactivity, write it in vanilla JS or reconsider whether it needs interactivity at all.

### 3. No External Services

No analytics (Google Analytics, Plausible, Fathom). No error tracking (Sentry). No A/B testing. No chat widgets. No cookie consent banners. No newsletter services. The site doesn't need to know who visits it, how long they stay, or what they click. It's an essay. You read it or you don't.

### 4. No Premature Abstraction

Don't extract shared CSS into a separate file "for reuse" when there are only three HTML pages. Don't create a component system when each page is self-contained. Don't add a templating layer on top of the HTML that already works. Three similar `<style>` blocks across three files is better than one shared stylesheet that creates coupling.

### 5. The Gemfile Doesn't Grow

The Gemfile exists for Jekyll, which exists for `manifesto.md` and `supporters.md`. Don't add gems unless they directly serve those two files. When the Vercel migration happens, the Gemfile should be deletable without affecting the main site.

## Key Files to Check

- `Gemfile` — Should not gain new dependencies
- `_config.yml` — Should not gain new plugins
- Root directory — Should not gain `package.json`, `node_modules/`, `webpack.config.js`, `tailwind.config.js`, or similar
- `index.html` — Inline CSS and JS should stay inline

## Exclusions

- Adding new static HTML pages — that's fine, static HTML is the whole point
- Adding new images — images are content, not complexity
- Updating existing Jekyll dependencies for security patches
