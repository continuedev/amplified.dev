---
name: Easter Egg Integrity
description: The secret should delight without disrupting — invisible until found, accessible when triggered, and true to the essay's voice.
---

# Easter Egg Integrity

## Context

The site has a hidden interaction: typing "amplify" on the page triggers a brief visual effect where the text lifts upward, the lavender accents glow, and a message appears — "↑ the work moves up." The page literally demonstrates its own thesis.

This is the only interactive surprise on the site. It should feel like finding a note someone left for you, not like a popup you didn't ask for. It must never interfere with reading, never break accessibility, and never add weight to the page.

## What to Check

### 1. The Trigger Word Matches the Theme

The secret word is `amplify` — the word the entire essay is about. Don't change it to something clever or obscure. The delight is in the connection between what you type and what happens. Someone reading the essay might type it on instinct.

### 2. The Effect Respects Reduced Motion

The JavaScript checks `window.matchMedia('(prefers-reduced-motion: reduce)')` before triggering. The CSS transitions are also neutralized inside the `@media (prefers-reduced-motion: reduce)` block — `transform: none`, `text-shadow: none`, `box-shadow: none`. If you modify the effect, both the JS guard and the CSS overrides must stay in sync.

GOOD:
```css
@media (prefers-reduced-motion: reduce) {
  body.amplified .new-element {
    transform: none;
  }
}
```

BAD: Adding a new animated property to the `.amplified` state without a reduced-motion override.

### 3. The Effect Doesn't Break Input

The keydown listener skips events when:
- The target is an `<input>`, `<textarea>`, or `contentEditable` element
- A modifier key (Meta, Ctrl, Alt) is held
- The key is not a single character (arrows, Escape, etc.)

Don't remove these guards. They prevent the easter egg from swallowing keystrokes that belong to something else.

### 4. The Message Is Hidden from Screen Readers

The "↑ the work moves up" element has `aria-hidden="true"`. It's a visual flourish, not content. Screen reader users don't need to hear it announced mid-read. Keep it hidden.

### 5. The Effect Is Temporary and Non-Destructive

The `.amplified` class is added to `<body>` and removed after ~2.8 seconds. The message fades in and out. Nothing changes permanently. The page returns to exactly the state it was in before. Don't make the effect persist, don't store state, don't add a cookie or localStorage flag.

### 6. The Implementation Stays Minimal

The easter egg is ~30 lines of vanilla JS and ~30 lines of CSS. No libraries, no dependencies, no external assets. It fits the site's philosophy of doing less but meaning it. Don't over-engineer it with particle effects, sound, or complex animation sequences.

## Key Files to Check

- `index.html` — The easter egg CSS (search for "Easter egg") and JS (search for "Easter egg: type")

## Exclusions

- The specific visual parameters (glow intensity, lift distance, timing) are tuning choices, not correctness issues
- Whether to tell people about the easter egg — that's a social decision, not a code one
