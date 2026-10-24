# Kometa Wiki

Documentation for [Kometa](https://github.com/Kometa-Team/Kometa), built with
[Zensical](https://zensical.org/) and published at **https://wiki.kometa.team/**.

This is a documentation-only repository. Kometa's application, runtime configuration,
Defaults distribution, and release tooling live in the application repository.

## Local development

Use Python 3.12 or newer, from the repository root:

```shell
python -m venv .venv
```

Activate the environment:

- Windows PowerShell: `.venv\Scripts\Activate.ps1`
- macOS/Linux: `source .venv/bin/activate`

```shell
python -m pip install -r requirements.txt
python -m zensical serve
```

Preview at http://127.0.0.1:8000. Build the static site with:

```shell
python -m zensical build --clean
```

Output is written to `site/`. Zensical reads `docs/` directly; no staging script
or generated configuration is required.

## Repository layout

| Path | Purpose |
| --- | --- |
| `zensical.toml` | Site configuration and navigation |
| `docs/` | Markdown pages, images, styles, scripts, and theme overrides |
| `docs/templates/` | Shared includes and documentation examples, excluded from publication |
| `docs-extension/` | Repository-owned Markdown include extension for Zensical |
| `requirements.txt` | Pinned build dependencies |
| `tests/` | Documentation and UI regression checks |
| `.github/workflows/docs.yml` | Build, validate, and deploy to GitHub Pages |

The include extension preserves Kometa's include syntax without depending on MkDocs.
Its attribution and license are retained in `docs-extension/NOTICE` and
`docs-extension/LICENSE`. Only the Defaults YAML files used by documentation
examples are kept, under `docs/templates/source-defaults/`; they are snapshots,
not a distribution of Kometa Defaults. The example configuration template is kept
at `docs/templates/config.yml.template`. Shared homepage and sponsor content lives
in `docs/templates/project.md`.

## Checks

```shell
python -m unittest discover -s tests -p "test_docs*.py"
node tests/docs_sticky_tables.cjs
python -m zensical build --clean
```

Node.js 22 or newer is used for the client-side checks. The installation questionnaire
check runs from the Python test suite when Node is available.

## GitHub Pages setup

1. Push this repository to GitHub. The workflow builds pushes and pull requests,
   and deploys only the repository's default branch.
2. In **Settings > Pages > Build and deployment**, choose **GitHub Actions**.
3. Set **Custom domain** to `wiki.kometa.team`.
4. At your DNS provider, create a CNAME record for `wiki.kometa.team` pointing to
   `<owner>.github.io` (for Kometa-Team, `kometa-team.github.io`), without a
   repository path. Enable **Enforce HTTPS** once GitHub provisions the certificate.

Custom domains for an Actions deployment are configured in repository settings;
a CNAME file alone does not configure Pages. See
[GitHub's custom-domain instructions](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site).

The canonical site URL is already configured as `https://wiki.kometa.team/`.
There is one documentation site, without Read the Docs language/version prefixes.
The header's GitHub link intentionally points to the Kometa application repository.

Builds fetch existing remote includes from related Kometa repositories, so network
access is required. Application release notes are loaded from Kometa's stable branch;
this repository does not maintain application release history.

See [CONTRIBUTING.md](.github/CONTRIBUTING.md) for authoring conventions.
