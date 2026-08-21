# AGENTS.md

## Repository

`sethhobson.com` is a single-page personal site served from the root of `main` by GitHub Pages. It is plain HTML/CSS with no framework, package manager, build step, or test suite. `CNAME` maps the custom domain and `.nojekyll` disables Jekyll processing.

Keep changes small and native to this stack. Do not introduce tooling, dependencies, or generated-site abstractions unless explicitly requested.

## Local verification

Preview the site:

    python3 -m http.server 8000

Before committing, run `git diff --check` and inspect both `/` and `/404.html` through the local server.

After editing `og-source.html`, regenerate the social image:

    "/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless=new \
      --screenshot=og-image.png --window-size=1200,630 --hide-scrollbars \
      "file://$PWD/og-source.html"

Pushing `main` deploys immediately. Verify the Pages workflow completed for the exact pushed SHA, then verify the live custom domain before claiming deployment success.

## Content contract

The profile README at [wshobson/wshobson](https://github.com/wshobson/wshobson) is the content source of truth. When its projects, title, or positioning changes, update this site in the same sitting.

Keep duplicated content synchronized across:

- `index.html`: rendered page, meta description, Open Graph fields, and JSON-LD graph
- `llms.txt`: crawler-facing Markdown summary
- `og-source.html`: social-card title and subtitle; regenerate `og-image.png` after changes

Update `sitemap.xml`'s `<lastmod>` when the homepage changes meaningfully. It must contain only the canonical, indexable homepage.

## Migration and analytics invariants

- The retired WordPress articles intentionally remain unavailable. Do not restore them, redirect them to unrelated pages, or add them to the sitemap. `404.html` must remain `noindex` and GitHub Pages must continue returning a real 404 status.
- Keep the GA4 and Ahrefs Web Analytics snippets in both `index.html` and `404.html`, using the same project IDs on each page. This preserves homepage measurement and visibility into visits arriving through retired backlinks.
- Ahrefs Site Audit is intentionally configured to use only `https://sethhobson.com/sitemap.xml`, with crawl depth `0` and Backlinks disabled as a URL source. Backlink analysis belongs in Site Explorer. Do not start a replacement crawl until the intended commit is live.
- The Ahrefs "Canonical URL has no incoming internal links" and indexable "Orphan page" issues are disabled for this project because the canonical homepage is the only indexable page.

## Structure and style

- All styling lives in `styles.css` and uses variables from `:root`. GitHub-dark is the default; light mode overrides via `prefers-color-scheme`. Do not hardcode theme colors.
- Preserve the terminal aesthetic and monospace typography. New sections use `.section-label`, an `h2` with an ID, and matching `aria-labelledby` on the section.
- Project cards use `.card`. Add shields.io star badges to GitHub-hosted projects, not external products.
