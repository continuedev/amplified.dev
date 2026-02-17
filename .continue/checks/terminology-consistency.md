---
name: Terminology & Language Consistency
description: Ensure consistent use of project-specific terminology across all content.
---

# Terminology & Language Consistency

## Context

This project uses specific terminology for AI software development concepts. PR reviewers have repeatedly flagged inconsistent language — for example, PR #9 required renaming "tab" to "autocomplete" throughout, and PR #50 corrected terminology around model descriptions. Maintaining consistent vocabulary is critical for a site that aims to establish shared language for the AI development community.

## What to Check

### 1. Core Terminology

Ensure these canonical terms are used consistently:

- **"autocomplete" model** (not "tab model", "tab-autocomplete model", or "code completion model" when referring to the component)
- **"chat" model** (not "conversation model" or "QA model")
- **"AI software development system"** (not "AI coding tool", "AI assistant", or "copilot" when referring to the full system — though "copilot" is acceptable when referring to the general industry category)
- **"development data"** (not "telemetry", "usage data", or "analytics" when referring to the data generated while coding with LLMs)
- **"amplified developers"** (not "augmented developers" or "AI-assisted developers" when referring to the core concept)

GOOD:
```markdown
The "autocomplete" model component is used to power code completion suggestions.
```

BAD:
```markdown
The tab model component is used to power code completion suggestions.
```

### 2. Component Names

The site defines specific system components in `index.md`. When referencing these, use the exact names:

- Autocomplete model
- Chat model
- Local context engine
- Remote context engine
- Filtering
- Async engines
- Training engine

GOOD:
```markdown
The local context engine frequently leverages embeddings and full-text search.
```

BAD:
```markdown
The local context system frequently leverages embeddings and full-text search.
```

### 3. Referring to Models and Providers

When listing example models, use their official names and avoid outdated references. Do not claim specific model capabilities that may have changed since publication.

## Key Files to Check

- `index.md` — Primary content with all terminology definitions
- Any new `.md` files added to the site

## Exclusions

- `supporters.md` — Contains only contributor names, not technical content
- Direct quotes from external sources where original terminology should be preserved
- References to third-party product names (e.g., "GitHub Copilot" is the product name and should not be changed)
