# Simkl builders

You can find items using the trending and DVD release lists provided by [Simkl](https://simkl.com/) via the [Kometa Simkl Service](https://utilities.kometa.wiki/simkl-service).

No API key or Simkl account is required.

| Builder                          | Description                                                                                         |             Works with Movies              |             Works with Shows               |    Works with Playlists and Custom Sort    |
|:---------------------------------|:----------------------------------------------------------------------------------------------------|:------------------------------------------:|:------------------------------------------:|:------------------------------------------:|
| [`simkl_trending`](#simkl-trending)  | Finds movies, TV shows, and anime in Simkl's trending lists.                                        | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
| [`simkl_dvd`](#simkl-dvd)            | Finds movies and TV shows in Simkl's DVD release lists.                                             | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |

## Simkl DVD — `simkl_dvd` {#simkl-dvd}

Finds movies and TV shows from [Simkl's DVD release lists](https://simkl.com/movies/dvd-releases/).

The list is filtered automatically to match your library type: movie libraries receive movies, show libraries receive TV shows, and playlists receive both.

The `sync_mode: sync` and `collection_order: custom` Setting are recommended since the lists are continuously updated and in a specific order.

???+ tip "Playlist ordering for DVD"

    The DVD release endpoint returns a single flat list of items.
    When used in a playlist (mixed library), each item is evaluated individually and
    **API order is preserved** -- movies and shows appear in the same sequence
    returned by Simkl.

### Attribute {#attribute}

| Attribute | Description                                                        | Required | Default |
|:----------|:-------------------------------------------------------------------|:--------:|:-------:|
| `limit`   | Maximum number of items to return. Must be between `1` and `500`. |    No    |  `20`   |

!!! note
    The Simkl service provides lists of the top 100 items (`small`) or top 500 items (`large`). Kometa automatically
    selects the appropriate list size based on your `limit` value: `small` is used when `limit` is 100 or fewer,
    `large` when `limit` is greater than 100.

### Example Simkl DVD Builder(s) {#example-simkl-dvd-builders}

Simple usage with just a limit:

```yaml
collections:
  New on DVD:
    simkl_dvd: 20
    collection_order: custom
    sync_mode: sync
```

Using a dict:

```yaml
collections:
  New on DVD:
    simkl_dvd:
      limit: 50
    collection_order: custom
    sync_mode: sync
```

## Simkl Trending — `simkl_trending` {#simkl-trending}

Finds movies, TV shows and anime from Simkl's trending lists.

- [Movies](https://simkl.com/movies/best-movies/most-watched/)
- [Shows](https://simkl.com/tv/best-shows/most-watched/)
- [Anime](https://simkl.com/anime/best-anime/most-watched/)

The list is filtered automatically to match your library type (movies, shows, or both for playlists).

The `sync_mode: sync` and `collection_order: custom` Setting are recommended since the lists are continuously updated and in a specific order.

???+ warning "Playlist ordering for trending"

    The Simkl API returns trending data in **separate sections** (movies, TV, anime).
    When used in a playlist (mixed library), items appear **grouped by type**:
    all movies first, then all TV shows, then all anime.
    The internal per-section order is preserved, but movies and shows are not interleaved.
    If you need strict per-item interleaving, consider using `text_file` instead.

### Attribute {#simkl-trending-attribute}

| Attribute | Description                                                         | Required | Default  |
|:----------|:--------------------------------------------------------------------|:--------:|:--------:|
| `period`  | Time period for the trending list. Options: `today`, `week`, `month` |    No    | `today`  |
| `limit`   | Maximum number of items to return. Must be between `1` and `500`.  |    No    |   `20`   |

!!! note
    The Simkl service provides lists of the top 100 items (`small`) or top 500 items (`large`). Kometa automatically
    selects the appropriate list size based on your `limit` value: `small` is used when `limit` is 100 or fewer,
    `large` when `limit` is greater than 100.

### Example Simkl Trending Builder(s) {#example-simkl-trending-builders}

Simple usage with just a limit:

```yaml
collections:
  Simkl Trending Today:
    simkl_trending: 20
    collection_order: custom
    sync_mode: sync
```

Using a specific period:

```yaml
collections:
  Simkl Trending This Week:
    simkl_trending:
      period: week
      limit: 50
    collection_order: custom
    sync_mode: sync
```

```yaml
collections:
  Simkl Trending This Month:
    simkl_trending:
      period: month
      limit: 100
    collection_order: custom
    sync_mode: sync
```
