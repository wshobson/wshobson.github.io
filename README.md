# sethhobson.com

Single-page personal site, served by GitHub Pages from this repo (`main`, root). Plain HTML/CSS — no build step.

## Maintenance contract

The profile README at [wshobson/wshobson](https://github.com/wshobson/wshobson) is the content source of truth. When it changes (new project, title or positioning change), update `index.html` here in the same sitting.

## Regenerating the OG image

Edit `og-source.html`, then:

    "/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless=new \
      --screenshot=og-image.png --window-size=1200,630 --hide-scrollbars \
      "file://$PWD/og-source.html"
