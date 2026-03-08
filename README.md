# Nam's Homepage (Hugo blog)

Personal blog and portfolio built with [Hugo](https://gohugo.io/) and the [PaperMod](https://github.com/adityatelange/hugo-PaperMod) theme. Deploys to GitHub Pages.

## Prerequisites

- **Hugo (extended)** — required for theme features (e.g. Sass). Install:
  - macOS: `brew install hugo`
  - Or: [Hugo releases](https://gohugo.io/installation/) (pick `hugo_extended_*`)

## Quick start

```bash
# Clone (include submodules for the theme)
git clone --recurse-submodules https://github.com/ndnam198/my-github-blog.git
cd my-github-blog

# If you already cloned without submodules
git submodule update --init --recursive

# Run the dev server (use dev config so baseURL is localhost)
hugo server --config hugo.dev.toml
```

Open **http://localhost:1313**. Without `--config hugo.dev.toml`, Hugo uses `hugo.toml` (production baseURL). Use `-D` to include draft posts: `hugo server --config hugo.dev.toml -D`.

## Build for production

```bash
# Output in ./public (gitignored)
hugo --minify
```

To test the production build locally:

```bash
hugo --minify && hugo server --disableLiveReload
```

## Deploy

Pushes to the **`develop`** branch trigger the GitHub Actions workflow (`.github/workflows/hugo.yaml`), which builds with Hugo and deploys to GitHub Pages. Configure the repo so Pages uses the “GitHub Actions” source.

## Project structure

| Path | Purpose |
|------|---------|
| `hugo.toml` | Production config (baseURL for GitHub Pages) |
| `hugo.dev.toml` | Dev config (localhost baseURL) |
| `content/` | All content: `_index.md`, `about.md`, `projects.md`, `contacts.md`, `posts/*.md` |
| `content/posts/` | Blog posts (front matter: title, date, draft, etc.) |
| `layouts/` | Overrides: `404.html`, `partials/extend_head.html`, `shortcodes/` |
| `static/` | Images, JSON, `.htaccess`, `_redirects` |
| `themes/PaperMod` | Theme (git submodule) |
| `archetypes/default.md` | Default front matter for new content |

## How to expand

### New blog post

```bash
hugo new posts/my-new-post.md
```

Edit `content/posts/my-new-post.md`: set `draft = false` when ready. Use `<!--more-->` for the “read more” break.

### New page (e.g. “Notes”)

1. Add `content/notes.md` (or `content/notes/_index.md` for a section).
2. Add a menu entry in `hugo.toml` and `hugo.dev.toml`:

```toml
[[menu.main]]
  name = "Notes"
  url = "/notes/"
  weight = 5
```

### Customize theme / layout

- **Partials:** Override PaperMod by adding or editing files under `layouts/partials/` (e.g. `extend_head.html` for extra CSS/JS). The site uses default PaperMod styling.
- **Shortcodes:** `layouts/shortcodes/` (e.g. `rawhtml.html`) for reusable bits in content.
- **404:** `layouts/404.html`.

Do not edit files inside `themes/PaperMod`; override in `layouts/` or `static/` so updates to the theme (e.g. `git submodule update`) don’t overwrite your changes.

### Update the theme

```bash
git submodule update --remote themes/PaperMod
git add themes/PaperMod
git commit -m "chore: update PaperMod theme"
```

### Add images

Put assets in `static/images/` and reference as `/images/yourfile.png`. An optional avatar on the home block can be set in config under `[params.homeInfoParams]` (see PaperMod docs).

### Environment-specific config

- **Dev:** Run with `hugo server --config hugo.dev.toml` so `baseURL` is set for localhost. Hugo does not auto-switch config by environment.
- **CI/production:** The workflow runs `hugo` without `--config`, so `hugo.toml` is used (GitHub Pages `baseURL`).

## Useful commands

| Command | Description |
|--------|-------------|
| `hugo server --config hugo.dev.toml` | Dev server (localhost baseURL) |
| `hugo server --config hugo.dev.toml -D` | Include draft posts |
| `hugo new posts/slug.md` | New post from archetype |
| `hugo --minify` | Production build |
| `hugo list drafts` | List draft content |

## License

Content and custom code: yours. PaperMod theme: see [hugo-PaperMod](https://github.com/adityatelange/hugo-PaperMod).
