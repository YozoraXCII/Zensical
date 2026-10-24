# MyAnimeList Charts and Rankings

Choose a builder below. Each section includes its supported inputs and a configuration example.

| Builder reference |
| --- |
| [MyAnimeList Top Airing](#myanimelist-top-airing) |
| [MyAnimeList Top All](#myanimelist-top-all) |
| [MyAnimeList Most Favorited](#myanimelist-most-favorited) |
| [MyAnimeList Top Movies](#myanimelist-top-movies) |
| [MyAnimeList Top OVA Series](#myanimelist-top-ova-series) |
| [MyAnimeList Most Popular](#myanimelist-most-popular) |
| [MyAnimeList Top Specials](#myanimelist-top-specials) |
| [MyAnimeList Top TV Series](#myanimelist-top-tv-series) |
| [MyAnimeList Top Upcoming](#myanimelist-top-upcoming) |

## MyAnimeList top airing — `mal_airing` {#myanimelist-top-airing}

Gets every anime in MyAnimeList's [Top Airing Anime](https://myanimelist.net/topanime.php?type=airing) list. (Maximum: 500)

The expected input value is a single integer value of how many movies/shows to query.

The `sync_mode: sync` and `collection_order: custom` Setting are recommended since the lists are continuously updated and in a specific order. 

???+ warning "MyAnimeList Configuration"

    [Configuring MyAnimeList](../../../config/myanimelist.md) in the config is required for any of these builders to function.

### Example MyAnimeList top airing builder(s) {#example-myanimelist-top-airing-builders}

```yaml
collections:
  Top Airing Anime:
    mal_airing: 10
    collection_order: custom
    sync_mode: sync
```

## MyAnimeList top all — `mal_all` {#myanimelist-top-all}

Gets every anime in MyAnimeList's [Top Airing Anime](https://myanimelist.net/topanime.php?type=airing) list. (Maximum: 500)

The expected input value is a single integer value of how many movies/shows to query.

The `sync_mode: sync` and `collection_order: custom` Setting are recommended since the lists are continuously updated and in a specific order. 

### Example MyAnimeList top all builder(s) {#example-myanimelist-top-all-builders}

```yaml
collections:
  Top All Anime:
    mal_all: 30
    collection_order: custom
    sync_mode: sync
```

## MyAnimeList most favorited — `mal_favorite` {#myanimelist-most-favorited}

Gets every anime in MyAnimeList's [Most Favorited Anime](https://myanimelist.net/topanime.php?type=favorite) list. (Maximum: 500)

The expected input value is a single integer value of how many movies/shows to query.

The `sync_mode: sync` and `collection_order: custom` Setting are recommended since the lists are continuously updated and in a specific order. 

### Example MyAnimeList most favorited builder(s) {#example-myanimelist-most-favorited-builders}

```yaml
collections:
  Most Favorited Anime:
    mal_favorite: 20
    collection_order: custom
    sync_mode: sync
```

## MyAnimeList top movies — `mal_movie` {#myanimelist-top-movies}

Gets every anime in MyAnimeList's [Top Anime Movies](https://myanimelist.net/topanime.php?type=movie) list. (Maximum: 500)

The expected input value is a single integer value of how many movies/shows to query.

The `sync_mode: sync` and `collection_order: custom` Setting are recommended since the lists are continuously updated and in a specific order. 

### Example MyAnimeList top movies builder(s) {#example-myanimelist-top-movies-builders}

```yaml
collections:
  Top Anime Movies:
    mal_movie: 20
    collection_order: custom
    sync_mode: sync
```

## MyAnimeList top OVA series — `mal_ova` {#myanimelist-top-ova-series}

Gets every anime in MyAnimeList's [Top Anime OVA Series](https://myanimelist.net/topanime.php?type=ova) list. (Maximum: 500)

The expected input value is a single integer value of how many movies/shows to query.

The `sync_mode: sync` and `collection_order: custom` Setting are recommended since the lists are continuously updated and in a specific order. 

### Example MyAnimeList top OVA series builder(s) {#example-myanimelist-top-ova-series-builders}

```yaml
collections:
  Top Anime OVA Series:
    mal_ova: 20
    collection_order: custom
    sync_mode: sync
```

## MyAnimeList most popular — `mal_popular` {#myanimelist-most-popular}

Gets every anime in MyAnimeList's [Most Popular Anime](https://myanimelist.net/topanime.php?type=bypopularity) list. (Maximum: 500)

The expected input value is a single integer value of how many movies/shows to query.

The `sync_mode: sync` and `collection_order: custom` Setting are recommended since the lists are continuously updated and in a specific order. 

### Example MyAnimeList most popular builder(s) {#example-myanimelist-most-popular-builders}

```yaml
collections:
  Most Popular Anime:
    mal_popular: 20
    collection_order: custom
    sync_mode: sync
```

## MyAnimeList top specials — `mal_special` {#myanimelist-top-specials}

Gets every anime in MyAnimeList's [Top Anime Specials](https://myanimelist.net/topanime.php?type=special) list. (Maximum: 500)

The expected input value is a single integer value of how many movies/shows to query.

The `sync_mode: sync` and `collection_order: custom` Setting are recommended since the lists are continuously updated and in a specific order. 

### Example MyAnimeList top specials builder(s) {#example-myanimelist-top-specials-builders}

```yaml
collections:
  Top Anime Specials:
    mal_special: 20
    collection_order: custom
    sync_mode: sync
```

## MyAnimeList top TV series — `mal_tv` {#myanimelist-top-tv-series}

Gets every anime in MyAnimeList's [Top Anime TV Series](https://myanimelist.net/topanime.php?type=tv) list. (Maximum: 500)

The expected input value is a single integer value of how many movies/shows to query.

The `sync_mode: sync` and `collection_order: custom` Setting are recommended since the lists are continuously updated and in a specific order. 

### Example MyAnimeList top TV series builder(s) {#example-myanimelist-top-tv-series-builders}

```yaml
collections:
  Top Anime TV Series:
    mal_tv: 20
    collection_order: custom
    sync_mode: sync
```

## MyAnimeList top upcoming — `mal_upcoming` {#myanimelist-top-upcoming}

Gets every anime in MyAnimeList's [Top Upcoming Anime](https://myanimelist.net/topanime.php?type=upcoming) list. (Maximum: 500)

The expected input value is a single integer value of how many movies/shows to query.

The `sync_mode: sync` and `collection_order: custom` Setting are recommended since the lists are continuously updated and in a specific order. 

### Example MyAnimeList top upcoming builder(s) {#example-myanimelist-top-upcoming-builders}

```yaml
collections:
  Top Upcoming Anime:
    mal_upcoming: 10
    collection_order: custom
    sync_mode: sync
```
