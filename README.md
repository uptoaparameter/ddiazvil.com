# David Díaz-Villarejo — academic website

A single-page static academic site. The design follows the minimal template at
[mvazcar.com](https://github.com/mvazcar/mvazcar.com) — a centred name, a photo on the
left, and content on the right — with a blue accent (`#0B4DA2`).

The key difference from that template: **all content lives in one markdown file,
[`content.md`](content.md)**. `index.html` loads that file in the browser and renders
it (the first heading becomes the centred name, the first image becomes the sidebar
photo, the rest becomes the main content). To update the site you only edit
`content.md` — no build step, no HTML.

## Edit the site

1. Open [`content.md`](content.md) and change the text. The cheat-sheet at the top of
   that file explains the (tiny) bit of markdown you need.
2. Replace the photo: drop your picture in `assets/` (e.g. `assets/photo.jpg`) and
   update the first line of `content.md` to `![David Díaz-Villarejo](assets/photo.jpg)`.
   A placeholder (`assets/photo.svg`) is shipped so nothing looks broken meanwhile.
3. The CV PDF lives at `assets/ddiavil_cv.pdf` (the bio links to it).
4. Add paper PDFs in `assets/papers/` and lecture slides in `assets/slides/`, then
   link them from `content.md`.

## Colour

The blue accent is `#0B4DA2`, set once in the `<style>` block of `index.html` via the
`--link` variable (with `--link-hover` for the hover state). Change those to recolour
the links across the whole site.

## Preview locally

Because the page loads `content.md` with `fetch()`, you must serve it over HTTP —
opening `index.html` directly from disk (`file://`) will not work. From this folder:

```bash
python -m http.server 8000
```

then open <http://localhost:8000>.

## Deploy on Netlify

This is a plain static site with no build step (`netlify.toml` is already configured).

- **Drag-and-drop:** zip this folder (or drag the folder) onto
  <https://app.netlify.com/drop>.
- **Git-based (recommended):** push this folder to a GitHub repo, then in Netlify
  choose *Add new site → Import from Git* and select it. Leave the build command empty
  and the publish directory as `.`. After that, every push to the repo redeploys the
  site automatically — so updating your website is just editing `content.md` and
  pushing.

## Files

```
index.html        page shell + styling (self-contained); loads and renders content.md
content.md        <-- the only file you normally edit
assets/
  photo.jpg       profile photo (shown in the left sidebar)
  marked.min.js   bundled markdown parser (no external/CDN dependency)
  photo.svg       placeholder profile photo (unused fallback)
  papers/         put paper PDFs here
netlify.toml      Netlify config (static, no build)
```
