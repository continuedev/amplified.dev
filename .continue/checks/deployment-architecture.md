---
name: Deployment Architecture Awareness
description: Ensure changes are compatible with the static site pipeline and don't introduce unnecessary build dependencies.
---

# Deployment Architecture Awareness

## Context

This site is deployed via Netlify, which auto-detects Jekyll from the `Gemfile` and `_config.yml`, runs `jekyll build`, and serves the `_site/` output from the `main` branch. The custom domain `amplified.dev` is configured in the Netlify dashboard. There is no `netlify.toml` — everything is inferred.

The main page (`index.html`) is a fully standalone HTML file with inline CSS, inline JS, and no Jekyll dependencies. Jekyll merely copies it to `_site/` unchanged. The only files that use Jekyll's markdown rendering are `manifesto.md` and `supporters.md`.

The image set is a mix of `.webp` (Nate's architectural pieces) and `.png` (Ty's watercolors) — all served as static files with no build-time processing.

A migration to Vercel is planned, at which point the Jekyll dependency can be dropped entirely in favor of a zero-build static deploy.

## What to Check

### 1. No Unnecessary Jekyll Dependencies

New pages should not introduce Jekyll-specific features (Liquid tags, front matter, `_includes`, `_data`). The site is moving toward plain static HTML.

GOOD:
```html
<!-- Self-contained HTML page with inline styles -->
<!DOCTYPE html>
<html lang="en">
<head>...</head>
<body>...</body>
</html>
```

BAD:
```html
---
layout: default
title: New Page
---
{{ site.title }}
{% include header.html %}
```

### 2. Assets Are Repo-Relative, Not Build-Dependent

Image paths in `index.html` are relative (`images/hero-7.webp`). Meta tags use absolute URLs (`https://amplified.dev/images/og.webp`). Don't introduce asset pipelines, CDN references, or build-time path rewriting.

GOOD:
```html
<img src="images/hero-7.webp" alt="..." />
<meta property="og:image" content="https://amplified.dev/images/og.webp">
```

BAD:
```html
<img src="{{ '/assets/images/hero-7.webp' | relative_url }}" alt="..." />
<img src="https://some-cdn.com/hero-7.webp" alt="..." />
```

### 3. Every Push to Main Is a Production Deploy

There is no staging environment or preview deploy. Every push to `main` triggers a production build on Netlify. Changes should be reviewed before merging to `main`, not after. This is especially important for image changes — a broken `og:image` reference means broken social cards immediately.

### 4. Keep the Build Minimal

Don't add gems, plugins, or build steps to `Gemfile` or `_config.yml` unless they serve `manifesto.md` or `supporters.md`. The goal is to eventually drop the build entirely. When the Vercel migration happens, the site should work by pointing Vercel at the repo root with no build command.

## Key Files to Check

- `index.html` — Main page, must remain fully self-contained
- `_config.yml` — Jekyll config, should stay minimal
- `Gemfile` — Build dependencies, avoid adding new ones
- `images/` — Static assets served as-is (mix of `.webp` and `.png`)

## Exclusions

- Changes to `supporters.md` or `manifesto.md` — these legitimately use Jekyll's markdown rendering
- CSS/JS changes within `index.html` — these don't affect the build pipeline
