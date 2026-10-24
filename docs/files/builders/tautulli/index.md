# Tautulli builders

You can find items in your Plex using the features of [Tautulli](https://tautulli.com/).

Tautulli builders use its popular and most-played lists. `tautulli_popular` gets popular items and `tautulli_top` gets the most-played items across movies, shows, and music. For music libraries, set `builder_level` to choose artists, albums, or tracks. `tautulli_watched` remains available as an alias for `tautulli_top`.

???+ warning "Tautulli Configuration"
    
    [Configuring Tautulli](../../../config/tautulli.md) in the config is required for any of these builders.

| Builder                                         | Description                                       |             Works with Movies              |              Works with Shows              |              Works with Music              |    Works with Playlists and Custom Sort    |
|:------------------------------------------------|:--------------------------------------------------|:------------------------------------------:|:------------------------------------------:|:------------------------------------------:|:------------------------------------------:|
| [`tautulli_popular`](#tautulli-popular)                | Gets the Tautulli Most Popular List               | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
| [`tautulli_top`](#tautulli-top)                        | Gets the Tautulli Top List                       | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |

## Tautulli Popular — `tautulli_popular`, `tautulli_top` {#tautulli-popular}

| Attribute      | Description                                                |                 Required                 | Default |
|:---------------|:-----------------------------------------------------------|:----------------------------------------:|:-------:|
| `list_days`    | Number of Days to look back of the list.                   | :fontawesome-solid-circle-xmark:{ .red } |  `30`   |
| `list_minimum` | Minimum Number of Users Watching/Plays to add to the list. | :fontawesome-solid-circle-xmark:{ .red } |   `0`   |
| `list_size`    | Number of items to add to this list.                       | :fontawesome-solid-circle-xmark:{ .red } |  `10`   |
| `list_buffer`  | Additional items to request when filtering movie/show results (older Tautulli versions only). | :fontawesome-solid-circle-xmark:{ .red } | `list_size * 3` |

The `sync_mode: sync` and `collection_order: custom` Setting are recommended since the lists are continuously updated 
and in a specific order. 

### Example Tautulli Popular Builder(s) {#example-tautulli-popular-builders}

```yaml
collections:
  Most Popular Movies (30 Days):
    sync_mode: sync
    collection_order: custom
    tautulli_popular:
      list_days: 30
      list_size: 10
```
```yaml
collections:
  Plex Popular:
    tautulli_popular:
      list_days: 30
      list_size: 20
    tautulli_top:
      list_days: 30
      list_size: 20
    sync_mode: sync
    summary: Movies Popular on Plex
    collection_order: alpha
```
```yaml
playlists:
  Plex Popular:
    libraries: Movies
    tautulli_popular:
      list_days: 30
      list_size: 20
    sync_mode: sync
    summary: Movies Popular on Plex
```

### Music {#music}

On a music library, `tautulli_popular` uses Tautulli's Popular Music list. Set `builder_level` to `artist`, `album`, or `track` to choose the output level. It defaults to `artist`. Artist and album results aggregate Tautulli's music stats; track results count distinct listeners from Tautulli history within `list_days`. `list_minimum` is the minimum listener count for the selected item.

```yaml
collections:
  Popular Music Tracks:
    builder_level: track
    tautulli_popular:
      list_days: 30
      list_size: 20
      list_minimum: 1
    sync_mode: sync
    collection_order: custom
```

## Tautulli Top — `tautulli_top`, `tautulli_popular` {#tautulli-top}

???+ tip "Tautulli Watched"

    This builder was previously `tautulli_watched` but has been renamed due to supporting Music libraries

| Attribute      | Description                                                |                 Required                 | Default |
|:---------------|:-----------------------------------------------------------|:----------------------------------------:|:-------:|
| `list_days`    | Number of Days to look back of the list.                   | :fontawesome-solid-circle-xmark:{ .red } |  `30`   |
| `list_minimum` | Minimum Number of Users Watching/Plays to add to the list. | :fontawesome-solid-circle-xmark:{ .red } |   `0`   |
| `list_size`    | Number of items to add to this list.                       | :fontawesome-solid-circle-xmark:{ .red } |  `10`   |
| `list_buffer`  | Additional items to request when filtering results (older Tautulli versions only). | :fontawesome-solid-circle-xmark:{ .red } | `list_size * 3` |

The `sync_mode: sync` and `collection_order: custom` Setting are recommended since the lists are continuously updated 
and in a specific order. 

`tautulli_watched` is accepted as a backward-compatible alias for `tautulli_top`.

On music libraries, set `builder_level` to `artist`, `album`, or `track` to choose results from Tautulli's Top Music list. The default is `album`. Artist and album results aggregate Tautulli's music stats; track results count plays from Tautulli history within `list_days`. `list_minimum` is the minimum play count for the selected item.

### Example Tautulli Top Builder(s) {#example-tautulli-top-builders}

```yaml
collections:
  Most Watched Movies (30 Days):
    sync_mode: sync
    collection_order: custom
    tautulli_top:
      list_days: 30
      list_size: 10
```
```yaml
collections:
  Plex Popular:
    tautulli_popular:
      list_days: 30
      list_size: 20
    tautulli_top:
      list_days: 30
      list_size: 20
    sync_mode: sync
    summary: Movies Popular on Plex
    collection_order: alpha
```

```yaml
collections:
  Top Music Albums:
    builder_level: album
    tautulli_top:
      list_days: 90
      list_size: 15
      list_minimum: 2
    sync_mode: sync
    collection_order: custom
```
