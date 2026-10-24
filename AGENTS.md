# Kometa Wiki — Agent Guide

This is a docs-only Zensical repository. The Kometa application lives at
https://github.com/Kometa-Team/Kometa. Production URL: https://wiki.kometa.team/.

- Read README.md and .github/CONTRIBUTING.md for setup and conventions.
- Edit docs/ and zensical.toml; do not edit generated site/ output.
- docs-extension/ is a Python Markdown extension, not a MkDocs plugin.
  Keep its LICENSE and NOTICE attribution.
- Local includes live in docs/templates/, including source-defaults YAML snapshots
  and shared homepage/sponsor content in project.md.
- Use Title Case for navigation folders and sentence case for individual pages,
  preserving proper names and acronyms.
- Target this repository's default branch for pull requests.
- Run python -m unittest discover -s tests -p "test_docs*.py",
  node tests/docs_sticky_tables.cjs, and python -m zensical build --clean.
- Keep requirements.txt limited to the docs build. Do not introduce application
  sources, Docker/release workflows, MkDocs, or Read the Docs configuration.
- GitHub Actions builds PRs and pushes; only the default branch deploys to Pages.
  The custom domain and DNS must be configured separately from repository files.
