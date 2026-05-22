# SOCRATIC — agent notes

This repository is published as a **GitHub Pages** site built with [MkDocs](https://www.mkdocs.org/) (Material theme). Pushes to `master` run `.github/workflows/mkdocs.yml`, which builds the site and deploys it via GitHub Actions. In the repo settings, Pages **Source** must be **GitHub Actions** (not “Deploy from branch”).

## Layout

| Path | Role |
|------|------|
| `mkdocs.yml` | Site config, theme, and **navigation** |
| `docs/` | All site markdown (`docs_dir` for MkDocs) |
| `docs/index.md` | Home page (canonical) |
| `docs/how-to-debate/` | Symlink → `.pi/skills/how-to-debate/` (skill + references; do not duplicate) |
| `docs/<TOPIC>/` | Debate content for a topic |

Edit markdown under `docs/` (and skills under `.pi/`). Paths in `nav:` are relative to `docs/`.

## Keep `mkdocs.yml` in sync with the repo

MkDocs does **not** auto-discover pages for the sidebar. The `nav:` section in `mkdocs.yml` is the source of truth for what appears on the site and in what order.

Whenever you **add, rename, move, or remove** a markdown file under `docs/` that should appear on the site:

1. Update the corresponding entry under `nav:` in `mkdocs.yml`.
2. If you add a new top-level item under `docs/`, add a `nav:` entry for it.
3. Run `mkdocs build` locally to confirm the site builds without warnings.

Example — after adding `docs/ISRAEL/new-item.md`, extend nav:

```yaml
  - Israel:
    - Initial position: ISRAEL/initial-position.md
    - New item: ISRAEL/new-item.md
```

**GitHub Pages** must use **GitHub Actions** as the source (not “Deploy from branch” → `/docs`). Otherwise visitors see raw markdown with no Material theme or sidebar. The `Publish MkDocs site` workflow deploys the `site/` artifact.

The **How to debate** section points at `how-to-debate/` (symlink into `.pi/skills/how-to-debate/`). New reference docs there need `nav:` entries; do not copy those files elsewhere.

Never build `mkdocs` locally - it is only meant to be published upon code commit and sync.
