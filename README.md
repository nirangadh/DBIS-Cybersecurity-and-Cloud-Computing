# DBIS-11 Cybersecurity and Cloud Computing: course site

Static site for GitHub Pages. No build step, no backend.

## Folder layout

| Folder | Contents |
|---|---|
| `index.html` | Course hub: links to every day's notes, games and slides |
| `notes/` | One Markdown note per session (`11-01.md` ...). GitHub Pages turns each into a web page (`11-01.html`) |
| `artifacts/dayN/` | One self-contained HTML game per file. Works online, offline, or from a USB stick |
| `slides/` | Session decks (PowerPoint). Student-safe: no test questions inside |
| `assets/img/` | Original flat vector illustrations (SVG) used in the notes, games and hub |
| `assets/css/style.scss` | Colours and fonts for the notes, on top of the Primer theme |
| `_config.yml` | GitHub Pages settings (Primer theme for the notes) |
| `LICENSE.md` | Licences: content CC BY-NC-SA 4.0, code MIT, plus third-party credits |


## Licence

Teaching content is licensed CC BY-NC-SA 4.0 and code is licensed MIT. See [LICENSE.md](LICENSE.md).

## Adding a new day

Copy the Day 1 pattern: add `notes/11-0N.md`, add `artifacts/dayN/`, add the decks to `slides/`, then replace that day's "Coming soon" block in `index.html` with links.
