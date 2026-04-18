# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Static personal site for Evan Paul (somatic bodywork / sensory-safe spaces / geometry research), deployed to **evanpaul.us** via GitHub Pages (`CNAME` sets the custom domain). No build step, no package manager, no tests — just HTML, CSS, and a small inline `<script>` per page.

## Running locally

Serve the directory over HTTP (parallax `background-attachment: fixed` and relative paths behave oddly from `file://`):

```
python3 -m http.server 8000
# then open http://localhost:8000
```

Publishing: push to `main`. GitHub Pages serves the repo root.

## Architecture

### Page structure
Each top-level section is a directory with its own `index.html` so URLs stay clean (`/bodywork/`, `/spaces/`, `/teaching/`, `/research/`, `/about/`, `/contact/`). The site root is `index.html`. The `research/` directory is labeled **"Geometry"** in the nav — don't rename one without the other.

### No templating — duplicated chrome
Every page hand-copies the same `<head>` (Google Analytics `G-9NYZ0M7GKR`, Cormorant Garamond + Outfit from Google Fonts, `img/handlogo.png` favicon), the same `<nav>`, the same `<footer>`, and the same inline `<script>` that handles the hamburger toggle and the `data-theme` light/dark toggle (persisted to `localStorage` under key `theme`). **When you change nav links, the theme script, or analytics, update all seven HTML files.** Subpages use `../` paths; root `index.html` uses `./`.

### Styling
All pages share `css/styles.css` (~1380 lines). Design tokens live in `:root` as CSS custom properties, with dark mode overrides under `[data-theme="dark"]`. Typography is `--font-display` (Cormorant Garamond, serif) for headings and `--font-body` (Outfit, sans) for body.

### Parallax backgrounds
Hero sections use `.parallax-hero` plus a `.bg-*` utility class that sets `background-image` to a file in `img/` (e.g. `.bg-fur` → `img/fur.jpg`, `.bg-hands` → `img/handsbackground.jpg`). To add a new background, add a new `.bg-foo { background-image: url('../img/foo.jpg'); }` rule alongside the others in `styles.css` rather than inlining the URL in HTML.

### Dead file
`evanpaul-site.zip` at the repo root is an old archive — ignore it, don't edit it.
