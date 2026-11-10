# CLAUDE.md — Zhaoyang-Jia.github.io

Personal academic site for Zhaoyang Jia (PhD student, CSE, UC San Diego; Bafna Lab).
Audience: recruiters and hiring managers at Google and bio-ML companies, plus academic
collaborators. Its job: in ten seconds, say who he is and what he has built; make the
publications, code, and CV one click away.

Live at https://zhaoyang-jia.github.io/ (GitHub Pages, served from `main`, root).
Local working copy: `/Users/zhaoyangjia/Github_Repos/Personal_Website`.

## What is here

| Path          | Role                                                                 |
|---------------|----------------------------------------------------------------------|
| `index.html`  | The entire site: markup, CSS, inline SVG, and a ~20-line theme toggle. |
| `resume.pdf`  | Compiled resume from the Overleaf project. Every "Resume" link points here. |
| `photo.jpg`   | Hero banner photo (1600 px, sRGB, EXIF stripped). Source of the palette. |
| `omkar-fig1-light.png`, `omkar-fig1-dark.png` | OMKar paper Figure 1, recolored to the palette, one per theme (see below). |
| `README.md`   | Deploy notes for humans.                                             |
| `CLAUDE.md`   | This file.                                                           |

There is no build step, no package manager, no framework, no test suite. Keep it that way.
The only external request is Google Fonts (`Source Serif 4`, `IBM Plex Sans`).

## How to work on it

```bash
# preview (fonts need network; file:// also works)
python3 -m http.server 8000      # then open http://localhost:8000

# deploy = push to main; Pages rebuilds in ~1 minute
git add -A && git commit -m "..." && git push
```

Before pushing, check all four: light theme, dark theme (toggle in footer or OS setting),
390 px wide (no horizontal scroll), and that every `href` in the file resolves
(`grep -o 'href="[^"]*"' index.html | sort -u`).

## Page structure (top to bottom, same order in the file)

1. `header.top` — small nav: About, Publications, Research, Resume.
2. `section.hero` — name (h1), one-line role, `p.contact` (email, Resume), then `ul.social`:
   three inline-SVG icon links (Google Scholar, GitHub, LinkedIn). The icons are
   Simple Icons paths pasted inline; no icon font, no CDN. Then `figure.banner`: `photo.jpg`
   cropped by CSS to 5:2 (16:10 on phones) with `object-position: 50% 45%`.
3. `#about` — "About me" h2 and two paragraphs of prose (user-written; edit only on request).
4. `#publications` — `ul.pubs`; each `li` has `.title`, `.authors`, `.meta` with a
   `.role` tag (First author / Joint first author / Co-author), optional `.talk`.
5. `#research` — four themes as prose paragraphs, each with an `h3` and a `.meta` line.
   In the first two themes the figure comes directly after the `h3`, before the prose.
   The Robertsonian theme holds `figure.schematic`: an inline `<svg class="rt">`
   (viewBox 2560x810) redrawn from the user's schematic.png, colored only by tokens
   (`--fig-blue`, `--fig-grey`, `--fig-dark`, `--loss`). It scrolls horizontally below 40rem.
   The OMKar theme holds `figure.paperfig`: two transparent PNGs (`omkar-fig1-light.png`,
   `omkar-fig1-dark.png`), swapped by the same three theme selectors the tokens use.
   The third theme (miR-25, Rana Lab) holds another `figure.schematic` with `<svg class="mir">`,
   a two-row pathway diagram; it shares the `.schematic` CSS classes with the RT figure.
   The fourth theme (Wu Lab wet-lab work) is prose only, written from the resume's Wu Lab bullets.
6. `#experience` — three `ul.timeline` lists: Experience, Teaching and mentoring, Education.
7. `footer` — contact links, location, "Last updated", theme toggle button.

## Design rules (deliberate; do not "improve" them away)

- **Two typefaces only.** `--sans` (IBM Plex Sans) for h1, h2, nav, dates, `.meta`;
  `--serif` (Source Serif 4) for body and h3. Do not add a third family.
- **Colors come only from the tokens in `:root`,** and the tokens come from `photo.jpg`
  (salt-flat paper, sky-blue accent, haze grey for muted text, jacket slate for ink; dark mode
  inverts to dusk water and snow).
  Dark mode is defined twice on purpose:
  under `@media (prefers-color-scheme: dark)` guarded by `:root:not([data-theme="light"])`,
  and again under `:root[data-theme="dark"]`. Any new color needs all three definitions.
- **Single column, max-width `--measure` (56rem; widened from 44rem on 2026-10-28 to cut the side
  white space), left-aligned.** No cards, no box shadows,
  no gradients, no rounded panels. Rules appear only where they encode structure
  (between publications; the timeline date column).
- **Sentence case everywhere.** No all-caps labels, no eyebrow labels, no "01/02/03"
  numbering, no arrows appended to links.
- **Four visuals: the hero photo, the Robertsonian schematic, OMKar Figure 1, and the miR-25
  pathway.** No further
  images, no icons beyond the three profile links in `ul.social`, no animation. The schematic's "loss" color is
  the hat khaki from the photo, standing in for the red of the original figure. (The read pile-up SVG was removed on 2026-11-09; see below
  if it is wanted back.)
- **No JavaScript beyond the theme toggle.** No analytics, no external scripts.
- **Keep it one file.** If a change needs a second file (other than `resume.pdf`,
  `photo.jpg`, the two `omkar-fig1-*.png`, or `CNAME`), ask first.

## Content rules

- **Facts come from the resume**, which is maintained in Overleaf and is the source of truth.
  Every number on the page (60+ TB, 25x, "up to three whole genomes per minute") was checked
  against it. The Robertsonian figures (1 in 800, 224 HPRC and 9 clinical samples, 100% recall,
  98% precision) and the OMKar figures (144 of 154 karyotypes, 94%, five newly explained cases)
  were supplied directly by the user on 2026-11-09. The miR-25 theme's content comes from the
  paper's abstract and author-contribution statement (70,617 single-cell transcriptomes; Z.J.
  among three authors who "performed computational and data analyses") plus the resume's Rana
  Lab bullets; drafted by Claude on 2026-11-10, pending the user's review.
  Do not change a number, a claim, or an author list without the user confirming it.
- Authorship tags must stay exact: Robertsonian paper = first author (manuscript in
  preparation, preprint expected Nov 2026; ASHG 2026 **lightning talk**, not "flash talk");
  OMKar = **joint** first author, *Genome Research* 2025, poster at the American
  **Cytogenomics** Conference (not "Cytogenetics"), Norfolk, June 2024;
  miR-25 = co-author, *Nature Communications* 2026.
- No course projects on the page (removed 2026-11-09). If they come back, label them with
  course code and term and don't present them as research.
- **Not on the site, by decision:** phone number, GPAs. Email is fine.
- Prose, not bullet lists, in Research. Write for a reader who is an ML
  engineer, not a geneticist: spell out an acronym once, then use it; cut jargon that
  doesn't earn its place.
- When the resume changes, mirror the change here, then update the footer's
  "Last updated" line.

## Open items (as of 2026-11-09)

- The resume's `Personal Website` link should point at `https://zhaoyang-jia.github.io/`.

## OMKar Figure 1 bitmaps

Source: the user's own vector figure, `~/Downloads/OMKar_Figures_Revision/Fig1_second.pdf`
(July 2025 revision; the published Genome Research Figure 1, CC BY-NC 4.0, user is joint first
author). Pipeline, all on this Mac with no extra installs: Ghostscript 9.53 rasterizes the PDF to
PPM at 200 dpi (1909x824); a pure-Python script decomposes each of the ~4,800 distinct colors as
"key color at alpha over white", maps each key to a palette color (red/orange to `--loss`,
yellow query bar to hat khaki, blues and pinks to `--fig-blue`/sky, greens to `--accent`/`--muted`,
greys to `--fig-grey`, black to `--ink`) and writes RGBA PNGs with that alpha, so the page
background shows through. Re-run the script if the palette changes; the key-to-target table is the
only part to edit.

## The read pile-up SVG (removed 2026-11-09, kept here for restoration)

Until 2026-11-09 the About section ended in a `figure.figure` holding a static inline
`<svg class="pileup">`: ~50 `<rect class="rd f|r">` reads on eight rows plus one dashed
`<line class="jx">` at the junction, with a one-line figcaption and a draw-in animation under
`@media (prefers-reduced-motion: no-preference)`. Its markup, CSS, and the `--read-f`,
`--read-r`, `--jx` tokens are in git history (commit 817613c and earlier). The SVG itself
comes from the script below (deterministic seed); keep `viewBox`,
`preserveAspectRatio="none"`, and `aria-hidden="true"` if it is restored.

```python
# regenerate the pile-up; prints the <svg> block to stdout
import random
random.seed(20261026)
W, H, rows, row_h, bar_h, jx = 1000, 120, 8, 14, 7, 560
out = []
for r in range(rows):
    y, x = 6 + r * row_h, random.randint(-120, 10)
    while x < W:
        length, gap = random.randint(60, 220), random.randint(8, 40)
        if x < jx < x + length and random.random() < 0.55:   # CN loss: fewer reads span the junction
            x = jx + random.randint(6, 30); continue
        length = min(length, W + 100 - x)
        s = 'f' if random.random() < 0.5 else 'r'
        out.append(f'<rect class="rd {s}" x="{x}" y="{y}" width="{length}" height="{bar_h}" rx="3.5"/>')
        x += length + gap
print(f'<svg class="pileup" viewBox="0 0 {W} {H}" preserveAspectRatio="none" aria-hidden="true" focusable="false">')
print('\n'.join(out))
print(f'<line class="jx" x1="{jx}" y1="0" x2="{jx}" y2="{H}"/>\n</svg>')
```

## Git

- Remote: `git@github.com:Zhaoyang-Jia/Zhaoyang-Jia.github.io.git` (SSH).
- Commit directly to `main`; there is nothing to review and Pages deploys from it.
- Commit messages: one line, imperative, what changed on the page
  ("Add Scholar link", "Update Robertsonian paragraph for preprint").
- Never commit `resume.tex` or Overleaf files here; only the compiled `resume.pdf`.
