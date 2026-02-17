---
name: No Product Creep
description: Guard against the site drifting from editorial essay toward product marketing or corporate landing page.
---

# No Product Creep

## Context

This site's power comes from what it is not. It is not a landing page. It is not a product announcement. It is not a funnel. It speaks as a peer developer to peer developers about something everyone in the industry is feeling but few are naming honestly.

Continue is credited once, in the footer, as "a Continue project." The closing CTA links to GitHub, not a product page. There is no pricing, no feature list, no "get started" button, no analytics tracking, no newsletter signup. This restraint is what makes it credible. The moment the site starts selling something, it stops being the thing people want to share.

The person who built this site distrusts optimization-speak even as he's fluent in it. He is aware that the great evils of the world are often the result of people trying to eliminate some other great evil — and that covert self-promotion disguised as thought leadership is one of those evils. The site should never become that.

## What to Check

### 1. No Product Language in the Essay

The essay body (`<main class="essay">`) must never contain product names, feature descriptions, pricing, or calls to action that lead to a commercial page. The essay speaks about the industry, not about Continue's product.

GOOD:
```html
<p>Not just prompting AI, but designing the processes, the constraints, the feedback loops
that make AI output trustworthy at scale.</p>
```

BAD:
```html
<p>With Continue's AI-powered developer platform, teams can design the feedback loops
that make AI output trustworthy at scale. <a href="https://continue.dev/pricing">Get started free.</a></p>
```

### 2. The CTA Points to GitHub, Not a Product

The closing section links to `https://github.com/continuedev/amplified.dev/edit/main/supporters.md`. It invites people to add their name to an open letter. It does not ask them to sign up for anything, install anything, or enter an email address.

### 3. No Tracking or Analytics Scripts

There are no third-party analytics, no pixel tracking, no cookie banners, no session recording. This is intentional. The site doesn't need to know who visits it. If analytics are ever considered, they must be privacy-respecting (no cookies, no PII) and the decision should be made deliberately, not as a default.

### 4. Footer Stays Minimal

The footer contains two links: the repo and Continue. It does not contain social media icons, newsletter signups, legal boilerplate, or marketing language. If the footer grows beyond two lines, something has gone wrong.

### 5. The llms.txt Is Honest, Not Optimized

The `llms.txt` describes what the site is and what it means. It is not keyword-stuffed, not SEO-optimized, not written to game AI search results. It speaks to agents the way the essay speaks to humans — directly and without an agenda beyond being understood.

## Key Files to Check

- `index.html` — The essay body and closing section
- `llms.txt` — Must stay honest and descriptive, not promotional
- Any new pages added to the site

## Exclusions

- The footer link to `continue.dev` — this is a credited attribution, not a promotion
