# 01 — Project Scaffolding

**Status:** Proposed — not yet built.

## Problem

`maraket.github.io` currently tracks only the compiled output of a Gatsby
build (HTML, hashed JS/CSS bundles, `page-data/`, `static/` assets,
`~partytown/` runtime files). No source has ever been committed to this
repository — `git log --diff-filter=A` on the full history shows only
build artifacts across every commit. This means:

- The site cannot be rebuilt or edited from this repo as-is.
- Any change (content, styling, dependency bump) requires either finding
  the original source elsewhere or reconstructing it from the build
  output.
- Evidence from the build output (component chunk names, meta tags)
  indicates the original source used:
  - **Gatsby 5.14.5**
  - **TypeScript** React components (`component---src-pages-index-tsx-*`,
    `component---src-pages-404-tsx-*`,
    `component---src-components-templates-resume-resume-tsx-*`)
  - **Partytown** for offloading third-party scripts
  - A `Resume` template component under
    `src/components/templates/resume/`

## Proposed scaffold

If reintroducing buildable source into this repo (recommended) or a
companion source repo:

```
.
├── gatsby-config.ts
├── gatsby-node.ts
├── package.json
├── tsconfig.json
├── .gitignore              # exclude public/, .cache/ (build output)
├── src/
│   ├── pages/
│   │   ├── index.tsx        # Resume/portfolio landing page
│   │   └── 404.tsx
│   ├── components/
│   │   └── templates/
│   │       └── resume/
│   │           └── resume.tsx
│   ├── images/               # Source images (e.g. profile photo)
│   └── styles/
└── docs/
    └── deployment.md          # How build output reaches this repo/Pages
```

## Deployment model decision needed

Two options for how source + build output coexist with GitHub Pages
serving from repo root:

1. **Two-branch model** — `main` (or `source`) holds application source;
   a `gh-pages`/`output` branch (or this repo, if GitHub Pages is
   reconfigured to serve from a `docs/` folder or a Pages-specific branch)
   holds only build output. Requires a CI workflow to build `main` and
   publish `public/` to the output branch.
2. **Single-branch model** — source and build output both live in `main`
   at repo root, with `public/` output copied to the tracked root files on
   each release. Simpler, but keeps generated files under source control
   review (noisy diffs).

**Recommendation:** option 1 (two-branch model with a CI publish step),
since GitHub Pages user sites (`<user>.github.io`) require the root of
`main` to be servable, and mixing generated build artifacts with
hand-written source in one branch makes diffs and reviews noisy.

## Next steps

- [ ] Confirm whether original source exists elsewhere (local machine,
      another repo, deleted branch) before reconstructing from scratch.
- [ ] Decide on the two-branch vs. single-branch deployment model above.
- [ ] Scaffold `package.json` / `gatsby-config.ts` per the layout above.
- [ ] Add a CI workflow (GitHub Actions) to build and publish output.
- [ ] Once source exists, fold this plan's "done" parts into
      `docs/deployment.md` and mark this entry complete.
