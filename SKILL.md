---
name: linear-style-illustration
description: Dark "Linear/AI-OS" style technical diagrams — near-black background, cyan × purple × lilac duotone, JetBrains Mono uppercase labels, pill-shaped SVG nodes, glowing hub/kernel layer. Use when the user wants a "Linear 风格 diagram", a dark tech/architecture diagram, a product flow / state machine / layered-stack / hub-and-spoke diagram for a deck or landing page, or references screenshots that look like a dark AI product OS deck. Outputs a self-contained HTML file with inline SVG, ready to drop into a slide deck or export as PNG. Keywords: Linear style diagram, dark tech diagram, kernel diagram, AI OS architecture diagram, cyan purple diagram, product flow diagram dark theme, state machine diagram, hub and spoke diagram, layered architecture diagram, 深色科技图, 暗色架构图, Linear 风格.
---

# Linear-Style Illustration (dark Linear/AI-OS style technical diagrams)

## What this is

A reusable visual system for **dark, technical, "AI operating system" style diagrams** — the kind used across `future-of-linear-v3.html` in this workspace. Not a general chart library — a specific, opinionated aesthetic:

- Near-black stage (`#06070a`), soft blurred color "orbs" in the background, faint grid, vignette.
- Pill / rounded-rect nodes with thin colored strokes and low-opacity fills — never solid filled boxes.
- **JetBrains Mono**, uppercase, wide letter-spacing (`0.14em`–`0.32em`) for labels/tags/state-names.
- **Inter Tight** (or `Carlito`/system sans as fallback) bold for the actual node text.
- Exactly one accent per diagram "state": **cyan** `#6ce0d6` = primary/success/current/AI-output, **purple** `#7b7fff` = human/decision/secondary, **lilac** `#b58bff` = tertiary/organizational, **warn orange** `#f0b464` = caution/gate/pause. Neutral nodes stay white-ish at low opacity.
- Arrows are thin (`1.4–1.8px`), color-matched to what they're leaving, often dashed for "loop back" / feedback paths.

Read `references/style-tokens.md` for the exact copy-pasteable CSS/defs, and `references/patterns.md` for 7 ready-to-adapt diagram archetypes (hub-and-spoke, layered stack, fan-in funnel, state machine, flywheel/cycle, waterfall steps, horizontal pill-chain).

## Workflow

1. **Figure out what shape the idea already has.** Ask only if genuinely ambiguous — most requests map obviously to one archetype:
   - "X routes/coordinates to multiple Y" → **hub-and-spoke** (coordinator pattern)
   - "3 layers, one is the core/kernel" → **layered stack**
   - "lots of small things become one big decision" → **fan-in funnel**
   - "a process with a decision point / retry / approval" → **state machine**
   - "a repeating loop that improves over time" → **flywheel / cycle**
   - "a numbered sequence of steps" → **waterfall / numbered steps**
   - "before → after" or a simple linear pipeline → **horizontal pill-chain**
2. **Pick 1 primary accent color** for the diagram's "hero" node/path (usually cyan) and 1–2 secondary colors for contrast paths (purple for human/decision, lilac for a third category, warn orange only for caution/gate states). Don't use all 4 colors unless the diagram genuinely has that many distinct categories — 2 colors is usually enough.
3. **Generate a self-contained `.html` file** (viewBox'd inline SVG, 1600–1920px canvas) using the boilerplate in `references/style-tokens.md` + the closest pattern in `references/patterns.md`. Save it to the location the user's project conventions expect (check for an existing deck file to append a `<section class="slide">` into, otherwise create a standalone file).
4. **If embedding into an existing deck** (like `future-of-linear-v3.html`): match the existing `:root` CSS variables and `.grid-bg`/`.orb`/`.vignette`/`.section-num`/`.stamp` classes already defined in that file instead of re-declaring them — just add the new `<section class="slide">` with its inline SVG in the same style as neighboring slides.
5. **If standalone**: use the full boilerplate (fonts + `:root` vars + base classes) so the file renders correctly with no external dependencies besides the Google Fonts link.
6. Keep text in nodes short (1–3 words) — this style relies on generous negative space, not dense labels. Put explanation in a `.sub`/caption line above or below the diagram, not inside nodes.

## Quick reference — do / don't

**Do:**
- Rounded pill nodes (`rx` = half height, or `rx="12-18"` for rect cards), 1–2px stroke, low-opacity fill (`0.06`–`0.16` alpha).
- Uppercase mono micro-labels above/inside the "hero" node (e.g. `STATE · 02`, `PROPOSED`, `LAYER 2 · LINEAR — THE OS`).
- One glowing/highlighted node per diagram max (drop-shadow filter + solid-opacity stroke) to show where the "center of gravity" is.
- Dashed strokes for conditional/feedback/loop-back paths; solid for the primary happy path.
- Curved `Q`-paths for many-to-one convergence; straight lines/right-angle paths for sequential flow.

**Don't:**
- Don't use solid filled boxes or drop-shadows on every node — reserve glow for the one "kernel" element.
- Don't mix in bright saturated colors outside the cyan/purple/lilac/warn-orange palette.
- Don't set canvas background to anything but the near-black `--slide-bg` (`#06070a`) — this style depends on high contrast against near-black.
- Don't cram more than ~6-7 nodes in one diagram; split into two diagrams or a "wheel" pattern instead.
