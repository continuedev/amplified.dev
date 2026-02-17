---
name: Content Quality & Technical Accuracy
description: Check that technical descriptions are precise, claims are well-supported, and writing is clear.
---

# Content Quality & Technical Accuracy

## Context

This site establishes a framework for how organizations should approach AI-assisted software development. PR reviewers have focused heavily on technical precision — for example, requiring specific model parameter counts be accurate, ensuring latency claims are realistic, and suggesting links to research papers instead of vague assertions. Since the content influences how engineering teams adopt AI tools, accuracy and clarity directly impact credibility.

## What to Check

### 1. Technical Claims

Any technical claims should be accurate and, where possible, supported by citations:

- Model parameter counts (e.g., "1-15B parameter model") should be current and reasonable
- Performance claims (e.g., "within 500ms") should be realistic for the described use case
- Comparisons between approaches should be fair and specific

GOOD:
```markdown
A good rule of thumb is that this requires domain-specific instruction data and hundreds of GPU hours.
```

BAD:
```markdown
Fine-tuning is easy and quick to do for any organization.
```

### 2. Writing Clarity

Content should be accessible to engineering leaders and senior developers:

- Avoid jargon without explanation on first use
- Keep sentences focused — one idea per sentence where possible
- Use concrete examples rather than abstract descriptions
- Ensure `<details>` sections have clear, descriptive `<summary>` labels

GOOD:
```markdown
Because developers need a suggestion within 500ms, you generally need to use a smaller model in order to meet the latency requirements.
```

BAD:
```markdown
Latency constraints necessitate the utilization of computationally efficient model architectures for real-time inference scenarios.
```

### 3. Actionable Guidance

The "Actions to take now" sections under each principle in `index.md` should be:

- Specific enough that a team could act on them
- Ordered from simplest to most complex
- Not redundant with each other

GOOD:
```markdown
- Set up a proxy server to make LLMs available to developers
- Make multiple models available and compare their usage
```

BAD:
```markdown
- Think about AI
- Consider using AI more
```

## Key Files to Check

- `index.md` — All technical content and guidance
- Any new content pages added to the site

## Exclusions

- `supporters.md` — Contributor list, no technical content
- Minor formatting-only changes (whitespace, line breaks)
- Changes that only modify HTML attributes without changing visible content
