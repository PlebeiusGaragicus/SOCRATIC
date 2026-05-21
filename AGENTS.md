# SOCRATIC — agent notes

This repository is published as a **GitHub Pages** site built with [MkDocs](https://www.mkdocs.org/) (Material theme). Pushes to `master` run `.github/workflows/mkdocs.yml`, which builds the site and deploys it via GitHub Actions. In the repo settings, Pages **Source** must be **GitHub Actions** (not “Deploy from branch”).

## Layout

| Path | Role |
|------|------|
| `README.md` | Symlink → `docs/README.md` (GitHub repo overview) |
| `docs/` | All site markdown (`docs_dir` for MkDocs) |
| `docs/README.md` | Home page |
| `docs/ISRAEL/` | Debate content for a topic |
| `docs/how-to-debate/` | Symlink → `.pi/skills/how-to-debate/` (skill + references; do not duplicate) |
| `mkdocs.yml` | Site config, theme, and **navigation** |
| `requirements.txt` | Python deps for local builds and CI |
| `site/` | Build output (gitignored; CI uploads this to Pages) |

Edit markdown under `docs/` (and skills under `.pi/`). Paths in `nav:` are relative to `docs/`.

## Keep `mkdocs.yml` in sync with the repo

MkDocs does **not** auto-discover pages for the sidebar. The `nav:` section in `mkdocs.yml` is the source of truth for what appears on the site and in what order.

Whenever you **add, rename, move, or remove** a markdown file under `docs/` that should appear on the site:

1. Update the corresponding entry under `nav:` in `mkdocs.yml`.
2. If you add a new top-level item under `docs/`, add a `nav:` entry for it.
3. Run `mkdocs build` locally to confirm the site builds without warnings.

Example — after adding `docs/ISRAEL/new-section.md`, extend nav:

```yaml
  - Israel:
    - Initial prompt: ISRAEL/initial-prompt.md
    - New section: ISRAEL/new-section.md
```

The **How to debate** section points at `how-to-debate/` (symlink into `.pi/skills/how-to-debate/`). New reference docs there need `nav:` entries; do not copy those files elsewhere.

## Local preview

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
mkdocs serve
```

## What not to edit for the site

- `site/` — generated; never commit
- `.pi/` — agent/skill source; exposed on the site only via `docs/how-to-debate/`
