# BB Engineering Project Health Dashboard

Live, single-screen dashboard for permanent display at Forge 44 (Irlam), accessed via Amazon Silk browser on a Fire Stick and viewable by team laptops on the same URL.

## Files in this repo

- `index.html` — the dashboard itself. **Don't edit this for routine updates.**
- `data.json` — the data the dashboard reads. **This is the file you update each week.**
- `support.js` — the rendering runtime (loads React from a CDN at runtime).
- `README.md` — this file.

## Architecture in one paragraph

On every page load, the dashboard fetches `data.json` and renders against it. The schemes, headline figures, ticker, and last-updated timestamp all come from `data.json`. The dashboard has an embedded copy of the data baked into `index.html` as a fallback — so even if `data.json` is missing, broken, or unreachable, the dashboard still displays something sensible. The fallback is also what shows for a fraction of a second before the JSON fetch completes.

## Updating the data each week

This is the weekly motion. You'll do this every Friday.

### What to update in `data.json`

The file structure mirrors what's on screen:

```json
{
  "updated_time": "14:00",
  "updated_date": "Fri 19 Jun 2026",
  "today": "2026-06-19",
  "ticker": "Short narrative line for the footer · separated by middle dots",
  "pipeline_gbp": 3310000,
  "pipeline_weighted_gbp": 1471000,
  "live_schemes": [
    {
      "code": "BB1674-1",
      "name": "Milne Graden Footbridge",
      "lead": "Michael Pach",
      "initials": "MP",
      "sector": "Footbridge",
      "start": "2026-01-15",
      "plannedEnd": "2026-09-30",
      "forecastEnd": "2026-10-15",
      "slice": 72000,
      "actualToDate": 46800,
      "supplierCommitted": 6000,
      "pct": 0.62,
      "rag": "Green",
      "schedVarDays": 15,
      "spendVarGbp": 1200
    },
    ...one block per live scheme...
  ]
}
```

The fields you'll typically change each week:

- `updated_time`, `updated_date`, `today` — bump to current
- `ticker` — fresh narrative line; up to three items separated by ` · `
- For each scheme: `actualToDate`, `supplierCommitted`, `pct`, `rag`, `forecastEnd`, `schedVarDays`, `spendVarGbp`

The fields that rarely change:

- `code`, `name`, `lead`, `initials`, `sector` — fixed per scheme
- `start`, `plannedEnd` — only if scope or programme is formally re-baselined
- `slice` — only if scope changes
- `pipeline_gbp`, `pipeline_weighted_gbp` — change when an opportunity is added, removed, or moves

### Field reference

| Field | What it is | Format / units |
|---|---|---|
| `updated_time` | Time of the last data refresh shown in header | "HH:MM" string |
| `updated_date` | Date of the last data refresh shown in header | "Dow DD Mmm YYYY" |
| `today` | The "today" line on the spend-vs-duration chart | ISO date "YYYY-MM-DD" |
| `ticker` | One-line narrative in the footer | String, ` · ` separators |
| `pipeline_gbp` | Total pipeline value, headline number | Integer £ |
| `pipeline_weighted_gbp` | Probability-weighted pipeline value | Integer £ |
| `code` | Project code shown on the ribbon card | Short string |
| `name` | Scheme name | String |
| `lead` | Lead engineer's full name | String |
| `initials` | Lead engineer's initials, shown in circle | 2 letters |
| `sector` | Categorisation | "Highway" \| "Footbridge" \| "Marine" \| "Refurb" \| "Inspection" \| "Rail" |
| `start` | Project start date | ISO date "YYYY-MM-DD" |
| `plannedEnd` | Planned end date | ISO date "YYYY-MM-DD" |
| `forecastEnd` | Current forecast end date | ISO date "YYYY-MM-DD" |
| `slice` | BB-ENG slice (£) — the engineering deliverable value | Integer £ |
| `actualToDate` | Cumulative internal actual spend to today (timesheets × rates) | Integer £ |
| `supplierCommitted` | Cumulative committed supplier costs (POs raised) absorbed in slice | Integer £ |
| `pct` | PM-assessed % complete | Decimal 0–1 (e.g. 0.65 for 65%) |
| `rag` | Status | "Green" \| "Amber" \| "Red" |
| `schedVarDays` | Schedule variance | Integer days (positive = late) |
| `spendVarGbp` | Spend variance vs plan | Integer £ (positive = over) |

### The actual update process

In a browser, sign into GitHub, open this repo, click `data.json`, click the pencil icon (Edit this file). Overtype the values you want to change. Scroll to the bottom, leave the default commit message or write something like "Week ending 19 Jun", and click **Commit changes**. Within about two minutes, GitHub Pages redeploys and the dashboard at Forge 44 shows the fresh data.

**Tip:** when editing JSON, watch out for trailing commas (don't leave one after the last item in a list) and matched quotes. GitHub's editor will highlight syntax errors as you go — if it shows red squiggles, fix them before committing. If you commit a broken `data.json`, the dashboard quietly falls back to the embedded data, so nothing visibly breaks — but check the page after committing to confirm your changes took.

## Fire Stick setup

Already done — see project notes.

## Companion files

- `BB-ENG_Dashboard_Data_Master.xlsx` — the engineering overlay master file
- `BB-ENG_Dashboard_Spec_v1.docx` — full build-ready specification

These live separately and feed `data.json` in a future automation phase.
