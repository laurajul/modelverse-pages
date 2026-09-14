# CivitAI Adapter Pedigree — static site

A self-contained WebGL visualization of ~350k CivitAI adapters (LoRAs,
checkpoints, …), each plotted as a dot and grouped into base-model
clusters. `public/index.html` is a single-file app (all JS/CSS inline);
`public/data/` is the real dataset it loads, `public/data_test/` a small
sample used by the in-page "Use test data" toggle.

## Deploy

1. Push this repo to GitHub.
2. In the repo's **Settings → Pages**, set **Source** to **GitHub Actions**
   (one-time, only needed the first time — the workflow can't set this
   itself).
3. Push to `main` (or run the workflow manually from the **Actions**
   tab) — `.github/workflows/deploy.yml` publishes `public/` as-is, no
   build step.

## Updating the data

This repo only holds the *output* of the visualization pipeline —
`public/index.html` plus the `meta.json` + `.bin` files it fetches at
load time (see the `FILES` list and the two `fetch(DATA + …)` calls near
the top of `index.html` for the exact set: nothing else is read at
runtime). To publish a new layout or a refreshed dataset, regenerate
those same files from the pipeline's own repo and copy them over
`public/data/` (and `public/data_test/` for the sample), replacing them
wholesale — then commit and push.

## Local preview

Any static file server works, e.g. from this repo's root:

```sh
python3 -m http.server 8000 --directory public
```

then open `http://localhost:8000/`. Append `?test` to the URL (or use
the in-page toggle) to load the small sample dataset instead of the full
one.
