# maraket.github.io

Personal portfolio / resume site for **Marcus Gilmore-Lim**, Senior Software
Engineer. Deployed via GitHub Pages as a user site
(`https://maraket.github.io`).

> **Note:** This repository currently contains only the **compiled static
> output** of a Gatsby build (HTML, JS/CSS bundles, page-data JSON, images).
> No application source (`src/`, `gatsby-config`, `package.json`, etc.) is
> tracked here — every commit in history has only ever added build
> artifacts. See [`plans/01-project-scaffolding.md`](plans/01-project-scaffolding.md)
> for a proposed source layout if/when the source is reintroduced into this
> repo (or documented as living elsewhere).

## What this site is

- A single-page portfolio/resume: site metadata describes Marcus as a
  Senior Software Engineer with 10 years of experience across Java, Python,
  C#, cloud architecture, and DevOps.
- Built with **Gatsby 5.14.5** (React + TypeScript, based on the
  `component---src-*-tsx` chunk names in the build output).
- Uses **Partytown** (`~partytown/`) to run third-party scripts off the
  main thread.
- Two pages are built: `index.html` (resume/portfolio) and `404.html`
  (custom not-found page).

## Repository layout (current — build output only)

```
.
├── index.html                  # Built resume/portfolio page
├── 404.html, 404/               # Built 404 page
├── page-data/                   # Gatsby page-data JSON (per-page + app-level)
├── static/                      # Hashed static assets (profile photos, etc.)
├── _gatsby/slices/               # Gatsby "slice" partial HTML
├── ~partytown/                  # Partytown web-worker runtime files
├── *.js / *.css                 # Hashed webpack bundles (app, commons, styles)
├── chunk-map.json, webpack.stats.json, webpack-runtime-*.js
└── CLAUDE.md                    # Working conventions for AI-assisted changes
```

## Deployment

This is a GitHub Pages **user site** repository
(`Maraket/maraket.github.io`), so GitHub Pages serves the contents of this
repo's root directly at `https://maraket.github.io` — there is no separate
build step in this repo; whatever static files are committed here are what
gets served.

## Working in this repo

Because only build output is tracked, there is currently no way to rebuild
or modify the site from within this repository. See
[`plans/01-project-scaffolding.md`](plans/01-project-scaffolding.md) for a
proposed scaffold to reintroduce buildable source.

See [`CLAUDE.md`](CLAUDE.md) for commit, documentation, and review
conventions used when making changes here.
