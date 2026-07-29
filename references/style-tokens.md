# Style tokens — copy-paste boilerplate

## Fonts (Google Fonts link, put in `<head>`)

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Carlito:ital,wght@0,400;0,700;1,400;1,700&family=Inter+Tight:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500;700&display=swap" rel="stylesheet">
```

- **Display / body font**: `'Carlito', 'Calibri', 'Inter Tight', sans-serif` — headings, body copy.
- **Node label font inside SVG**: `'Inter Tight', sans-serif` — bold (600–700), for the actual node names.
- **Mono / micro-label font**: `'JetBrains Mono', monospace` — uppercase tags, state numbers, section labels. Always paired with `letter-spacing` between `2px` and `3px` (in SVG) or `0.14em`–`0.32em` (in CSS).

## CSS custom properties

```css
:root {
    --stage-bg: #06070a;
    --slide-bg: #06070a;
    --ink: #eaeaf2;
    --ink-dim: #7a7d90;
    --ink-mute: #464858;
    --line: rgba(255,255,255,0.07);
    --line-strong: rgba(255,255,255,0.14);
    --purple: #7b7fff;
    --purple-soft: rgba(123,127,255,0.18);
    --cyan: #6ce0d6;
    --cyan-soft: rgba(108,224,214,0.18);
    --lilac: #b58bff;
    --warn: #f0b464;
    --font-display: 'Carlito', 'Calibri', 'Inter Tight', sans-serif;
    --font-mono: 'JetBrains Mono', monospace;
}
```

## Background atmosphere (grid + orb glow + vignette)

Every slide/canvas stacks these three absolute-positioned layers behind the content, in this order:

```html
<div class="grid-bg"></div>
<div class="orb tr small cyan"></div>  <!-- position + size + color modifiers, see below -->
<div class="vignette"></div>
```

```css
.grid-bg {
    position: absolute; inset: 0;
    background-image:
        linear-gradient(rgba(255,255,255,0.03) 1px, transparent 1px),
        linear-gradient(90deg, rgba(255,255,255,0.03) 1px, transparent 1px);
    background-size: 80px 80px; pointer-events: none;
}
.vignette { position: absolute; inset: 0; background: radial-gradient(ellipse at 50% 50%, transparent 25%, rgba(0,0,0,0.65) 100%); pointer-events: none; }

.orb {
    position: absolute; width: 900px; height: 900px; border-radius: 50%;
    background:
        radial-gradient(circle at 35% 35%, rgba(123,127,255,0.55) 0%, transparent 55%),
        radial-gradient(circle at 65% 65%, rgba(108,224,214,0.35) 0%, transparent 55%);
    filter: blur(60px); opacity: 0.9; pointer-events: none;
}
.orb.tr { right: -180px; top: -180px; }
.orb.bl { left: -260px; bottom: -260px; }
.orb.tl { left: -220px; top: -220px; }
.orb.br { right: -220px; bottom: -220px; }
.orb.center { left: 50%; top: 50%; transform: translate(-50%,-50%); opacity: 0.5; }
.orb.small { width: 560px; height: 560px; }
.orb.cyan   { background: radial-gradient(circle at 50% 50%, rgba(108,224,214,0.45), transparent 60%); }
.orb.purple { background: radial-gradient(circle at 50% 50%, rgba(123,127,255,0.55), transparent 60%); }
.orb.lilac  { background: radial-gradient(circle at 50% 50%, rgba(181,139,255,0.45), transparent 60%); }
```

Pick ONE corner (`tr`/`bl`/`tl`/`br`) or `center`, plus `small` for a single-diagram canvas (full `.orb` with no `small` is for full 1920×1080 hero slides). One orb color per canvas is enough — match it to the diagram's primary accent.

## Text component classes

```css
.tag {
    display: inline-flex; align-items: center; gap: 12px;
    font-family: var(--font-mono); font-size: 13px; color: var(--cyan);
    letter-spacing: 0.2em; text-transform: uppercase;
    padding: 10px 16px; border: 1px solid rgba(108,224,214,0.35); border-radius: 999px;
    background: rgba(108,224,214,0.05); width: fit-content;
}
.tag .pulse { width: 8px; height: 8px; border-radius: 50%; background: currentColor; box-shadow: 0 0 12px currentColor; }

.section-num {
    font-family: var(--font-mono); font-size: 15px; color: var(--cyan);
    letter-spacing: 0.28em; text-transform: uppercase;
    display: flex; align-items: center; gap: 20px;
}
.section-num .bar { width: 60px; height: 1px; background: var(--cyan); opacity: 0.6; }
.section-num.purple { color: var(--purple); } .section-num.purple .bar { background: var(--purple); }
.section-num.lilac  { color: var(--lilac); }  .section-num.lilac .bar  { background: var(--lilac); }

.h-slide { font-family: var(--font-display); font-size: 76px; font-weight: 600; line-height: 1.05; letter-spacing: -0.03em; color: var(--ink); }
.h-slide em {
    font-style: normal;
    background: linear-gradient(120deg, var(--cyan) 0%, var(--purple) 100%);
    -webkit-background-clip: text; background-clip: text; -webkit-text-fill-color: transparent;
    padding-right: 0.05em; margin-right: -0.05em;
}
.sub { font-family: var(--font-display); font-size: 24px; color: var(--ink-dim); line-height: 1.5; max-width: 900px; font-weight: 400; }
```

`.h-slide em` and `.sub` give you the standard "headline with a gradient-highlighted key phrase, then a dim descriptive sentence" pattern seen throughout the deck (e.g. "Linear becomes the *coordinator*." + dim explanatory sentence below).

## SVG marker defs (arrowheads, reused across diagrams)

```html
<defs>
  <marker id="arr-cyan" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="6" markerHeight="6" orient="auto">
    <path d="M0,0 L10,5 L0,10 z" fill="#6ce0d6"/>
  </marker>
  <marker id="arr-purple" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="6" markerHeight="6" orient="auto">
    <path d="M0,0 L10,5 L0,10 z" fill="#7b7fff"/>
  </marker>
  <marker id="arr-warn" viewBox="0 0 10 10" refX="10" refY="5" markerWidth="7" markerHeight="7" orient="auto-start-reverse">
    <path d="M 0 0 L 10 5 L 0 10 z" fill="#f0b464"/>
  </marker>
  <marker id="arr-dim" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="6" markerHeight="6" orient="auto">
    <path d="M0,0 L10,5 L0,10 z" fill="rgba(232,238,255,0.45)"/>
  </marker>
</defs>
```

## Node "recipes" (fill/stroke opacity pairs by role)

| Role | fill | stroke |
|---|---|---|
| Neutral / today / baseline | `rgba(255,255,255,0.04-0.06)` | `rgba(255,255,255,0.18-0.35)` |
| Cyan hero / highlighted / current-state | `rgba(108,224,214,0.08-0.16)` | `#6ce0d6` or `rgba(108,224,214,0.7-0.85)`, width 1.5-2, optional `filter="drop-shadow(0 0 24-36px rgba(108,224,214,0.28-0.35))"` |
| Purple / human / decision | `rgba(123,127,255,0.09-0.11)` | `rgba(123,127,255,0.6-0.75)` |
| Lilac / tertiary / organizational | `rgba(181,139,255,0.08-0.10)` | `rgba(181,139,255,0.45-0.75)` |
| Warn / gate / paused | `rgba(240,180,100,0.08-0.09)` | `rgba(240,180,100,0.75-0.8)` |

Node text: `fill="#e8eeff"` or `#eaeaf2`, `font-family="Inter Tight, sans-serif"`, `font-weight="600-700"`, centered with `text-anchor="middle"`.
Micro-labels above/below node text: matching accent color at higher opacity, `font-family="JetBrains Mono, monospace"`, `font-size="10-12"`, `letter-spacing="2-3"`, uppercase.

## Minimal standalone HTML skeleton

```html
<!DOCTYPE html>
<html lang="en"><head>
<meta charset="UTF-8" />
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Carlito:ital,wght@0,400;0,700;1,400;1,700&family=Inter+Tight:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500;700&display=swap" rel="stylesheet">
<style>
  /* :root vars + .grid-bg/.orb/.vignette/.tag/.section-num/.h-slide/.sub from above */
  html,body{margin:0;background:var(--stage-bg);font-family:var(--font-display);}
  .canvas{position:relative;width:1600px;padding:96px;overflow:hidden;}
</style>
</head>
<body>
<div class="canvas">
  <div class="grid-bg"></div>
  <div class="orb tr small cyan"></div>
  <div class="vignette"></div>
  <!-- header: .section-num + .h-slide + .sub -->
  <!-- diagram: inline <svg viewBox="0 0 W H"> ... </svg> -->
</div>
</body></html>
```
