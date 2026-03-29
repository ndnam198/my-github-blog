---
name: create-blog-post
description: >-
  Creates Hugo markdown posts under content/posts/ with TOML front matter,
  tags, categories, and draft = false. Follows existing post structure and
  tone. Use when the user asks for a new blog post, a post from a topic
  (e.g. compare X and Y), or a post built from pasted content; or when adding
  content to this PaperMod Hugo site.
---

# Create blog post (Hugo / PaperMod)

## Goal

Add a new file at `content/posts/<slug>.md` that matches how other posts in this repo are written.

## Before writing

1. Skim **one or two** existing posts in `content/posts/` (pick ones similar in topic) for sectioning, heading levels, and voice.
2. If `.cursor/rules/writing.mdc` applies, follow it for prose (banned words, tone, lists vs numbers).

## Front matter (required)

Use **TOML** between `+++` (not YAML `---`):

```toml
+++
date = 'YYYY-MM-DDTHH:MM:SS+07:00'
draft = false
title = 'Title in Title Case or Sentence Style; Match Existing Posts'
tags = ["tag1", "tag2", "tag3"]
categories = ["OneCategory"]
+++
```

- **date**: Current datetime in `+07:00` unless the user specifies otherwise.
- **draft**: Set to `false` when the post is ready to publish. Use `draft = true` only if the user explicitly wants a draft.
- **title**: Clear; many posts use a promise-style or "TIL:" prefix where it fits.
- **tags**: Lowercase; 3–6 items; specific to the post (stack, domain, technique). Reuse tags from sibling posts when they fit.
- **categories**: One primary category is typical. Prefer labels already used in this repo when accurate, for example: `Security`, `Tools`, `Windows`, `Backend`, `Testing`, `Cloud`. Add a new category only when nothing fits.

## Filename (slug)

- `content/posts/<kebab-case-slug>.md`
- Derive the slug from the title: lowercase, hyphens, no special characters.

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

- [ ] File created under `content/posts/` with correct slug
- [ ] TOML front matter complete; **`draft = false`** unless user asked for a draft
- [ ] Tags and `categories` set and consistent with taxonomy
- [ ] Structure aligned with nearby posts in `content/posts/`
