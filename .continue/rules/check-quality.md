---
name: Check Quality
description: Checks are the site's immune system. They should be judgment-based, project-specific, and honest — never bureaucratic, never redundant with linters, never stale.
---

# Check Quality

## Context

The `.continue/rules/` directory is the institutional memory of this project. Each check encodes a decision that was made, usually after something went wrong or almost went wrong. They run on every PR as AI-powered code review rules — targeting issues that require judgment and context, not things a linter can catch.

There are currently 10 checks. That number should grow slowly. A bad check is worse than no check — it trains reviewers (human and AI) to ignore the checks entirely.

## What to Check

### 1. Every Check Earns Its Place

A check exists because something went wrong, or because a pattern is subtle enough that it would be easy to violate without realizing. If you can't point to a real scenario where the check would have caught a mistake, it's bureaucracy.

Don't add a check for something that's never been a problem. Don't add a check "just in case." Don't add a check that restates what a linter already enforces.

BAD: A check that says "use semicolons" (that's a linter rule). A check that says "don't delete the repo" (that's not a real risk).

### 2. Checks Are Judgment, Not Lint

Checks target things that require context and taste — editorial voice, visual cohesion, architectural intent, design philosophy. They answer questions like "does this change feel right?" not "does this code compile?"

If a rule can be expressed as a regex or an AST check, it belongs in a linter, not a check. If it requires reading the essay, understanding the site's ethos, or evaluating aesthetic coherence, it belongs in a check.

### 3. The Format Is Consistent

Every check file follows this structure:
- **Frontmatter**: `name` and `description` (one sentence, captures the spirit)
- **Context**: Why this check exists, what it protects
- **What to Check**: Numbered rules with concrete instructions, GOOD/BAD examples where useful
- **Key Files to Check**: Specific file paths to examine
- **Exclusions**: Cases where the check intentionally does not apply

Don't add severity levels. Don't add priority scores. Don't add automation hooks. The format is prose because the judgments are prose.

### 4. Checks Stay in Sync with the Codebase

When the codebase changes, the checks must update. If a feature is removed, the check that governed it should be updated or deleted. If a check references a file that no longer exists, or a CSS class that was removed, or a pattern that was replaced, the check is lying.

Stale checks are actively harmful — they give false confidence and confuse AI reviewers. After any significant change, verify that every check's "Key Files to Check" section points to real files and every rule describes the actual current behavior.

BAD: A check that references `.nav-active` CSS after the visual indicator was removed. A check that says "the manifesto should be excluded from Jekyll" after the manifesto was deleted.

### 5. Each Check Has One Coherent Focus

A check should protect one thing. "Accessibility as Care" protects accessibility. "Easter Egg Integrity" protects the easter egg. Don't create a check that covers "miscellaneous stuff I noticed." Don't merge unrelated concerns into one check to keep the count down.

If a check starts accumulating unrelated rules, split it. If two checks overlap significantly, merge them.

### 6. Descriptions Carry the Voice

The one-sentence `description` in frontmatter is the check's elevator pitch. It should sound like the person who built this site — direct, opinionated, no corporate hedging. It's what an AI reviewer sees first. Make it count.

GOOD: `"The site is HTML, CSS, and images. That's the point. Don't add what you don't need."`

BAD: `"This check ensures that unnecessary dependencies are not introduced into the project."`

### 7. GOOD/BAD Examples Are From This Project

When a check includes examples, they should reference actual patterns from this codebase — real CSS classes, real file paths, real mistakes that happened or almost happened. Don't use generic textbook examples.

## Key Files to Check

- `.continue/rules/` — all check files

## Exclusions

- The specific number of checks — that depends on how many things need protecting
- The order of rules within a check — that's an authoring choice
- Whether a check is "too strict" — strictness is the point; the exclusions section is where you carve out exceptions
