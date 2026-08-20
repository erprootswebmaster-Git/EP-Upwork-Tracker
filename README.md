# Upwork Proposal Tracker

Live dashboard for Upwork proposal activity (account: DineshDurai N).
Static single-page site. No build step, no dependencies to install.

## Files

| File | Purpose |
|---|---|
| `index.html` | The entire dashboard. Self-contained HTML, CSS and JS. |
| `vercel.json` | Disables caching so a redeploy shows immediately. |
| `robots.txt` | Blocks search engine indexing. |

## One-time setup

1. Create a **public** GitHub repo, e.g. `upwork-tracker`.
2. Clone it with **GitHub Desktop** (stores your credentials on Windows).
3. Copy these three files into the cloned folder. Commit and push.
4. Go to vercel.com, **Add New > Project**, import the repo.
   - Framework preset: **Other**
   - Build command: leave empty
   - Output directory: leave empty
5. Deploy. You get a URL like `upwork-tracker.vercel.app`.

Every push to `main` redeploys automatically.

## Automatic refresh

A Cowork scheduled task runs Mondays and Thursdays at 11:00.
It reads the Upwork account through Chrome, rewrites the data inside
`index.html`, commits, and pushes. Vercel picks up the push and redeploys.

Only two things in `index.html` change on each run:

- the `SCRAPED` constant (the date stamp)
- the `D` array (the proposal rows)

Everything else - layout, styling, chart logic - stays untouched.

## Data notes

- `viewed` and `replied` use `1` (yes), `0` (no), `null` (unknown).
- Upwork removes the "Viewed by client" indicator once a job closes, so
  archived proposals are recorded as `null`, never as `0`. Treating them as
  "not viewed" would understate the real view rate.
- Three early entries are hand-logged from before automated scraping and are
  carried forward on every run.

## Privacy

`robots.txt` and a `noindex` meta tag keep this out of search results, but the
URL is still public. Anyone who has the link can read it. Do not treat it as
private.
