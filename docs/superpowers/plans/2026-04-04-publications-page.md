# Publications Page Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add a Publications page listing 9 peer-reviewed papers in reverse chronological order, accessible via a nav link between the AI & Automation link and the EN/FR/IT switcher.

**Architecture:** All changes are inside the single `index.html` file. CSS is added inline in the `<style>` block. The `showPage()` routing function already handles any page id generically — no JS changes needed. The new `#page-publications` div is inserted after the AI page div (line ~1799). i18n keys are added to `T.en`, `T.fr`, `T.it`.

**Tech Stack:** Vanilla HTML/CSS/JS. Fonts: Bebas Neue (headings), VT323 (badge), DM Mono (body). No build tools.

---

## File map

| File | Change |
|------|--------|
| `index.html` line ~525 | Add `#page-publications` accent CSS rule |
| `index.html` lines ~210–530 | Add `.pub-year-sep`, `.pub-card`, `.pub-badge`, `.pub-doi` CSS |
| `index.html` lines ~555–560 | Add `<li>` nav link for Publications |
| `index.html` line ~1025 | Add `nav_pub`, `pub_heading`, `pub_subtitle`, `pub_first_author_badge`, `pub_doi_label` to `T.en` |
| `index.html` line ~1151 | Add same keys to `T.fr` |
| `index.html` line ~1285 | Add same keys to `T.it` |
| `index.html` line ~1800 | Add full `#page-publications` HTML block after AI page closing `</div>` |

---

## Task 1: Add CSS

**Files:**
- Modify: `index.html` — inside the `<style>` block, after line 525 (`#page-ai{--accent:var(--purple);}`)

- [ ] **Step 1: Locate insertion point**

Find this line (around line 525):
```css
#page-ai{--accent:var(--purple);}
```

- [ ] **Step 2: Insert accent rule + pub CSS immediately after it**

Add the following block right after `#page-ai{--accent:var(--purple);}`:

```css
#page-publications{--accent:var(--mag);}
/* Publications page */
.pub-wrap{max-width:860px;margin:0 auto;padding:7rem clamp(1.5rem,5vw,3rem) 5rem;}
.pub-heading{font-family:var(--bb);font-size:clamp(3rem,6vw,5rem);color:var(--accent);line-height:1;margin-bottom:.4rem;}
.pub-subtitle{font-family:var(--mo);font-size:.72rem;letter-spacing:.15em;text-transform:uppercase;color:rgba(240,236,224,.4);margin-bottom:3rem;}
.pub-year-sep{display:flex;align-items:center;gap:1rem;margin:2.5rem 0 1.2rem;}
.pub-year-sep hr{flex:1;border:none;border-top:1px solid rgba(255,0,170,.2);}
.pub-year-label{font-family:var(--bb);font-size:1.1rem;letter-spacing:.2em;color:var(--accent);}
.pub-card{background:rgba(255,255,255,.03);border:1px solid rgba(255,255,255,.07);border-radius:4px;padding:1.2rem 1.4rem;margin-bottom:.9rem;position:relative;}
.pub-card.first-author{border-left:3px solid var(--mag);}
.pub-badge{font-family:var(--vt);font-size:.75rem;letter-spacing:.1em;text-transform:uppercase;background:var(--mag);color:var(--b);padding:2px 7px;border-radius:2px;display:inline-block;margin-bottom:.55rem;}
.pub-title{font-family:var(--mo);font-size:.92rem;color:var(--w);font-weight:400;margin-bottom:.35rem;line-height:1.45;}
.pub-authors{font-family:var(--mo);font-size:.7rem;color:rgba(240,236,224,.42);margin-bottom:.3rem;}
.pub-journal{font-family:var(--bb);font-size:.95rem;letter-spacing:.08em;color:var(--accent);margin-bottom:.35rem;}
.pub-doi a{font-family:var(--mo);font-size:.65rem;color:rgba(240,236,224,.32);text-decoration:none;transition:color .2s;}
.pub-doi a:hover{color:var(--accent);}
@media(max-width:600px){.pub-card{padding:.9rem 1rem;}.pub-title{font-size:.82rem;}}
```

- [ ] **Step 3: Verify**

Open `index.html` in a browser locally. Navigate to any page — confirm no visual regressions (the CSS rules above are namespaced to `.pub-*` and `#page-publications`, so they can't affect other pages).

- [ ] **Step 4: Commit**

```bash
cd "C:/Users/fabio/OneDrive/Documents/github/masterclass"
git add index.html
git commit -m "[pub] add CSS for publications page and cards"
```

---

## Task 2: Add nav link

**Files:**
- Modify: `index.html` lines 555–560 (the `<ul class="nav-center">` block)

- [ ] **Step 1: Locate the nav list closing tag**

Find this exact block (around line 559–560):
```html
    <li><a href="#" onclick="showPage('ai')" id="nav-ai" data-i18n="nav_ai">AI &amp; Automation</a></li>
  </ul>
```

- [ ] **Step 2: Add Publications nav item before `</ul>`**

Replace with:
```html
    <li><a href="#" onclick="showPage('ai')" id="nav-ai" data-i18n="nav_ai">AI &amp; Automation</a></li>
    <li><a href="#" onclick="showPage('publications')" id="nav-publications" data-i18n="nav_pub">Publications</a></li>
  </ul>
```

- [ ] **Step 3: Verify**

Reload browser. The nav should now show "Publications" between "AI & Automation" and the EN/FR/IT buttons. Clicking it will throw a JS error until Task 4 adds the page div — that's expected at this stage.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "[pub] add Publications nav link"
```

---

## Task 3: Add i18n keys

**Files:**
- Modify: `index.html` — three locations in the `const T = { ... }` block

### 3a — T.en (around line 1025)

- [ ] **Step 1: Locate**

Find this line in `T.en`:
```javascript
  nav_home:'Home',nav_code:'Code & Art',nav_physics:'Physics, Arduino & Domotics',
```

- [ ] **Step 2: Add `nav_pub` to the nav keys line**

Replace with:
```javascript
  nav_home:'Home',nav_code:'Code & Art',nav_physics:'Physics, Arduino & Domotics',nav_pub:'Publications',
```

- [ ] **Step 3: Find a suitable spot for the pub content keys**

Locate the end of `T.en` — find the closing `},` before `fr:{`. Add the following keys before that closing `},`. A good anchor is the last key in `T.en`. Search for `nav_ai:'AI & Automation'` in the `T.en` block and add after the line that contains it:

```javascript
  pub_heading:'Publications',pub_subtitle:'9 peer-reviewed papers · 2 first-author',pub_first_author_badge:'First Author',pub_doi_label:'→',
```

### 3b — T.fr (around line 1151)

- [ ] **Step 4: Locate**

Find this line in `T.fr`:
```javascript
  nav_home:'Accueil',nav_code:'Code & Art',nav_physics:'Physique, Arduino & Domotique',
```

- [ ] **Step 5: Add `nav_pub` to T.fr nav line**

Replace with:
```javascript
  nav_home:'Accueil',nav_code:'Code & Art',nav_physics:'Physique, Arduino & Domotique',nav_pub:'Publications',
```

- [ ] **Step 6: Add pub content keys to T.fr** (fallback to EN is fine, but add nav key)

Find the `nav_ai` key in T.fr and add on the same line or after:
```javascript
  pub_heading:'Publications',pub_subtitle:'9 articles révisés par des pairs · 2 premier auteur',pub_first_author_badge:'Premier auteur',pub_doi_label:'→',
```

### 3c — T.it (around line 1285)

- [ ] **Step 7: Locate**

Find this line in `T.it`:
```javascript
  nav_home:'Home',nav_code:'Codice & Arte',nav_physics:'Fisica, Arduino & Domotica',
```

- [ ] **Step 8: Add `nav_pub` to T.it nav line**

Replace with:
```javascript
  nav_home:'Home',nav_code:'Codice & Arte',nav_physics:'Fisica, Arduino & Domotica',nav_pub:'Pubblicazioni',
```

- [ ] **Step 9: Add pub content keys to T.it**

Find the `nav_ai` key in T.it and add:
```javascript
  pub_heading:'Pubblicazioni',pub_subtitle:'9 articoli peer-reviewed · 2 primo autore',pub_first_author_badge:'Primo autore',pub_doi_label:'→',
```

- [ ] **Step 10: Verify i18n**

Reload browser. Switch between EN / FR / IT — the "Publications" nav label should update. (The page itself isn't built yet, clicking still errors.)

- [ ] **Step 11: Commit**

```bash
git add index.html
git commit -m "[pub] add i18n keys for publications page (en/fr/it)"
```

---

## Task 4: Add publications page HTML

**Files:**
- Modify: `index.html` — insert after line 1799 (the `</div>` that closes `#page-ai`)

- [ ] **Step 1: Locate insertion point**

Find this exact text (around line 1799):
```html
  <footer><span class="footer-copy">© 2025 Fabio Marchianò</span><div class="footer-socials"><a href="https://www.linkedin.com/in/fabiomarchiano/" target="_blank" rel="noopener">LinkedIn</a><a href="https://github.com/fmarchiano" target="_blank" rel="noopener">GitHub</a><button class="email-copy-btn" onclick="copyEmail()">Email</button></div></footer>
</div>
```

- [ ] **Step 2: Insert the full publications page block immediately after the closing `</div>` of the AI page**

Add the following block:

```html

<!-- ══ PUBLICATIONS PAGE ══ -->
<div class="page" id="page-publications">
  <div class="pub-wrap">
    <h1 class="pub-heading" data-i18n="pub_heading">Publications</h1>
    <p class="pub-subtitle" data-i18n="pub_subtitle">9 peer-reviewed papers · 2 first-author</p>

    <!-- 2024 -->
    <div class="pub-year-sep"><hr><span class="pub-year-label">2024</span><hr></div>

    <div class="pub-card reveal">
      <p class="pub-title">Integrative study of skeletal muscle mitochondrial dysfunction in a murine pancreatic cancer-induced cachexia model</p>
      <p class="pub-authors">et al. (Marchianò F co-author)</p>
      <p class="pub-journal">eLife · 2024</p>
      <p class="pub-doi"><a href="https://doi.org/10.7554/eLife.93312.2" target="_blank" rel="noopener"><span data-i18n="pub_doi_label">→</span> doi.org/10.7554/eLife.93312.2</a></p>
    </div>

    <!-- 2023 -->
    <div class="pub-year-sep"><hr><span class="pub-year-label">2023</span><hr></div>

    <div class="pub-card reveal">
      <p class="pub-title">Reconstructing human Brown Fat developmental trajectory in vitro</p>
      <p class="pub-authors">et al. (Marchianò F co-author)</p>
      <p class="pub-journal">Developmental Cell · 2023</p>
      <p class="pub-doi"><a href="https://doi.org/10.1016/j.devcel.2023.08.001" target="_blank" rel="noopener"><span data-i18n="pub_doi_label">→</span> doi.org/10.1016/j.devcel.2023.08.001</a></p>
    </div>

    <!-- 2022 -->
    <div class="pub-year-sep"><hr><span class="pub-year-label">2022</span><hr></div>

    <div class="pub-card first-author reveal">
      <span class="pub-badge" data-i18n="pub_first_author_badge">First Author</span>
      <p class="pub-title">The mitoXplorer 2.0 update: integrating and interpreting mitochondrial expression dynamics within a cellular context</p>
      <p class="pub-authors">Marchianò F et al.</p>
      <p class="pub-journal">Nucleic Acids Research · 2022</p>
      <p class="pub-doi"><a href="https://doi.org/10.1093/nar/gkac306" target="_blank" rel="noopener"><span data-i18n="pub_doi_label">→</span> doi.org/10.1093/nar/gkac306</a></p>
    </div>

    <div class="pub-card reveal">
      <p class="pub-title">Tension-driven multi-scale self-organisation in human iPSC-derived muscle fibers</p>
      <p class="pub-authors">et al. (Marchianò F co-author)</p>
      <p class="pub-journal">eLife · 2022</p>
      <p class="pub-doi"><a href="https://doi.org/10.7554/eLife.76649" target="_blank" rel="noopener"><span data-i18n="pub_doi_label">→</span> doi.org/10.7554/eLife.76649</a></p>
    </div>

    <!-- 2021 -->
    <div class="pub-year-sep"><hr><span class="pub-year-label">2021</span><hr></div>

    <div class="pub-card first-author reveal">
      <span class="pub-badge" data-i18n="pub_first_author_badge">First Author</span>
      <p class="pub-title">AnnoMiner is a new web-tool to integrate epigenetics, transcription factor occupancy and transcriptomics data to predict transcriptional regulators</p>
      <p class="pub-authors">Marchianò F et al.</p>
      <p class="pub-journal">Scientific Reports · 2021</p>
      <p class="pub-doi"><a href="https://doi.org/10.1038/s41598-021-94805-1" target="_blank" rel="noopener"><span data-i18n="pub_doi_label">→</span> doi.org/10.1038/s41598-021-94805-1</a></p>
    </div>

    <div class="pub-card reveal">
      <p class="pub-title">The Hippo pathway controls myofibril assembly and muscle fiber growth by regulating sarcomeric gene expression</p>
      <p class="pub-authors">et al. (Marchianò F co-author)</p>
      <p class="pub-journal">eLife · 2021</p>
      <p class="pub-doi"><a href="https://doi.org/10.7554/eLife.63726" target="_blank" rel="noopener"><span data-i18n="pub_doi_label">→</span> doi.org/10.7554/eLife.63726</a></p>
    </div>

    <div class="pub-card reveal">
      <p class="pub-title">Prednisolone rescues Duchenne muscular dystrophy phenotypes in human pluripotent stem cell-derived skeletal muscle in vitro</p>
      <p class="pub-authors">et al. (Marchianò F co-author)</p>
      <p class="pub-journal">PNAS · 2021</p>
      <p class="pub-doi"><a href="https://doi.org/10.1073/pnas.2022960118" target="_blank" rel="noopener"><span data-i18n="pub_doi_label">→</span> doi.org/10.1073/pnas.2022960118</a></p>
    </div>

    <div class="pub-card reveal">
      <p class="pub-title">Evolution of mechanisms controlling epithelial morphogenesis across animals: new insights from dissociation-reaggregation experiments in the sponge Oscarella lobularis</p>
      <p class="pub-authors">et al. (Marchianò F co-author)</p>
      <p class="pub-journal">BMC Evolutionary Biology · 2021</p>
      <p class="pub-doi"><a href="https://doi.org/10.1186/s12862-021-01866-x" target="_blank" rel="noopener"><span data-i18n="pub_doi_label">→</span> doi.org/10.1186/s12862-021-01866-x</a></p>
    </div>

    <!-- 2020 -->
    <div class="pub-year-sep"><hr><span class="pub-year-label">2020</span><hr></div>

    <div class="pub-card reveal">
      <p class="pub-title">mitoXplorer, a visual data mining platform to systematically analyze and visualize mitochondrial expression dynamics and mutations</p>
      <p class="pub-authors">Yin A et al. (Marchianò F co-author)</p>
      <p class="pub-journal">Nucleic Acids Research · 2020</p>
      <p class="pub-doi"><a href="https://doi.org/10.1093/nar/gkz1128" target="_blank" rel="noopener"><span data-i18n="pub_doi_label">→</span> doi.org/10.1093/nar/gkz1128</a></p>
    </div>

    <a class="course-back" href="#" onclick="showPage('home')" data-i18n="back_home">Back to home</a>
  </div>
  <footer><span class="footer-copy">© 2025 Fabio Marchianò</span><div class="footer-socials"><a href="https://www.linkedin.com/in/fabiomarchiano/" target="_blank" rel="noopener">LinkedIn</a><a href="https://github.com/fmarchiano" target="_blank" rel="noopener">GitHub</a><button class="email-copy-btn" onclick="copyEmail()">Email</button></div></footer>
</div>
```

- [ ] **Step 3: Verify full page**

Reload browser. Click "Publications" in nav:
- Page renders with magenta accent
- "PUBLICATIONS" heading in magenta Bebas Neue
- Year separators visible (2024, 2023, 2022, 2021, 2020)
- Two cards have a magenta left border + "First Author" badge (mitoXplorer 2.0 and AnnoMiner)
- All 9 DOI links are clickable and open the correct papers
- "Back to home" link works
- EN/FR/IT switching updates "Publications"/"Publications"/"Pubblicazioni" in nav
- Scroll reveal animates cards on scroll

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "[pub] add Publications page with 9 papers, year separators and first-author highlights"
```

---

## Self-review

**Spec coverage:**
- ✅ Nav link next to language selector
- ✅ Magenta accent (only unused palette color)
- ✅ Horizontal cards with year separators (2024 → 2020)
- ✅ 2 first-author papers highlighted (left border + badge)
- ✅ Each card: title, journal, year, DOI hyperlink, authors
- ✅ i18n keys in EN/FR/IT
- ✅ `.reveal` scroll animation on all cards
- ✅ `showPage()` routing unchanged (works generically)
- ✅ `back_home` link reuses existing i18n key
- ✅ Footer reused from other pages
- ✅ Single-file rule respected

**Placeholder scan:** No TBDs, no "implement later", no vague steps — all code is complete.

**Type consistency:** `pub-card`, `pub-badge`, `pub-doi`, `pub-year-sep`, `pub-year-label`, `pub-wrap` — used consistently across CSS (Task 1) and HTML (Task 4). `first-author` class applied only to the 2 correct cards.
