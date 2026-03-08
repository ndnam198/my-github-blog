# PaperMod theme-aware styling: summary and reuse guide

## What was done

### Problem

- **Invisible borders in light theme:** Card-style blocks (Professional Summary, Education, Skills, project cards, contact cards, CTAs) used inline styles like `border: 1px solid rgba(255, 255, 255, 0.1)` and `background: rgba(255, 255, 255, 0.03)`. On a white background these are effectively invisible.
- **Contrast in light theme:** Text used fixed dark-theme colors (`#fff`, `#aaa`, `#ccc`, `#888`), which are hard to read on light backgrounds.

### Scope of changes

| Page / area | Changes |
|-------------|--------|
| **About** (`content/about.md`) | Hero: plain markdown + `.hero-badges`. Professional Summary: `##` + `.summary-block` (paragraph + list). Education, Skills, Languages, Interests: markdown headings and lists. CTA: `.cta-block` with `.cta-primary` / `.cta-secondary`. Removed gradients and fixed colors. |
| **Contacts** (`content/contacts.md`) | Intro as markdown. Each contact in `.contact-card`; bottom CTA uses `.cta-block`. Removed dark-only shadows and `#fff`-style colors; URL lines use `var(--secondary)` where needed. |
| **Projects** (`content/projects.md`) | Hero: `## My Projects` + paragraph. Each project in `.project-card` with `.category-badge`, `.tech-tag`, `.project-meta`, `.project-link`. All text and accents driven by CSS using theme vars. Bottom CTA: `.cta-block` + `.cta-primary` / `.cta-secondary`. |
| **Custom CSS** (`assets/css/extended/custom.css`) | Single theme-aware stylesheet using only PaperMod variables. No hardcoded colors. |

### Result

- Borders and block backgrounds are visible in **both** light and dark themes.
- Text contrast is correct in both themes because colors come from PaperMod’s CSS variables.

---

## Reusable solution for future work

### Rule: use PaperMod variables, not fixed colors

PaperMod defines theme variables in `themes/PaperMod/assets/css/core/theme-vars.css`:

- **Surfaces:** `--theme`, `--entry`, `--code-bg`
- **Borders:** `--border`
- **Text:** `--primary` (main text/headings), `--content` (body), `--secondary` (muted/meta)
- **Layout:** `--radius`, `--gap`, `--content-gap`

Light and dark themes set different values for these; using them keeps styling consistent and readable in both modes.

### Where to add custom styles

- **File:** `assets/css/extended/custom.css` (project root). Hugo bundles it with the theme’s CSS (PaperMod’s `head.html` concats `css/extended/*.css`).
- **Scoping:** Prefer selectors under `.post-content` so styles apply only to page content (e.g. `.post-content .summary-block`).

### Patterns to reuse

1. **Card / block with visible border (both themes)**  
   Use theme vars for border and background:
   ```css
   .post-content .your-block {
     border: 1px solid var(--border);
     background: var(--code-bg);
     border-radius: var(--radius);
     padding: 1rem;
   }
   ```

2. **Text that works in both themes**  
   Use semantic vars, not hex:
   - Headings: `color: var(--primary);`
   - Body: `color: var(--content);`
   - Muted/meta: `color: var(--secondary);`

3. **Badges / tags / pills**  
   Same idea: surface and border from theme, text from content/primary:
   ```css
   .post-content .your-badge {
     background: var(--code-bg);   /* or var(--entry) */
     border: 1px solid var(--border);
     color: var(--content);
     border-radius: 12px;
     padding: 0.2rem 0.6rem;
   }
   ```

4. **Primary/secondary buttons**  
   Reuse or mirror the CTA pattern:
   - Primary: `background: var(--primary); color: var(--theme);`
   - Secondary: `background: var(--entry); color: var(--primary); border: 1px solid var(--border);`

### What to avoid

- **In content (Markdown/HTML):** No `color: #fff`, `#888`, `#aaa`, or `rgba(255,255,255,…)` for borders/backgrounds. They only work in dark theme.
- **In custom CSS:** No hardcoded hex/rgba for surfaces, borders, or text. Use `var(--…)` only so both themes stay consistent.

### Quick reference: existing classes

| Class | Use |
|-------|-----|
| `.summary-block` | Highlighted block (e.g. Professional Summary) with border and background |
| `.hero-badges` | Centered row of pill-style badges (e.g. location, experience) |
| `.cta-block` | Call-to-action container; use with `.cta-primary` / `.cta-secondary` on links |
| `.contact-card` | Contact entry card (border + background) |
| `.project-card` | Project card; contains `.category-badge`, `.tech-tag`, `.project-meta`, `.project-link` |

New card-like sections elsewhere on the site should follow the same pattern: a wrapper class styled in `custom.css` with `var(--border)` and `var(--code-bg)` (or `var(--entry)`), and text via `var(--primary)` / `var(--content)` / `var(--secondary)`.
