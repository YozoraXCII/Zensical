# Letterboxd Builders

You can find items using the lists on [Letterboxd.com](https://letterboxd.com/) (Letterboxd). 

Letterboxd support is powered by `letterboxdpy`. Builder inputs stay the same, but behavior that previously depended on Kometa's custom Letterboxd scraping now follows the fields exposed by `letterboxdpy`.

| Builder                      | Description                              |             Works with Movies              |             Works with Shows             |    Works with Playlists and Custom Sort    |
|:-----------------------------|:-----------------------------------------|:------------------------------------------:|:----------------------------------------:|:------------------------------------------:|
| [`letterboxd_list`](#letterboxd-list) | Finds every movie in the Letterboxd List | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-xmark:{ .red } | :fontawesome-solid-circle-check:{ .green } |
| [`letterboxd_crew`](discovery.md#crew) | Finds movies credited to a person in a selected role | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-xmark:{ .red } | :fontawesome-solid-circle-check:{ .green } |
| [`letterboxd_studio`](discovery.md#other-discovery-builders) | Finds movies from a studio | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-xmark:{ .red } | :fontawesome-solid-circle-check:{ .green } |
| [`letterboxd_country`](discovery.md#other-discovery-builders) | Finds movies from a country | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-xmark:{ .red } | :fontawesome-solid-circle-check:{ .green } |
| [`letterboxd_language`](discovery.md#other-discovery-builders) | Finds movies in a language | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-xmark:{ .red } | :fontawesome-solid-circle-check:{ .green } |
| [`letterboxd_genre`](discovery.md#other-discovery-builders) | Finds movies in a genre | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-xmark:{ .red } | :fontawesome-solid-circle-check:{ .green } |
| [`letterboxd_theme`](discovery.md#other-discovery-builders) | Finds movies in a theme | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-xmark:{ .red } | :fontawesome-solid-circle-check:{ .green } |
| [`letterboxd_similar`](discovery.md#other-discovery-builders) | Finds movies similar to a film | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-xmark:{ .red } | :fontawesome-solid-circle-check:{ .green } |
| [`letterboxd_collection`](discovery.md#other-discovery-builders) | Finds movies in a film collection | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-xmark:{ .red } | :fontawesome-solid-circle-check:{ .green } |
| [`letterboxd_user_films`](#letterboxd-user-films) | Finds every movie in a user's watched films | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-xmark:{ .red } | :fontawesome-solid-circle-check:{ .green } |
| [`letterboxd_user_reviews`](#letterboxd-user-reviews) | Finds every movie in a user's reviewed films | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-xmark:{ .red } | :fontawesome-solid-circle-check:{ .green } |

## Letterboxd list — `letterboxd_list`, `letterboxd_list_details` {#letterboxd-list}

Finds every movie in a Letterboxd list or [Letterboxd Films Search](https://letterboxd.com/films/).

The expected input is a supported Letterboxd URL. Multiple values are supported as either a list :material-information-outline:{ data-tooltip data-tooltip-id="tippy-yaml-lists" } or a comma-separated string.

Private links (which start with the URL `https://boxd.it/`) are also supported.

Kometa now uses `letterboxdpy` for Letterboxd access. Standard list URLs continue to work, and `/films/...` URLs remain supported.

Use the [Letterboxd Discovery Builders](discovery.md) for people, studios, genres, themes, countries, languages, film collections, and similar movies.

You can add different filters directly to this Builder.

| Filter Attribute                                                                                  | Description                                                                                                                                                                                                |
|:--------------------------------------------------------------------------------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `limit`                                                                                           | **Description:** Max number of items per returned.<br>**Values:** number greater than `1`                                                                                                                  |
| `rating` :material-numeric-1-circle:{ data-tooltip data-tooltip-id="tippy-letterboxd-filters-1" } | **Description:** Search for the specified rating range. The rating is the list owner's rating not site wide rating.<br>**Values:** range of int i.e. `8-10` (convert Letterboxd stars to a 10 point scale) |
| `year` :material-numeric-1-circle:{ data-tooltip data-tooltip-id="tippy-letterboxd-filters-1" }   | **Description:** Search for the specified year range.<br>**Values:** range of int i.e. `1990-1999`                                                                                                         |
| `note` :material-numeric-2-circle:{ data-tooltip data-tooltip-id="tippy-letterboxd-filters-2" }   | **Description:** Search for the specified value in the note. The note is the list owner's note not site wide note.<br>**Values:** Any String                                                               |

The `sync_mode: sync` and `collection_order: custom` Setting are recommended since the lists are continuously updated and in a specific order.

Using the `limit` filter attribute is recommended when using a Letterboxd Film Search as the number of results returned could be very large.

???+ warning "Filter Support Depends on URL Type"

    The `year` filter works for both standard list URLs and `/films/...` URLs.

    The `rating` and `note` filters are only available for `/films/...` URLs exposed through `letterboxdpy`. Standard user list URLs do not expose per-item owner ratings or notes, so those filters are ignored for those URLs.

???+ tip "Details Builder"

    You can replace `letterboxd_list` with `letterboxd_list_details` if you would like to fetch and use the description from the list


### Example Letterboxd list builder(s) {#example-letterboxd-list-builders}

```yaml
collections:
  Vulture’s 101 Best Movie Endings:
    letterboxd_list: https://letterboxd.com/brianformo/list/vultures-101-best-movie-endings/
    collection_order: custom
    sync_mode: sync
```

* You can update the collection details with the Letterboxd List's description by using `letterboxd_list_details`.
  * You can specify multiple collections in `letterboxd_list_details` but it will only use the first one to update the collection summary.

```yaml
collections:
  Vulture’s 101 Best Movie Endings:
    letterboxd_list_details: https://letterboxd.com/brianformo/list/vultures-101-best-movie-endings/
    collection_order: custom
    sync_mode: sync
```

```yaml
collections:
  Vulture’s 101 Best Movie Endings From the 90s:
    letterboxd_list_details: 
      url: https://letterboxd.com/brianformo/list/vultures-101-best-movie-endings/
      year: 1990-1999
    collection_order: custom
    sync_mode: sync
```

## Letterboxd user films — `letterboxd_user_films` {#letterboxd-user-films}

Finds every movie in a Letterboxd user's watched films page.

The expected input is a username or a dictionary with the username and optional parameters. Multiple values are supported as either a list :material-information-outline:{ data-tooltip data-tooltip-id="tippy-yaml-lists" } or a comma-separated string.

Kometa now uses `letterboxdpy` for Letterboxd access. The builder contract is unchanged, but watched-film ordering now follows the default order returned by `letterboxdpy`.

You can add different filters directly to this Builder.

| Filter Attribute                                                                                  | Description                                                                                                                                                                                                |
|:--------------------------------------------------------------------------------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `username`                                                                                        | **Description:** Letterboxd username<br>**Values:** Username string (required)                                                                                                                          |
| `sort_by`                                                                                         | **Description:** Accepted for compatibility with older configs.<br>**Default:** `release_date_newest`<br>**Values:** `release_date_newest`, `release_date_earliest`, `name`, `popularity`, `when_added_newest`, `when_added_earliest`, `when_rated_newest`, `when_rated_earliest`, `average_rating_highest`, `average_rating_lowest`, `user_rating_highest`, `user_rating_lowest`, `length_shortest`, `length_longest` |
| `min_rating` :material-numeric-1-circle:{ data-tooltip data-tooltip-id="tippy-letterboxd-filters-1" } | **Description:** Filter by minimum user rating (on 10-point scale)<br>**Values:** number from `0` to `10`                                                                                                  |
| `limit`                                                                                           | **Description:** Max number of items per returned.<br>**Values:** number greater than `1`                                                                                                                  |
| `year` :material-numeric-1-circle:{ data-tooltip data-tooltip-id="tippy-letterboxd-filters-1" }   | **Description:** Search for the specified year range.<br>**Values:** range of int i.e. `1990-1999`                                                                                                         |
| `note` :material-numeric-2-circle:{ data-tooltip data-tooltip-id="tippy-letterboxd-filters-2" }   | **Description:** Accepted for compatibility with older configs, but watched-film notes are not exposed by `letterboxdpy` and this filter is ignored.<br>**Values:** Any String                                                               |
| `incremental`                                                                                      | **Description:** Accepted for compatibility with older configs.<br>**Default:** `false` at runtime<br>**Values:** `true` or `false` |

The `sync_mode: sync` and `collection_order: custom` Setting are recommended since the lists are continuously updated and in a specific order.

???+ warning "Sort, Note, and Incremental Behavior"

    `sort_by` values are still accepted so existing configs do not break, but `letterboxdpy` does not expose a stable way for Kometa to force those sort orders for watched films. Kometa therefore uses the default page order returned by `letterboxdpy` and logs a warning when a non-default `sort_by` is supplied.

    `note` filtering is currently ignored for watched films because `letterboxdpy` does not expose watched-film notes for Kometa to match against.

    `incremental` parsing is currently disabled for Letterboxd user films because `letterboxdpy` does not expose stable incremental state for Kometa to track. If `incremental: true` is set, Kometa logs a warning and continues with a normal full fetch.

Using the `limit` filter attribute is recommended when using a user with many watched films as the number of results returned could be very large.

???+ tip "Details Builder"

    You can replace `letterboxd_user_films` with `letterboxd_user_films_details` if you would like to use the details variant (currently no description is available for user pages, but this maintains consistency with other builders).


### Example Letterboxd user films builder(s) {#example-letterboxd-user-films-builders}

```yaml
collections:
  User Watched Films:
    letterboxd_user_films: {username}
    collection_order: custom
    sync_mode: sync
```

```yaml
collections:
  User Highly Rated Films:
    letterboxd_user_films:
      username: {username}
      min_rating: 8
      sort_by: user_rating_highest
    collection_order: custom
    sync_mode: sync
```

```yaml
collections:
  User 90s Films:
    letterboxd_user_films:
      username: {username}
      year: 1990-1999
      sort_by: release_date_earliest
    collection_order: custom
    sync_mode: sync
```

```yaml
collections:
  Multiple Users' Watched Films:
    letterboxd_user_films:
      - {username1}
      - {username2}
      - {username3}
    collection_order: custom
    sync_mode: sync
```

```yaml
collections:
  Multiple Users' Highly Rated Films:
    letterboxd_user_films:
      - username: {username1}
        min_rating: 8
        sort_by: user_rating_highest
      - username: {username2}
        min_rating: 9
        sort_by: user_rating_highest
    collection_order: custom
    sync_mode: sync
```

## Letterboxd user reviews — `letterboxd_user_reviews` {#letterboxd-user-reviews}

Finds every movie in a Letterboxd user's reviewed films page.

The expected input is a username or a dictionary with the username and optional parameters. Multiple values are supported as either a list :material-information-outline:{ data-tooltip data-tooltip-id="tippy-yaml-lists" } or a comma-separated string.

Kometa now uses `letterboxdpy` for Letterboxd access. The builder contract is unchanged, but user review ordering now follows the default order returned by `letterboxdpy`.

You can add different filters directly to this Builder.

| Filter Attribute                                                                                  | Description                                                                                                                                                                                                |
|:--------------------------------------------------------------------------------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `username`                                                                                        | **Description:** Letterboxd username<br>**Values:** Username string (required)                                                                                                                          |
| `sort_by`                                                                                         | **Description:** Accepted for compatibility with older configs.<br>**Default:** `release_date_newest`<br>**Values:** `release_date_newest`, `release_date_earliest`, `name`, `popularity`, `when_added_newest`, `when_added_earliest`, `when_rated_newest`, `when_rated_earliest`, `average_rating_highest`, `average_rating_lowest`, `user_rating_highest`, `user_rating_lowest`, `length_shortest`, `length_longest` |
| `min_rating` :material-numeric-1-circle:{ data-tooltip data-tooltip-id="tippy-letterboxd-filters-1" } | **Description:** Filter by minimum user rating (on 10-point scale)<br>**Values:** number from `0` to `10`                                                                                                  |
| `limit`                                                                                           | **Description:** Max number of items per returned.<br>**Values:** number greater than `1`                                                                                                                  |
| `year` :material-numeric-1-circle:{ data-tooltip data-tooltip-id="tippy-letterboxd-filters-1" }   | **Description:** Search for the specified year range.<br>**Values:** range of int i.e. `1990-1999`                                                                                                         |
| `note` :material-numeric-2-circle:{ data-tooltip data-tooltip-id="tippy-letterboxd-filters-2" }   | **Description:** Search for the specified value in the review text returned by `letterboxdpy`.<br>**Values:** Any String                                                               |
| `incremental`                                                                                      | **Description:** Accepted for compatibility with older configs.<br>**Default:** `false` at runtime<br>**Values:** `true` or `false` |

The `sync_mode: sync` and `collection_order: custom` Setting are recommended since the lists are continuously updated and in a specific order.

???+ warning "Sort and Incremental Behavior"

    `sort_by` values are still accepted so existing configs do not break, but `letterboxdpy` does not expose a stable way for Kometa to force those sort orders for reviewed films. Kometa therefore uses the default page order returned by `letterboxdpy` and logs a warning when a non-default `sort_by` is supplied.

    `incremental` parsing is currently disabled for Letterboxd user reviews because `letterboxdpy` does not expose stable incremental state for Kometa to track. If `incremental: true` is set, Kometa logs a warning and continues with a normal full fetch.

Using the `limit` filter attribute is recommended when using a user with many reviewed films as the number of results returned could be very large.

???+ tip "Details Builder"

    You can replace `letterboxd_user_reviews` with `letterboxd_user_reviews_details` if you would like to use the details variant (currently no description is available for user pages, but this maintains consistency with other builders).


### Example Letterboxd user reviews builder(s) {#example-letterboxd-user-reviews-builders}

```yaml
collections:
  User Reviewed Films:
    letterboxd_user_reviews: {username}
    collection_order: custom
    sync_mode: sync
```

```yaml
collections:
  User Top Rated Reviews:
    letterboxd_user_reviews:
      username: {username}
      min_rating: 9
      sort_by: user_rating_highest
    collection_order: custom
    sync_mode: sync
```

```yaml
collections:
  User Recent Reviews:
    letterboxd_user_reviews:
      username: {username}
      sort_by: when_rated_newest
      limit: 50
    collection_order: custom
    sync_mode: sync
```

```yaml
collections:
  Multiple Users' Reviewed Films:
    letterboxd_user_reviews:
      - {username1}
      - {username2}
      - {username3}
    collection_order: custom
    sync_mode: sync
```

```yaml
collections:
  Multiple Users' Top Rated Reviews:
    letterboxd_user_reviews:
      - username: {username1}
        min_rating: 9
        sort_by: user_rating_highest
      - username: {username2}
        min_rating: 8
        sort_by: user_rating_highest
    collection_order: custom
    sync_mode: sync
```

## More Letterboxd references

- [Discovery and filmographies](discovery.md)
