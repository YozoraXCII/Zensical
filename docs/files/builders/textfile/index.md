# Text and File Lists

You can find items using IDs written directly in YAML or maintained in a local or remote text file.

No external service configuration is required for this Builder.

| Builder                     | Description                                                                                 |             Works with Movies              |             Works with Shows             |    Works with Playlists and Custom Sort    |
|:----------------------------|:--------------------------------------------------------------------------------------------|:------------------------------------------:|:----------------------------------------:|:------------------------------------------:|
| [`text`](#text)           | Reads supported IDs and URLs directly from a YAML scalar, multiline string, or list.        | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
| [`text_file`](#text-file) | Reads supported IDs and URLs from a local or remote text file while preserving source order. | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |

## Text file — `text_file` {#text-file}

Finds items using a manually created local or remote text file.

The expected input is a path or URL to a text file, or a list of text file paths and URLs.

Each non-empty line can contain one of the following. Lines beginning with `#` are ignored, and you can also add trailing inline comments using ` # comment` after a value:

- a TMDb ID
- a TVDb ID
- an IMDb ID or IMDb title URL
- a URL returning a JSON list of supported items, including gzip-compressed JSON responses
- `plex://movie/<24-char-id>`
- `plex://show/<24-char-id>`
- `plex://episode/<24-char-id>`
- a bare 24-character Plex metadata ID
- an explicit typed value such as `imdb:`, `tmdb:`, `tvdb:`, `tvdb_season:`, `tvdb_episode:`, `plex:`, or `url:`

Numeric lines are interpreted by library type:

- Movie libraries: TMDb IDs
- Show libraries: TVDb IDs
- Playlists or mixed/unknown contexts: generic numeric IDs matched against available movie/show libraries

The `sync_mode: sync` and `collection_order: custom` settings are recommended when you want the collection order to match the source exactly. If a line expands into multiple items from a JSON list URL, those items keep the order returned by that JSON list. If you provide multiple files or URLs, they are concatenated in the order listed and treated as a single `text_file` builder.

???+ tip "Playlist ordering with mixed movie/show `tmdb:` entries"

    When a `tmdb:` entry (e.g. `tmdb:550`) is used in a playlist or mixed library context, Kometa emits
    **two** internal ID types (`"tmdb"` and `"tmdb_show"`) so both movies and shows are considered.
    Only the correct type resolves to an item; the other is silently skipped.
    This means **line order is preserved** even when movies and shows are interleaved.

A URL used directly as the `text_file` value can return either plain text content using the same line syntax as a local file, or a JSON list using the JSON list format shown below.

On show libraries, `text_file` can also be used with `builder_level: season` or `builder_level: episode` collections. In those cases, `tvdb_season` and `tvdb_episode` entries can target specific show parts directly.

### Episode and season part syntax {#episode-and-season-part-syntax}

For show-part collections, the following explicit values are supported:

- `tvdb_season:12345_1`
- `tvdb_season:12345/1`
- `tvdb_episode:12345_1_2`
- `tvdb_episode:12345-1-2`
- `tvdb_episode:12345/1/2`

Behavior depends on the collection level:

- `builder_level: season` + `tvdb_season` finds the matching season.
- `builder_level: episode` + `tvdb_season` expands to every episode in that season.
- `builder_level: episode` + `tvdb_episode` finds one specific episode.

If multiple lines point at the same episode, Kometa will only keep the episode once in the final collection.

### JSON list example {#json-list-example}

```json
[
  {
    "imdb_id":"tt26443597"
  },
  {
    "tmdb_id":83533
  },
  {
    "tvdb_season":"12345_1"
  },
  {
    "tvdb_episode":{
      "tvdb_id":12345,
      "season":1,
      "episode":2
    }
  },
  {
    "type":"tvdb_episode",
    "id":[12345, 1, 3]
  },
  ...
]
```

### Example text file builder(s) {#example-text-file-builders}

```yaml
collections:
  My Hand Curated List:
    text_file: config/lists/hand-curated.txt
    collection_order: custom
    sync_mode: sync
```

```yaml
collections:
  My Remote Hand Curated List:
    text_file: https://example.com/hand-curated.txt
    collection_order: custom
    sync_mode: sync
```

```yaml
collections:
  Tracker Episodes:
    builder_level: episode
    text_file: config/lists/tracker-episodes.txt
    collection_order: custom
    sync_mode: sync
```

```yaml
collections:
  My Combined Text Files:
    text_file:
      - config/lists/priority.txt
      - https://example.com/overflow.txt
    collection_order: custom
    sync_mode: sync
```

When multiple files or URLs are listed, Kometa reads them as one `text_file` builder input in the order shown above. The source boundaries are not kept as separate builder groups; only the combined item order is preserved.

### Example text file contents {#example-text-file-contents}

```text
# Movie library example
tt0079945   # Star Trek: The Motion Picture IMDb
174         # Star Trek VI: The Undiscovered Country assumed TMDb
tmdb:154    # Star Trek II: The Wrath of Khan unambiguous TMDb
plex://movie/5d7768243c3c2a001fbca85b # Plex movie GUID
5d776824880197001ec901ab              # Plex movie GUID
plex:5d7768244de0ee001fcc7ff2         # typed Plex GUID
url:https://example.com/list.json     # URL returning a JSON list
    # [see example JSON list above]

# Show library example
tt8466564    # Obi-Wan Kenobi IMDB
tmdb:83867   # Andor unambiguous TMDB
361702       # The Mandalorian assumed TVDb
tvdb:393117  # Ahsoka unambiguous TVDb
plex://show/63e3eedd166819851638a316 # Plex show GUID

# Episode example
tt22408116  # Tracker S1.E1 Klamath Falls
tt30221360  # Tracker S1.E3 Springland
tt31092062  # Tracker S1.E5 St. Louis
tt31092069  # Tracker S1.E7 Chicago
tvdb_season:383275/1 # Tracker Season 1 expanded to episodes in episode-level collections
tvdb_episode:383275_1_2 # Tracker S1.E2 Missoula


# Playlist or mixed library example
tt0079945    # Star Trek: The Motion Picture IMDb
tmdb:154     # Star Trek II: The Wrath of Khan unambiguous TMDB
tvdb:361702  # The Mandalorian unambiguous TVDb
plex://show/63e3eedd166819851638a316 # Plex show GUID
```

## Text — `text` {#text}

Finds items using IDs written directly in the collection or playlist YAML. It supports the same identifier syntax as the [`text_file`](#text-file) builder without requiring a separate file.

The builder accepts a scalar string or integer, a literal multiline string, or a list of strings and integers. Entries are processed in their declared order.

The `sync_mode: sync` and `collection_order: custom` settings are recommended when you want the collection and its order to exactly match the inline source.

### Supported values {#supported-values}

Each entry can contain one of the following:

- a TMDb ID
- a TVDb ID
- an IMDb ID or IMDb title URL
- a URL returning a JSON list of supported items
- `plex://movie/<24-char-id>`
- `plex://show/<24-char-id>`
- `plex://episode/<24-char-id>`
- a bare 24-character Plex metadata ID
- an explicit typed value such as `imdb:`, `tmdb:`, `tvdb:`, `tvdb_season:`, `tvdb_episode:`, `plex:`, or `url:`

Blank lines and lines beginning with `#` are ignored. Literal multiline strings can also contain trailing inline comments introduced by whitespace followed by `#`.

Numeric entries are interpreted by library type:

- Movie libraries: TMDb IDs
- Show libraries: TVDb IDs
- Playlists or mixed/unknown contexts: generic numeric IDs matched against the available movie/show libraries

On show libraries, `text` can be used with `builder_level: season` or `builder_level: episode`. The `tvdb_season` and `tvdb_episode` forms described in the [`text_file` documentation](#episode-and-season-part-syntax) target the corresponding show parts.

### Single value {#single-value}

```yaml
collections:
  Star Trek:
    text: tt0079945 # Star Trek: The Motion Picture
    collection_order: custom
    sync_mode: sync
```

YAML removes the trailing comment from a scalar or list value before Kometa receives it.

An unquoted numeric ID is also accepted:

```yaml
collections:
  Star Trek VI:
    text: 174
```

### Multiline string {#multiline-string}

Use YAML's literal `|` or `|-` block style so each identifier remains on its own line:

```yaml
collections:
  Star Trek Movies:
    text: |-
      tt0079945   # Star Trek: The Motion Picture IMDb
      174         # Star Trek VI: The Undiscovered Country assumed TMDb
      tmdb:154    # Star Trek II: The Wrath of Khan unambiguous TMDb
      plex://movie/5d7768243c3c2a001fbca85b # Plex movie GUID
      5d776824880197001ec901ab              # Plex movie GUID
    collection_order: custom
    sync_mode: sync
```

Do not use YAML's folded `>` block style. Folded blocks replace line breaks with spaces, which destroys the one-entry-per-line structure. `>|` is not valid YAML syntax.

### YAML list {#yaml-list}

```yaml
collections:
  Star Trek Movies:
    text:
      - tt0079945
      - 174
      - tmdb:154
      - plex://movie/5d7768243c3c2a001fbca85b
      - 5d776824880197001ec901ab
    collection_order: custom
    sync_mode: sync
```

List entries may be strings or integers. Quote Plex metadata IDs if YAML could interpret the value as a number or discard leading zeroes.

### Playlist example {#playlist-example}

```yaml
playlists:
  Mixed Watchlist:
    text: |-
      tt0079945
      tmdb:154
      tvdb:361702
      plex://show/63e3eedd166819851638a316
    sync_mode: sync
```

In a playlist, `tmdb:` entries are considered as both movie and show IDs so mixed item types retain their declared order. Only the type that resolves on the configured Plex libraries is added.

### URL entries {#url-entries}

A URL within `text` must return a JSON list in the format supported by [`text_file`](#json-list-example):

```yaml
collections:
  Combined List:
    text: |-
      tt0079945
      url:https://example.com/additional-items.json
```

Use `text_file` when the remote URL returns plain-text lines rather than a JSON list.
