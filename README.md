# DBIS-11 Cybersecurity and Cloud Computing: course site

Static site for GitHub Pages. No build step, no backend.

## Folder layout

| Folder | Contents |
|---|---|
| `index.html` | Course hub: links to every day's notes, games and slides |
| `notes/` | One Markdown note per session (`11-01.md` ...). GitHub Pages turns each into a web page (`11-01.html`) |
| `artifacts/dayN/` | One self-contained HTML game per file. Works online, offline, or from a USB stick |
| `slides/` | Session decks (PowerPoint). Student-safe: no test questions inside |
| `_config.yml` | GitHub Pages settings (Primer theme for the notes) |

## Publish on GitHub Pages

1. Create a public repository, for example `dbis11-cyber-cloud`.
2. Upload everything in this folder **except** `lecturer-only/`.
3. Go to Settings, then Pages. Under "Build and deployment", choose "Deploy from a branch", branch `main`, folder `/ (root)`.
4. Wait about a minute. The site appears at `https://<your-username>.github.io/dbis11-cyber-cloud/`.

Do **not** add a `.nojekyll` file: GitHub Pages needs its normal Jekyll build to turn the Markdown notes into web pages.

## Keep tests private

The `lecturer-only/` folder holds the daily test questions and marking guides. It is listed under `exclude` in `_config.yml` as a safety net, but the safest rule is simple: never upload it to the public repository.

## Adding a new day

Copy the Day 1 pattern: add `notes/11-0N.md`, add `artifacts/dayN/`, add the decks to `slides/`, then replace that day's "Coming soon" block in `index.html` with links.
