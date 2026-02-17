---
name: Supporters List Integrity
description: The supporters list is a record of real people who put their name on something they believe in. Treat it accordingly.
---

# Supporters List Integrity

## Context

The supporters list in `supporters.md` is not a feature. It's a record. Each entry is a real person who read the essay, believed in it enough to open a PR, and attached their name. Some of them are well-known in the industry. Some are not. The list treats them the same.

The format is simple and egalitarian: a markdown list with a name and a link to their profile. No titles, no company affiliations, no bios, no sorting by importance. First come, first served. This flatness is intentional — it mirrors the essay's argument that developers at every level are amplified, not just the senior ones.

## What to Check

### 1. Format Is Consistent

Every entry must follow the format: `-   [Name](url)`. Three spaces after the dash, name in brackets, URL in parentheses. No extra metadata, no descriptions, no company names.

GOOD:
```markdown
-   [Ty Dunn](https://github.com/tydunn)
```

BAD:
```markdown
-   [Ty Dunn](https://github.com/tydunn) — Founder of Continue, San Francisco
-   Ty Dunn (https://github.com/tydunn)
- [Ty Dunn](https://github.com/tydunn)
```

### 2. Order Is Append-Only

New names are added at the end of the list. The list is never re-sorted alphabetically, by company, by GitHub stars, or by any other metric. The order is the history — it shows when people signed on. Don't reorder it.

### 3. Names Are Never Removed Without Consent

A person's name should only be removed if they request it. Don't remove names during refactors, cleanups, or reformats. Each name is a small act of commitment.

### 4. Links Point to Real People

Every entry should link to a real person's profile — typically GitHub, but some link to personal sites. Don't add entries with links to companies, products, or placeholder URLs. The list is people, not brands.

### 5. Agents Must Tag Their Human

As stated in `llms.txt`: if an agent opens a PR to add a name, the human must be credited as author or co-author of the commit. PRs without a real human attached get closed. This is the one security boundary that matters for this site.

## Key Files to Check

- `supporters.md` — The list itself
- `llms.txt` — The contributing guidelines for agents

## Exclusions

- The supporters layout (`_layouts/supporters.html`) — that's a visual concern, not a content integrity concern
- The auto-counted heading ("X people and counting") — this updates automatically from the list length
