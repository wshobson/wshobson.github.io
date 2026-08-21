# AGENTS.md

## Repository

`sethhobson.com` is a static personal and project site served from the root of `main` by GitHub Pages. It is plain HTML/CSS with no framework, package manager, build step, or test suite. `CNAME` maps the custom domain and `.nojekyll` disables Jekyll processing.

Keep changes small and native to this stack. Do not introduce tooling, dependencies, or generated-site abstractions unless explicitly requested.

## Local verification

Preview the site:

    python3 -m http.server 8000

Before committing:

- Run `git diff --check`.
- Parse every JSON-LD block as JSON and parse `sitemap.xml` as XML.
- Inspect `/`, `/projects/agents/`, `/projects/commands/`, `/projects/pensyve/`, and `/404.html` through the local server.
- Check that every internal link resolves.

After editing `og-source.html`, regenerate the social image:

    "/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless=new \
      --screenshot=og-image.png --window-size=1200,630 --hide-scrollbars \
      "file://$PWD/og-source.html"

Pushing `main` deploys immediately. Verify the Pages workflow completed for the exact pushed SHA, then verify the live custom domain before claiming deployment success. Test an unknown live path and confirm it returns the custom page with HTTP 404; Python's local static server does not reproduce that GitHub Pages behavior.

## Content contract

The profile README at [wshobson/wshobson](https://github.com/wshobson/wshobson) is the source of truth for Seth's profile, project selection, title, and positioning. Each project's canonical README is the source of truth for volatile project facts such as counts, supported environments, interfaces, and licensing. Verify those facts at the source before publishing updates here.

Keep duplicated content synchronized across:

- `index.html`: rendered page, meta description, Open Graph fields, and JSON-LD graph
- `llms.txt`: crawler-facing Markdown summary
- `og-source.html`: social-card title and subtitle; regenerate `og-image.png` after changes
- `projects/*/index.html`: durable project explanations, unique metadata, visible updated dates, and page-specific JSON-LD

When a canonical page changes meaningfully, update its visible `<time>`, JSON-LD `dateModified`, `llms.txt` facts, and `sitemap.xml` `<lastmod>` together. `sitemap.xml` must list every canonical, indexable HTML page and no retired or error URLs.

## Agent and AI discovery

- Keep important identity and project facts in visible semantic HTML. JSON-LD and `llms.txt` summarize that content; they must not introduce claims that the rendered pages do not support.
- Use one stable `@id` for each entity across the JSON-LD graph. Use `https://sethhobson.com/#person` for the person and `https://sethhobson.com/#website` for the site.
- Give every indexable page a unique title, meta description, canonical URL, primary heading, direct summary, internal links, and accurate structured data.
- Preserve reciprocal discovery: the homepage links to project pages, project pages link home and to related projects, and `llms.txt` links both the first-party overview and canonical source.
- Prefer durable first-hand explanations over keyword variations or AI-specific filler. Do not add claims, testimonials, statistics, FAQ markup, or schema solely to target search systems.
- `robots.txt` is the crawler-access policy. Do not change AI search or training bot access without an explicit policy decision.
- `AGENTS.md` is repository guidance for coding agents; it is not public search content or a ranking signal.

## Migration and analytics invariants

- The retired WordPress articles intentionally remain unavailable. Do not restore them, redirect them to unrelated pages, or add them to the sitemap. `404.html` must remain `noindex` and GitHub Pages must continue returning a real 404 status.
- Keep the GA4 and Ahrefs Web Analytics snippets on every visitor-facing HTML page, including `404.html`, using the same project IDs. Shared project IDs preserve measurement across canonical pages and visits arriving through retired backlinks. `og-source.html` is a render-only asset source and does not need analytics.
- Ahrefs Site Audit is intentionally configured to use only `https://sethhobson.com/sitemap.xml`, with crawl depth `0` and Backlinks disabled as a URL source. Backlink analysis belongs in Site Explorer. Do not start a replacement crawl until the intended commit is live.
- Keep the Ahrefs "Canonical URL has no incoming internal links" and indexable "Orphan page" checks enabled. The homepage and project pages form a reciprocal internal-link graph, so either issue now indicates a real regression.

## Structure and style

- All styling lives in `styles.css` and uses variables from `:root`. GitHub-dark is the default; light mode overrides via `prefers-color-scheme`. Do not hardcode theme colors.
- Preserve the terminal aesthetic and monospace typography. New sections use `.section-label`, an `h2` with an ID, and matching `aria-labelledby` on the section.
- Project cards use `.card`. Add shields.io star badges to GitHub-hosted projects, not external products.
- Project detail pages live at `projects/<slug>/index.html`, use root-relative asset links, include a breadcrumb navigation landmark, and link back to the homepage plus related projects.
