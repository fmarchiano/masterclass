# Design Rules — masterclass website

## Palette (CSS :root variables — NEVER change without explicit request)
```
--cyan   #00f5ff   Home accent / global secondary
--mag    #ff00aa   Home gradient pair
--acid   #aaff00   Code page accent
--amber  #ff9500   Physics page accent
--purple #9b30ff   AI page accent
--fog    #8a9a8a   Dimmed labels
--b      #0a0a0a   Background primary
--b2     #0f0f14   Background secondary (cards, bands)
--w      #f0ece0   Warm white (body text)
--accent var(--cyan) by default; overridden per page via #page-X { --accent: var(--Xcolor) }
```
No yellow anywhere. Per-page accent: home=cyan, code=acid, physics=amber, ai=purple.

## Typography (Google Fonts — loaded in <head>)
```
--bb  'Bebas Neue'       Display / hero titles — condensed, all caps
--vt  'VT323'            Section labels, nav links, tags, stickers, footer — pixel monospace
--pm  'Permanent Marker' Hero subtitles, one-liner blocks — handwritten
--mo  'DM Mono'          All body text, descriptions, pricing, form elements
```

### Font usage rules
- Hero H1 (`hero-name`, `course-title`): Bebas Neue, `clamp(4rem,12vw,10rem)`
- Section labels (`section-label`): VT323, `.9rem`, `letter-spacing:.28em`, accent color
- Body text: Syne, `clamp(1rem,1.8vw,1.25rem)`, weight 300, `line-height:1.7`
- Pricing main (`price-main`): Bebas Neue, `clamp(1.6rem,3.5vw,2.8rem)`
- Module titles: Syne, `.85rem`, weight 600
- Module text: Syne, `.75rem`, weight 300, `line-height:1.4`
- Pills/tags: DM Mono, `.52rem`, `letter-spacing:.12em`, border-radius 20px

## Spacing system
- Page padding: `clamp(1.5rem,5vw,5rem)` horizontal
- Section vertical padding: `clamp(5rem,10vh,9rem)`
- Hero top padding: `clamp(6rem,12vh,9rem)` (to clear fixed nav)
- Card gaps: `1.2rem` (learn grid), `1.5rem` (paths grid), `3rem` (demo wrap)

## Breakpoints
```
< 800px   learn-grid, demo-wrap, sim-wrap → 1 col
< 720px   paths-grid → 1 col
< 700px   bio-grid, courses-grid, for-split → 1 col
< 600px   nav-center hidden (mobile nav)
< 500px   seasons-grid → 1 col
```

## Visual effects (do not remove)
- Grain overlay: SVG feTurbulence, `z-index:200`, `pointer-events:none`, opacity .65
- Custom cursor: 9px yellow dot + 34px ring. Hidden on `@media(pointer:coarse)`
- Scroll reveal: `.reveal` → `IntersectionObserver` → `.visible`. threshold 0.08
- Canvas: one per page, `position:absolute`, `z-index:0`. Lazy init on first page visit.

## Canvas color identity
- Home: cyan `0,245,255` — flow field particles
- Code: acid `170,255,0` — ASCII rain + particles
- Physics: amber `255,149,0` — circuit grid nodes
- AI: purple `155,48,255` — neural network nodes + edges

## Tone of copy
- Direct, honest, zero corporate speak
- No "passionate" / "innovative" / "best-in-class" filler
- First person singular ("I", not "we")
- Short punchy sentences for CTAs
- Slightly longer for explanatory copy but never academic
- Anti-patterns to avoid: "leverage", "synergy", "cutting-edge", "unlock your potential"

## Button hierarchy
1. `.btn-y` — primary (yellow bg, black text) — main CTA per page
2. `.path-cta-y` — secondary primary (yellow bg) — featured path-card CTA
3. `.path-cta-o` — secondary outlined (transparent bg, yellow border) — standard path-card CTA
4. `.email-copy-btn` — ghost (no border, no bg) — footer email

## Section label format
Always: `// Title` — forward slashes, DM Mono, yellow, `letter-spacing:.28em`
