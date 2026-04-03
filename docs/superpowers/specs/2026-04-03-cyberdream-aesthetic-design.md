# Analog Punk Cyberdream — Aesthetic Redesign
**Date:** 2026-04-03  
**Status:** Approved  
**Scope:** Full visual overhaul of `index.html` — palette, typography, effects, per-page identity

---

## Context

The masterclass site is functional. This redesign makes it personal — applying the "Analog Punk Cyberdream / Forest Room Edition" aesthetic defined in `style-card.html`. The site remains a single-file SPA with no build tools or external frameworks.

---

## Palette

Replace the existing yellow-primary palette entirely. No yellow anywhere in the final result.

```css
:root {
  --cyan:   #00f5ff;   /* Home accent / global secondary */
  --mag:    #ff00aa;   /* Home gradient pair */
  --acid:   #aaff00;   /* Code page accent */
  --amber:  #ff9500;   /* Physics page accent */
  --purple: #9b30ff;   /* AI page accent */
  --fog:    #8a9a8a;   /* Dimmed labels / secondary text */
  --b:      #0a0a0a;   /* Background (replaces #080808) */
  --b2:     #0f0f14;   /* Card / band background */
  --w:      #f0ece0;   /* Warm white body text (unchanged) */
}
```

Remove `--y`, `--dim`, `--dim2` variables. Replace all references:
- Former `var(--y)` → `var(--accent)` (page-scoped) or `var(--cyan)` globally
- Former `var(--dim)` → `rgba(240,236,224,0.32)`
- Former `var(--dim2)` → `rgba(240,236,224,0.55)`
- Former `var(--b2)` → `var(--b2)` (updated value `#0f0f14`)

Each page div gets `--accent` set to its color:
```css
#page-home    { --accent: var(--cyan); }
#page-code    { --accent: var(--acid); }
#page-physics { --accent: var(--amber); }
#page-ai      { --accent: var(--purple); }
```

---

## Typography

### Remove
- Syne (`--sy`) — eliminated entirely
- Remove from Google Fonts `<link>`

### Add
- VT323 (`--vt`) — section labels, nav links, tags, stickers, footer
- Permanent Marker (`--pm`) — hero subtitles, one-liner / tagline blocks

### Updated Google Fonts link
```html
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=VT323&family=Permanent+Marker&family=DM+Mono:wght@300;400&display=swap" rel="stylesheet">
```

### Updated CSS variables
```css
--bb: 'Bebas Neue', sans-serif;   /* hero titles — unchanged */
--vt: 'VT323', monospace;          /* labels, tags, nav, stickers */
--pm: 'Permanent Marker', cursive; /* subtitles, one-liners */
--mo: 'DM Mono', monospace;        /* all body text, descriptions, pricing */
```

### Font role mapping
| Role | Before | After |
|------|--------|-------|
| Hero H1 | Bebas Neue | Bebas Neue (unchanged) |
| Hero subtitle | Syne 300 | Permanent Marker |
| Section labels | DM Mono | VT323 |
| Body / descriptions | Syne 300 | DM Mono 300 |
| Nav links | DM Mono | VT323 |
| Tags / pills | DM Mono | VT323 |
| Pricing | DM Mono | DM Mono (unchanged) |
| Footer | DM Mono | VT323 |

---

## Global Effects

### Scanlines (new)
Add CRT scanline overlay on top of existing grain. The grain stays on `body::before`. Scanlines go on `body::after`:
```css
body::after {
  content: '';
  position: fixed;
  inset: 0;
  background: repeating-linear-gradient(
    0deg,
    transparent, transparent 2px,
    rgba(0,0,0,0.07) 2px, rgba(0,0,0,0.07) 4px
  );
  pointer-events: none;
  z-index: 199; /* just below grain at 200 */
}
```

### Blinking LED on section labels
Every `section-label` element gets a blinking dot prepended:
```html
<div class="section-label"><span class="led"></span>// Title</div>
```
```css
.led {
  display: inline-block;
  width: 7px; height: 7px;
  border-radius: 50%;
  background: var(--accent);
  box-shadow: 0 0 8px var(--accent), 0 0 16px var(--accent);
  margin-right: 7px;
  vertical-align: middle;
  animation: ledBlink 1s ease-in-out infinite;
}
@keyframes ledBlink {
  0%, 100% { opacity: 1; box-shadow: 0 0 10px var(--accent), 0 0 20px var(--accent); }
  50%       { opacity: 0.1; box-shadow: none; }
}
```

### Sticker elements (new)
Floating rotated badge on each page's hero section. 1–2 per page. Example:
```html
<div class="sticker" style="--rot:4deg; top:1rem; right:1.5rem; --sc:var(--accent)">
  DIY · PERSONAL
</div>
```
```css
.sticker {
  position: absolute;
  font-family: var(--vt);
  font-size: 0.7rem;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: var(--sc, var(--accent));
  border: 1.5px solid var(--sc, var(--accent));
  padding: 3px 10px;
  transform: rotate(var(--rot, -3deg));
  box-shadow: 0 0 10px var(--sc, var(--accent));
  white-space: nowrap;
  z-index: 10;
}
```

### Custom cursor
Cursor dot stays. Change color from yellow to `var(--cyan)` globally.

---

## Per-page Identity

### Home (`#page-home`)
- `--accent: var(--cyan)`
- Hero H1 title: `background: linear-gradient(135deg, var(--cyan) 0%, var(--mag) 50%, var(--amber) 100%)` with `-webkit-background-clip: text`
- Canvas: cyan primary particles. If the existing canvas code supports a secondary color without major surgery, add magenta as secondary; otherwise cyan only.
- Sticker: e.g. `v2.1 · PERSONAL` top-right, cyan

### Code (`#page-code`)
- `--accent: var(--acid)`
- Hero title: acid glow via `filter: drop-shadow(0 0 15px rgba(170,255,0,0.4))`
- Canvas: acid green particles (replaces current cyan `0,255,180`)
- Sticker: e.g. `Processing · p5.js` top-right, acid

### Physics (`#page-physics`)
- `--accent: var(--amber)`
- Hero title: amber glow
- Canvas: amber particles (replaces current orange `255,140,0` — similar, just use `255,149,0`)
- Sticker: e.g. `Arduino · DIY` top-right, amber

### AI (`#page-ai`)
- `--accent: var(--purple)`
- Hero title: purple glow
- Canvas: purple particles (replaces current green `0,230,120`)
- Sticker: e.g. `Automation · AI` top-right, purple

---

## Buttons

| Type | Before | After |
|------|--------|-------|
| Primary CTA (`.btn-y`) | yellow bg, black text | `var(--accent)` bg, `var(--b)` text |
| Secondary outlined (`.path-cta-o`) | yellow border | `var(--accent)` border |
| Featured path CTA (`.path-cta-y`) | yellow bg | `var(--accent)` bg |
| Ghost (`.email-copy-btn`) | yellow on hover | `var(--accent)` on hover |

Rename `.btn-y` → `.btn-primary`, `.path-cta-y` → `.path-cta-primary` in both CSS and HTML to remove yellow-specific naming.

---

## What Doesn't Change

- SPA routing (`showPage()`)
- i18n system (`setLang()`, all `data-i18n` keys, `T` object)
- All copy text
- Cal.com button data attributes
- Canvas guard logic (`if(!isFinite(x))`)
- Scroll reveal (`.reveal` / IntersectionObserver)
- Grain overlay on `body::before`
- Responsive breakpoints
- Single-file constraint

---

## CLAUDE.md Updates Required

Update the palette section:
- Remove `--y:#FFE600` rule
- Add new palette variables
- Update canvas color identity table to match new per-page accents
- Update font list (add VT323, Permanent Marker; remove Syne)
