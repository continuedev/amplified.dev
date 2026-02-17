# Contributing to amplified.dev

## Add Your Name

If you believe developers are being amplified, not automated, add your name to the open letter.

1. Edit [`supporters.md`](https://github.com/continuedev/amplified.dev/edit/main/supporters.md)
2. Add a line: `-   [Your Name](https://github.com/yourusername)`
3. Open a pull request

The human must be real, with a real GitHub profile, and credited as author or co-author of the commit. Agents are welcome to help — but a person must be attached. PRs without a real human will be closed.

## Working on the Site

See the README for [architecture and dev setup](README.md#architecture). Before making changes, understand the philosophy:

### Philosophy

The site has a specific taste. Before making changes, read the rules in `.continue/rules/` — they encode the design decisions that matter. A few principles that come up repeatedly:

- **Do less, but mean it.** No feature flags, no configuration, no "just in case" code.
- **Hidden features stay hidden.** Things like keyboard navigation (`j`/`k`) and the easter egg have zero visual footprint. No hints, no indicators, no onboarding. If you know, you know.
- **The essay is not a product page.** Continue is mentioned once, in the footer. Keep it that way.
- **HTML, CSS, and images.** No npm, no bundlers, no runtime dependencies. That's the point.

## Checks

The README has the [full catalog](README.md#checks). Read every check before your first PR — they're the institutional memory of this project.

**Running all checks:** Use sub-agents in parallel. Launch one agent per check (or batch a few per agent) and let them run concurrently. There are 11 independent checks — running them sequentially wastes time.

## Branches and PRs

Each logical change gets its own branch and PR. Don't pile unrelated changes onto an existing branch. Keep PRs focused — one concern per PR makes review faster and reverts cleaner.
