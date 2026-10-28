# zhaoyang-jia.github.io

Single-file personal site. No build step, no dependencies beyond Google Fonts.

## Files

| File          | Purpose                                                        |
|---------------|----------------------------------------------------------------|
| `index.html`  | The whole site: markup, styles, and a 20-line theme toggle.    |
| `resume.pdf`  | Your compiled resume. The "CV" links point here. (Add it.)     |
| `photo.jpg`   | Optional portrait. Uncomment the `<img class="portrait">` block in `index.html` to show it. |

## Deploy

Live at `https://zhaoyang-jia.github.io/`, served by GitHub Pages from `main` (root).
Pushing to `main` redeploys automatically in about a minute.

## Still to do

- Add `resume.pdf` at the repo root; until then the CV links 404.
- Point the resume's `Personal Website` link at `https://zhaoyang-jia.github.io/`.

## Editing

Everything is in `index.html`, top to bottom in the same order as the page. Colors and fonts are
CSS variables in the `:root` block; the dark theme overrides them under `prefers-color-scheme`.
The read pile-up in the hero is a static inline SVG (no JavaScript); regenerate or hand-edit the
`<rect>` rows if you want a different pattern.

## Optional: custom domain

Add a `CNAME` file containing the domain (e.g. `zhaoyangjia.com`) and set the DNS records GitHub
lists under **Settings → Pages → Custom domain**.
