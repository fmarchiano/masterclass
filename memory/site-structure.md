# Site Structure — masterclass website

## Global elements

### Fixed nav
```
FM.SYS logo → showPage('home')
Home | Code & Art | Physics, Arduino & Domotics | AI & Automation
EN | FR | IT
```
Mobile (<600px): nav-center links hidden. Logo + lang switcher only.

### Toast notification
`#toast-copied` — appears on email copy click. "fabio.marchiano.phd@gmail.com ✓ Copied"

### Custom cursor
`#cur` (9px dot) + `#curR` (34px ring). Hidden on touch via `@media(pointer:coarse)`.

### Grain overlay
`body::before` — SVG feTurbulence, z-index:200.

---

## Page: Home (page-home)

| Section | Class | Key i18n | Notes |
|---------|-------|----------|-------|
| Hero | `.home-hero` | `hero_eyebrow`, `hero_tagline`, `cred_*` | Canvas: yellow particles. Persona buttons. |
| About | `.section` | `about_label`, `bio_text`, `fact*_title`, `fact*_text` | Two-col: bio text + photo + facts + polymath strip |
| In-person | `.inperson-section` | `inperson_label`, `s1_*`, `s2_*` | 2 cards: Europa + Asia |
| Masterclasses | `.courses-teaser` | `courses_label`, `card1_*`, `card2_*`, `card3_*` | 3-col grid → course pages |
| Footer | `footer` | — | LinkedIn, GitHub, Email copy |

Canvas ID: `canvas-home`

---

## Page: Code & Creative Art (page-code)

| Section | Class | Key i18n | Notes |
|---------|-------|----------|-------|
| Hero | `.course-hero` | `c1_title`, `c1_sub`, `course1_tag` | Canvas: cyan ASCII rain |
| Pills | `.pills-section` | — | Hardcoded tags (no i18n needed) |
| What you'll learn | `.learn-section` | `lc1_*` to `lc6_*` | 6 cards, 3-col grid |
| Simulator | `.sim-section` | `c_sim_title`, `c_sim_desc`, `sim_perk*` | pic/processing.gif |
| Materials | `.materials-band` | `mat_headline`, `mat_sub_code`, `mat1`–`mat6` | Dark band |
| Dual paths | `.paths-section` | `c_aud*`, `c_path*`, `cm1_*`, `cm2_*` | Foundation + Advanced |
| Is this for you | `.for-section` | `c_yes*`, `c_no*` | Yes/No lists |
| CTA | `.cta-section` | `cta1_title`, `cta_guarantee` | Cal.com /15min |
| Footer | `footer` | — | |

Canvas ID: `canvas-code` (lazy init on first visit)

Pricing cards:
- Foundation: `c1_pack_hs` — €50/CHF 60 · pack €220/CHF 250
- Advanced: `c2_pack_uni` — €80/CHF 95 · pack €350/CHF 400

---

## Page: Physics, Arduino & Domotics (page-physics)

| Section | Class | Key i18n | Notes |
|---------|-------|----------|-------|
| Hero | `.course-hero` | `c2_title`, `c2_sub`, `course2_tag` | Canvas: orange circuit grid |
| Pills | `.pills-section` | — | Hardcoded tags |
| What you'll learn | `.learn-section` | `lp1_*` to `lp6_*` | Incl. KNX & Domotics |
| Simulator | `.sim-section` | `p_sim_title`, `p_sim_desc`, `p_sim_perk*` | pic/arduino.gif |
| Materials | `.materials-band` | `mat_headline`, `mat_sub_phys`, `pmat1`–`pmat6` | Physics-specific list |
| Dual paths | `.paths-section` | `p_aud*`, `p_path*`, `pm1_*`, `pm2_*` | Foundation + Advanced |
| Is this for you | `.for-section` | `p_yes*`, `p_no*` | |
| CTA | `.cta-section` | `cta2_title`, `cta_guarantee` | |
| Footer | `footer` | — | |

Canvas ID: `canvas-physics` (lazy init on first visit)

Pricing cards:
- Foundation: `p1_pack_hs` — €50/CHF 60 · pack €220/CHF 250
- Advanced: `p2_pack_uni` — €80/CHF 95 · pack €350/CHF 400

---

## Page: AI & Automation (page-ai)

| Section | Class | Key i18n | Notes |
|---------|-------|----------|-------|
| Hero | `.course-hero` | `c3_title`, `c3_sub`, `course3_tag` | Canvas: green neural net |
| Pills | `.pills-section` | — | Hardcoded tags |
| What you'll work on | `.learn-section` | `la1_*` to `la6_*` | 6 cards |
| Who is this for | `.paths-section` | `ai_path1_*`, `ai_path2_*`, `am1_*`, `am2_*` | AI Literacy + Custom |
| Quote form | `#ai-form-section` | `ai_form_*`, `ai_budget_*` | mailto: emailer |
| Is this for you | `.for-section` | `a_yes*`, `a_no*` | |
| CTA | `.cta-section` | `cta3_title`, `cta3_sub` | |
| Footer | `footer` | — | |

Canvas ID: `canvas-ai` (lazy init on first visit)

Pricing:
- AI Literacy: €80/CHF 95 · pack €350/CHF 400 (`book_session` → /30min)
- Custom Integration: `ai_quote_price`, `ai_quote_sub` → "Tell me your project" → form scroll

---

## i18n key naming conventions

| Pattern | Used for |
|---------|---------|
| `c1_*` | Code page specific |
| `c2_*` | Physics page specific |
| `c3_*` | AI page specific |
| `lc*` | Learn cards — Code |
| `lp*` | Learn cards — Physics |
| `la*` | Learn cards — AI |
| `cm*` | Course modules — Code |
| `pm*` | Course modules — Physics |
| `am*` | Course modules — AI |
| `mat*` | Materials list — Code |
| `pmat*` | Materials list — Physics |
| `ai_*` | AI page copy |
| `sim_*` | Simulator section shared |
| `p_sim_*` | Simulator section — Physics |
| `c_sim_*` | Simulator section — Code |
| `pf_*` | Path features (shared bullet points) |

---

## Persona system

Two states: `hs` (High School) and `uni` (Uni/Pro).
- Buttons live on home hero
- On click: `setPersona(p)` → highlights matching `.path-card`, dims other
- Banner appears at top of each course page
- `clearPersona()` resets state
- Applied to pages: code, physics, ai

---

## Cal.com integration

Script in `<head>`: `app.cal.com/embed/embed.js`
Namespace: `fabio-marchiano`
Brand color: `#FFE600`
Layout: `month_view`

CTA buttons use `data-cal-link`, `data-cal-namespace`, `data-cal-config` attributes.
Never use `href="mailto:"` for main CTAs.

| Button | Slug | Used in |
|--------|------|---------|
| Free call | `/15min` | Hero CTAs, CTA sections |
| Book session | `/30min` | Pricing card CTAs |
