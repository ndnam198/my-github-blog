# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A personal blog and portfolio built with **Hugo** using the **PaperMod** theme (vendored as a git submodule). Deploys to GitHub Pages via GitHub Actions. Requires **Hugo extended** (the theme uses Sass).

## Commands

```bash
# Dev server — MUST pass the dev config so baseURL is localhost (otherwise it
# uses the production GitHub Pages baseURL from hugo.toml and links break locally)
hugo server --config hugo.dev.toml
hugo server --config hugo.dev.toml -D   # include drafts (draft = true posts)

# Production build → ./public (gitignored)
hugo --minify

# New post (scaffolds from archetypes/posts.md, draft = false by default)
hugo new posts/my-new-post.md
```

There is no separate test/lint step — `hugo --minify` building cleanly is the check.

After cloning, the theme submodule must be initialized: `git submodule update --init --recursive`.

## Deploy

Pushing to **`develop`** (the main branch here) triggers `.github/workflows/hugo.yaml`, which builds and deploys to GitHub Pages. There is no separate `main`/release branch — `develop` is production.

## Architecture & conventions

- **Two config files, intentional.** `hugo.toml` (production baseURL) and `hugo.dev.toml` (localhost baseURL). Any config change — menu entries, params — must usually be made in **both**. `mainSections = ["posts"]` is what makes `content/posts/*` the blog feed; home outputs HTML + RSS + JSON (the JSON output powers PaperMod's client-side search at `/search/`).

- **Never edit `themes/PaperMod/`.** It is a submodule and updates will overwrite changes. Override instead via:
  - `layouts/` — partials (`layouts/partials/extend_head.html`, `extend_footer.html`), shortcodes (`layouts/shortcodes/rawhtml.html`), `404.html`, and render hooks (`layouts/_default/_markup/render-codeblock-mermaid.html` renders ```` ```mermaid ```` blocks into `<div class="mermaid">`).
  - `assets/css/extended/custom.css` — PaperMod auto-includes any CSS here.
  - `static/` — copied verbatim to site root (`static/images/foo.png` → `/images/foo.png`).

- **Styling rule (important): use PaperMod CSS variables, never hardcoded colors.** The theme supports light + dark, and `defaultTheme = "light"`. Hardcoded colors (e.g. `#fff`, `rgba(255,255,255,...)`) are invisible or low-contrast in one mode. Use `var(--border)`, `var(--code-bg)`, `var(--entry)`, `var(--theme)` for surfaces/borders and `var(--primary)`, `var(--content)`, `var(--secondary)` for text. See `context.md` for the full rationale and the custom class set (`.summary-block`, `.hero-badges`, `.cta-block`, `.project-card`, etc.) used by the About/Projects/Contacts pages.

- **Content is TOML front matter (`+++`).** Posts live in `content/posts/`. Set `draft = false` to publish; use `tags` and `categories` arrays (these drive the `/tags/` and `/categories/` taxonomy pages). Markdown allows raw HTML (`markup.goldmark.renderer.unsafe = true`), so inline `<div class="...">` with the custom CSS classes is the styling pattern for the standalone pages.

- **Standalone pages** (`content/about.md`, `projects.md`, `contacts.md`, `archives.md`, `search.md`) are not posts; `search.md` uses `layout = "search"`.
