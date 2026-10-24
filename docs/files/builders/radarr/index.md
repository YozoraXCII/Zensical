# Radarr Builders

You can find items in your Plex using the features of [Radarr](https://radarr.video/).

???+ warning "Radarr Configuration"

    [Configuring Radarr](../../../config/radarr.md) in the config is required for any of these builders.

| Builder                        | Description                                  |             Works with Movies              |             Works with Shows             |   Works with Playlists and Custom Sort   |
|:-------------------------------|:---------------------------------------------|:------------------------------------------:|:----------------------------------------:|:----------------------------------------:|
| [`radarr_all`](#radarr-all)         | Gets all Movies in Radarr.                   | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-xmark:{ .red } | :fontawesome-solid-circle-xmark:{ .red } |
| [`radarr_taglist`](#radarr-taglist) | Gets Movies from Radarr based on their tags. | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-xmark:{ .red } | :fontawesome-solid-circle-xmark:{ .red } |

## Radarr all — `radarr_all` {#radarr-all}

Gets all Movies in Radarr.

### Example Radarr all builder(s) {#example-radarr-all-builders}

```yaml
collections:
  ALL Radarr Movies:
    radarr_all: true
```

## Radarr taglist — `radarr_taglist` {#radarr-taglist}

Gets Movies from Radarr based on their tags. 

Set the attribute to the tag you want to search for. Multiple values are supported as either a list :material-information-outline:{ data-tooltip data-tooltip-id="tippy-yaml-lists" } or a comma-separated string. 

### Example Radarr taglist builder(s) {#example-radarr-taglist-builders}

```yaml
collections:
  Radarr Tag1 and Tag2 Movies:
    radarr_taglist: tag1, tag2
```

If no tag is specified then it gets every Movie without a tag.

```yaml
collections:
  Radarr Movies Without Tags:
    radarr_taglist: 
```

### Sync to MDBList {#sync-to-mdblist}

When used with [`sync_to_mdb_list`](../../settings.md#mdblist-sync-example),
`radarr_taglist` uses the matching movies in Radarr as the source of truth.
The sync does not depend on the items being present in Plex or on a Plex
collection being built. Removing a tag in Radarr also removes
the movie from the MDBList static list. Only movies are removed, so this can
safely share a list with [`sonarr_taglist`](../sonarr/index.md#sonarr-taglist) syncs.

```yaml
collections:
  Radarr Test:
    radarr_taglist: kometa_test
    sync_to_mdb_list: My Kometa Test Tags
    build_collection: false
```
