# AniList Builders

You can find anime using the features of [AniList.co](https://anilist.co/) (AniList).

| Builder                             | Description                                                                                                              |             Works with Movies              |              Works with Shows              |    Works with Playlists and Custom Sort    |
|:------------------------------------|:-------------------------------------------------------------------------------------------------------------------------|:------------------------------------------:|:------------------------------------------:|:------------------------------------------:|
| [`anilist_search`](search.md)       | Finds the anime specified by the AniList search parameters provided                                                      | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
| [`anilist_top_rated`](#anilist-top-rated) | Finds every anime in AniList's [Top Rated Anime](https://anilist.co/search/anime?sort=SCORE_DESC) list                   | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
| [`anilist_popular`](#anilist-popular)     | Finds every anime in AniList's [Popular Anime](https://anilist.co/search/anime/popular) list                             | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
| [`anilist_trending`](#anilist-trending)   | Finds every anime in AniList's [Trending Anime](https://anilist.co/search/anime/trending) list                           | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
| [`anilist_relations`](#anilist-relations) | Finds the anime specified by the AniList ID and every relation in its relation tree except Character and Other relations | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
| [`anilist_studio`](#anilist-studio)       | Finds all anime specified by the AniList Studio ID                                                                       | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
| [`anilist_id`](#anilist-id)               | Finds the anime specified by the AniList ID                                                                              | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
| [`anilist_userlist`](#anilist-userlist)   | Finds the anime in AniList User's Anime list the options are detailed below                                              | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |

## AniList ID — `anilist_id` {#anilist-id}

Finds the anime specified by the AniList ID.

The expected input is an AniList ID. Multiple values are supported as either a list :material-information-outline:{ data-tooltip data-tooltip-id="tippy-yaml-lists" } or a comma-separated string.

### Example AniList ID builder(s) {#example-anilist-id-builders}

```yaml
collections:
  Cowboy Bebop:
    anilist_id: 23, 219
```

## AniList popular — `anilist_popular` {#anilist-popular}

Finds every anime in AniList's [Popular Anime](https://anilist.co/search/anime/popular) list.

The expected input is a single integer value of how many movies/shows to query. 

The `sync_mode: sync` and `collection_order: custom` Setting are recommended since the lists are continuously updated and in a specific order. 

### Example AniList popular builder(s) {#example-anilist-popular-builders}

```yaml
collections:
  Popular Anime:
    anilist_popular: 10
    collection_order: custom
    sync_mode: sync
```

## AniList relations — `anilist_relations` {#anilist-relations}

Finds the anime specified by the AniList ID and every relation in its relation tree except Character and Other relations.

The expected input is an AniList ID. Multiple values are supported as either a list :material-information-outline:{ data-tooltip data-tooltip-id="tippy-yaml-lists" } or a comma-separated string.

### Example AniList relations builder(s) {#example-anilist-relations-builders}

```yaml
collections:
  One Piece:
    anilist_relations: 21
```

## AniList studio — `anilist_studio` {#anilist-studio}

Finds all anime specified by the AniList Studio ID.

The expected input is an AniList ID. Multiple values are supported as either a list :material-information-outline:{ data-tooltip data-tooltip-id="tippy-yaml-lists" } or a comma-separated string.

### Example AniList studio builder(s) {#example-anilist-studio-builders}

```yaml
collections:
  Studio Ghibli:
    anilist_studio: 21
```

## AniList top rated — `anilist_top_rated` {#anilist-top-rated}

Finds every anime in AniList's [Top Rated Anime](https://anilist.co/search/anime?sort=SCORE_DESC) list.

The expected input is a single integer value of how many movies/shows to query. 

The `sync_mode: sync` and `collection_order: custom` Setting are recommended since the lists are continuously updated and in a specific order. 

### Example AniList top rated builder(s) {#example-anilist-top-rated-builders}

```yaml
collections:
  Top Rated Anime:
    anilist_top_rated: 30
    collection_order: custom
    sync_mode: sync
```

## AniList trending — `anilist_trending` {#anilist-trending}

Finds every anime in AniList's [Trending Anime](https://anilist.co/search/anime/trending) list.

The expected input is a single integer value of how many movies/shows to query. 

The `sync_mode: sync` and `collection_order: custom` Setting are recommended since the lists are continuously updated and in a specific order. 

### Example AniList trending builder(s) {#example-anilist-trending-builders}

```yaml
collections:
  Trending Anime:
    anilist_trending: 10
    collection_order: custom
    sync_mode: sync
```

## AniList UserList — `anilist_userlist` {#anilist-userlist}

Gets anime in AniList User's Anime list. The different sub-attributes are detailed below. 

Both `username` and `list_name` are required.

The `sync_mode: sync` and `collection_order: custom` Setting are recommended since the lists are continuously updated and in a specific order.

| Attribute                                                                                     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|:----------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `username`                                                                                    | **Description:** A user's AniList Username                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `list_name`                                                                                   | **Description:** A user's AniList List Name                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `score.gt` :material-numeric-1-circle:{ data-tooltip data-tooltip-id="tippy-score-filters" }  | **Description:** Only return items that have a score greater than the given number.<br>**Values:** `0.0`-`10.0`                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `score.gte` :material-numeric-1-circle:{ data-tooltip data-tooltip-id="tippy-score-filters" } | **Description:** Only return items that have a score greater than or equal to the given number.<br>**Values:** `0.0`-`10.0`                                                                                                                                                                                                                                                                                                                                                                                                                                                       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         
| `score.lt` :material-numeric-1-circle:{ data-tooltip data-tooltip-id="tippy-score-filters" }  | **Description:** Only return items that have a score less than the given number.<br>**Values:** `0.0`-`10.0`                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          
| `score.lte` :material-numeric-1-circle:{ data-tooltip data-tooltip-id="tippy-score-filters" } | **Description:** Only return items that have a score less than or equal to the given number.<br>**Values:** `0.0`-`10.0`                                                                                                                                                                                                                                                                                                                                                                                                                                                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          
| `sort_by`                                                                                     | **Description:** Sort Order to return<br>**Default:** `score`<br>**Values:**<table class="clearTable"><tr><td>`score`</td><td>Sort by User Score</td></tr><tr><td>`popularity`</td><td>Sort by Popularity</td></tr><tr><td>`status`</td><td>Sort by Status</td></tr><tr><td>`progress`</td><td>Sort by Progress</td></tr><tr><td>`last_updated`</td><td>Sort by Last Updated</td></tr><tr><td>`last_added`</td><td>Sort by Last Added</td></tr><tr><td>`start_date`</td><td>Sort by Start Date</td></tr><tr><td>`completed_date`</td><td>Sort by Completed Date</td></tr></table> |

### Example AniList UserList builder(s) {#example-anilist-userlist-builders}

```yaml
collections:
  Currently Watching Anime:
    anilist_userlist:
      username: Username
      list_name: Watching
      sort_by: score
    collection_order: custom
    sync_mode: sync
```

## More AniList references

- [Advanced search](search.md)
