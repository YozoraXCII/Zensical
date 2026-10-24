# FlickList Builders

You can find items using lists and personal data from [FlickList](https://flicklist.tv/).

???+ warning "FlickList Configuration"

    [Configuring FlickList](../../../config/flicklist.md) in the config is required for any of these builders.

| Builder                              | Description                                                         | Works with Movies                          | Works with Shows                           | Works with Playlists and Custom Sort       |
|:-------------------------------------|:--------------------------------------------------------------------|:------------------------------------------:|:------------------------------------------:|:------------------------------------------:|
| [`flicklist_list`](#flicklist-list)          | Finds every item in a FlickList list.                               | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
| [`flicklist_user_lists`](#flicklist-list)    | Finds every item across a FlickList user's public lists.            | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
| [`flicklist_watchlist`](#flicklist-personal-data) | Finds every item in the configured FlickList user's watchlist.      | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
| [`flicklist_favorites`](#flicklist-personal-data) | Finds every item in the configured FlickList user's favorites.      | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
| [`flicklist_watched`](#flicklist-personal-data)   | Finds every item the configured FlickList user has watched.         | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
| [`flicklist_up_next`](#flicklist-personal-data)   | Finds the configured FlickList user's next-unwatched-episode queue. | :fontawesome-solid-circle-xmark:{ .red }   | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
| [`flicklist_tracked`](#flicklist-personal-data)   | Finds shows the configured FlickList user is tracking.              | :fontawesome-solid-circle-xmark:{ .red }   | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
| [`flicklist_ratings`](#flicklist-ratings)    | Finds every item the configured FlickList user has rated.           | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |

## FlickList list — `flicklist_list`, `flicklist_list_details`, `flicklist_user_lists` {#flicklist-list}

Finds every item in a FlickList list, or across a FlickList user's public lists.

???+ warning "FlickList Configuration"

    [Configuring FlickList](../../../config/flicklist.md) in the config is required for these builders.

### flicklist_list {#flicklist_list}

The expected input is a FlickList list URL (`https://flicklist.tv/list/4821`) or its bare numeric id (`4821`).
Multiple values are supported as either a list :material-information-outline:{ data-tooltip data-tooltip-id="tippy-yaml-lists" } or a comma-separated string.

The `sync_mode: sync` and `collection_order: custom` settings are recommended since FlickList lists can be
updated externally and are returned in list order.

???+ tip "Details Builder"

    You can replace `flicklist_list` with `flicklist_list_details` if you would like to fetch and use the
    FlickList list description as the collection summary. Only the first list's description is used when
    multiple lists are given.

### Example FlickList list builder(s) {#example-flicklist-list-builders}

```yaml
collections:
  FlickList List:
    flicklist_list: https://flicklist.tv/list/4821
    collection_order: custom
    sync_mode: sync
```

```yaml
collections:
  FlickList List:
    flicklist_list_details:
      - 4821
      - 9310
    collection_order: custom
    sync_mode: sync
```

### flicklist_user_lists {#flicklist_user_lists}

Finds the union of every item across a named FlickList user's public lists.

The expected input is a FlickList username. This does not require an API key with any particular scope — public
lists are readable without authentication — but Kometa still requires the `flicklist` config block to be present.

A user with many public lists means more requests; Kometa logs how many lists it found for that user before
processing them.

### Example FlickList user lists builder {#example-flicklist-user-lists-builder}

```yaml
collections:
  FlickList Community Picks:
    flicklist_user_lists: some_flicklist_username
    collection_order: custom
    sync_mode: sync
```

## FlickList personal data — `flicklist_watchlist`, `flicklist_favorites`, `flicklist_watched`, `flicklist_tracked`, `flicklist_up_next` {#flicklist-personal-data}

Finds items from the configured FlickList API key's own watchlist, favorites, watched history, up-next queue,
or tracked shows.

???+ warning "FlickList Configuration"

    [Configuring FlickList](../../../config/flicklist.md) in the config is required for these builders. Each
    of these builders reads the `read`-scoped personal data of whichever FlickList account the configured
    `api_key` belongs to.

Each of these builders accepts a blank value or `true`:

```yaml
collections:
  FlickList Watchlist:
    flicklist_watchlist:
    collection_order: custom
    sync_mode: sync

  FlickList Favorites:
    flicklist_favorites: true
    collection_order: custom
    sync_mode: sync

  FlickList Watched:
    flicklist_watched:
    sync_mode: sync

  FlickList Tracked:
    flicklist_tracked:
    collection_order: custom
    sync_mode: sync
```

`flicklist_up_next` and `flicklist_tracked` are show-library only, since a next-unwatched-episode queue and a
tracked-shows list are both inherently show concepts.

`flicklist_up_next` additionally accepts an integer limit on how many upcoming episodes to return:

```yaml
collections:
  FlickList Up Next:
    flicklist_up_next: 20
    collection_order: custom
    sync_mode: sync
```

| Builder               | Blank/`true` means     | Also accepts  | Library restriction |
|:----------------------|:-----------------------|:--------------|:--------------------|
| `flicklist_watchlist` | Entire watchlist       | —             | Movies and Shows    |
| `flicklist_favorites` | Entire favorites list  | —             | Movies and Shows    |
| `flicklist_watched`   | Entire watched history | —             | Movies and Shows    |
| `flicklist_up_next`   | All up-next episodes   | Integer limit | Shows only          |
| `flicklist_tracked`   | Every tracked show     | —             | Shows only          |

!!! note "`flicklist_watchlist` covers more than "plan to watch""

    FlickList's watchlist stores more than a simple plan-to-watch state: every item carries a
    `status` of `plan_to_watch`, `watching`, `completed`, `on_hold`, or `dropped`. `flicklist_watchlist`
    currently returns the entire watchlist regardless of status - there is no way to filter to just
    one status yet. If you're looking for "shows I've marked completed" specifically, note that this
    is a different concept from `flicklist_watched`, which reflects actual play history (has the
    episode/movie been played), not a manually-set watchlist status.

## FlickList ratings — `flicklist_ratings` {#flicklist-ratings}

Finds every item the configured FlickList API key's account has rated.

???+ warning "FlickList Configuration"

    [Configuring FlickList](../../../config/flicklist.md) in the config is required for this builder.

`flicklist_ratings` accepts a blank value or `true` for every rated item, a number as a minimum rating, or an
object with `minimum`/`maximum` bounds. FlickList ratings are documented as half-point increments (0.5–10) but
the API does not currently enforce that, so a fractional rating like `5.3` can come back from FlickList itself.

### Example FlickList ratings builder(s) {#example-flicklist-ratings-builders}

```yaml
collections:
  FlickList Rated:
    flicklist_ratings:
    sync_mode: sync
```

```yaml
collections:
  FlickList Rated 7+:
    flicklist_ratings: 7
    sync_mode: sync
```

```yaml
collections:
  FlickList Rated 7 to 9:
    flicklist_ratings:
      minimum: 7
      maximum: 9
    sync_mode: sync
```

### Attributes {#attributes}

| Attribute | Description               | Values                   |
|:----------|:--------------------------|:-------------------------|
| `minimum` | Lowest rating to include  | Number, 0.5–10, optional |
| `maximum` | Highest rating to include | Number, 0.5–10, optional |
