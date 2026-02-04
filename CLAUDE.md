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

Old URLs (e.g., `/opengl/`, `/molbio/`) redirect via Hugo aliases.

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

Images go in `static/images/` and are referenced as `/images/filename.jpg`. Twitter card images should be 1200x628 pixels.

## Theme

Uses custom minimal theme at `themes/minimal/` with:
- CSS dark/light mode via `@media (prefers-color-scheme: dark)`
- Responsive mobile navigation
- Twitter Card and Open Graph meta tags

## Configuration

Split configuration in `config/_default/`:
- `hugo.toml` - Core Hugo settings
- `menus.toml` - Navigation menu
- `params.toml` - Site parameters

Markdown rendering allows unsafe HTML (`markup.goldmark.renderer.unsafe = true`) for embedded content.
