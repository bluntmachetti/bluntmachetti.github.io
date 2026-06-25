# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Personal site + writing hub for Kehinde "Kenny" Ademolu, served at **bluntmachetti.github.io**. Plain Jekyll on GitHub Pages — no Node, no JS framework, no CSS build step. Content is hand-authored Markdown/HTML; all styling lives in one stylesheet.

## Commands

```bash
bundle install              # first-time setup
bundle exec jekyll serve    # local dev server with live reload (http://localhost:4000)
bundle exec jekyll build    # output to _site/
```

There is no test suite, linter, or CSS/JS pipeline. `Gemfile.lock` is intentionally not committed.

**Important — this sandbox has no Ruby/bundler/jekyll installed**, so the commands above cannot run here. When working in this environment, verify changes by: (1) source-level inspection/grep of `_layouts/*.html` and `assets/css/site.css`; then after pushing, (2) `gh run list --branch main` until `pages-build-deployment` is `completed/success`; then (3) `curl -fsSL "https://bluntmachetti.github.io/?cb=<sha>"` (the cache-bust query bypasses the Fastly CDN) and grep the raw HTML.

## Deployment (read before touching CI)

Pages source is **"Deploy from a branch"** (`build_type: legacy`, `main` / `/`). Pushing to `main` triggers GitHub's built-in `pages-build-deployment`, which builds Jekyll and publishes. The live site updates from `main` directly — committing to a feature branch does **not** deploy.

Because the built-in builder runs in safe mode, only GitHub-Pages-allowlisted plugins work (currently `jekyll-feed`, `jekyll-seo-tag` via the `github-pages` gem).

**Do NOT add a custom `.github/workflows/*.yml` Pages workflow while the source is "Deploy from a branch".** The custom workflow (`actions/deploy-pages`) and the built-in builder race for the same deployment lock and fail with `Deployment request failed ... due to in progress deployment` — pushes then silently never go live. (This exact bug previously froze the site for ~30 min.) If a custom Actions workflow is ever needed, first switch the repo's Pages source to "GitHub Actions" (`gh api -X PUT repos/bluntmachetti/bluntmachetti.github.io/pages -f build_type=workflow`) so the built-in builder is disabled — never run both.

## Architecture

**Layout inheritance** — everything funnels through one shell:
- `_layouts/default.html` — the chrome: sticky top nav, footer, SEO/feed meta, and the post reading-progress script. **The nav and footer live only here.** Nav = `Writing · Builds · About ↗` where **Builds links to the on-page anchor `/#builds`** (there is no separate builds page) and **About links externally to `github.com/bluntmachetti`** (there is no about page).
- `_layouts/home.html` (`layout: default`) — the homepage, a stack of hardcoded sections: hero → current focus → latest essay (pulls newest `category: writing` post) → **builds (`<section id="builds">`)** → connect.
- `_layouts/page.html` (`layout: default`) — generic titled page: `.page-head` + `.prose`. Used by `writing/index.md`.
- `_layouts/post.html` (`layout: default`) — the essay reader.

**Builds are hardcoded HTML** in the `#builds` section of `_layouts/home.html` (not data-driven). To add/change a project, edit that section. Card status uses `flag ok` (LIVE) / `flag warn` (ACTIVE) / bare `flag` (PRIVATE), and `build-card-dim` for private/placeholder cards.

**Essays** live in `_posts/`. They appear in lists only when `category: writing`. `writing/index.md` renders `site.posts | where: "category", "writing"`. Front-matter schema beyond the standard `title`/`date`/`description`:
- `summary` — used for card/excerpt text (falls back to `description`)
- `log` — sequence id shown as `LOG-001`
- `read` — e.g. `"6 min"`
- `flags` — list of `{text, kind}`; `kind` ∈ `ok` / `warn` / `crit`, mapping to colored `.flag` chips.

**Styling** is entirely in `assets/css/site.css`, a single file driven by CSS custom properties (design tokens in `:root`: color ramp, fonts, spacing). Dark "command-center" aesthetic, IBM Plex Mono (labels) + IBM Plex Sans (body), one accent (`--info`, cyan). Section anchors that the sticky nav scrolls to need `scroll-margin-top` (see `.builds-section`).

**Site-wide content** (nav/footer/connect links, author name, SEO) is driven by `_config.yml` — `site.links.{github,linkedin,x,redoubt}` and `site.author.name`. `future: true` is set so dated-today/future posts publish.

## Conventions

- Content uses British spelling ("organisation", "modelling", "behaviour").
- `_preview/` holds throwaway static HTML/PNG snapshots for visual review. It's underscore-prefixed so Jekyll never publishes it, and it can be **stale** — never treat it as source of truth.
