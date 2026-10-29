# My Personal Movie Tracker

A small web page for managing my BookMyShow show watcher. It doesn't scrape anything itself. It's a control panel for the private watcher repo, [`HarshJha995/bms-tracker`](https://github.com/HarshJha995/bms-tracker), which runs the checks and sends the phone alerts.

## What it does

- **Watching:** lists every watch with its poster, theatres, languages, formats, dates and last check. Each one can be edited, paused, resumed or removed.
- **Add:** add a movie by name, BookMyShow share link or event code. Pick theatres and languages from dropdowns, and optionally set a release date or date range.
- **Account:** the scheduler on/off switch, spending limits and GitHub connection.
- **Progress:** every action shows live status while the workflow runs.

## How it works

```
this page ──GitHub API──▶ bms-tracker (private)
                              ├─ control workflow: add / edit / pause / remove / posters
                              └─ watcher workflow: checks BookMyShow ─▶ ntfy alert
```

The page reads `watches.json` and `state.json` from the watcher repo and starts the `control` workflow when you act. There is no server and no database.

## Setup

1. **Host it:** enable GitHub Pages for this repo (Settings → Pages → deploy from the `main` branch, root folder). The page is `index.html`.
2. **Create a token:** GitHub → Settings → Developer settings → Fine-grained personal access tokens. Limit it to the `bms-tracker` repo only, with these permissions:
   - Actions: Read and write
   - Contents: Read
3. **Connect:** open the page, go to Account, and enter the repo (`HarshJha995/bms-tracker`) and the token.
4. **Optional:** on iPhone, Share → Add to Home Screen to use it like an app.

## Security notes

- The token is saved only in your browser's local storage. It is sent only to `api.github.com`.
- Keep the token scoped to the one repo, and set an expiry. If you lose a device, revoke it in GitHub.
- Never commit a token or any API key to this repo. The Apify, ntfy, TMDB and cron keys all live in the watcher repo's secrets, not here.
- Because this repo is public, the page is public too. Anyone who finds it sees an empty form with no data until they enter their own token.

## Posters

Movie posters come from [TMDB](https://www.themoviedb.org/). This product uses the TMDB API but is not endorsed or certified by TMDB.

## Updating

Replace `index.html` with the latest version from `bms-tracker/ui/index.html` and commit. Pages redeploys in about a minute. Hard-refresh the page if your device cached the old one.
