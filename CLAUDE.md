# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Personal academic blog for Joris Vankerschaver, built with **Quarto** and deployed to **GitHub Pages** at https://jvkersch.github.io/.

## Build Commands

```bash
# Install Python dependencies
uv sync

# Preview site locally (live reload)
quarto preview

# Render full site
quarto render
```

Deployment is automatic via GitHub Actions on push to `main` (see `.github/workflows/publish.yml`). Do not manually deploy.

## Architecture

- **Framework**: Quarto website project (`_quarto.yml`)
- **Theme**: Litera (Bootstrap-based)
- **Python**: 3.12, managed with `uv` (lockfile: `uv.lock`)
- **Execution**: Frozen (`freeze: true`) — Jupyter outputs are cached in `_freeze/` and committed. Posts with code aren't re-executed on every build.
- **Post-render**: `rsync -av static/. _site/` copies static assets into the build output.

## Content Structure

- **`posts/YYYY-MM-DD-slug/index.qmd`** — Blog posts (Quarto markdown). Each post is self-contained in its own directory with any images, bib files, etc.
- **`index.qmd`** — Home page
- **`static/`** — Files copied verbatim into `_site/`
- **`_freeze/`** — Cached Jupyter execution outputs (committed to repo)
- **`_site/`** — Generated HTML output (gitignored)

## Key Dependencies

Scientific Python stack: `numpy`, `scipy`, `matplotlib`, `mpmath`, `jupyter`, `tabulate`.
