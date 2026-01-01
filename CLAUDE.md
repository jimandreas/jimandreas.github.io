# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Hugo static site for jimandreas.github.io - a personal blog covering OpenGL/graphics, molecular biology, and Android/Kotlin development.

## Build Commands

```bash
# Local development server
hugo server

# Production build
hugo --gc --minify
```

## Deployment

Pushes to `main` branch automatically trigger GitHub Actions deployment via `.github/workflows/hugo.yml`. The workflow uses Hugo 0.153.5 extended.

## Content Structure

| Section | Path | URL |
|---------|------|-----|
| OpenGL/Graphics | `content/opengl/` | `/opengl/` |
| Molecular Biology | `content/molbio/` | `/molbio/` |
| Android/Kotlin | `content/android-kotlin/` | `/android-kotlin/` |
| Static pages | `content/page/` | `/page/` |

## Adding Blog Posts

Create new `.md` files in the appropriate content folder with front matter:

```yaml
---
title: "Post Title"
date: YYYY-MM-DD
draft: false
categories:
  - OpenGL
tags:
  - tag1
twitterImage: "/images/image.jpg"
---
```

Images go in `static/images/` and are referenced as `/images/filename.jpg`.

## Theme

Uses [Hugo-Octopress](https://github.com/parsiya/Hugo-Octopress) theme as a git submodule. After cloning, run:

```bash
git submodule update --init --recursive
```

## Configuration

Main config in `hugo.toml`. Key settings:
- Site URL: `https://jimandreas.github.io/`
- Pagination: 10 posts per page
- Syntax highlighting: solarized-dark
- Twitter cards enabled
