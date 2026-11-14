# K4os — Personal Website

Source for [k4os-1534.github.io](https://k4os-1534.github.io) — my blog on
penetration testing, CTF writeups, and security concepts.

## Stack

Static site built with [Jekyll](https://jekyllrb.com) and the Chirpy theme
(installed as a Ruby gem), deployed to GitHub Pages by GitHub Actions
(`.github/workflows/pages-deploy.yml`). No Node toolchain; all styling and
JavaScript come from the theme gem, with third-party libraries loaded from a
CDN.

## Working on the site

```shell
bundle install        # once
bash tools/run.sh     # dev server with live reload on 127.0.0.1:4000
```

Build for production and run the link/image checker:

```shell
bash tools/test.sh
```

Write a new post by copying `.post-template.md` into `_posts/` named
`YYYY-MM-DD-slug.md`. Images go under `assets/img/<post-slug>/`.

## Layout

- `_posts/` — blog posts
- `_tabs/` — fixed pages (About, Archives, Categories, Tags)
- `_config.yml` — site identity, navigation, and routing
- `_data/` — sidebar contact options and post share buttons
- `_includes/` — site-specific overrides of theme components
- `assets/` — images and favicons
