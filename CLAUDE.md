# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Static personal and project site for sethhobson.com, served by GitHub Pages from `main` (root). The site uses plain HTML and CSS with no build step, framework, package manager, or tests. Pushing to `main` deploys. `CNAME` maps the custom domain, and `.nojekyll` disables Jekyll processing.

## Commands

Preview locally (any static server works):

    python3 -m http.server 8000

Regenerate the OG image after editing `og-source.html`:

    "/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless=new \
      --screenshot=og-image.png --window-size=1200,630 --hide-scrollbars \
      "file://$PWD/og-source.html"

## Content contract

The profile README at [wshobson/wshobson](https://github.com/wshobson/wshobson) is the source of truth for profile content and project selection. Canonical project READMEs are the source of truth for project-specific facts. Verify volatile counts and supported environments before publishing them here.

The same profile and project content is duplicated in several places that must stay in sync when it changes:

- `index.html` — the page itself, plus its `<meta>` description, OG tags, and JSON-LD `@graph` in `<head>`
- `llms.txt` — plain-markdown summary for LLM crawlers
- `og-source.html` — title/subtitle on the social card (regenerate `og-image.png` after editing)
- `projects/*/index.html` — durable project summaries with page-specific metadata and structured data
- `sitemap.xml` — every canonical, indexable page and no retired URLs

## Structure and style

- All styling lives in `styles.css`, driven by CSS variables in `:root`. Dark theme (GitHub-dark palette) is the default; light theme overrides via `@media (prefers-color-scheme: light)`. Use the variables, not hardcoded colors.
- The design is a terminal aesthetic: monospace font throughout, section labels rendered as shell commands (`~ $ whoami`, `ls projects/`) via the `.section-label` class. New sections should follow the same pattern: `<p class="section-label">…</p>` + `<h2 id="…">` + `aria-labelledby` on the `<section>`.
- Project cards in the grid use `.card` with an optional shields.io star badge; GitHub-hosted projects get one, external products (e.g. Capital Companion) don't.
- Project detail pages use root-relative assets, breadcrumb navigation, and reciprocal links to the homepage and related projects.
