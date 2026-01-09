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

| Section | Path | URL |
|---------|------|-----|
| OpenGL/Graphics | `content/opengl/` | `/opengl/` |
| Molecular Biology | `content/molbio/` | `/molbio/` |
| Claude | `content/android-kotlin/` | `/android-kotlin/` |
| About | `content/about/` | `/about/` |

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
---
```

Images go in `static/images/` and are referenced as `/images/filename.jpg`. Twitter card images should be 1200x628 pixels.

## Theme

Uses [Hugo-Octopress](https://github.com/parsiya/Hugo-Octopress) theme as a git submodule. After cloning:

```bash
git submodule update --init --recursive
```

## Configuration

Main config in `hugo.toml`. Markdown rendering allows unsafe HTML (`markup.goldmark.renderer.unsafe = true`) for embedded content.
