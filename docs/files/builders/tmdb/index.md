# TMDb builders

You can find items using the features of [TheMovieDb.org](https://www.themoviedb.org/) (TMDb).

## TMDb Standard Builders

| Builder                                                              | Description                                                                                                                                                                                                                                                                                                                   |             Works with Movies              |              Works with Shows              |    Works with Playlists and Custom Sort    |
|:---------------------------------------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:------------------------------------------:|:------------------------------------------:|:------------------------------------------:|
| `tmdb_discover`([movie](discover/movie.md)/[show](discover/show.md)) | Uses [TMDb's Discover Search](https://developer.themoviedb.org/docs/search-and-query-for-details) to find every movie/show based on the [movie search parameters](https://developers.themoviedb.org/3/discover/movie-discover) or [show search parameters](https://developers.themoviedb.org/3/discover/tv-discover) provided | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
| [`tmdb_collection`](#tmdb-collection)                          | Finds every item in the TMDb collection                                                                                                                                                                                                                                                                                       | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |
| [`tmdb_list`](#tmdb-list)                                      | Finds every item in the TMDb List                                                                                                                                                                                                                                                                                             | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
| [`tmdb_movie`](#tmdb-movie)                                    | Finds the movie specified                                                                                                                                                                                                                                                                                                     | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |
| [`tmdb_show`](#tmdb-show)                                      | Finds the show specified                                                                                                                                                                                                                                                                                                      |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
| [`tmdb_company`](#tmdb-company)                                | Finds every item from the TMDb company's movie/show list                                                                                                                                                                                                                                                                      | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
| [`tmdb_network`](#tmdb-network)                                | Finds every item from the TMDb network's show list                                                                                                                                                                                                                                                                            |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
| [`tmdb_keyword`](#tmdb-keyword)                                | Finds every item from the TMDb keyword's movie/show list                                                                                                                                                                                                                                                                      | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |

## TMDb Chart Builders

| Builder                                            | Description                                                                                                                                                     |             Works with Movies              |              Works with Shows              |    Works with Playlists and Custom Sort    |
|:---------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------|:------------------------------------------:|:------------------------------------------:|:------------------------------------------:|
| [`tmdb_popular`](charts.md#tmdb-popular)                 | Finds the movies/shows in TMDb's [Popular Movies](https://www.themoviedb.org/movie)/[Popular Shows](https://www.themoviedb.org/tv) list                         | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
| [`tmdb_now_playing`](charts.md#tmdb-now-playing)         | Finds the movies in TMDb's [Now Playing](https://www.themoviedb.org/movie/now-playing) list                                                                     | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
| [`tmdb_top_rated`](charts.md#tmdb-top-rated)             | Finds the movies/shows in TMDb's [Top Rated Movies](https://www.themoviedb.org/movie/top-rated)/[Top Rated Shows](https://www.themoviedb.org/tv/top-rated) list | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
| [`tmdb_upcoming`](charts.md#tmdb-upcoming)               | Finds the movies in TMDb's [Upcoming Movies](https://www.themoviedb.org/movie/upcoming) list                                                                    | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
| [`tmdb_airing_today`](charts.md#tmdb-airing-today)       | Finds the shows in TMDb's [Airing Today Shows](https://www.themoviedb.org/tv/airing-today) list                                                                 |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
| [`tmdb_on_the_air`](charts.md#tmdb-on-the-air)           | Finds the shows in TMDb's [On TV Shows](https://www.themoviedb.org/tv/on-the-air) list                                                                          |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
| [`tmdb_trending_daily`](charts.md#tmdb-trending-daily)   | Finds the movies/shows in TMDb's Trending Daily list                                                                                                            | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
| [`tmdb_trending_weekly`](charts.md#tmdb-trending-weekly) | Finds the movies/shows in TMDb's Trending Weekly list                                                                                                           | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |


## TMDb People Builders

    ???+ tip "People Collections"
    
        As Plex does not allow People to be part of Collections, Kometa will instead add any media that the person is associated with based om the Builder criteria.
    
        You can not have a Collection of "Top 10 Actors" for example, as Plex does not allow this.

| Builder                               | Description                                            |             Works with Movies              |              Works with Shows              |   Works with Playlists and Custom Sort   |
|:--------------------------------------|:-------------------------------------------------------|:------------------------------------------:|:------------------------------------------:|:----------------------------------------:|
| [`tmdb_actor`](people.md#tmdb-actor)       | Finds every item in the TMDb Person's Actor Credits    | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-xmark:{ .red } |
| [`tmdb_crew`](people.md#tmdb-crew)         | Finds every item in the TMDb Person's Crew Credits     | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-xmark:{ .red } |
| [`tmdb_director`](people.md#tmdb-director) | Finds every item in the TMDb Person's Director Credits | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-xmark:{ .red } |
| [`tmdb_producer`](people.md#tmdb-producer) | Finds every item in the TMDb Person's Producer Credits | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-xmark:{ .red } |
| [`tmdb_writer`](people.md#tmdb-writer)     | Finds every item in the TMDb Person's Writer Credits   | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-xmark:{ .red } |

## TMDb Collection — `tmdb_collection`, `tmdb_collection_details` {#tmdb-collection}

Finds every item in the TMDb collection.

This Builder is expected to have the full URL to the item or the TMDb ID of the item. Multiple values are supported as either a list :material-information-outline:{ data-tooltip data-tooltip-id="tippy-yaml-lists" } or a comma-separated string.

### Example TMDb Collection Builder(s) {#example-tmdb-collection-builders}

```yaml title="Press the + icon to learn more"
collections:
  The Lord of the Rings:
    tmdb_collection: 
        - 121938 #(3)!
  The Hobbit:
    tmdb_collection:  https://www.themoviedb.org/collection/119 
  Middle Earth:
    tmdb_collection_details: #(1)!
      - 119 #(2)!
      - https://www.themoviedb.org/collection/121938
```

1. You can replace `tmdb_collection` with `tmdb_collection_details` if you would like to fetch and use the TMDb collection's summary, poster, and background from the list. 
2. You can specify multiple collections in `tmdb_collection_details` but it will only use the first one to update the collection details.
3. https://www.themoviedb.org/collection/121938-the-hobbit-collection also accepted

* Posters and background in the library's asset directory will be used over the collection details unless `tmdb_poster`/`tmdb_background` is also specified.

## TMDb Company — `tmdb_company` {#tmdb-company}

Finds every movie from the TMDb company's movie list.

This Builder is expected to have the full URL to the item or the TMDb ID of the item. Multiple values are supported as either a list :material-information-outline:{ data-tooltip data-tooltip-id="tippy-yaml-lists" } or a comma-separated string.

### Example TMDb Company Builder(s) {#example-tmdb-company-builders}

```yaml
collections:
  Studio Ghibli:
    tmdb_company: 10342 #(1)!
```

1. https://www.themoviedb.org/company/10342 also accepted

## TMDb Keyword — `tmdb_keyword` {#tmdb-keyword}

Finds every item from the TMDb keyword's movie/show list.

### Example TMDb Keyword Builder(s) {#example-tmdb-keyword-builders}

```yaml
collections:
  Marvel Cinematic Universe:
    tmdb_keyword: 180547 #(1)!
```

1.   https://www.themoviedb.org/keyword/180547 also accepted

## TMDb List — `tmdb_list`, `tmdb_list_details` {#tmdb-list}

Finds every item in the TMDb List.

This Builder is expected to have the full URL to the item or the TMDb ID of the item. Multiple values are supported as either a list :material-information-outline:{ data-tooltip data-tooltip-id="tippy-yaml-lists" } or a comma-separated string.

The `sync_mode: sync` and `collection_order: custom` Setting are recommended since the lists are continuously updated 
and in a specific order. 

### Example TMDb List Builder(s) {#example-tmdb-list-builders}

```yaml title="Press the + icon to learn more"
collections:
  Top 50 Grossing Films of All Time (Worldwide):
    tmdb_list: 10 #(1)!
    collection_order: custom
    sync_mode: sync
  Marvel & DC Universes:
    tmdb_list_details: #(2)!
      - 1 #(3)!
      - 3
    collection_order: custom
    sync_mode: sync
```

1. https://www.themoviedb.org/list/10 also accepted
2. You can replace `tmdb_list` with `tmdb_list_details` if you would like to fetch and use the TMDb collection's summary, poster, and background from the list
3. You can specify multiple lists in `tmdb_list_details` but it will only use the first one to update the collection details

## TMDb Movie — `tmdb_movie`, `tmdb_movie_details` {#tmdb-movie}

Finds the movie specified.

This Builder is expected to have the full URL to the item or the TMDb ID of the item. Multiple values are supported as either a list :material-information-outline:{ data-tooltip data-tooltip-id="tippy-yaml-lists" } or a comma-separated string.

### Example TMDb Movie Builder(s) {#example-tmdb-movie-builders}

```yaml title="Press the + icon to learn more"
collections:
  Anaconda:
    tmdb_movie: #(1)!
      - 336560
  Wizard of Oz & Wicked:
    tmdb_movie_details: #(2)!
      - 630 #(3)!
      - 402431
```

1. You can replace `tmdb_movie` with `tmdb_movie_details` if you would like to fetch and use the TMDb show's summary, poster, and background from the list
2. You can specify multiple shows in `tmdb_movie_details` but it will only use the first one to update the collection details
3. https://www.themoviedb.org/movie/630-the-wizard-of-oz also accepted

* Posters and background in the library's asset directory will be used over the collection details unless `tmdb_poster`/`tmdb_background` is also specified.

## TMDb Network — `tmdb_network` {#tmdb-network}

Finds every item from the TMDb network's movie/show list.

This Builder is expected to have the full URL to the item or the TMDb ID of the item. Multiple values are supported as either a list :material-information-outline:{ data-tooltip data-tooltip-id="tippy-yaml-lists" } or a comma-separated string.

### Example TMDb Network Builder(s) {#example-tmdb-network-builders}

```yaml
collections:
  CBS:
    tmdb_network: 16 #(1)!
```

1.  https://www.themoviedb.org/network/16 also accepted

## TMDb Show — `tmdb_show` {#tmdb-show}

Finds the show specified.

This Builder is expected to have the full URL to the item or the TMDb ID of the item. Multiple values are supported as either a list :material-information-outline:{ data-tooltip data-tooltip-id="tippy-yaml-lists" } or a comma-separated string.

### Example TMDb Show Builder(s) {#example-tmdb-show-builders}

```yaml title="Press the + icon to learn more"
collections:
  Star Wars (Animated Shows):
    tmdb_show:
      - 4194 #(1)!
      - 60554
    Pokémon Evolutions & Chronicles:
      tmdb_show_details: #(2)!
        - 132636 #(3)!
        - 13230
```

1. https://www.themoviedb.org/tv/4194-star-wars-the-clone-wars also accepted
2. You can replace `tmdb_show` with `tmdb_show_details` if you would like to fetch and use the TMDb show's summary, poster, and background from the list
3. You can specify multiple shows in `tmdb_show_details` but it will only use the first one to update the collection details

* Posters and background in the library's asset directory will be used over the collection details unless `tmdb_poster`/`tmdb_background` is also specified.

## More TMDb references

- [Charts](charts.md)
- [People](people.md)
- [Discover movies](discover/movie.md)
- [Discover shows](discover/show.md)
