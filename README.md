# zhaoyang-jia.github.io

Single-file personal site. No build step, no dependencies beyond Google Fonts.

## Files

| File          | Purpose                                                        |
|---------------|----------------------------------------------------------------|
| `index.html`  | The whole site: markup, styles, and a 20-line theme toggle.    |
| `resume.pdf`  | Your compiled resume. The "CV" links point here. (Add it.)     |
| `photo.jpg`   | Optional portrait. Uncomment the `<img class="portrait">` block in `index.html` to show it. |

## Deploy on GitHub Pages

1. Create a **public** repository named exactly `Zhaoyang-Jia.github.io`
   (the name must match your GitHub username; case-insensitive).
2. Put `index.html`, `resume.pdf`, and (optionally) `photo.jpg` at the repo root and push to `main`.
3. In the repo: **Settings → Pages → Build and deployment → Source: Deploy from a branch**,
   branch `main`, folder `/ (root)`. Save.
4. After a minute the site is live at `https://zhaoyang-jia.github.io/`.
   Put that URL in the resume's `Personal Website` link.

Pushing to `main` redeploys automatically.

## Things to fill in before publishing

- `Google Scholar` link in the hero: replace `https://scholar.google.com/` with your profile URL
  (or delete the link if you don't have a profile yet).
- `Last updated` line in the footer.
- The Bafna Lab link (`https://bafnalab.ucsd.edu/`): check it resolves, or point it at the
  lab's current page.

## Editing

Everything is in `index.html`, top to bottom in the same order as the page. Colors and fonts are
CSS variables in the `:root` block; the dark theme overrides them under `prefers-color-scheme`.
The read pile-up in the hero is a static inline SVG (no JavaScript); regenerate or hand-edit the
`<rect>` rows if you want a different pattern.

## Optional: custom domain

Add a `CNAME` file containing the domain (e.g. `zhaoyangjia.com`) and set the DNS records GitHub
lists under **Settings → Pages → Custom domain**.
