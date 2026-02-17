---
name: Deployment Architecture Awareness
description: Ensure changes are compatible with the static site pipeline and don't introduce unnecessary build dependencies.
---

# Deployment Architecture Awareness

## Context

This site is deployed via Netlify, which auto-detects Jekyll from the `Gemfile` and `_config.yml`, runs `jekyll build`, and serves the `_site/` output from the `main` branch. The custom domain `amplified.dev` is configured in the Netlify dashboard. There is no `netlify.toml` — everything is inferred.

The main page (`index.html`) is a fully standalone HTML file with inline CSS, inline JS, and no Jekyll dependencies. Jekyll merely copies it to `_site/` unchanged. The only file that uses Jekyll's markdown rendering is `supporters.md`.

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

Don't add gems, plugins, or build steps to `Gemfile` or `_config.yml` unless they serve `supporters.md`. The goal is to eventually drop the build entirely. When the Vercel migration happens, the site should work by pointing Vercel at the repo root with no build command.

### 5. Canonical URL and SEO Fundamentals

`index.html` must include `<link rel="canonical" href="https://amplified.dev">` to prevent search engines from indexing `www.amplified.dev` and `amplified.dev` as separate sites. Don't remove or change this.

### 6. Font Loading Is Resilient

Google Fonts are loaded via `<link rel="preload" as="style">` followed by a regular `<link rel="stylesheet">`. The preload ensures the font CSS downloads in parallel with parsing. The fonts themselves use `display=swap`, so the page renders immediately with system fallbacks and swaps when fonts arrive. Don't remove the preload or change `display=swap` to `display=block` — that would block rendering on a third-party CDN.

### 7. Discoverability Files Are Maintained

The site has three root-level discoverability files that must stay in sync with the site's content:

- **`llms.txt`** — Markdown file following the [llms.txt spec](https://llmstxt.org/) so LLMs and AI agents can understand the site. Must include an H1 with the site name, a blockquote summary of the essay's thesis, and links to the main content. If new pages are added, they should be listed here.
- **`robots.txt`** — Allows all crawlers and points to the sitemap. Don't add `Disallow` rules unless there's a specific reason to block a path.
- **`sitemap.xml`** — Lists all public URLs. If new pages are added, they must be added to the sitemap.

GOOD: Adding a new page and updating all three files to reference it.

BAD: Adding a new page but forgetting to add it to `sitemap.xml` and `llms.txt`, so search engines and LLMs don't know it exists.

## Key Files to Check

- `index.html` — Main page, must remain fully self-contained
- `404.html` — Must also be standalone HTML (no Jekyll layout dependency)
- `_layouts/supporters.html` — Jekyll layout for `supporters.md`, the only legitimate Jekyll template
- `llms.txt` — LLM discoverability, must stay in sync with site content
- `robots.txt` — Crawler permissions, points to sitemap
- `sitemap.xml` — All public URLs
- `_config.yml` — Jekyll config, should stay minimal
- `Gemfile` — Build dependencies, avoid adding new ones
- `images/` — Static assets served as-is (mix of `.webp` and `.png`)

## Exclusions

- Changes to `supporters.md` — legitimately uses Jekyll's markdown rendering via `_layouts/supporters.html`
- CSS/JS changes within `index.html` — these don't affect the build pipeline
