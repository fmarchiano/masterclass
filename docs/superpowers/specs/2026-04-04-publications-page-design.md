# Publications Page — Design Spec
Date: 2026-04-04

## Overview
Add a "Publications" page to the masterclass SPA, accessible via a new nav link placed between the AI & Automation link and the EN/FR/IT language switcher. The page lists Fabio Marchianò's 9 peer-reviewed papers in reverse chronological order, with year separators and highlighted first-author cards.

---

## Navigation change

- Add `<li>` to `.nav-center` between the AI link and `.lang-switcher`
- Element: `<a href="#" onclick="showPage('publications')" id="nav-publications" data-i18n="nav_pub">Publications</a>`
- `showPage('publications')` added to the existing routing function (no canvas init needed)

---

## Page element

```html
<div class="page" id="page-publications" style="--accent:var(--mag)">
```

No canvas. Static page, dark background inherited from `body`.

---

## Layout

- Centered column: `max-width: 860px`, `margin: 0 auto`, padded top for nav clearance (`padding-top: 7rem`)
- Section header: "PUBLICATIONS" — Bebas Neue, `clamp(3rem,6vw,5rem)`, `var(--accent)`
- Subtitle: "9 peer-reviewed papers · 2 first-author" — DM Mono, `0.72rem`, `var(--dim2)`, `data-i18n="pub_subtitle"`

---

## Year separators

Rendered as a flex row: `<hr>` left · year text center · `<hr>` right.

- Year text: Bebas Neue, `1.1rem`, `var(--accent)`, letter-spacing `.2em`
- HR lines: `1px solid rgba(255,0,170,.2)`, `flex:1`
- Years rendered (newest first): 2024, 2023, 2022, 2021, 2020

---

## Publication cards

### Card shell
```css
.pub-card {
  background: rgba(255,255,255,.03);
  border: 1px solid rgba(255,255,255,.07);
  border-radius: 4px;
  padding: 1.2rem 1.4rem;
  margin-bottom: 1rem;
  position: relative;
}
.pub-card.first-author {
  border-left: 3px solid var(--mag);
}
```

### Card contents (top to bottom)
1. **First-author badge** (`.pub-card.first-author` only)
   - `<span class="pub-badge" data-i18n="pub_first_author_badge">First Author</span>`
   - VT323, `0.75rem`, uppercase, background `var(--mag)`, color `var(--b)`, padding `2px 6px`, border-radius `2px`

2. **Title** — DM Mono, `0.92rem`, `var(--w)`, `font-weight: 400`, `margin-bottom: .4rem`

3. **Authors** — DM Mono, `0.7rem`, `rgba(240,236,224,.45)`, `margin-bottom: .35rem`

4. **Journal · Year** — Bebas Neue, `0.95rem`, `var(--accent)`, letter-spacing `.08em`

5. **DOI link** — DM Mono, `0.65rem`, `rgba(240,236,224,.35)`, hover `var(--accent)`
   - Format: `→ doi.org/10.xxxx/...`
   - `target="_blank" rel="noopener"`
   - `data-i18n="pub_doi_label"` for the arrow prefix

Cards have `.reveal` class.

---

## Publication data (chronological, newest first)

### 2024
| Field | Value |
|-------|-------|
| Title | Integrative study of skeletal muscle mitochondrial dysfunction in a murine pancreatic cancer-induced cachexia model |
| Journal | eLife |
| Authors | et al. (Marchianò F co-author) |
| DOI | https://doi.org/10.7554/eLife.93312.2 |
| First author | No |

### 2023
| Field | Value |
|-------|-------|
| Title | Reconstructing human Brown Fat developmental trajectory in vitro |
| Journal | Developmental Cell |
| Authors | et al. (Marchianò F co-author) |
| DOI | https://doi.org/10.1016/j.devcel.2023.08.001 |
| First author | No |

### 2022 — two papers under this separator

**Paper 1 (first author)**
| Field | Value |
|-------|-------|
| Title | The mitoXplorer 2.0 update: integrating and interpreting mitochondrial expression dynamics within a cellular context |
| Journal | Nucleic Acids Research |
| Authors | Marchianò F et al. |
| DOI | https://doi.org/10.1093/nar/gkac306 |
| First author | Yes |

**Paper 2**
| Field | Value |
|-------|-------|
| Title | Tension-driven multi-scale self-organisation in human iPSC-derived muscle fibers |
| Journal | eLife |
| Authors | et al. (Marchianò F co-author) |
| DOI | https://doi.org/10.7554/eLife.76649 |
| First author | No |

### 2021 — four papers under this separator

**Paper 1 (first author)**
| Field | Value |
|-------|-------|
| Title | AnnoMiner is a new web-tool to integrate epigenetics, transcription factor occupancy and transcriptomics data to predict transcriptional regulators |
| Journal | Scientific Reports |
| Authors | Marchianò F et al. |
| DOI | https://doi.org/10.1038/s41598-021-94805-1 |
| First author | Yes |

**Paper 2**
| Field | Value |
|-------|-------|
| Title | The Hippo pathway controls myofibril assembly and muscle fiber growth by regulating sarcomeric gene expression |
| Journal | eLife |
| Authors | et al. (Marchianò F co-author) |
| DOI | https://doi.org/10.7554/eLife.63726 |
| First author | No |

**Paper 3**
| Field | Value |
|-------|-------|
| Title | Prednisolone rescues Duchenne muscular dystrophy phenotypes in human pluripotent stem cell-derived skeletal muscle in vitro |
| Journal | PNAS |
| Authors | et al. (Marchianò F co-author) |
| DOI | https://doi.org/10.1073/pnas.2022960118 |
| First author | No |

**Paper 4**
| Field | Value |
|-------|-------|
| Title | Evolution of mechanisms controlling epithelial morphogenesis across animals: new insights from dissociation-reaggregation experiments in the sponge Oscarella lobularis |
| Journal | BMC Evolutionary Biology |
| Authors | et al. (Marchianò F co-author) |
| DOI | https://doi.org/10.1186/s12862-021-01866-x |
| First author | No |

### 2020

| Field | Value |
|-------|-------|
| Title | mitoXplorer, a visual data mining platform to systematically analyze and visualize mitochondrial expression dynamics and mutations |
| Journal | Nucleic Acids Research |
| Authors | Yin A et al. (Marchianò F co-author) |
| DOI | https://doi.org/10.1093/nar/gkz1128 |
| First author | No |

---

## i18n keys to add to `T.en`

| Key | EN value |
|-----|----------|
| `nav_pub` | `Publications` |
| `pub_heading` | `Publications` |
| `pub_subtitle` | `9 peer-reviewed papers · 2 first-author` |
| `pub_first_author_badge` | `First Author` |
| `pub_doi_label` | `→` |

FR and IT fall back to EN via existing `T[l][k]??T['en'][k]` pattern. Optional: `nav_pub` IT → `Pubblicazioni`.

---

## Notes
- PNAS DOI confirmed by user: `10.1073/pnas.2022960118`
- Co-author full author lists not provided — cards show `et al.` with a parenthetical note. If full lists are provided later, they can be added as a `data-authors` attribute and truncated with "show more".

---

## What does NOT change
- No separate CSS/JS files (single-file rule)
- No new CDN dependencies
- No canvas on this page
- Existing pages, routing, and i18n system untouched
