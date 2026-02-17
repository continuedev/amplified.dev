---
name: Keyboard Section Navigation
description: j/k navigation should feel like a purpose-built reader — moving between the essay's meaningful content blocks without touching browser defaults or the existing tab order.
---

# Keyboard Section Navigation

## Context

The site has 4 focusable elements (skip-link, CTA, 2 footer links). Keyboard users can Tab through those, but there's no way to navigate the essay's content sections — you're stuck with arrow keys and Space for raw scrolling. The `j`/`k` keys let you jump between the essay's meaningful content blocks: the hero, the five text sections, the two pull quotes, and the closing CTA.

The system is desktop-only, shown-once hint, scroll-tracked. It should feel like infrastructure the reader discovers, not UI that demands attention.

## What to Check

### 1. j/k Are the Only Nav Keys

Don't bind arrows, Space, Tab, or any other key. Those belong to the browser. `j` advances to the next stop, `k` goes back. That's the entire vocabulary.

BAD: Binding `ArrowDown` or `Space` as aliases for `j`.

### 2. The Stops Array Matches the Reading Flow

The navigable stops are collected in DOM order: `.hero`, `.essay .section`, `.essay .pull-quote`, and `.closing`. That gives 9 stops total. Images, separators, and image pairs are skipped — they're breathing room, not reading destinations.

If a new content block is added to the essay, it should be added to the stops if and only if it carries argumentative weight. A new `.section` or `.pull-quote` will be picked up automatically by the selector. A decorative element should not be.

### 3. The Keydown Guards Stay in Sync with the Easter Egg

The nav keydown handler must skip the same targets as the easter egg:
- `<input>`, `<textarea>`, or `contentEditable` elements
- Modifier keys (Meta, Ctrl, Alt)

If the easter egg's guards change, these must change too. They share the same keyboard space and must agree on when to yield.

### 4. The Hint Is Shown Once and Only Once

The "j / k to navigate" hint appears either when the essay first enters the viewport (scroll trigger) or on first `j`/`k` press — whichever comes first. It auto-dismisses after 3 seconds. It is never shown again. No repeated prompts, no persistent UI. It's a whisper, not a tooltip.

The hint element has `aria-hidden="true"` — it's a visual affordance, not content for screen readers.

### 5. The Indicator Uses box-shadow, Not Pseudo-elements

The `.nav-active` class uses `box-shadow: -3px 0 0 0 rgba(123, 111, 160, 0.3)` for a subtle left-edge lavender line. This avoids conflicts with `.pull-quote::before` (which draws the top decorative rule) and keeps the approach uniform across all stop types. The indicator is skipped on the hero.

BAD: Using `::before` or `::after` for the indicator — that would collide with pull-quote styling.

### 6. Scroll Tracking and Keyboard Stay in Sync

The IntersectionObserver (with `rootMargin: '-20% 0px -20% 0px'` and `threshold: 0.3`) and the keydown handler write to the same `currentIndex`. If the user scrolls with the mouse to a middle section and then presses `j`, navigation continues from where they are — not from where the last `j`/`k` left off. Don't add a second source of truth.

### 7. Desktop Only

The entire system — observer, keydown listener, hint — checks `window.innerWidth > 768` at init and does not initialize on mobile viewports. The CSS also hides `.nav-active` and `.nav-hint` at `max-width: 768px` as a safety net.

### 8. No Focus Management on Sections

Sections are `div` elements, not interactive. Don't add `tabindex`. The page's Tab order must remain exactly: skip-link, CTA, footer links. `j`/`k` scrolls the viewport — it does not move focus.

BAD: Adding `tabindex="-1"` to sections and calling `.focus()` on navigation.

## Key Files to Check

- `index.html` — The nav CSS (search for "Section nav") and JS (search for "Section navigation")

## Exclusions

- The specific visual parameters (shadow intensity, transition duration, hint timing) are tuning choices, not correctness issues
- Whether 9 stops is the right number — that depends on the essay's content, not on this system
- The 20% viewport offset for scroll positioning — that's a comfort preference
