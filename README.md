# zhaoyang-jia.github.io

Single-file personal site. No build step, no dependencies beyond Google Fonts.

## Files

| File          | Purpose                                                        |
|---------------|----------------------------------------------------------------|
| `index.html`  | The whole site: markup, styles, and a 20-line theme toggle.    |
| `resume.pdf`  | Compiled resume from Overleaf. The "Resume" links point here.     |
| `photo.jpg`   | Hero banner photo, 1600 px wide, sRGB, EXIF stripped. The site's colors are sampled from it. |

## Deploy

Live at `https://zhaoyang-jia.github.io/`, served by GitHub Pages from `main` (root).
Pushing to `main` redeploys automatically in about a minute.

## Still to do

- Point the resume's `Personal Website` link at `https://zhaoyang-jia.github.io/`.

## Editing

Everything is in `index.html`, top to bottom in the same order as the page. Colors and fonts are
CSS variables in the `:root` block; the dark theme overrides them under `prefers-color-scheme`.
The hero photo is `photo.jpg`; crop and position are set in the `.banner img` rule.

## Optional: custom domain

Add a `CNAME` file containing the domain (e.g. `zhaoyangjia.com`) and set the DNS records GitHub
lists under **Settings → Pages → Custom domain**.
