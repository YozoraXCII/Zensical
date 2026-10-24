# IMDb builders

You can find items using the features of [IMDb.com](https://www.imdb.com/) (IMDb).

| Builder                          | Description                                                                                                           |             Works with Movies              |              Works with Shows              |    Works with Playlists and Custom Sort    |
|:---------------------------------|:----------------------------------------------------------------------------------------------------------------------|:------------------------------------------:|:------------------------------------------:|:------------------------------------------:|
| [`imdb_id`](#imdb-id)               | Gets the movie/show specified.                                                                                        | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
| [`imdb_chart`](#imdb-chart)         | Gets every movie/show in an IMDb Chart like [IMDb Top 250 Movies](https://www.imdb.com/chart/top).                    | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
| [`imdb_search`](search.md)       | Gets every movie/show in an [IMDb Search](https://www.imdb.com/search/title/). Can also be used for Keyword searches. | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
| [`imdb_list`](#imdb-list)           | Gets every movie/show in an IMDb List                                                                                 | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
| [`imdb_watchlist`](#imdb-watchlist) | Gets every movie/show in an IMDb User's Watchlist.                                                                    | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
| [`imdb_award`](#imdb-award)         | Gets every movie/show in an [IMDb Event](https://www.imdb.com/event/).                                                | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |

## IMDb Award — `imdb_award` {#imdb-award}

Finds every item in an [IMDb Event](https://www.imdb.com/event/).

| Award Parameter              | Description                                                                                                                                                                                                                                                                                                                   |
|:-----------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `event_id`                   | Specify the IMDb Event ID to search. **This attribute is required.**<br>**Options:** The ID found in the URLs linked on the [IMDb Events Page](https://www.imdb.com/event/). (ex. `ev0000003`)                                                                                                                                |
| `event_year`<sup>**1**</sup> | Specify the year of the Event to look at. **This attribute is required.**<br>**Options:** `all`, any year, any negative year (ex. `-10` for 10 years ago), list of years, or year range (ex. `2000-2009`,  `2000-current`, or `-30-current` (Last 30 Years)) from the years under the Event History Sidebar on an Event page. |
| `award_filter`               | Filter by the Award heading. Can only accept multiple values as a list.<br>**Options:** Any Black Award heading on an Event Page.                                                                                                                                                                                             |
| `category_filter`            | Filter by the Category heading. Can only accept multiple values as a list.<br>**Options:** Any Gold/Yellow Category heading on an Event Page.                                                                                                                                                                                 |
| `winning`                    | Filter by if the Item Won the award.<br>**Options:** `true`/`false`<br>**Default:** `false`                                                                                                                                                                                                                                   |

???+ example "Example Award and Category Filter"

    In the below example, "Grand Jury Prize" is the award_filter, and "Documentary" is the `category_filter`. You can use both of these filters together.

    ![imdbfilter.png](../../assets/images/files/builders/imdb-award-filters.png)

1. When using multiple years the only available Event IDs are:

```yaml
{%    
  include-markdown "https://raw.githubusercontent.com/Kometa-Team/IMDb-Awards/master/event_ids.yml"
  comments=false
%}
```
### Example IMDb Award Builder(s) {#example-imdb-award-builders}

```yaml
collections:
  Academy Award Winners 2023:
    imdb_award: 
      event_id: ev0000003
      event_year: 2023
      winning: true
```
```yaml
collections:
  Academy Award 2023 Best Picture Nominees:
    imdb_award: 
      event_id: ev0000003
      event_year: 2023
      category_filter: Best Motion Picture of the Year
```

## IMDb Chart — `imdb_chart` {#imdb-chart}

Finds every item in an IMDb Chart.

The expected input are the options below. Multiple values are supported as either a list :material-information-outline:{ data-tooltip data-tooltip-id="tippy-yaml-lists" } or a comma-separated string.

The `sync_mode: sync` and `collection_order: custom` Setting are recommended since the lists are continuously updated and in a specific order.

| Name                                                                                 | Attribute         |             Works with Movies              |              Works with Shows              |
|:-------------------------------------------------------------------------------------|:------------------|:------------------------------------------:|:------------------------------------------:|
| [Box Office](https://www.imdb.com/chart/boxoffice)                                   | `box_office`      | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
| [Most Popular Movies](https://www.imdb.com/chart/moviemeter)                         | `popular_movies`  | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
| [Top 250 Movies](https://www.imdb.com/chart/top)                                     | `top_movies`      | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
| [Top Rated English Movies](https://www.imdb.com/chart/top-english-movies)            | `top_english`     | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
| [Most Popular TV Shows](https://www.imdb.com/chart/tvmeter)                          | `popular_shows`   |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
| [Top 250 TV Shows](https://www.imdb.com/chart/toptv)                                 | `top_shows`       |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
| [Lowest Rated Movies](https://www.imdb.com/chart/bottom)                             | `lowest_rated`    | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
| [Top Rated Indian Movies](https://www.imdb.com/india/top-rated-indian-movies/)       | `top_indian`      | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
| [Top Rated Tamil Movies](https://www.imdb.com/india/top-rated-tamil-movies/)         | `top_tamil`       | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
| [Top Rated Telugu Movies](https://www.imdb.com/india/top-rated-telugu-movies/)       | `top_telugu`      | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
| [Top Rated Malayalam Movies](https://www.imdb.com/india/top-rated-malayalam-movies/) | `top_malayalam`   | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
| [Trending Indian Movies & Shows](https://www.imdb.com/india/upcoming/)               | `trending_india`  | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
| [Trending Tamil Movies](https://www.imdb.com/india/tamil/)                           | `trending_tamil`  | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
| [Trending Telugu Movies](https://www.imdb.com/india/telugu/)                         | `trending_telugu` | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |

### Example IMDb Chart Builder(s) {#example-imdb-chart-builders}

```yaml
collections:
  IMDb Top 250:
    imdb_chart: top_movies
    collection_order: custom
    sync_mode: sync
```

## IMDb ID — `imdb_id` {#imdb-id}

Gets the movie/show specified.

The expected input is an IMDb ID. Multiple values are supported as either a list :material-information-outline:{ data-tooltip data-tooltip-id="tippy-yaml-lists" } or a comma-separated string.

### Example IMDb ID Builder(s) {#example-imdb-id-builders}

```yaml
collections:
  Star Wars (Animated Shows):
    imdb_id: tt0458290, tt2930604
```

## IMDb List — `imdb_list` {#imdb-list}

???+ danger "Important Notice"

    Due to recent changes in IMDb's code, `imdb_list` can no longer be used for any url which starts with 
    `https://www.imdb.com/search/` or `https://www.imdb.com/filmosearch/`.

    These must instead use the [IMDb Search Builder](search.md)


Finds every item in an IMDb List.

| List Parameter | Description                                                                                                                                                                                                                                                                                                                                   |
|:---------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `list_id`      | Specify the IMDb List ID. **This attribute is required.**<br>**Options:** The ID that starts with `ls` found in the URL of the list. (ex. `ls005526372`)                                                                                                                                                                                      |
| `limit`        | Specify how items you want returned by the query.<br>**Options:** Any Integer `0` or greater where `0` get all items.<br>**Default:** `0`                                                                                                                                                                                                     |
| `sort_by`      | Choose from one of the many available sort options.<br>**Options:** `custom.asc`, `custom.desc`, `title.asc`, `title.desc`, `rating.asc`, `rating.desc`, `popularity.asc`, `popularity.desc`, `votes.asc`, `votes.desc`, `release.asc`, `release.desc`, `runtime.asc`, `runtime.desc`, `added.asc`, `added.desc`<br>**Default:** `custom.asc` |

Multiple values are supported as a list only a comma-separated string will not work.

The `sync_mode: sync` and `collection_order: custom` Setting are recommended since the lists are continuously updated and in a specific order.

### Example IMDb List Builder(s) {#example-imdb-list-builders}

```yaml
collections:
  James Bonds:
    imdb_list: 
      list_id: ls006405458
      limit: 100
      sort_by: rating.asc
    collection_order: custom
    sync_mode: sync
```

You can search multiple lists in one collection by using a list.

```yaml
collections:
  Christmas:
    imdb_list:
      - list_id: ls025976544
        limit: 10
        sort_by: rating.asc
      - list_id: ls003863000
        limit: 10
        sort_by: rating.asc
      - list_id: ls027454200
        limit: 10
        sort_by: rating.asc
      - list_id: ls027886673
        limit: 10
        sort_by: rating.asc
      - list_id: ls097998599
        limit: 10
        sort_by: rating.asc
    sync_mode: sync
    collection_order: alpha
```

## IMDb Watchlist — `imdb_watchlist` {#imdb-watchlist}

Finds every item in an IMDb User's Watchlist.

| List Parameter | Description                                                                                                                                                                                                                                                                                                                                   |
|:---------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `user_id`      | Specify the User ID for the IMDb Watchlist. **This attribute is required.**<br>**Options:** The `ur########` ID (legacy format) or the `p.xxxxxxx` ID (new format) found in the URL of the watchlist, or a full watchlist URL. (ex. `ur12345678`, `p.fl6ssgsolkgcctcuxapgh6chsa`, or `https://www.imdb.com/user/p.fl6ssgsolkgcctcuxapgh6chsa/watchlist`) |
| `limit`        | Specify how items you want returned by the query.<br>**Options:** Any Integer `0` or greater where `0` get all items.<br>**Default:** `0`                                                                                                                                                                                                     |
| `sort_by`      | Choose from one of the many available sort options.<br>**Options:** `custom.asc`, `custom.desc`, `title.asc`, `title.desc`, `rating.asc`, `rating.desc`, `popularity.asc`, `popularity.desc`, `votes.asc`, `votes.desc`, `release.asc`, `release.desc`, `runtime.asc`, `runtime.desc`, `added.asc`, `added.desc`<br>**Default:** `custom.asc` |

Multiple values are supported as a list only a comma-separated string will not work.

The `sync_mode: sync` and `collection_order: custom` Setting are recommended since the lists are continuously updated and in a specific order.

### Example IMDb Watchlist Builder(s) {#example-imdb-watchlist-builders}

```yaml
collections:
  My Watch Watchlist:
    imdb_watchlist: 
      user_id: ur64054558
      sort_by: rating.asc
    collection_order: custom
    sync_mode: sync
```

```yaml
collections:
  My Friends Watchlists:
    imdb_watchlist: 
      - user_id: ur64054558
        sort_by: rating.asc
        limit: 100
      - user_id: p.fl6ssgsolkgcctcuxapgh6chsa
        sort_by: rating.asc
        limit: 100
    sync_mode: sync
```

## More IMDb references

- [Advanced search](search.md)
