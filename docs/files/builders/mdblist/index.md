# MDBList builders

You can find items using the features of [MDBList.com](https://mdblist.com/) (MDBList).

| Builder                   | Description                                                               |             Works with Movies              |              Works with Shows              |    Works with Playlists and Custom Sort    |
|:--------------------------|:--------------------------------------------------------------------------|:------------------------------------------:|:------------------------------------------:|:------------------------------------------:|
| [`mdblist_list`](#mdblist-list) | Gets every movie/show in a [MDBList List](https://mdblist.com/toplists/). | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
| [`mdblist_streaming`](#mdblist-streaming) | Gets the JustWatch streaming chart from MDBList. | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-xmark:{ .red } |

## MDBList List — `mdblist_list` {#mdblist-list}


???+ tip "Note on `mdb` sources"

     MDBList is not a live reflection of third-party sites. The data on MDBList is often days, weeks and months out of date as it is only periodically refreshed. As such, the data that Kometa fetches and applies from MDBList may not be the same as you see if you visit those third-party sources directly.
 
Finds every item in a [MDBList List](https://mdblist.com/toplists/).

MDBList episode lists can create episode collections by setting `builder_level: episode`.

The expected input is an MDBList List URL. Multiple values are supported **as a list only**; a comma-separated string will not work.

The `sync_mode: sync` and `collection_order: custom` Setting are recommended since the lists are continuously updated and in a specific order.

???+ tip "Playlist ordering with mixed content"

    When used in a playlist (mixed movie/show library), MDBList calls its **unified** endpoint and
    returns items in the API's response order, preserving any interleaving of movies and shows.
    No grouping by type occurs.

### Sort Options {#sort-options}

For these sorts to be reflected in your collection you **must** use `collection_order: custom`.

| Option                                        | Description                                           |
|:----------------------------------------------|:------------------------------------------------------|
| `rank.asc`<br>`rank.desc`                     | Sort by MDBList Rank                                  |
| `score.asc`<br>`score.desc`                   | Sort by MDBList Score                                 |
| `score_average.asc`<br>`score_average.desc`   | Sort by MDBList Average Score                         |
| `released.asc`<br>`released.desc`             | Sort by Release Date                                  |
| `releasedigital.asc`<br>`releasedigital.desc` | Sort by Digital Release Date                          |
| `imdbrating.asc`<br>`imdbrating.desc`         | Sort by IMDb Rating                                   |
| `imdbvotes.asc`<br>`imdbvotes.desc`           | Sort by IMDb Votes                                    |
| `imdbpopular.asc`<br>`imdbpopular.desc`       | Sort by IMDb Popular                                  |
| `tmdbpopular.asc`<br>`tmdbpopular.desc`       | Sort by TMDb Popular                                  |
| `rogerebert.asc`<br>`rogerebert.desc`         | Sort by RogerEbert Score                              |
| `rtomatoes.asc`<br>`rtomatoes.desc`           | Sort by Rotten Tomatoes Score                         |
| `rtaudience.asc`<br>`rtaudience.desc`         | Sort by Rotten Tomatoes Audience Score                |
| `metacritic.asc`<br>`metacritic.desc`         | Sort by Metacritic Score                              |
| `myanimelist.asc`<br>`myanimelist.desc`       | Sort by MyAnimeList Score                             |
| `letterrating.asc`<br>`letterrating.desc`     | Sort by Letterboxd Rating                             |
| `lettervotes.asc`<br>`lettervotes.desc`       | Sort by Letterboxd Votes                              |
| `last_air_date.asc`<br>`last_air_date.desc`   | Sort by Last Air Date                                 |
| `budget.asc`<br>`budget.desc`                 | Sort by Budget                                        |
| `revenue.asc`<br>`revenue.desc`               | Sort by Revenue                                       |
| `runtime.asc`<br>`runtime.desc`               | Sort by Runtime                                       |
| `title.asc`<br>`title.desc`                   | Sort by Title                                         |
| `sort_title.asc`<br>`sort_title.desc`         | Sort by Sort Title                                    |
| `random.asc`<br>`random.desc`                 | Sort by Random (Randomized Daily)                     |
| `usort.asc`<br>`usort.desc`                   | Sort by User Sort [not available for external lists]  |
| `added.asc`<br>`added.desc`                   | Sort by Date Added [not available for external lists] |

### Example MDBList List Builder(s) {#example-mdblist-list-builders}

```yaml
collections:
  Top Movies of The Week:
    mdblist_list: https://mdblist.com/lists/linaspurinis/top-watched-movies-of-the-week
    collection_order: custom
    sync_mode: sync
```
You can also limit the number of items to search for by using the `limit` and `url` attributes under `mdblist_list`.

```yaml
collections:
  Top 10 Movies of The Week:
    mdblist_list: 
      url: https://mdblist.com/lists/linaspurinis/top-watched-movies-of-the-week
      limit: 10
    collection_order: custom
    sync_mode: sync
```
You can also sort the items by using the `sort_by` and `url` attributes under `mdblist_list`.

If no `sort_by` option is specified, the list will use the sort order saved when the list was created.

```yaml
collections:
  Top 10 Movies of The Week:
    mdblist_list: 
      url: https://mdblist.com/lists/linaspurinis/top-watched-movies-of-the-week
      sort_by: imdbrating.desc
    collection_order: custom
    sync_mode: sync
```

### "External" MDBList(s) {#external-mdblists}

MDBList supports "external lists", which basically mirror a list from another site.  For example, this one:
```
https://mdblist.com/lists/chazlarson/external/2868
```
Which mirrors:
```
https://imdb.com/list/ls089009459
```
These lists can be used with Kometa, **provided** one or the other of these criteria are true:

1. The owner of the MDBList API Key also owns the MDBList external list **OR**
2. The owner of the MDBList external list has **unchecked** the `Make your external lists private` setting in their MDBList account settings.

```yaml
collections:
  Esquire 60 Scariest Movies of All Time:
    mdblist_list: https://mdblist.com/lists/chazlarson/external/2868
    collection_order: custom
    sync_mode: sync
```

## MDBList Streaming — `mdblist_streaming` {#mdblist-streaming}

`mdblist_streaming` builds a collection from MDBList's [JustWatch streaming chart](https://api.mdblist.com/docs/#/Official%20Lists/justwatch_streaming_charts_retrieve). It uses the Plex library type automatically: movie libraries request movie charts and show libraries request show charts.

The builder defaults to the United States (`US`), the daily chart, and all providers and genres. It cannot be used in playlists because a playlist has no single media type. Values are case-insensitive; use either the code or the displayed name.

| Attribute | Description | Default |
|:----------|:------------|:--------|
| `country` | Country code, locale, or name. | `US` / United States |
| `period` | Chart period code or name. | `1` / Daily |
| `provider` | JustWatch provider code or name. | All providers |
| `genre` | JustWatch genre code or name. | All genres |

### Countries {#countries}

| Code | Locale | Name |
|:-----|:-------|:-----|
| `all` |  | All countries |
| `US` | `en_US` | United States |
| `GB` or `UK` | `en_GB` | United Kingdom |
| `CA` | `en_CA` | Canada |
| `AU` | `en_AU` | Australia |
| `DE` | `de_DE` | Germany |

### Periods {#periods}

| Code | Name |
|:-----|:-----|
| `1` or `1d` | Daily |
| `7` or `7d` | Weekly |
| `30` or `30d` | Monthly |

### Providers {#providers}

| Code | Name |
|:-----|:-----|
| `all` | All providers |
| `nfx` | Netflix |
| `amp` | Amazon Prime Video |
| `atp` | Apple TV+ |
| `dnp` | Disney+ |
| `mxx` | Max |
| `hlu` | Hulu |
| `pct` | Peacock Premium |
| `pcp` | Peacock Premium Plus |
| `ppp` | Paramount+ Premium |
| `ppe` | Paramount+ Essential |
| `cru` | Crunchyroll |
| `fuv` | fuboTV |
| `acp` | AMC+ |
| `shd` | Shudder |
| `stz` | Starz |
| `epx` | MGM+ |
| `dpu` | Discovery+ |
| `mbi` | MUBI |
| `crc` | Criterion Channel |
| `act` | Acorn TV |
| `bbo` | BritBox |
| `knp` | Kanopy |
| `rkc` | The Roku Channel |
| `ptv` | Pluto TV |
| `tbv` | Tubi |
| `plx` | Plex |
| `vuf` | Fandango at Home Free |

### Genres {#genres}

| Code | Name |
|:-----|:-----|
| `all` | All genres |
| `act` | Action |
| `ani` | Animation |
| `cmy` | Comedy |
| `crm` | Crime |
| `doc` | Documentary |
| `drm` | Drama |
| `fnt` | Fantasy |
| `hst` | History |
| `hrr` | Horror |
| `rma` | Romance |
| `scf` | Science Fiction |
| `trl` | Thriller |

Use `collection_order: custom` to retain MDBList's chart order.

```yaml
collections:
  Daily Streaming Movies:
    mdblist_streaming: {}
    collection_order: custom
    sync_mode: sync

  Weekly Netflix Action Shows:
    mdblist_streaming:
      country: United Kingdom
      period: 7
      provider: Netflix
      genre: Action
    collection_order: custom
    sync_mode: sync
```
