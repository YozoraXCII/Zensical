# Contributing to the Kometa Wiki

Make focused documentation changes and open pull requests against this repository's
default branch. Application bugs and runtime changes belong in
[Kometa](https://github.com/Kometa-Team/Kometa).

Install the build dependencies and run the checks listed in the root README.
Author pages in `docs/` and maintain navigation in `zensical.toml`.
Navigation folders use Title Case; individual page labels use sentence case,
preserving product names and acronyms. Each page has one sidebar location, and
folder entries begin with their clickable `index.md`.

Reusable content belongs in `docs/templates/`. Use the existing `include` and
`include-markdown` directives; the local Markdown extension expands them directly
within Zensical. Keep local include sources inside `docs/`. When updating a
Defaults YAML example, refresh only its corresponding documentation snapshot from
the application repository.

Point links directly at final pages and headings. Internal moves do not need
redirect maps; external shortcuts such as Discord retain their redirects.
Use the root site URL, https://wiki.kometa.team/, without language or branch prefixes.

Do not add application code, runtime dependencies, Docker publishing, Read the Docs
configuration, MkDocs plugins, generated site output, caches, or local environments.
Preserve the include engine's license and provenance notices.
