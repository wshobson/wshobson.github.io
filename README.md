# sethhobson.com

Static personal and project site, served by GitHub Pages from this repo (`main`, root). The site uses plain HTML and CSS with no build step.

## Maintenance contract

The profile README at [wshobson/wshobson](https://github.com/wshobson/wshobson) is the source of truth for profile content and project selection. Canonical project READMEs are the source of truth for project-specific facts. Keep `index.html`, `projects/*/index.html`, `llms.txt`, and `sitemap.xml` synchronized when those facts change.

## Regenerating the OG image

Edit `og-source.html`, then:

    "/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless=new \
      --screenshot=og-image.png --window-size=1200,630 --hide-scrollbars \
      "file://$PWD/og-source.html"
