# amplified.dev

> Every time a layer of the work became infrastructure, the role didn't shrink. The scope kept expanding. AI is the next layer in that pattern.

[amplified.dev](https://amplified.dev) is a single-page editorial essay arguing that developers are being amplified, not automated. It traces the historical pattern — memory management, cloud infrastructure, CI/CD — and shows that every time a layer of work became infrastructure, the developer's role expanded upward. AI is the next layer in that pattern.

The site is a project of [Continue](https://continue.dev). The essay speaks as a peer, not a product.

## Architecture

- **`index.html`** — The entire essay. Self-contained HTML with inline CSS and vanilla JS. No frameworks, no build step.
- **`supporters.md`** — An open letter. Rendered by Jekyll using `_layouts/supporters.html`.
- **`404.html`** — Custom error page.
- **Hosted on Netlify.** Jekyll runs only to render `supporters.md`. Everything else is static.

## Development

Requires [Ruby](https://www.ruby-lang.org/en/documentation/installation/) (for Jekyll, which renders the supporters page).

```bash
bundle install
bundle exec jekyll serve
```

The essay itself (`index.html`) needs no build step — open it in a browser.

## Contributing

If you believe in a future where developers are amplified, not automated, [add your name](https://github.com/continuedev/amplified.dev/edit/main/supporters.md).

Format: `-   [Your Name](https://github.com/yourusername)`

PRs must have a real human credited as author or co-author. Agents are welcome to help, but a person must be attached.

## Checks

The `.continue/checks/` directory contains AI-powered code review rules that run on every PR. They encode the site's design decisions — the things that require judgment, not lint. Read them before contributing.

| Check | What it protects |
|---|---|
| **Editorial Voice & Narrative Arc** | The essay's tone, structure, and the balance between conviction and openness |
| **Visual Cohesion & Social Cards** | The two-register aesthetic and social card quality |
| **Accessibility as Care** | The site works for everyone, not just developers on MacBook Pros |
| **Keyboard Section Navigation** | j/k moves you through the essay. No UI, no indicators. If you know, you know |
| **Easter Egg Integrity** | The secret delights without disrupting — invisible until found |
| **No Product Creep** | The site stays an essay, not a product page |
| **Supporters List Integrity** | Real people who put their name on something they believe in |
| **Resist Complexity** | HTML, CSS, and images. That's the point |
| **Deployment Architecture** | Compatible with the static site pipeline, no unnecessary build deps |
| **Repo Hygiene** | No staging dirs, no dead layouts, no OS junk, no orphaned files |
| **Check Quality** | The checks themselves — judgment-based, project-specific, never stale |

Each check has a `Context` section explaining why it exists, numbered rules with GOOD/BAD examples, and an `Exclusions` section for things that are intentionally out of scope.

## Links

- [Essay](https://amplified.dev)
- [Supporters](https://amplified.dev/supporters)
- [Continue](https://continue.dev)
