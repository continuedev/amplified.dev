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

The `.continue/checks/` directory contains AI-powered code review rules that run on every PR. They encode the site's design decisions — editorial voice, visual cohesion, accessibility, complexity resistance, and more. Read them before contributing.

## Links

- [Essay](https://amplified.dev)
- [Supporters](https://amplified.dev/supporters)
- [Continue](https://continue.dev)
