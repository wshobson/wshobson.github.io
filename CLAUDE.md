# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Single-page personal site for sethhobson.com, served by GitHub Pages from `main` (root). Plain HTML/CSS — no build step, no framework, no package manager, no tests. Pushing to `main` deploys. `CNAME` maps the custom domain; `.nojekyll` disables Jekyll processing.

## Commands

Preview locally (any static server works):

    python3 -m http.server 8000

Regenerate the OG image after editing `og-source.html`:

    "/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless=new \
      --screenshot=og-image.png --window-size=1200,630 --hide-scrollbars \
      "file://$PWD/og-source.html"

## Content contract

The profile README at [wshobson/wshobson](https://github.com/wshobson/wshobson) is the content source of truth. When it changes (new project, title or positioning change), update `index.html` here in the same sitting.

The same bio/projects/experience content is duplicated in three places that must stay in sync when it changes:

- `index.html` — the page itself, plus its `<meta>` description, OG tags, and JSON-LD `@graph` in `<head>`
- `llms.txt` — plain-markdown summary for LLM crawlers
- `og-source.html` — title/subtitle on the social card (regenerate `og-image.png` after editing)

## Structure and style

- All styling lives in `styles.css`, driven by CSS variables in `:root`. Dark theme (GitHub-dark palette) is the default; light theme overrides via `@media (prefers-color-scheme: light)`. Use the variables, not hardcoded colors.
- The design is a terminal aesthetic: monospace font throughout, section labels rendered as shell commands (`~ $ whoami`, `ls projects/`) via the `.section-label` class. New sections should follow the same pattern: `<p class="section-label">…</p>` + `<h2 id="…">` + `aria-labelledby` on the `<section>`.
- Project cards in the grid use `.card` with an optional shields.io star badge; GitHub-hosted projects get one, external products (e.g. Capital Companion) don't.
