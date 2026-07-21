# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Hugo static site for jimandreas.github.io - a personal blog covering OpenGL/graphics, molecular biology, and Android/Kotlin development.

## Build Commands

```bash
# Local development server
hugo server

# Include draft posts during development
hugo server -D

# Production build
hugo --gc --minify
```

## Deployment

Pushes to `master` branch automatically trigger GitHub Actions deployment via `.github/workflows/hugo.yml`. The workflow uses Hugo 0.153.5 extended. The `CNAME` file at the repo root points the published site at www.jimandreas.com.

`public/` is Hugo build output (gitignored) — never edit it directly. `archive/` holds the old pre-Hugo static site, kept for history; it is not part of the Hugo build.

## Content Structure

All content is organized under `content/docs/`:

| Section | Path | URL |
|---------|------|-----|
| OpenGL/Graphics | `content/docs/opengl/` | `/docs/opengl/` |
| Molecular Biology | `content/docs/molbio/` | `/docs/molbio/` |
| Claude | `content/docs/claude/` | `/docs/claude/` |
| Websites | `content/docs/websites/` | `/docs/websites/` |
| About | `content/docs/about/` | `/docs/about/` |

Each section has an `_index.md` that controls the section landing page. Old URLs (e.g., `/opengl/`, `/molbio/`) redirect via Hugo aliases in front matter.

## Adding Blog Posts

Create new `.md` files in the appropriate content folder. File naming convention: `YYYY-MM-DD-title.md`

Front matter format:

```yaml
---
title: "Post Title"
date: YYYY-MM-DD
draft: false
categories:
  - OpenGL
tags:
  - android
  - graphics
twitterImage: "/images/image-1200x628.jpg"
aliases:
  - /oldpath/post-slug/
---
```

Images go in `static/images/` and are referenced as `/images/filename.jpg`. Twitter card images should be 1200x628 pixels — omitting `twitterImage` falls back to a plain `summary` card instead of `summary_large_image`.

`README.newBlogEntry.md` is the user's step-by-step guide for new posts. Note the theme does not implement a `toc` front-matter field — table-of-contents settings in `hugo.toml` are currently unused by the layouts.

## AI-REF Markers

Draft posts may contain `AI-REF` markers — a protocol (documented fully in `README.newBlogEntry.md`) for the user to defer work to Claude Code while drafting:

- HTML comments carry the instruction: `<!-- AI-REF: Replace with citation + <url> -->`, `Insert image <path>`, `Expand <topic>`, `Verify <claim>`
- An inline `[AI-REF]` placeholder in the prose marks where a resolved citation belongs
- When asked to "fix up AI-REF markers": resolve each marker (fetch the URL, format the citation, insert the image, etc.), then remove the marker comments. Find them with `grep -r "AI-REF" content/`

## Theme

Custom theme at `themes/minimal/` with a single CSS file (`themes/minimal/static/css/style.css`) using CSS custom properties for theming. Dark mode is handled automatically via `@media (prefers-color-scheme: dark)` — no JS toggle.

All links render in the same tab by design (`themes/minimal/layouts/_default/_markup/render-link.html` overrides Hugo's default behavior).

Navigation menu items are defined in `config/_default/menus.toml`. The GitHub link in the header is driven by `params.github` in `config/_default/params.toml`, not a menu entry. Adding a new section to the nav requires both a new `[[main]]` entry in `menus.toml` and a corresponding `_index.md` in the content directory.

## Configuration

Split configuration in `config/_default/`:
- `hugo.toml` - Core Hugo settings; `mainSections = ["docs"]` controls what appears on the home page
- `menus.toml` - Navigation menu order and URLs
- `params.toml` - Site description, author, GitHub URL, and Twitter card handles (`twitterCardSite`, `twitterCreator`)

Markdown rendering allows unsafe HTML (`markup.goldmark.renderer.unsafe = true`) for embedded content (iframes, raw HTML blocks).

Code syntax highlighting uses the Dracula theme (`markup.highlight.style = "dracula"`).
