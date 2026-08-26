# Airdrop Tracker · live dashboard

Single-file static HTML dashboard that groups active airdrops by chain with
filtering and search. No build step, no npm install — just plain HTML+CSS+JS
served as static files.

## Local preview

```
python3 -m http.server -d . 8000
# then open http://127.0.0.1:8000
```

## How it's generated

```
python3 ~/airdrop-tracker/scripts/airdrop-tracker.py export --out ~/airdrop-tracker/site
```

The export reads `~/airdrop-tracker/data/airdrops.db` (SQLite, populated by
`drop refresh`) and writes:

- `index.html` — single self-contained page (CSS+JS inlined, JSON embedded)
- `airdrops.json` — raw data dump for any downstream tool

## Deploy to Vercel

1. Push this directory to a GitHub repo
2. On Vercel, "Import Project" → point to that repo
3. Framework preset: "Other" (no build step required)
4. Output directory: `./` (the index.html is at the root)

## Deploy to GitHub Pages

1. Push this directory to `<username>.github.io/<repo>` 
2. Enable Pages in repo settings → branch: `main`, root: `/`

## Update frequency

The script re-generates `index.html` from the latest SQLite data on every
`drop export` run. A cron job at 6-hour cadence is recommended; Vercel will
re-deploy on each push to GitHub.