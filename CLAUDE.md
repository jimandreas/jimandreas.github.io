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

Pushes to `master` branch automatically trigger GitHub Actions deployment via `.github/workflows/hugo.yml`. The workflow uses Hugo 0.153.5 extended.

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
