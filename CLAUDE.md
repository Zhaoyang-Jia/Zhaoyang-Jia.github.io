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
| `resume.pdf`  | Compiled resume from the Overleaf project. Every "CV" link points here. |
| `photo.jpg`   | Optional portrait (not present yet). See "Portrait" below.           |
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

1. `header.top` — small nav: About, Research, Publications, Projects, CV.
2. `section.hero` — name (h1), one-line role, `p.contact` (email, CV), then `ul.social`:
   three inline-SVG icon links (Google Scholar, GitHub, LinkedIn). The icons are
   Simple Icons paths pasted inline; no icon font, no CDN.
3. `#about` — "About me" h2, the three-sentence lede, then `figure.figure` containing the
   **read pile-up SVG** (see below).
4. `#research` — three themes as prose paragraphs, each with an `h3` and a `.meta` line.
5. `#publications` — `ul.pubs`; each `li` has `.title`, `.authors`, `.meta` with a
   `.role` tag (First author / Joint first author / Co-author), optional `.talk`.
6. `#projects` — `div.proj` entries: `h3` (linked to the repo), `.meta`, one paragraph.
7. `#experience` — three `ul.timeline` lists: Experience, Teaching and mentoring, Education.
8. `footer` — contact links, location, "Last updated", theme toggle button.

## Design rules (deliberate; do not "improve" them away)

- **Two typefaces only.** `--sans` (IBM Plex Sans) for h1, h2, nav, dates, `.meta`;
  `--serif` (Source Serif 4) for body and h3. Do not add a third family.
- **Colors come only from the tokens in `:root`.** Dark mode is defined twice on purpose:
  under `@media (prefers-color-scheme: dark)` guarded by `:root:not([data-theme="light"])`,
  and again under `:root[data-theme="dark"]`. Any new color needs all three definitions.
- **Single column, max-width `--measure` (56rem; widened from 44rem on 2026-10-28 to cut the side
  white space), left-aligned.** No cards, no box shadows,
  no gradients, no rounded panels. Rules appear only where they encode structure
  (between publications; the timeline date column).
- **Sentence case everywhere.** No all-caps labels, no eyebrow labels, no "01/02/03"
  numbering, no arrows appended to links.
- **The pile-up is the one visual.** Don't add hero images or decorative motion. The only
  icons are the three profile links in `ul.social` (added at the user's request, 2026-10-28).
  The only animation is the reads drawing in once on load, inside
  `@media (prefers-reduced-motion: no-preference)`. Keep that guard.
- **No JavaScript beyond the theme toggle.** No analytics, no external scripts.
- **Keep it one file.** If a change needs a second file (other than `resume.pdf`,
  `photo.jpg`, or `CNAME`), ask first.

## Content rules

- **Facts come from the resume**, which is maintained in Overleaf and is the source of truth.
  Every number on the page (60+ TB, 25x, 30% over LSTM baseline, 19–82% MSE, 408 samples,
  60,660 genes, 102 patients, "up to three whole genomes per minute") was checked against it.
  Do not change a number, a claim, or an author list without the user confirming it.
- Authorship tags must stay exact: Robertsonian paper = first author (manuscript in
  preparation, preprint expected Nov 2026; ASHG 2026 **lightning talk**, not "flash talk");
  OMKar = **joint** first author, *Genome Research* 2025, poster at the American
  **Cytogenomics** Conference (not "Cytogenetics"), Norfolk, June 2024;
  miR-25 = co-author, *Nature Communications* 2026.
- Course projects are labeled as such (course code and term in `.meta`). Don't present
  them as research.
- **Not on the site, by decision:** phone number, GPAs. Email is fine.
- Prose, not bullet lists, in Research and Projects. Write for a reader who is an ML
  engineer, not a geneticist: spell out an acronym once, then use it; cut jargon that
  doesn't earn its place.
- When the resume changes, mirror the change here, then update the footer's
  "Last updated" line.

## Open items (as of 2026-10-28)

- `resume.pdf` must be present at the repo root or the CV links 404.
- Portrait: optional. Drop `photo.jpg` (~400 px square) at the root and uncomment the
  `<img class="portrait">` block above the `h1`. CSS for it already exists.
- The resume's `Personal Website` link should point at `https://zhaoyang-jia.github.io/`.

## The read pile-up SVG

The hero figure is a static inline `<svg class="pileup">`: ~50 `<rect class="rd f|r">`
reads on eight rows plus one dashed `<line class="jx">` at the junction. Classes `f`/`r`
(forward/reverse strand) are colored by tokens `--read-f`/`--read-r`; the line by `--jx`.
It was generated by the script below (deterministic seed). Re-run and paste the output
over the existing `<svg>…</svg>` if the pattern needs to change; keep `viewBox`,
`preserveAspectRatio="none"`, and `aria-hidden="true"`.

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
