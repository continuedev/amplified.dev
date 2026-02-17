---
name: Markdown Structure & Link Quality
description: Verify consistent markdown formatting, valid links, and proper page structure.
---

# Markdown Structure & Link Quality

## Context

This Jekyll site mixes markdown with inline HTML (`<details>`, `<summary>`, `<p>`, `<a>` tags) in `index.md`. PR reviewers have flagged link quality issues — preferring authoritative sources like research papers over informal references. Since the site has no automated linting or link checking, these issues must be caught in review. The `supporters.md` file has a strict format that community contributors must follow.

## What to Check

### 1. Link Quality

All links should point to authoritative, stable sources:

- Prefer research papers (arxiv.org), official documentation, and company engineering blogs
- Avoid linking to social media posts (tweets/X posts) when a more authoritative source exists
- Ensure links are not broken or pointing to defunct pages
- Links should use HTTPS where available

GOOD:
```markdown
[Code Llama](https://arxiv.org/pdf/2308.12950.pdf)
```

BAD:
```markdown
[Code Llama](https://twitter.com/someone/status/123456)
```

### 2. Supporters List Format

Entries in `supporters.md` must follow this exact format:

```markdown
-   [Full Name](https://github.com/username)
```

Check for:
- Three spaces after the `-` (matching existing convention)
- Name in square brackets, URL in parentheses
- GitHub profile URL preferred (though personal sites are acceptable)
- Entry added at the end of the list (not inserted in the middle)
- No duplicate entries

GOOD:
```markdown
-   [Jane Smith](https://github.com/janesmith)
```

BAD:
```markdown
- [Jane Smith](https://github.com/janesmith)
-   [Jane Smith](github.com/janesmith)
-   Jane Smith
```

### 3. HTML/Markdown Consistency

The `index.md` file uses a specific pattern for expandable sections:

```html
<details>
<summary>Section Title</summary>
<br>
<p>Content here...</p>
</details>
```

New expandable sections should follow this same pattern:
- `<br>` immediately after `<summary>` closing tag
- Content wrapped in `<p>` tags (not raw markdown inside HTML blocks)
- Sub-sections use `<h3>` tags (not markdown `###` inside HTML)
- Properly closed `</details>` tag

### 4. Internal Anchor Links

The table of contents in `index.md` uses anchor links (e.g., `#1-establish-an-architecture-of-participation`). If headings are modified, ensure corresponding anchor links are updated to match.

## Key Files to Check

- `index.md` — Primary content with mixed HTML/markdown
- `supporters.md` — Community contributor list with strict format
- Any new `.md` files

## Exclusions

- `_site/` directory (build output, not source)
- Changes to `_config.yml` or `Gemfile` (configuration, not content)
- Image files in `assets/`
