---
name: Repo Hygiene
description: The repo should only contain what the site needs. No staging directories, no dead layouts, no OS junk, no orphaned files that "might be useful later."
---

# Repo Hygiene

## Context

This repo serves a single-page essay (`index.html`), a supporters list (`supporters.md` rendered by Jekyll), and a few supporting files. Everything else is either configuration, images, or discoverability files.

The site used to be a GitHub Pages Jekyll project with a long-form manifesto. It's now a static site on Netlify with Jekyll only for `supporters.md`. The manifesto is gone — the essay replaced it. Remnants of the old architecture should not accumulate. When in doubt about whether a file belongs, the answer is almost always no.

## What to Check

### 1. No Staging or Scratch Directories

The repo root should not contain directories used for drafting, experimenting, or staging content. If you need to try something, use a branch. Don't commit a `new-content/`, `drafts/`, `tmp/`, or `old/` directory.

BAD: A `new-content/` directory with duplicate images and an older version of index.html sitting in main.

### 2. No Dead Layouts

The `_layouts/` directory should only contain layouts that are actively referenced by front matter in a file Jekyll processes. If a layout exists but nothing uses it, delete it. The old `default.html` (GitHub Pages boilerplate with CDN scripts and Liquid conditionals) is gone and should stay gone.

### 3. No OS or Editor Junk

`.DS_Store`, `Thumbs.db`, `.idea/`, `.vscode/` (unless it contains project-specific settings the team agreed on), `*.swp`, etc. should be in `.gitignore` and never tracked. If one slips in, remove it from tracking.

### 4. Jekyll Only Processes What It Needs

The `_config.yml` `exclude:` list should keep Jekyll from touching files that aren't meant to be rendered as site pages. `Gemfile`, `Gemfile.lock`, `README.md`, and `LICENSE` are repo files, not site content. They should be excluded.

### 5. No Ghosts of the Old Manifesto

The repo used to contain a `manifesto.md` — a long-form technical document that predated the essay. The essay replaced it. The manifesto is deleted. Don't bring it back, don't add a new one, and don't add references to it in `llms.txt` or anywhere else. If you find a stale link to `amplified.dev/manifesto`, remove it.

### 6. README Is Accurate for Humans and AI

The README is the first thing a human sees on GitHub and the first thing an AI agent reads when exploring the repo. It must be honest and current. If the architecture changes, the README changes. If a dev setup step changes, the README changes.

It should cover:
- What the site is (one paragraph, no marketing)
- Architecture (what files do what, how it's hosted)
- Dev setup (accurate commands that actually work)
- How to contribute (link to supporters.md edit)
- That `.continue/rules/` exists and matters

It should NOT contain:
- Badges, shields, or status indicators
- Marketing copy or feature lists
- Instructions for a build system that doesn't exist
- Links to pages that have been removed

BAD: A README that says "Requires Ruby" and gives Jekyll commands when the main page is a static HTML file that needs no build step. A README that references a manifesto that was deleted.

### 7. llms.txt and README Tell the Same Story

The `llms.txt` and `README.md` both describe the project but for different audiences — `llms.txt` for AI agents discovering the site via URL, `README.md` for humans and agents on GitHub. They should agree on the facts: what the site is, what pages exist, how to contribute. If one is updated, check the other.

### 8. Every File in the Repo Has a Job

If you can't say what a file does in one sentence, it probably shouldn't be here. The inventory is small and should stay small:

- `index.html` — the essay
- `404.html` — error page
- `supporters.md` — the open letter
- `_layouts/supporters.html` — layout for supporters page
- `_config.yml` — Jekyll config
- `images/` — curated artwork
- `assets/favicon.ico` — favicon
- `robots.txt`, `sitemap.xml`, `llms.txt` — discoverability
- `.gitignore`, `Gemfile`, `Gemfile.lock`, `.ruby-version`, `LICENSE`, `README.md`, `CONTRIBUTING.md` — repo infrastructure
- `.continue/` — agent checks and guidelines

If a file doesn't fit one of these categories, justify it or delete it.

## Key Files to Check

- Root directory listing — no unexpected directories or files
- `README.md` — accurate architecture, dev setup, and contribution instructions
- `llms.txt` — in sync with README on facts
- `_config.yml` — `exclude:` list is current
- `.gitignore` — covers OS junk
- `_layouts/` — only `supporters.html`

## Exclusions

- The Gemfile's specific gem versions — that's dependency management
