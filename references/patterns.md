# Diagram patterns — 7 archetypes

Each is a real, working template distilled from `future-of-linear-v3.html`. Swap the text/counts, keep the structure and color logic. All use the marker defs and node recipes from `style-tokens.md`.

---

## 1. Horizontal pill-chain (simple pipeline / before-after)

Use for: "today it's A→B→C→D, tomorrow it's different". Two stacked rows, optionally divided by a small pill label ("X ARRIVES").

```html
<svg viewBox="0 0 560 300" xmlns="http://www.w3.org/2000/svg">
  <text x="0" y="20" fill="rgba(232,238,255,0.55)" font-family="JetBrains Mono, monospace" font-size="12" letter-spacing="3">TODAY · BASELINE</text>

  <g><rect x="0" y="55" width="110" height="42" rx="21" fill="rgba(255,255,255,0.04)" stroke="rgba(255,255,255,0.18)"/><text x="55" y="81" fill="#e8eeff" font-family="Inter Tight, sans-serif" font-size="16" text-anchor="middle" font-weight="600">Step A</text></g>
  <line x1="112" y1="76" x2="148" y2="76" stroke="rgba(232,238,255,0.45)" stroke-width="1.5" marker-end="url(#arr-dim)"/>
  <g><rect x="150" y="55" width="110" height="42" rx="21" fill="rgba(255,255,255,0.04)" stroke="rgba(255,255,255,0.18)"/><text x="205" y="81" fill="#e8eeff" font-family="Inter Tight, sans-serif" font-size="16" text-anchor="middle" font-weight="600">Step B</text></g>
  <!-- repeat pill + arrow for each step -->

  <!-- divider pill -->
  <line x1="0" y1="145" x2="560" y2="145" stroke="rgba(108,224,214,0.25)" stroke-width="1" stroke-dasharray="4 6"/>
  <rect x="170" y="130" width="220" height="30" rx="15" fill="rgba(108,224,214,0.1)" stroke="rgba(108,224,214,0.4)"/>
  <text x="280" y="150" fill="#6ce0d6" font-family="JetBrains Mono, monospace" font-size="11" text-anchor="middle" letter-spacing="2.5">THE CHANGE ARRIVES</text>

  <text x="0" y="192" fill="#6ce0d6" font-family="JetBrains Mono, monospace" font-size="12" letter-spacing="3">TOMORROW · NEW STATE</text>
  <!-- second row of pills, same pattern with cyan/purple accents on the new nodes -->
</svg>
```

---

## 2. Hub-and-spoke / coordinator

Use for: "one node routes/coordinates work out to several others, then results converge back". One node in the middle glows (cyan), spokes fan out in accent color (purple), dashed convergence lines lead back to an output node.

Key elements: input node → glowing hub (rounded pill, `filter="drop-shadow(...)"`) → straight fan-out lines to N stacked boxes on the right → dashed convergence lines from those boxes down to a single output node below the hub → solid arrow hub→output.

```html
<g><rect x="0" y="255" width="110" height="42" rx="21" fill="rgba(255,255,255,0.04)" stroke="rgba(255,255,255,0.22)"/><text x="55" y="281" fill="#e8eeff" font-family="Inter Tight, sans-serif" font-size="16" text-anchor="middle" font-weight="600">Input</text></g>
<line x1="112" y1="276" x2="150" y2="276" stroke="rgba(108,224,214,0.55)" stroke-width="1.5" marker-end="url(#arr-cyan)"/>

<g>
  <rect x="152" y="246" width="170" height="60" rx="30" fill="rgba(108,224,214,0.16)" stroke="#6ce0d6" stroke-width="2" filter="drop-shadow(0 0 24px rgba(108,224,214,0.35))"/>
  <text x="237" y="273" fill="#e8eeff" font-family="Inter Tight, sans-serif" font-size="18" text-anchor="middle" font-weight="700">Hub Name</text>
  <text x="237" y="292" fill="#6ce0d6" font-family="JetBrains Mono, monospace" font-size="10" text-anchor="middle" letter-spacing="2.5">COORDINATOR</text>
</g>

<!-- fan-out (repeat per spoke, staggered y-targets) -->
<line x1="322" y1="276" x2="418" y2="220" stroke="#b58bff" stroke-width="1.5" stroke-opacity="0.7" marker-end="url(#arr-purple)"/>
<g><rect x="420" y="203" width="140" height="34" rx="17" fill="rgba(181,139,255,0.10)" stroke="rgba(181,139,255,0.45)"/><text x="490" y="225" fill="#e8eeff" font-family="Inter Tight, sans-serif" font-size="14" text-anchor="middle" font-weight="600">Spoke 1</text></g>
<!-- ...repeat 2-4x, spaced 38px apart vertically... -->

<!-- convergence back to output (dashed, dim) -->
<line x1="420" y1="220" x2="322" y2="415" stroke="rgba(108,224,214,0.4)" stroke-width="1" stroke-dasharray="3 4"/>
<!-- repeat per spoke -->

<line x1="237" y1="308" x2="237" y2="415" stroke="rgba(108,224,214,0.55)" stroke-width="1.5" marker-end="url(#arr-cyan)"/>
<g><rect x="167" y="420" width="140" height="46" rx="23" fill="rgba(255,255,255,0.05)" stroke="rgba(232,238,255,0.35)"/><text x="237" y="449" fill="#e8eeff" font-family="Inter Tight, sans-serif" font-size="17" text-anchor="middle" font-weight="600">Output</text></g>
```

---

## 3. Layered stack (architecture / "kernel" diagram)

Use for: "N layers stacked vertically, one of them (usually the middle) is the highlighted core system". Each layer is a large rounded rect containing several small pills. The core layer gets the cyan glow treatment (`url(#glowGradient)` fill + thick cyan stroke + drop-shadow); the layers above/below are plain low-opacity outline rects. Thin dashed vertical connectors link the layers.

```html
<defs>
  <linearGradient id="coreGlow" x1="0" y1="0" x2="0" y2="1">
    <stop offset="0%" stop-color="rgba(108,224,214,0.18)"/>
    <stop offset="100%" stop-color="rgba(123,127,255,0.14)"/>
  </linearGradient>
</defs>

<!-- top layer -->
<rect x="0" y="10" width="600" height="150" rx="16" fill="rgba(255,255,255,0.03)" stroke="rgba(255,255,255,0.14)"/>
<text x="24" y="40" fill="rgba(232,238,255,0.8)" font-family="JetBrains Mono, monospace" font-size="12" font-weight="600" letter-spacing="3">LAYER 3 · LABEL</text>
<!-- 3-5 small pills inside, same recipe as pattern 1 -->

<line x1="300" y1="160" x2="300" y2="200" stroke="rgba(108,224,214,0.6)" stroke-width="1.5" stroke-dasharray="3 5"/>

<!-- CORE / kernel layer — highlighted -->
<rect x="0" y="200" width="600" height="240" rx="18" fill="url(#coreGlow)" stroke="#6ce0d6" stroke-width="2" filter="drop-shadow(0 0 36px rgba(108,224,214,0.28))"/>
<text x="24" y="230" fill="#6ce0d6" font-family="JetBrains Mono, monospace" font-size="12" letter-spacing="3">LAYER 2 · THE CORE</text>
<text x="24" y="282" fill="#e8eeff" font-family="Inter Tight, sans-serif" font-size="34" font-weight="700">Core System Name</text>
<text x="24" y="314" fill="rgba(232,238,255,0.7)" font-family="Inter Tight, sans-serif" font-size="17">One-line description of what it does.</text>
<!-- 3-4 capability pills inside (rx=12 rect cards, not full pills), fill rgba(0,0,0,0.25), stroke rgba(108,224,214,0.4) -->

<line x1="300" y1="440" x2="300" y2="480" stroke="rgba(181,139,255,0.6)" stroke-width="1.5" stroke-dasharray="3 5"/>

<!-- bottom layer -->
<rect x="0" y="480" width="600" height="130" rx="16" fill="rgba(255,255,255,0.03)" stroke="rgba(255,255,255,0.14)"/>
<text x="24" y="510" fill="rgba(232,238,255,0.8)" font-family="JetBrains Mono, monospace" font-size="12" font-weight="600" letter-spacing="3">LAYER 1 · LABEL</text>
<!-- pills -->

<text x="300" y="600" fill="rgba(232,238,255,0.55)" font-family="JetBrains Mono, monospace" font-size="11" text-anchor="middle" letter-spacing="3">CLOSING CAPTION LINE</text>
```

---

## 4. Fan-in funnel (many sources → one decision → one output)

Use for: "scattered signals/inputs converge into a single reviewable thing, then a human/gate decides, then it becomes a bigger output". Left column = small circle+label nodes stacked vertically. Curved `Q` paths converge into a center highlighted box. A labeled arrow (with a "human decision" micro-caption above/below) leads to a final wider box on the right.

```html
<!-- left: source nodes -->
<g font-family="JetBrains Mono, monospace" font-size="22" fill="#eaeaf2">
  <circle cx="60" cy="40" r="12" fill="rgba(255,255,255,0.05)" stroke="rgba(255,255,255,0.45)" stroke-width="1.2"/>
  <text x="94" y="48">Source 1</text>
  <!-- repeat for each source, 90px apart vertically -->
</g>

<!-- curved convergence -->
<g stroke="rgba(108,224,214,0.4)" stroke-width="1.4" fill="none">
  <path d="M 72 40  Q 400 40  740 265"/>
  <!-- one path per source, all curving to the same target point -->
</g>

<!-- center: the synthesized thing -->
<rect x="740" y="205" width="260" height="120" rx="16" fill="rgba(108,224,214,0.09)" stroke="rgba(108,224,214,0.75)" stroke-width="2"/>
<text x="870" y="235" text-anchor="middle" fill="#6ce0d6" font-family="JetBrains Mono, monospace" font-size="18" letter-spacing="3">PROPOSED</text>
<text x="870" y="285" text-anchor="middle" fill="#eaeaf2" font-family="Inter Tight, sans-serif" font-size="36" font-weight="600">Opportunity</text>

<!-- decision arrow with dual caption (primary path + alt path) -->
<g stroke="rgba(123,127,255,0.75)" stroke-width="2" fill="none">
  <line x1="1000" y1="265" x2="1220" y2="265"/>
  <polygon points="1220,265 1205,257 1205,273" fill="rgba(123,127,255,0.85)"/>
</g>
<text x="1110" y="238" text-anchor="middle" fill="#7a7d90" font-family="JetBrains Mono, monospace" font-size="18" letter-spacing="3">HUMAN · APPROVE</text>
<text x="1110" y="298" text-anchor="middle" fill="#7b7fff" font-family="JetBrains Mono, monospace" font-size="18" letter-spacing="3">↳ OR REDIRECT</text>

<!-- final output box, wider, purple accent -->
<rect x="1230" y="205" width="440" height="120" rx="16" fill="rgba(123,127,255,0.11)" stroke="rgba(123,127,255,0.75)" stroke-width="2"/>
<text x="1450" y="238" text-anchor="middle" fill="#7b7fff" font-family="JetBrains Mono, monospace" font-size="18" letter-spacing="3">RESULT</text>
<text x="1450" y="278" text-anchor="middle" fill="#eaeaf2" font-family="Inter Tight, sans-serif" font-size="26" font-weight="600">What gets created</text>
<text x="1450" y="306" text-anchor="middle" fill="#7a7d90" font-family="Inter Tight, sans-serif" font-size="16">Supporting detail line</text>
```

---

## 5. State machine (with decision gate + feedback loops)

Use for: "a process has states, a confidence/approval gate, and human-in-the-loop branches that resume or advance the flow". Happy path is a straight horizontal row of state boxes connected by solid arrows. A **diamond** (polygon) is the decision gate, colored warn-orange. The low-confidence branch drops down (dashed orange) to a "paused" box, which splits into two human-action boxes below; each loops back up (dashed, color-matched: purple = redirect/retry, cyan = confirm/advance) to rejoin the main flow.

```html
<defs>
  <marker id="arr-p" viewBox="0 0 10 10" refX="10" refY="5" markerWidth="7" markerHeight="7" orient="auto-start-reverse"><path d="M 0 0 L 10 5 L 0 10 z" fill="#7b7fff"/></marker>
  <marker id="arr-c" viewBox="0 0 10 10" refX="10" refY="5" markerWidth="7" markerHeight="7" orient="auto-start-reverse"><path d="M 0 0 L 10 5 L 0 10 z" fill="#6ce0d6"/></marker>
  <marker id="arr-w" viewBox="0 0 10 10" refX="10" refY="5" markerWidth="7" markerHeight="7" orient="auto-start-reverse"><path d="M 0 0 L 10 5 L 0 10 z" fill="#f0b464"/></marker>
  <marker id="arr-g" viewBox="0 0 10 10" refX="10" refY="5" markerWidth="7" markerHeight="7" orient="auto-start-reverse"><path d="M 0 0 L 10 5 L 0 10 z" fill="rgba(232,238,255,0.55)"/></marker>
</defs>

<!-- state boxes: neutral(idle) -> purple(in progress) -> warn diamond (gate) -> cyan(executing) -> cyan-bright(resolved) -->
<rect x="20" y="70" width="180" height="100" rx="14" fill="rgba(255,255,255,0.04)" stroke="rgba(255,255,255,0.3)" stroke-width="1.4"/>
<text x="110" y="105" text-anchor="middle" fill="#7a7d90" font-family="JetBrains Mono, monospace" font-size="11" letter-spacing="3">STATE · 01</text>
<text x="110" y="140" text-anchor="middle" fill="#eaeaf2" font-family="Inter Tight, sans-serif" font-size="22" font-weight="600">Idle</text>

<!-- ...(In progress state, purple, same shape)... -->

<!-- decision diamond -->
<polygon points="700,120 830,60 960,120 830,180" fill="rgba(240,180,100,0.08)" stroke="rgba(240,180,100,0.8)" stroke-width="1.5"/>
<text x="830" y="115" text-anchor="middle" fill="#f0b464" font-family="JetBrains Mono, monospace" font-size="11" letter-spacing="3">GATE · 03</text>
<text x="830" y="142" text-anchor="middle" fill="#eaeaf2" font-family="Inter Tight, sans-serif" font-size="18" font-weight="600">Confidence?</text>

<!-- ...(Executing, Resolved states, cyan)... -->

<!-- happy-path arrows -->
<line x1="200" y1="120" x2="270" y2="120" stroke="#7b7fff" stroke-width="1.6" marker-end="url(#arr-p)"/>
<!-- HIGH branch continues straight to Executing; LOW branch drops down dashed -->
<path d="M 830 180 L 830 300" fill="none" stroke="#f0b464" stroke-width="1.6" stroke-dasharray="6 5" marker-end="url(#arr-w)"/>
<text x="852" y="245" fill="#f0b464" font-family="JetBrains Mono, monospace" font-size="11" letter-spacing="2">LOW · NOTIFY</text>

<!-- paused box, splits to two human-action boxes below, each loops back up dashed -->
<rect x="700" y="310" width="260" height="100" rx="14" fill="rgba(240,180,100,0.09)" stroke="rgba(240,180,100,0.75)" stroke-width="1.5"/>
<!-- Redirect (purple, loops back to "In progress") / Confirm (cyan, loops forward to "Executing") -->
```

---

## 6. Flywheel / cycle (repeating loop that compounds over time)

Use for: "N steps in a loop that keeps repeating and improving". 5-6 boxes arranged roughly in an ellipse/ring (not a perfect circle — stagger sizes/positions like the reference), connected clockwise by solid arrows, with the LAST arrow (closing the loop) dashed and warn-colored to signal "this is the feedback/learning edge". A center text label states what compounds each cycle.

```html
<!-- boxes placed around a ring: 01 (left), 02 (top-left), 03 (top-right), 04 (far right), 05 (right side, lower), 06 (bottom-center) -->
<rect x="270" y="14" width="280" height="122" rx="12" fill="rgba(108,224,214,0.08)" stroke="rgba(108,224,214,0.55)" stroke-width="1.5"/>
<text x="410" y="50" text-anchor="middle" fill="#6ce0d6" font-family="JetBrains Mono, monospace" font-size="10" letter-spacing="3">02 · SURFACE</text>
<text x="410" y="84" text-anchor="middle" fill="#f7f8f8" font-family="Inter Tight, sans-serif" font-size="22" font-weight="600">Step Name</text>
<text x="410" y="110" text-anchor="middle" fill="#8a8f98" font-family="Inter Tight, sans-serif" font-size="12">short description</text>
<!-- repeat per step, alternating cyan/purple/lilac/warn accents by step "type" (surface=cyan, human=purple, materialize=lilac, execute=neutral, learn=warn) -->

<!-- center label -->
<text x="800" y="255" text-anchor="middle" fill="#7b7fff" font-family="JetBrains Mono, monospace" font-size="11" letter-spacing="3">EACH TURN OF THE LOOP</text>
<text x="800" y="298" text-anchor="middle" fill="#f7f8f8" font-family="Inter Tight, sans-serif" font-size="34" font-weight="600">What compounds, in one line.</text>

<!-- clockwise arrows: use Q-curves between non-adjacent corner boxes, straight lines between horizontally-aligned boxes -->
<path d="M 232 250 Q 240 140 270 80" fill="none" stroke="#7b7fff" stroke-width="1.6" marker-end="url(#arr-purple)"/>
<!-- ...continue clockwise... -->
<!-- closing arrow (last step -> first step): dashed, warn-colored -->
<path d="M 860 480 Q 500 510 130 336" fill="none" stroke="#f0b464" stroke-width="1.6" stroke-dasharray="6 5" marker-end="url(#arr-purple)"/>
```

---

## 7. Numbered waterfall (vertical step list, non-SVG — pure HTML/CSS)

Use for: simpler "N sequential steps, each building on the last" without needing SVG geometry. Full-width rounded panels stacked vertically, connected by a small centered `↓` arrow between them; step 1 = cyan, step 2 = lilac/purple, step 3 = purple (progression toward action).

```html
<div style="display:flex;flex-direction:column;gap:8px;">
  <div style="border:1px solid rgba(108,224,214,0.4);border-radius:10px;padding:20px 28px;background:rgba(108,224,214,0.06);">
    <span style="font-family:var(--font-mono);font-size:12px;color:#6ce0d6;letter-spacing:0.1em;">01</span>
    <b style="color:#eaeaf2;font-size:18px;margin-left:12px;">Creates <span style="color:#6ce0d6;">Opportunity</span></b>
    <div style="color:var(--ink-dim);font-size:14px;margin-top:4px;">Names the emerging pattern · links evidence.</div>
  </div>
  <div style="text-align:center;color:var(--ink-mute);">↓</div>
  <!-- repeat per step -->
</div>
```

---

## Color-by-role cheat sheet (applies to all patterns above)

- **Cyan** = the "good"/primary/AI/current path, the thing being highlighted right now.
- **Purple** = human involvement, decisions, secondary category.
- **Lilac** = a third distinct category (e.g. "organizational" vs "individual"), used sparingly.
- **Warn orange** = gates, pauses, caution, the loop-closing/feedback edge.
- **Neutral white/dim** = baseline/today/unremarkable nodes that aren't the point of the diagram.
