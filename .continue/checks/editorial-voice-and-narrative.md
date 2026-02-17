---
name: Editorial Voice & Narrative Arc
description: Ensure the essay maintains its specific tone, narrative structure, and the balance between conviction and openness.
---

# Editorial Voice & Narrative Arc

## Context

The essay in `index.html` is not a blog post or a manifesto — it's a carefully paced editorial with a specific narrative arc, documented in HTML comments above each section:

1. **The Landscape** — Present tense. Chaos. The questions everyone's asking. ("Something shifted.")
2. **The Pattern** — History. The consistent arc. Every shift expanded the role, it never shrank it.
3. **The Hinge** — Pull quote. "AI doesn't break that trend. It's the next layer in it."
4. **Code is Abundant** — The fork in the road. Curators of machine output, or builders of the systems that channel it.
5. **The Pivot** — Tension. "Curly braces until the curly braces don't need them" vs. "the most interesting work of their careers."
6. **Amplified** — Resolution. Volume and signal. "The tools are here, the work is real, and it's yours."

The voice is second-person ("you"), present tense, and walks the line between conviction and empathy — it names the anxiety without dismissing it, then resolves it through historical pattern rather than hype. Pull quotes are the emotional beats. Sections are separated by visual breathers (images, separators) that give the reader time to absorb.

## What to Check

### 1. Narrative Arc Is Preserved

The essay follows a deliberate emotional shape: disorientation → recognition → fork → resolution. New sections or edits should not break this arc. If adding content, it should slot into the existing structure with a clear reason for where it lives.

GOOD: Adding a sentence to "The Pattern" section that provides another historical example of abstraction moving up (e.g., ORMs replacing hand-written SQL).

BAD: Inserting a section about pricing models or product features between "The Pattern" and the pull quote — this breaks the emotional momentum toward the hinge.

### 2. Voice Is Second-Person, Not Corporate

The essay speaks directly to the reader as a peer developer. It uses "you" and "your," not "we at [Company]" or "our platform." The only brand mention is in the footer ("a Continue project"). The closing CTA links to GitHub, not a product page.

GOOD:
```html
<p>What does seniority look like when a new grad with good prompts can generate the same code you can?</p>
```

BAD:
```html
<p>Our AI-powered platform helps senior developers maintain their edge in an increasingly automated landscape.</p>
```

### 3. Prose Is Concrete and Unflinching

The writing names specific realities rather than abstracting them away. It doesn't hedge with qualifiers ("might," "could potentially," "in some cases") or pad with jargon. Sentences are direct. Claims are grounded in observable patterns, not predictions.

GOOD:
```html
<p>Junior engineers are standing up services in hours that used to take senior devs a week.</p>
```

BAD:
```html
<p>AI tools may potentially enable less experienced developers to achieve productivity gains in certain scenarios.</p>
```

### 4. Pull Quotes Are Emotional Beats, Not Summaries

The two pull quotes ("AI doesn't break that trend. It's the next layer in it." and "The work doesn't disappear. It moves up.") are turning points in the essay's argument. They use `<em>` for the word that carries the emotional weight. New pull quotes should earn their emphasis — they mark where the reader's understanding shifts, not where we repeat a point.

GOOD:
```html
<div class="pull-quote">
  The work doesn't disappear. It <em>moves up.</em>
</div>
```

BAD:
```html
<div class="pull-quote">
  AI is <em>really</em> <em>important</em> for the <em>future</em> of development.
</div>
```

### 5. Hero Heading Line Break Is Sacred

The hero heading reads "Developers amplified," on line one and "not automated" on line two. This line break is intentional at every screen size — it's the thesis of the entire site, and the two-line structure mirrors the two ideas (amplified vs. automated). The `<br>` must never be hidden or removed on any breakpoint.

GOOD:
```html
<h1>Developers <em>amplified</em>, <br>not automated</h1>
<!-- br is always visible, "not automated" is always on its own line -->
```

BAD:
```css
/* Hiding the br collapses the heading into one line on mobile */
.hero h1 br { display: none; }
```

### 6. Images and Text Breathe Together

Each image break sits between sections as a visual pause — giving the reader time to absorb what they just read before the next idea. The HTML comments document *why* each image sits where it does (e.g., "No clear structure yet. The feeling of being in it before the pattern is visible."). Content changes that remove image breaks or stack multiple text sections without visual breathing room break the essay's pacing.

## Key Files to Check

- `index.html` — All `<p>` content within `.section-text` divs, `.pull-quote` elements, and `.closing` section
- HTML comments above each section and image block — these document editorial intent

## Exclusions

- `supporters.md` — Contributor list, no editorial content
- `manifesto.md` — Separate document with its own voice (more technical, less personal)
- Changes to CSS animations, layout classes, or responsive breakpoints — these affect presentation, not editorial voice
