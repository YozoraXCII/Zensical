# TMDb Charts

Each chart builder accepts an integer: the number of items to query. Use `sync_mode: sync` and `collection_order: custom` to keep the collection synchronized in chart order. Each section below identifies its supported media and regional options.

| Builder reference |
| --- |
| [TMDb Airing Today](#tmdb-airing-today) |
| [TMDb Now Playing](#tmdb-now-playing) |
| [TMDb On the Air](#tmdb-on-the-air) |
| [TMDb Popular](#tmdb-popular) |
| [TMDb Top Rated](#tmdb-top-rated) |
| [TMDb Trending Daily](#tmdb-trending-daily) |
| [TMDb Trending Weekly](#tmdb-trending-weekly) |
| [TMDb Upcoming](#tmdb-upcoming) |

## TMDb airing today — `tmdb_airing_today` {#tmdb-airing-today}

Finds the shows in TMDb's [Airing Today Shows](https://www.themoviedb.org/tv/airing-today) list.

### Example TMDb airing today builder(s) {#example-tmdb-airing-today-builders}

```yaml
collections:
  TMDb Airing Today:
    tmdb_airing_today: 30
    collection_order: custom
    sync_mode: sync
```

## TMDb now playing — `tmdb_now_playing` {#tmdb-now-playing}

Finds the movies in TMDb's [Now Playing](https://www.themoviedb.org/movie/now-playing) list.

Use `tmdb_region` with this Builder to set the region.

### Example TMDb now playing builder(s) {#example-tmdb-now-playing-builders}

```yaml
collections:
  TMDb Now Playing:
    tmdb_now_playing: 30
    collection_order: custom
    sync_mode: sync
```

## TMDb on the air — `tmdb_on_the_air` {#tmdb-on-the-air}

Finds the shows in TMDb's [On TV Shows](https://www.themoviedb.org/tv/on-the-air) list.

### Example TMDb on the air builder(s) {#example-tmdb-on-the-air-builders}

```yaml
collections:
  TMDb On the Air:
    tmdb_on_the_air: 30
    collection_order: custom
    sync_mode: sync
```

## TMDb popular — `tmdb_popular` {#tmdb-popular}

Finds the movies/shows in TMDb's [Popular Movies](https://www.themoviedb.org/movie)/[Popular Shows](https://www.themoviedb.org/tv) list.

Use `tmdb_region` with this Builder to set the region.

### Example TMDb popular builder(s) {#example-tmdb-popular-builders}

```yaml
collections:
  TMDb Popular:
    tmdb_popular: 30
    collection_order: custom
    sync_mode: sync
```

## TMDb top rated — `tmdb_top_rated` {#tmdb-top-rated}

Finds the movies/shows in TMDb's [Top Rated Movies](https://www.themoviedb.org/movie/top-rated)/[Top Rated Shows](https://www.themoviedb.org/tv/top-rated) list.

Use `tmdb_region` with this Builder to set the region.

### Example TMDb top rated builder(s) {#example-tmdb-top-rated-builders}

```yaml
collections:
  TMDb Top Rated:
    tmdb_top_rated: 30
    collection_order: custom
    sync_mode: sync
```

## TMDb trending daily — `tmdb_trending_daily` {#tmdb-trending-daily}

Finds the movies/shows in TMDb's Trending Daily list.

### Example TMDb trending daily builder(s) {#example-tmdb-trending-daily-builders}

```yaml
collections:
  TMDb Daily Trending:
    tmdb_trending_daily: 30
    collection_order: custom
    sync_mode: sync
```

## TMDb trending weekly — `tmdb_trending_weekly` {#tmdb-trending-weekly}

Finds the movies/shows in TMDb's Trending Weekly list.

### Example TMDb trending weekly builder(s) {#example-tmdb-trending-weekly-builders}

```yaml
collections:
  TMDb Weekly Trending:
    tmdb_trending_weekly: 30
    collection_order: custom
    sync_mode: sync
```

## TMDb upcoming — `tmdb_upcoming` {#tmdb-upcoming}

Finds the movies in TMDb's [Upcoming Movies](https://www.themoviedb.org/movie/upcoming) list.

Use `tmdb_region` with this Builder to set the region.

### Example TMDb upcoming builder(s) {#example-tmdb-upcoming-builders}

```yaml
collections:
  TMDb Upcoming:
    tmdb_upcoming: 30
    collection_order: custom
    sync_mode: sync
```
