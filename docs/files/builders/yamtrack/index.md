# YamTrack Builders

You can find items using lists from your [YamTrack](https://github.com/FuzzyGrim/YamTrack) instance.

???+ warning "YamTrack Configuration"

    [Configuring YamTrack](../../../config/yamtrack.md) in the config is required for any of these builders.

| Builder                         | Description                                      |             Works with Movies              |              Works with Shows              |    Works with Playlists and Custom Sort    |
|:--------------------------------|:-------------------------------------------------|:------------------------------------------:|:------------------------------------------:|:------------------------------------------:|
| [`yamtrack_list`](#yamtrack-list)      | Finds every movie/show in the YamTrack List. Extracts both TMDb and TVDB IDs. | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
| [`yamtrack_tracked`](#yamtrack-tracked)| Finds tracked movies/shows/anime by YamTrack status. Extracts both TMDb and TVDB IDs. | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |

## YamTrack list — `yamtrack_list`, `yamtrack_list_details` {#yamtrack-list}

Finds every item in the YamTrack List.

The expected input is a YamTrack List URL from the configured YamTrack instance. Multiple values are supported as either a list :material-information-outline:{ data-tooltip data-tooltip-id="tippy-yaml-lists" } or a comma-separated string.

The `sync_mode: sync` and `collection_order: custom` Setting are recommended since the lists can be updated in YamTrack and are returned in list order.

???+ tip "Details Builder"

    You can replace `yamtrack_list` with `yamtrack_list_details` if you would like to fetch and use the YamTrack list description as the collection summary.

### Example YamTrack list builder(s) {#example-yamtrack-list-builders}

```yaml
collections:
  YamTrack List:
    yamtrack_list: https://yamtrack.domain.com/list/1
    collection_order: custom
    sync_mode: sync
```

```yaml
collections:
  YamTrack List:
    yamtrack_list_details:
      - https://yamtrack.domain.com/list/1
    collection_order: custom
    sync_mode: sync
```

* You can update the collection summary with the YamTrack list description by using `yamtrack_list_details`.
* You can specify multiple lists in `yamtrack_list_details`, but only the first one is used to update the collection summary.

## YamTrack tracked — `yamtrack_tracked` {#yamtrack-tracked}

Finds every tracked item from the configured YamTrack user's movie and TV pages with the selected statuses.

???+ warning "YamTrack Configuration"

    [Configuring YamTrack](../../../config/yamtrack.md) in the config is required for this builder.

### Example YamTrack tracked builder {#example-yamtrack-tracked-builder}

```yaml
collections:
  YamTrack Tracked:
    yamtrack_tracked:
      movies:
        dropped: false
        planning: true
        in_progress: true
        paused: false
        completed: false
      tv_shows:
        dropped: false
        planning: true
        in_progress: true
        paused: false
        completed: false
      anime:
        dropped: false
        planning: true
        in_progress: true
        paused: false
        completed: false
```

In the above example, Kometa adds only items marked `Planning` or `In Progress`.

### Attributes {#attributes}

| Attribute     | Description                            | Values        |
|:--------------|:---------------------------------------|:--------------|
| `movies`      | Movie statuses to include. Optional.   | Status block  |
| `tv_shows`    | TV show statuses to include. Optional. | Status block  |
| `anime`       | Anime statuses to include. Optional.   | Status block  |

Note that `anime` can have both Movies and TV Shows in YamTrack. Kometa will filter only the media type that correlates with the library that is being run.

Status blocks support these boolean attributes. When a status attribute is omitted from a present `movies`, `tv_shows`, or `anime` block, it defaults to `true`.

| Attribute     | YamTrack Status | Accepted Values | Default |
|:--------------|:----------------|:----------------|:--------|
| `dropped`     | Dropped         | `true`/`false`  | `true`  |
| `planning`    | Planning        | `true`/`false`  | `true`  |
| `in_progress` | In Progress     | `true`/`false`  | `true`  |
| `paused`      | Paused          | `true`/`false`  | `true`  |
| `completed`   | Completed       | `true`/`false`  | `true`  |
