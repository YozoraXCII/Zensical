# WeTrakr Builders

You can find items using lists and personal data from [WeTrakr](https://wetrakr.com/).

???+ warning "WeTrakr Configuration"

    [Configuring WeTrakr](../../../config/wetrakr.md) in the config is required for any of these builders.

| Builder                            | Description                                                    | Works with Movies                          | Works with Shows                           | Works with Playlists and Custom Sort       |
|:------------------------------------|:----------------------------------------------------------------|:------------------------------------------:|:------------------------------------------:|:------------------------------------------:|
| [`wetrakr_list`](#wetrakr-list)          | Finds every item in a WeTrakr list.                             | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
| [`wetrakr_user_lists`](#wetrakr-list)    | Finds every item across a WeTrakr user's public lists.          | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
| [`wetrakr_tracking`](#wetrakr-personal-data)  | Finds items in the configured WeTrakr account's tracking list, filtered by status. | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
| [`wetrakr_favorites`](#wetrakr-personal-data) | Finds every item in the configured WeTrakr account's favorites. | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
| [`wetrakr_ratings`](#wetrakr-ratings)    | Finds every item the configured WeTrakr account has rated.      | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |

## WeTrakr list — `wetrakr_list`, `wetrakr_list_details`, `wetrakr_user_lists` {#wetrakr-list}

Finds every item in a WeTrakr list, or across a WeTrakr user's public lists.

???+ warning "WeTrakr Configuration"

    [Configuring WeTrakr](../../../config/wetrakr.md) in the config is required for these builders.

### wetrakr_list {#wetrakr_list}

The expected input is a WeTrakr list URL (`https://wetrakr.com/lists/13255`) or its bare numeric id (`13255`).
Multiple values are supported as either a list :material-information-outline:{ data-tooltip data-tooltip-id="tippy-yaml-lists" } or a comma-separated string.

The `sync_mode: sync` and `collection_order: custom` settings are recommended since WeTrakr lists can be
updated externally and are returned in list order.

Private and friends-only lists are only readable when they belong to the authenticated WeTrakr account; a
private list belonging to someone else returns an error naming the list.

???+ tip "Details Builder"

    You can replace `wetrakr_list` with `wetrakr_list_details` if you would like to fetch and use the
    WeTrakr list description as the collection summary. Only the first list's description is used when
    multiple lists are given.

### Example WeTrakr list builder(s) {#example-wetrakr-list-builders}

```yaml
collections:
  WeTrakr List:
    wetrakr_list: https://wetrakr.com/lists/13255
    collection_order: custom
    sync_mode: sync
```

```yaml
collections:
  WeTrakr List:
    wetrakr_list_details:
      - 13255
      - 1033032976
    collection_order: custom
    sync_mode: sync
```

### wetrakr_user_lists {#wetrakr_user_lists}

Finds the union of every item across a WeTrakr user's public lists.

The input can be a numeric WeTrakr user id, a bare username, or a profile URL
(`wetrakr.com/user/<username>`) — a username or URL is resolved to its numeric id via WeTrakr's search API,
matched on an exact (case-insensitive) username.

A user with many public lists means more requests; Kometa logs how many lists it found for that user before
processing them. Locked or non-public lists in that user's list collection are skipped automatically.

### Example WeTrakr user lists builder {#example-wetrakr-user-lists-builder}

```yaml
collections:
  WeTrakr Community Picks:
    wetrakr_user_lists: 275
    collection_order: custom
    sync_mode: sync
```

## WeTrakr personal data — `wetrakr_tracking`, `wetrakr_favorites` {#wetrakr-personal-data}

Finds items from the configured WeTrakr account's own tracking list or favorites.

???+ warning "WeTrakr Configuration"

    [Configuring WeTrakr](../../../config/wetrakr.md) in the config is required for these builders. Each of
    these builders reads the personal data of whichever WeTrakr account the configured `authorization` belongs to.

### wetrakr_tracking {#wetrakr_tracking}

WeTrakr's tracking list carries one of six statuses per item: `planning`, `watching`, `waiting`, `watched`,
`paused`, `dropped`. A blank value or `true` includes every status valid for the library type; `false` disables
the builder entirely; an object lets you pick specific statuses.

```yaml
collections:
  WeTrakr Tracking:
    wetrakr_tracking:
    collection_order: custom
    sync_mode: sync

  WeTrakr Currently Watching:
    wetrakr_tracking:
      watching: true
    collection_order: custom
    sync_mode: sync
```

Movie libraries only ever request the `planning`, `watched`, and `dropped` statuses — `watching`, `waiting`, and
`paused` are show-only concepts and are skipped automatically for movie libraries.

### wetrakr_favorites {#wetrakr_favorites}

Accepts a blank value or `true`:

```yaml
collections:
  WeTrakr Favorites:
    wetrakr_favorites:
    collection_order: custom
    sync_mode: sync
```

| Builder             | Blank/`true` means                              | Also accepts             | Library restriction |
|:---------------------|:-------------------------------------------------|:--------------------------|:---------------------|
| `wetrakr_tracking`   | Every status valid for the library type          | Object of specific statuses, or `false` | Movies and Shows    |
| `wetrakr_favorites`  | Entire favorites list                            | —                          | Movies and Shows    |

## WeTrakr ratings — `wetrakr_ratings` {#wetrakr-ratings}

Finds every item the configured WeTrakr account has rated.

???+ warning "WeTrakr Configuration"

    [Configuring WeTrakr](../../../config/wetrakr.md) in the config is required for this builder.

`wetrakr_ratings` accepts a blank value or `true` for every rated item, a number as a minimum rating, or an
object with `minimum`/`maximum` bounds. WeTrakr ratings are on a 0–10 scale with one decimal place.

### Example WeTrakr ratings builder(s) {#example-wetrakr-ratings-builders}

```yaml
collections:
  WeTrakr Rated:
    wetrakr_ratings:
    sync_mode: sync
```

```yaml
collections:
  WeTrakr Rated 7+:
    wetrakr_ratings: 7
    sync_mode: sync
```

```yaml
collections:
  WeTrakr Rated 7 to 9:
    wetrakr_ratings:
      minimum: 7
      maximum: 9
    sync_mode: sync
```

### Attributes {#attributes}

| Attribute | Description               | Values                 |
|:----------|:--------------------------|:------------------------|
| `minimum` | Lowest rating to include  | Number, 0–10, optional |
| `maximum` | Highest rating to include | Number, 0–10, optional |
