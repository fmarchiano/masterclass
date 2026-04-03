# CLAUDE.md — Masterclass Website Project

## What this project is
Single-file SPA website for Fabio Marchianò's 1:1 teaching masterclasses.
Live at: https://fmarchiano.github.io/masterclass/
Single source of truth: `index.html` (~136KB, all CSS + JS inline, zero build tools)

## Owner
- Name: Fabio Marchianò
- Email: fabio.marchiano.phd@gmail.com
- GitHub: fmarchiano
- LinkedIn: linkedin.com/in/fabiomarchiano/
- Cal.com: cal.com/fabio-marchiano (slugs: /15min, /30min)

---

## Three masterclasses

| # | Title | Nav ID | Target |
|---|-------|--------|--------|
| 01 | Code & Creative Art | `page-code` | High school / Uni students |
| 02 | Physics, Arduino & Domotics | `page-physics` | High school / Uni students |
| 03 | AI & Automation | `page-ai` | Freelancers, nomads, small business |

---

## Absolute rules — NEVER break these

1. **Single file** — everything stays in `index.html`. No separate CSS, JS or HTML files.
2. **Zero frameworks** — vanilla JS only. No React, Vue, jQuery, Tailwind.
3. **Google Fonts is the only CDN** — Bebas Neue + VT323 + Permanent Marker + DM Mono.
4. **Palette**: `--cyan:#00f5ff` · `--mag:#ff00aa` · `--acid:#aaff00` · `--amber:#ff9500` · `--purple:#9b30ff` · `--b:#0a0a0a` · `--w:#f0ece0`. No yellow. Per-page `--accent` scoped on each `#page-X` div (home=cyan, code=acid, physics=amber, ai=purple).
5. **i18n always** — every new visible string needs a key in `T.en`. FR/IT fall back to EN via `T[l][k]??T['en'][k]`.
6. **data-i18n on every text element** — never hardcode visible copy directly in HTML.
7. **Canvas guards** — always wrap `createRadialGradient` with `if(!isFinite(x))` checks.
8. **Routing** — new pages must be added to `showPage()` and get a `<div class="page" id="page-X">`.
9. **No lorem ipsum** — all copy must come from `memory/content-bank.md`.
10. **Cal.com buttons** — use `<button data-cal-link="...">` never `<a href="mailto:">` for CTAs.

---

## Architecture quick reference

```
SPA routing:     showPage(id)  — toggles .active on .page divs
i18n:            setLang(l)    — iterates [data-i18n], uses T[l][k]??T['en'][k]
Persona system:  setPersona(p) — highlights matching path-card, dims other
Canvases:        lazy-init on first showPage() call for each page
Scroll reveal:   IntersectionObserver on .reveal, threshold 0.08
Custom cursor:   hidden on touch devices via @media(pointer:coarse)
```

## Key CSS classes

```
.home-hero          Full-height hero (home)
.course-hero        Full-height hero (course pages) — flex-start
.pills-section      Tag strip below hero
.learn-section      What you'll learn grid
.sim-section        Simulator / GIF section
.materials-band     "Every session. Every material." band
.paths-section      Dual path-card grid
.ai-form            Quote form (AI page only)
.path-card.featured Yellow top border = highlighted card
.price-row          EUR/CHF price line
.price-pack         Pack offer line below price
```

## Pricing (always keep in sync)

| Track | Single | Pack ×5 |
|-------|--------|---------|
| Foundation | €50 / CHF 60 | €220 / CHF 250 — save €30/50 |
| Advanced | €80 / CHF 95 | €350 / CHF 400 — save €50/75 |
| AI Sessions | €80 / CHF 95 | €350 / CHF 400 — save €50/75 |
| AI Custom | Quote-based | N/A |

## Files that must exist alongside index.html

```
pic/about.jpg        Profile photo (About section)
pic/processing.gif   Creative coding simulator (Code page)
pic/arduino.gif      Arduino simulator (Physics page)
```

---

## Memory files (read before editing)

- `memory/design-rules.md` — visual rules, font sizes, spacing, tone
- `memory/content-bank.md` — bio, USPs, copy blocks in EN/FR/IT
- `memory/site-structure.md` — full section map with i18n keys

## Commands (run with /command-name)

- `/deploy` — git add, commit, push to GitHub
- `/new-section` — scaffold a new section into a page
- `/translate` — sync FR/IT keys to match EN
- `/update-prices` — update all price occurrences consistently
