# BB Engineering Project Health Dashboard

Live, single-screen dashboard for permanent display at Forge 44 (Irlam), accessed via Amazon Silk browser on a Fire Stick and viewable by team laptops on the same URL.

Built from a build-ready specification by Claude Design. Powered by a small React runtime that loads from a CDN at runtime.

## Live URL

After GitHub Pages is enabled, the dashboard is live at:

```
https://<your-github-username>.github.io/<repo-name>/
```

## Files in this repo

- `index.html` — the dashboard itself
- `support.js` — the rendering runtime (loads React 18 from unpkg.com at runtime)
- `data.json` — companion data file (currently representative, for reference)
- `README.md` — this file

## Updating the data

The scheme data is currently embedded inside `index.html` in the `schemes()` function (around line 270). To update:

1. Open `index.html` in the GitHub repo, click the pencil icon to edit
2. Find the `schemes()` function and update the values
3. Commit the change
4. Within ~2 minutes, GitHub Pages redeploys and the dashboard shows fresh data

A future enhancement will move the scheme data into `data.json` and have the dashboard fetch it on refresh — that decouples data from code and makes weekly updates a single JSON file change.

## Fire Stick setup

1. On the Fire Stick, install **Silk Browser** from the Amazon Appstore
2. Open Silk, navigate to the live URL above
3. Open Silk's menu (three dots) → **Set as homepage**
4. On the Fire TV home: Settings → Display & Sounds → Screensaver → set "Start After" to its longest available value

## Hosting notes

- This repo is intentionally public to use the free GitHub Pages tier
- Data on the dashboard is currently **representative** (not real BB-ENG commercial figures)
- Before swapping in real values: consider whether a public-URL host is acceptable, or upgrade to a paid GitHub plan for private Pages, or revisit hosting

## Companion files (not in this repo)

- `BB-ENG_Dashboard_Data_Master.xlsx` — the engineering overlay master file
- `BB-ENG_Dashboard_Spec_v1.docx` — full build-ready specification

These live separately (likely on BB SharePoint) and feed into this dashboard via a Power Automate flow in a later phase.
