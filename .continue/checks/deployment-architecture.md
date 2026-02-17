---
name: Deployment Architecture Awareness
description: Ensure changes are compatible with the static site deployment pipeline and don't introduce unnecessary build dependencies.
---

# Deployment Architecture Awareness

## Context

This site is deployed via Netlify, which auto-detects Jekyll from the `Gemfile` and `_config.yml`, runs `jekyll build`, and serves the `_site/` output from the `main` branch. The custom domain `amplified.dev` is configured in the Netlify dashboard. There is no `netlify.toml` or explicit build config in the repo — everything is inferred.

Critically, the main page (`index.html`) is a fully standalone HTML file with inline CSS and JS. It does not use Jekyll templates, Liquid, or markdown rendering. Jekyll merely copies it to `_site/` unchanged. The only files that still rely on Jekyll's markdown processing are `manifesto.md` and `supporters.md`.

A future migration to Vercel is planned, at which point the Jekyll dependency could be dropped entirely in favor of a zero-build static deploy.

## What to Check

### 1. No Unnecessary Jekyll Dependencies

New pages should not introduce Jekyll-specific features (Liquid tags, front matter, `_includes`, `_data`) unless there is a clear reason. The site is moving toward plain static HTML.

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

### 2. Assets Must Be Repo-Relative

All image and asset paths in `index.html` use relative paths (`images/hero-7.webp`). Meta tags use absolute URLs (`https://amplified.dev/images/og.webp`). Don't introduce asset pipelines, CDN references, or build-time path rewriting that would break the standalone nature of the HTML.

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

### 3. Deployment Happens on Push to Main

There is no staging environment or preview deploy configured. Every push to `main` triggers a production build on Netlify. Changes should be reviewed before merging to `main`, not after.

### 4. Keep the Build Minimal

The Jekyll build exists only for `manifesto.md` and `supporters.md`. Don't add gems, plugins, or build steps to `Gemfile` or `_config.yml` unless they serve a clear purpose. The goal is to eventually drop the build step entirely.

## Key Files to Check

- `index.html` — Main page, must remain self-contained
- `_config.yml` — Jekyll config, should stay minimal
- `Gemfile` — Build dependencies, avoid adding new ones
- `images/` — Static assets served as-is

## Exclusions

- Changes to `supporters.md` or `manifesto.md` — these legitimately use Jekyll's markdown rendering
- CSS/JS changes within `index.html` — these don't affect the build pipeline
