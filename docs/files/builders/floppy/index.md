# Floppy builders

You can find movies and shows using lists from your [Floppy](https://github.com/dannyvfilms/Floppy) instance.

???+ warning "Floppy Configuration"

    [Configuring Floppy](../../../config/floppy.md) in the config is required for this builder.

| Builder | Description | Works with Movies | Works with Shows | Works with Playlists and Custom Sort |
|:--------|:------------|:-----------------:|:----------------:|:------------------------------------:|
| [`floppy_list`](#floppy-list) | Finds every supported movie/show in a Floppy list. | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
| [`floppy_list_details`](#floppy-list) | Finds list items and uses the Floppy description as the Plex collection summary. | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
| [`floppy_tracked`](#floppy-tracked) | Finds Floppy items tracked with selected statuses and media types. | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |

## Floppy List — `floppy_list_details`, `floppy_list` {#floppy-list}

Finds every supported movie, show, or episode in a Floppy list. The expected input is a list URL from the configured Floppy instance. Multiple URLs are supported. Episode entries require `builder_level: episode` and are added as the exact listed episodes.

Public lists work without a token. Episode collections read exact episode entries from the list RSS feed. Private lists require an API token in the [Floppy connector](../../../config/floppy.md). Use `floppy_list_details` to copy the Floppy list description to the Plex collection summary.

Each list also accepts an optional `sync_tags` attribute. When enabled, the Floppy list tags are added as Plex labels to the items in the resulting collection.

The `sync_mode: sync` and `collection_order: custom` settings are recommended because Floppy lists can change and their list order is preserved.

```yaml
collections:
  Floppy List:
    floppy_list_details:
      url: https://floppy.example.com/list/1
      sync_tags: true
    collection_order: custom
    sync_mode: sync
```

```yaml
collections:
  Floppy Lists:
    floppy_list:
      - url: https://floppy.example.com/list/1
        sync_tags: false
      - url: https://floppy.example.com/list/2
        sync_tags: true
    collection_order: custom
    sync_mode: sync
```

## Floppy Tracked — `floppy_tracked` {#floppy-tracked}

Finds items in the configured Floppy instance by tracking status. A private Floppy API token is required.

`status` accepts `no_status`, `completed`, `in_progress`, `planning`, `paused`, `dropped`, or `all`. The `all` value includes every tracked item regardless of status. `type` accepts `movie`, `show`, `season`, and `anime`; it defaults to `movie` for movie libraries and `show,season` for show libraries.

```yaml
collections:
  Tracked In Progress:
    floppy_tracked:
      status: in_progress

  Tracked Anime:
    floppy_tracked:
      status: [completed, in_progress]
      type: anime
```

Anime entries are read by MyAnimeList ID and converted through Kometa's existing anime mappings. Only anime that resolves to an item in the current library is included.
