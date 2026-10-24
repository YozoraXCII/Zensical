# Sonarr builders

You can find items in your Plex using the features of [Sonarr](https://sonarr.tv/).

???+ warning "Sonarr Configuration"

    [Configuring Sonarr](../../../config/sonarr.md) in the config is required for any of these builders.

| Builder                        | Description                                  |            Works with Movies             |              Works with Shows              |   Works with Playlists and Custom Sort   |
|:-------------------------------|:---------------------------------------------|:----------------------------------------:|:------------------------------------------:|:----------------------------------------:|
| [`sonarr_all`](#sonarr-all)         | Gets all Series in Sonarr.                   | :fontawesome-solid-circle-xmark:{ .red } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-xmark:{ .red } |
| [`sonarr_taglist`](#sonarr-taglist) | Gets Series from Sonarr based on their tags. | :fontawesome-solid-circle-xmark:{ .red } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-xmark:{ .red } |

## Sonarr All — `sonarr_all` {#sonarr-all}
    
Gets all Series in Sonarr.

### Example Sonarr All Builder(s) {#example-sonarr-all-builders}

```yaml
collections:
  ALL Sonarr Series:
    sonarr_all: true
```

## Sonarr Taglist — `sonarr_taglist` {#sonarr-taglist}

Gets Series from Sonarr based on their tags. 

Set the attribute to the tag you want to search for. Multiple values are supported as either a list :material-information-outline:{ data-tooltip data-tooltip-id="tippy-yaml-lists" } or a comma-separated 
string. 

### Example Sonarr Taglist Builder(s) {#example-sonarr-taglist-builders}

```yaml
collections:
  Sonarr Tag1 and Tag2 Series:
    sonarr_taglist: tag1, tag2
```

If no tag is specified then it gets every Movie without a tag.

```yaml
collections:
  Sonarr Series Without Tags:
    sonarr_taglist: 
```

### Sync to MDBList {#sync-to-mdblist}

When used with [`sync_to_mdb_list`](../../settings.md#mdblist-sync-example),
`sonarr_taglist` uses the matching series in Sonarr as the source of truth.
The sync does not depend on the items being present in Plex or on a Plex
collection being built. Removing a tag in Sonarr also removes
the series from the MDBList static list. Only series are removed, so this can
safely share a list with [`radarr_taglist`](../radarr/index.md#radarr-taglist) syncs.

```yaml
collections:
  Sonarr Test:
    sonarr_taglist: kometa_test
    sync_to_mdb_list: My Kometa Test Tags
    build_collection: false
```
