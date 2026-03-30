---
name: create-blog-post
description: >-
  Creates Hugo markdown posts under content/posts/ using the Hugo CLI and
  archetypes, then fills TOML front matter (tags, categories, draft). Matches
  existing post structure and tone. Use when the user asks for a new blog post,
  a post from a topic (e.g. compare X and Y), or a post built from pasted
  content; or when adding content to this PaperMod Hugo site.
---

# Create blog post (Hugo / PaperMod)

## Goal

Add a new post under `content/posts/` using **`hugo new content`**, then edit front matter and body so it matches sibling posts.

## Create the file (required)

From the **repository root** (where `hugo.toml` lives):

```bash
hugo new content posts/<kebab-case-slug>.md
```

- **Slug:** derive from the title; lowercase, hyphens, no special characters.
- **Optional time:** pin the front matter `date` when you need a specific publish time (defaults to “now” in +07:00):

  ```bash
  hugo new content posts/<slug>.md --clock '2026-03-30T14:30:00+07:00'
  ```

- **Overwrite:** if you are redoing a bad file:

  ```bash
  hugo new content posts/<slug>.md --force
  ```

Hugo writes `date`, `draft`, `title` (from the slug), `tags`, and `categories` using `archetypes/posts.md`. Do **not** hand-create an empty `content/posts/*.md` for new posts; always start with `hugo new content` so dates and structure stay consistent.

## Before writing the body

1. Skim **one or two** existing posts in `content/posts/` (pick ones similar in topic) for sectioning, heading levels, and voice.
2. If `.cursor/rules/writing.mdc` applies, follow it for prose (banned words, tone, lists vs numbers).

## Front matter (after `hugo new`)

The archetype seeds **TOML** between `+++`. Adjust as needed:

- **title:** Replace the auto title from the slug with the real headline (many posts use a promise-style or "TIL:" prefix where it fits).
- **date:** Usually leave what Hugo wrote unless you used `--clock` or the user asked for a specific datetime. Timezone for this site is **`+07:00`** unless the user specifies otherwise.
- **draft:** Archetype uses `draft = false` for this repo; set `draft = true` only if the user explicitly wants a draft.
- **tags:** Lowercase; 3–6 items; specific to the post (stack, domain, technique). Reuse tags from sibling posts when they fit. Replace the empty `[]` from the archetype.
- **categories:** One primary category is typical. Prefer labels already used in this repo when accurate, for example: `Security`, `Tools`, `Windows`, `Backend`, `Testing`, `Cloud`, `Machine Learning`. Add a new category only when nothing fits.

## Body structure (match existing posts)

- Opening: 1–3 short paragraphs that state what the reader gets.
- Use `---` between major sections where other posts do.
- Headings: `##` / `###` with numbered section titles when it reads naturally (`### 1. ...`, `### 2. ...`).
- Code: fenced blocks with language tags; mermaid allowed if the topic benefits (see `how-digital-certificates-works.md`).
- Tables and lists: use when they clarify comparisons or steps.

## Two input modes

**Topic only** (e.g. "compare Flutter and React Native"):

- Research or reason from general knowledge; structure the article clearly.
- Enrich with sections the repo’s posts would use: context, comparison table or bullet tradeoffs, when to pick which, pitfalls, short wrap-up.

**Pasted content**:

- Treat the paste as source of truth; reorganize into the repo’s structure, fix headings and formatting, and fill gaps only where needed for clarity (note major additions if non-obvious).
- Do not invent facts beyond what the paste + reasonable framing allows.

## Done checklist

- [ ] File created with `hugo new content posts/<slug>.md` (optionally `--clock` / `--force`)
- [ ] Title, tags, and `categories` filled in; **`draft`** matches intent
- [ ] Structure aligned with nearby posts in `content/posts/`
