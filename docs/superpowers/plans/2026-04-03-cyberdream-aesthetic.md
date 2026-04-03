# Analog Punk Cyberdream Aesthetic Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Transform `index.html` from yellow-primary minimalist to full Analog Punk Cyberdream palette with per-page accent colors, CRT effects, VT323/Permanent Marker fonts, blinking LEDs, and sticker elements.

**Architecture:** Single-file SPA — all changes in `index.html`. CSS edits first (variables, new classes), then HTML markup additions (LEDs, stickers), then JS canvas color updates. No new files created.

**Tech Stack:** Vanilla HTML/CSS/JS, Google Fonts (add VT323 + Permanent Marker, remove Syne)

---

## Task 1: Update Google Fonts link and CSS root variables

**Files:**
- Modify: `index.html:8` (Google Fonts link)
- Modify: `index.html:11-15` (`:root` variables)

- [ ] **Step 1: Replace Google Fonts link (line 8)**

Change:
```html
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=DM+Mono:wght@300;400&family=Syne:wght@300;400;600;800&display=swap" rel="stylesheet">
```
To:
```html
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=VT323&family=Permanent+Marker&family=DM+Mono:wght@300;400&display=swap" rel="stylesheet">
```

- [ ] **Step 2: Replace `:root` block (lines 11-15)**

Change:
```css
:root{
  --y:#FFE600;--b:#080808;--b2:#111111;--w:#F0EDE5;
  --dim:rgba(240,237,229,.32);--dim2:rgba(240,237,229,.55);
  --bb:'Bebas Neue',sans-serif;--sy:'Syne',sans-serif;--mo:'DM Mono',monospace;
}
```
To:
```css
:root{
  --cyan:#00f5ff;--mag:#ff00aa;--acid:#aaff00;--amber:#ff9500;--purple:#9b30ff;
  --fog:#8a9a8a;--b:#0a0a0a;--b2:#0f0f14;--w:#f0ece0;
  --accent:var(--cyan);
  --bb:'Bebas Neue',sans-serif;--vt:'VT323',monospace;--pm:'Permanent Marker',cursive;--mo:'DM Mono',monospace;
}
```

---

## Task 2: Add per-page accent scoping and scanlines/LED/sticker CSS

**Files:**
- Modify: `index.html` — CSS block, just before the closing `</style>` tag (line 496)

- [ ] **Step 1: Add per-page accent scoping, scanlines, LED, and sticker rules**

Insert before `</style>` (line 496):
```css
/* PER-PAGE ACCENT */
#page-home{--accent:var(--cyan);}
#page-code{--accent:var(--acid);}
#page-physics{--accent:var(--amber);}
#page-ai{--accent:var(--purple);}

/* CRT SCANLINES */
body::after{content:'';position:fixed;inset:0;background:repeating-linear-gradient(0deg,transparent,transparent 2px,rgba(0,0,0,.07) 2px,rgba(0,0,0,.07) 4px);pointer-events:none;z-index:199;}

/* BLINKING LED */
.led{display:inline-block;width:7px;height:7px;border-radius:50%;background:var(--accent);box-shadow:0 0 8px var(--accent),0 0 16px var(--accent);margin-right:7px;vertical-align:middle;flex-shrink:0;animation:ledBlink 1s ease-in-out infinite;}
@keyframes ledBlink{0%,100%{opacity:1;box-shadow:0 0 10px var(--accent),0 0 20px var(--accent);}50%{opacity:.1;box-shadow:none;}}

/* STICKER */
.sticker{position:absolute;font-family:var(--vt);font-size:.68rem;letter-spacing:.18em;text-transform:uppercase;color:var(--accent);border:1.5px solid var(--accent);padding:3px 10px;transform:rotate(var(--rot,-3deg));box-shadow:0 0 10px var(--accent);white-space:nowrap;z-index:10;}

/* HERO GRADIENT TITLE (home) */
.hero-name-gradient{background:linear-gradient(135deg,var(--cyan) 0%,var(--mag) 50%,var(--amber) 100%);-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;filter:drop-shadow(0 0 20px rgba(0,245,255,.35));}

/* COURSE TITLE GLOW */
.course-title-glow{filter:drop-shadow(0 0 15px var(--accent));}
```

---

## Task 3: Replace all `var(--y)` with `var(--accent)` in CSS

**Files:**
- Modify: `index.html` CSS block (lines 17–496)

This task replaces every `var(--y)` occurrence in CSS rules with `var(--accent)`.

- [ ] **Step 1: Apply all CSS replacements**

Use replace-all for each pattern:

| Find | Replace |
|------|---------|
| `var(--y)` | `var(--accent)` |
| `rgba(255,230,0,` | `rgba(0,245,255,` |
| `255,230,0` (in inline rgba strings not already covered) | `0,245,255` |

Specifically update these rules:
- `.hero-eyebrow` color → `var(--accent)`
- `.hero-name .y` → `.hero-name .y{color:var(--accent);}`
- `.hero-name .outline` → `-webkit-text-stroke:1.5px rgba(0,245,255,.2)`
- `.cred-val` color → `var(--accent)`
- `.cred-label` color → `var(--fog)` (was `var(--dim)`)
- `.btn-y` → rename to `.btn-primary`, background `var(--accent)`, color `var(--b)`, hover box-shadow `4px 4px 0 var(--accent)`
- `.btn-o` border → `1px solid rgba(0,245,255,.3)`, hover border/color → `var(--accent)`
- `.section-label` color → `var(--accent)`, `::after` background → `rgba(0,245,255,.15)`
- `.bio-text .hl` → `color:var(--accent)`
- `.fact` border-left → `rgba(0,245,255,.25)`, hover → `var(--accent)`
- `.fact-title` → `var(--accent)`
- `.season-card` border → `rgba(0,245,255,.1)`, hover border → `rgba(0,245,255,.45)`
- `.season-card::before` gradient → `var(--accent),transparent`
- `.season-label` → `var(--accent)`
- `.course-card` border → `rgba(0,245,255,.1)`, hover → `rgba(0,245,255,.5)`
- `.course-card::before` → `var(--accent),transparent`
- `.card-num` → `rgba(0,245,255,.07)`
- `.card-sub` → `var(--accent)`
- `.card-link` → `var(--accent)`
- `.footer-socials a:hover` → `var(--accent)`
- `.course-back:hover` → `var(--accent)`
- `.course-tag` border/color → `var(--accent)`
- `.course-title .accent` → `var(--accent)`
- `.pill` border → `rgba(0,245,255,.25)`, color → `rgba(0,245,255,.6)`, hover → `var(--accent)`, hover bg → `rgba(0,245,255,.06)`
- `.learn-card` border → `rgba(0,245,255,.1)`, hover → `rgba(0,245,255,.4)`
- `.path-card` border → `rgba(0,245,255,.12)`, hover → `rgba(0,245,255,.4)`
- `.path-card.featured` border → `rgba(0,245,255,.3)`
- `.path-card.featured::before` background → `var(--accent)`
- `.path-audience` → `var(--accent)`
- `.path-divider` → `rgba(0,245,255,.1)`
- `.module-num` → `var(--accent)`
- `.module-item:hover` → `rgba(0,245,255,.04)`
- `.path-pricing` border-top → `rgba(0,245,255,.1)`, background → `rgba(0,245,255,.02)`
- `.price-pack` → `rgba(0,245,255,.8)`
- `.price-pack strong` → `var(--accent)`
- `.path-features li::before` → `var(--accent)`
- `.path-cta-y` → rename `.path-cta-primary`, background `var(--accent)`, hover box-shadow `4px 4px 0 var(--accent)`
- `.path-cta-o` border → `rgba(0,245,255,.35)`, hover → `var(--accent)`
- `.for-col-title.good` → `var(--accent)`
- `.for-list.good li::before` → `var(--accent)`
- `.cta-title .y` → `var(--accent)`
- `.cta-section` border-top → `rgba(0,245,255,.08)`
- `.persona-btn` border → `rgba(0,245,255,.25)`, background → `rgba(0,245,255,.03)`
- `.persona-btn::before` background → `var(--accent)`
- `.persona-btn:hover,.persona-btn.active` border-color → `var(--accent)`
- `.path-card.persona-match` border-color → `rgba(0,245,255,.55)`
- `.path-card.persona-match .path-header` → `rgba(0,245,255,.04)`
- `.persona-banner` background → `var(--accent)`
- `.lang-btn` border → `rgba(0,245,255,.2)`, hover/active → `var(--accent)`
- `.email-copy-btn:hover` → `var(--accent)`
- `.form-input` border → `rgba(0,245,255,.2)`, focus → `rgba(0,245,255,.7)`
- `.form-label` → `var(--accent)`
- `.materials-list li::before` → `var(--accent)`
- `.poly-tag` border → `rgba(0,245,255,.15)`, color → `rgba(0,245,255,.45)`, hover → `var(--accent)` border/color

---

## Task 4: Replace all Syne (`var(--sy)`) with DM Mono (`var(--mo)`) in CSS

**Files:**
- Modify: `index.html` CSS block

- [ ] **Step 1: Replace `var(--sy)` with `var(--mo)` everywhere**

Use replace-all: `var(--sy)` → `var(--mo)`

- [ ] **Step 2: Replace section label font with VT323**

Change `.section-label`:
```css
.section-label{font-family:var(--vt);font-size:.9rem;letter-spacing:.28em;text-transform:uppercase;color:var(--accent);margin-bottom:2.5rem;display:flex;align-items:center;gap:.8rem;}
.section-label::after{content:'';flex:1;height:1px;background:rgba(0,245,255,.15);max-width:120px;}
```

- [ ] **Step 3: Replace nav link font with VT323**

Change `.nav-center a`:
```css
.nav-center a{font-family:var(--vt);font-size:.85rem;letter-spacing:.1em;text-transform:uppercase;color:rgba(240,236,224,.55);text-decoration:none;cursor:none;transition:color .2s;position:relative;padding-bottom:3px;white-space:nowrap;}
```

- [ ] **Step 4: Replace nav logo font with VT323**

Change `.nav-logo`:
```css
.nav-logo{font-family:var(--vt);font-size:.95rem;letter-spacing:.22em;text-transform:uppercase;color:var(--accent);text-decoration:none;cursor:none;flex-shrink:0;}
```

- [ ] **Step 5: Replace tag/pill fonts with VT323**

Change `.pill`:
```css
.pill{font-family:var(--vt);font-size:.8rem;letter-spacing:.12em;text-transform:uppercase;padding:.35rem .9rem;border:1px solid rgba(0,245,255,.25);border-radius:20px;color:rgba(0,245,255,.6);transition:all .22s;white-space:nowrap;}
```

Change `.poly-tag`:
```css
.poly-tag{font-family:var(--vt);font-size:.75rem;letter-spacing:.14em;text-transform:uppercase;padding:.3rem .8rem;border:1px solid rgba(0,245,255,.15);border-radius:20px;color:rgba(0,245,255,.45);transition:all .2s;}
```

Change `.dna-tag` (if present), `.lang-btn`, footer copy to use `var(--vt)`.

Change `.lang-btn`:
```css
.lang-btn{font-family:var(--vt);font-size:.75rem;letter-spacing:.1em;text-transform:uppercase;padding:.22rem .55rem;border:1px solid rgba(0,245,255,.2);border-radius:2px;background:transparent;color:rgba(240,236,224,.32);cursor:pointer;transition:all .2s;}
```

Change `.footer-copy`, `.footer-socials a`:
```css
.footer-copy{font-family:var(--vt);font-size:.75rem;letter-spacing:.12em;text-transform:uppercase;color:rgba(240,236,224,.32);}
.footer-socials a{font-family:var(--vt);font-size:.75rem;letter-spacing:.12em;text-transform:uppercase;color:rgba(240,236,224,.32);text-decoration:none;cursor:none;transition:color .2s;}
```

- [ ] **Step 6: Replace hero-tagline and subtitles to Permanent Marker**

Change `.hero-tagline`:
```css
.hero-tagline{font-family:var(--pm);font-size:clamp(1rem,2vw,1.35rem);color:rgba(240,236,224,.55);max-width:42ch;line-height:1.5;margin-top:1.4rem;opacity:0;animation:rise .8s ease .75s forwards;}
```

Change `.course-subtitle`:
```css
.course-subtitle{font-family:var(--pm);font-size:clamp(.95rem,1.8vw,1.2rem);color:rgba(240,236,224,.55);max-width:48ch;line-height:1.55;margin-bottom:2rem;}
```

---

## Task 5: Update cursor color from yellow to cyan

**Files:**
- Modify: `index.html:190-191` (cursor CSS)

- [ ] **Step 1: Update cursor rules**

Change:
```css
.cur{width:9px;height:9px;background:var(--y);border-radius:50%;}
.cur-r{width:34px;height:34px;border:1.5px solid rgba(255,230,0,.5);border-radius:50%;z-index:9998;transition:all .13s ease;}
```
To:
```css
.cur{width:9px;height:9px;background:var(--cyan);border-radius:50%;}
.cur-r{width:34px;height:34px;border:1.5px solid rgba(0,245,255,.5);border-radius:50%;z-index:9998;transition:all .13s ease;}
```

---

## Task 6: Update HTML — home hero gradient title + stickers

**Files:**
- Modify: `index.html:529` (hero-name span)
- Modify: `index.html:525-527` (home-hero div, add stickers)

- [ ] **Step 1: Add gradient class to hero name**

Change (line 529):
```html
<h1 class="hero-name">FABIO<br><span class="y">MARCHIANÒ</span><span class="outline" aria-hidden="true">MASTERCLASS</span></h1>
```
To:
```html
<h1 class="hero-name hero-name-gradient">FABIO<br>MARCHIANÒ<span class="outline" aria-hidden="true">MASTERCLASS</span></h1>
```

- [ ] **Step 2: Add sticker to home hero**

Inside `.home-hero` div (after `<canvas id="canvas-home"></canvas>`), add:
```html
<div class="sticker" style="--rot:4deg;top:7rem;right:clamp(1.5rem,5vw,5rem)">v2.1 · PERSONAL</div>
<div class="sticker" style="--rot:-2deg;top:10rem;right:clamp(1.5rem,5vw,5rem);--accent:var(--mag)">Forest Room Ed.</div>
```

---

## Task 7: Update HTML — course pages hero glow + stickers

**Files:**
- Modify: `index.html` — course hero sections for Code (line ~627), Physics (line ~815), AI (line ~1422)

- [ ] **Step 1: Add glow class to course titles**

For each of the three `.course-title` headings, add class `course-title-glow`:
```html
<h1 class="course-title course-title-glow" ...>
```

- [ ] **Step 2: Add stickers to each course hero**

After each `<canvas id="canvas-X">`, add a sticker:

Code page (inside `.course-hero`):
```html
<div class="sticker" style="--rot:3deg;top:7rem;right:clamp(1.5rem,5vw,5rem)">Processing · p5.js</div>
```

Physics page:
```html
<div class="sticker" style="--rot:-2deg;top:7rem;right:clamp(1.5rem,5vw,5rem)">Arduino · DIY</div>
```

AI page:
```html
<div class="sticker" style="--rot:4deg;top:7rem;right:clamp(1.5rem,5vw,5rem)">Automation · AI</div>
```

---

## Task 8: Update HTML — LED spans on section labels

**Files:**
- Modify: `index.html` — all `<div class="section-label">` elements

- [ ] **Step 1: Add `<span class="led"></span>` to every section-label**

Find every `<div class="section-label"...>` and prepend a `<span class="led"></span>` as the first child. There are ~12 section labels across all pages. Example:

```html
<div class="section-label" data-i18n="about_label"><span class="led"></span>// About</div>
```

---

## Task 9: Update HTML — rename yellow button classes

**Files:**
- Modify: `index.html` HTML (all occurrences of `btn-y`, `path-cta-y`)

- [ ] **Step 1: Rename `btn-y` to `btn-primary` in HTML**

Use replace-all: `class="btn btn-y"` → `class="btn btn-primary"`

- [ ] **Step 2: Rename `path-cta-y` to `path-cta-primary` in HTML**

Use replace-all: `class="path-cta path-cta-y"` → `class="path-cta path-cta-primary"`

---

## Task 10: Update canvas RGB colors in JavaScript

**Files:**
- Modify: `index.html:1449` (home canvas)
- Modify: `index.html:1468-1470` (code canvas)
- Modify: `index.html:1488-1493` (physics canvas)
- Modify: `index.html:1791` (AI canvas)
- Modify: `index.html:1438` (vig() background color)

- [ ] **Step 1: Update home canvas RGB (line 1449)**

Change:
```js
function draw(){if(!W||!H)return void(rAF=requestAnimationFrame(draw));t+=.004;ctx.clearRect(0,0,W,H);moveP(pts,W,H,t);edges(ctx,pts,140,255,230,0);drawNodes(ctx,pts,t,255,230,0);vig(ctx,W,H);rAF=requestAnimationFrame(draw);}
```
To:
```js
function draw(){if(!W||!H)return void(rAF=requestAnimationFrame(draw));t+=.004;ctx.clearRect(0,0,W,H);moveP(pts,W,H,t);edges(ctx,pts,140,0,245,255);drawNodes(ctx,pts,t,0,245,255);vig(ctx,W,H);rAF=requestAnimationFrame(draw);}
```

- [ ] **Step 2: Update code canvas RGB (line 1468-1470)**

Change `rgba(0,255,180,.018)` → `rgba(170,255,0,.018)` (ASCII rain color)
Change `edges(ctx,pts,120,0,255,180)` → `edges(ctx,pts,120,170,255,0)`
Change `drawNodes(ctx,pts,t,0,255,180)` → `drawNodes(ctx,pts,t,170,255,0)`

- [ ] **Step 3: Update physics canvas RGB (lines 1488-1493)**

Change `rgba(255,140,0,` → `rgba(255,149,0,` (amber from style card, matches `--amber:#ff9500`)

- [ ] **Step 4: Update AI canvas RGB (line 1791)**

Change:
```js
const COL='0,230,120';
```
To:
```js
const COL='155,48,255';
```

- [ ] **Step 5: Update vig() background hardcoded color (line 1438)**

Change:
```js
function vig(ctx,W,H){if(!W||!H||!isFinite(W)||!isFinite(H))return;const v=ctx.createRadialGradient(W/2,H/2,H*.2,W/2,H/2,H*.85);v.addColorStop(0,'rgba(8,8,8,0)');v.addColorStop(1,'rgba(8,8,8,.88)');ctx.fillStyle=v;ctx.fillRect(0,0,W,H);}
```
To:
```js
function vig(ctx,W,H){if(!W||!H||!isFinite(W)||!isFinite(H))return;const v=ctx.createRadialGradient(W/2,H/2,H*.2,W/2,H/2,H*.85);v.addColorStop(0,'rgba(10,10,10,0)');v.addColorStop(1,'rgba(10,10,10,.88)');ctx.fillStyle=v;ctx.fillRect(0,0,W,H);}
```

Also update the AI canvas vignette (line 1844-1846) which has `rgba(8,8,8,...)` hardcoded → `rgba(10,10,10,...)`.

---

## Task 11: Update Cal.com brand color and remaining hardcoded yellows

**Files:**
- Modify: `index.html:500` (Cal.com CSS vars)

- [ ] **Step 1: Update Cal.com brand color**

Change:
```js
Cal.ns["fabio-marchiano"]("ui",{hideEventTypeDetails:false,layout:"month_view",cssVarsPerTheme:{light:{"cal-brand":"#FFE600","cal-brand-text":"#080808"},dark:{"cal-brand":"#FFE600","cal-brand-text":"#080808"}}});
```
To:
```js
Cal.ns["fabio-marchiano"]("ui",{hideEventTypeDetails:false,layout:"month_view",cssVarsPerTheme:{light:{"cal-brand":"#00f5ff","cal-brand-text":"#0a0a0a"},dark:{"cal-brand":"#00f5ff","cal-brand-text":"#0a0a0a"}}});
```

---

## Task 12: Update CLAUDE.md palette and font rules

**Files:**
- Modify: `CLAUDE.md`
- Modify: `memory/design-rules.md`

- [ ] **Step 1: Update CLAUDE.md palette rule (rule #4)**

Change:
```
4. **Palette**: `--y:#FFE600` (yellow) · `--b:#080808` (black) · `--w:#F0EDE5` (warm white)
```
To:
```
4. **Palette**: `--cyan:#00f5ff` · `--mag:#ff00aa` · `--acid:#aaff00` · `--amber:#ff9500` · `--purple:#9b30ff` · `--b:#0a0a0a` · `--w:#f0ece0`. Per-page `--accent` scoped on each `#page-X` div. No yellow.
```

- [ ] **Step 2: Update CLAUDE.md font rule**

Update "Google Fonts is the only CDN" note to list: Bebas Neue + VT323 + Permanent Marker + DM Mono.

- [ ] **Step 3: Update canvas color identity in CLAUDE.md**

Change:
```
- Home: yellow `255,230,0` — flow field particles
- Code: cyan `0,255,180` — ASCII rain + particles
- Physics: orange `255,140,0` — circuit grid nodes
- AI: green `0,230,120` — neural network nodes + edges
```
To:
```
- Home: cyan `0,245,255` — flow field particles
- Code: acid `170,255,0` — ASCII rain + particles
- Physics: amber `255,149,0` — circuit grid nodes
- AI: purple `155,48,255` — neural network nodes + edges
```

- [ ] **Step 4: Update design-rules.md palette and font sections**

Replace palette variables and font list to match new values.
