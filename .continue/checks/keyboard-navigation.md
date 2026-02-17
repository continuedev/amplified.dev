---
name: Keyboard Section Navigation
description: j/k moves you through the essay. That's it. No UI, no indicators, no announcements. If you know, you know.
---

# Keyboard Section Navigation

## Context

The site has a hidden `j`/`k` navigation system. It lets you jump between the essay's meaningful content blocks — the hero, the five text sections, the two pull quotes, and the closing CTA. Nine stops, in reading order.

This is not a feature. It's not announced, not indicated, not onboarded. There is no visible trace of it on the page. It exists for people who already expect `j`/`k` to work because they've used vim, Gmail, or a hundred other tools that respect that convention. If you don't know it's there, you lose nothing. If you do, the essay becomes easier to read with a keyboard.

This is the same philosophy as the easter egg: invisible until found, zero footprint when not used.

## What to Check

### 1. Zero Visual Footprint

This is the most important rule. The navigation adds nothing visible to the page. No indicators, no highlights, no active states, no progress bars, no section counters, no hints, no tooltips, no onboarding messages, no "press j/k" prompts. Not even subtle ones. Not even ones that fade out. Not even ones that only show once.

If you're tempted to add visual feedback "just to help people discover it" — don't. Discovery is not the goal. The people who would use this already know to try it.

BAD: `.nav-active` class, box-shadow indicators, "j / k to navigate" hints, progress dots, highlighted sections, any CSS that only exists to support this feature's visibility.

### 2. j/k Are the Only Keys

Don't bind arrows, Space, Tab, or anything else. Those belong to the browser. `j` goes forward, `k` goes back. That's it.

### 3. The Stops Match the Reading Flow

Stops are collected in DOM order: `.hero`, `.essay .section`, `.essay .pull-quote`, `.closing`. Images, separators, and image pairs are skipped — they're breathing room, not arguments. If a new content block carries argumentative weight, the selector picks it up automatically. If it doesn't, it shouldn't be a stop.

### 4. The Keydown Guards Match the Easter Egg

Same guards, same reasons:
- Skip `<input>`, `<textarea>`, `contentEditable`
- Skip modifier keys (Meta, Ctrl, Alt)

If the easter egg's guards change, these change too.

### 5. Position Is Computed on Keypress, Not Tracked

There is no persistent `currentIndex` and no IntersectionObserver for scroll tracking. On each `j`/`k` press, the handler finds the stop closest to the scroll target line (20% from viewport top) and navigates from there. This means mouse scrolling and keyboard always agree — there's nothing to drift out of sync.

BAD: An IntersectionObserver that writes to a `currentIndex` variable — when multiple stops are visible (especially near the bottom), the observer races and the index lands on the wrong stop.

### 6. Desktop Only

`window.innerWidth > 768` gate at init. No observers, no listeners on mobile. There's no physical keyboard to use them with.

### 7. No Focus Management

Sections are `div`s, not interactive elements. No `tabindex`. Tab order stays exactly as it is: skip-link, CTA, footer links. `j`/`k` scrolls the viewport — it does not move focus.

## Key Files to Check

- `index.html` — search for "Section navigation" in the JS

## Exclusions

- Scroll offset and easing are comfort preferences, not correctness issues
- The number of stops depends on the essay's content
