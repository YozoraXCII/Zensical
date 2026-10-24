---
search:
  boost: 2
---

# Serializd builders

Serializd builders use Serializd's JSON API to find shows. They are available only for show libraries and require [Serializd authentication](../../../config/serializd.md) in the Kometa configuration file.

| Builder | Description |
| ------- | ----------- |
| [`serializd_list`](#serializd-list) | Finds every show in a public Serializd list. |
| [`serializd_watchlist`](#serializd-watchlist) | Finds every show in the authenticated user's or another public user's watchlist. |
| [`serializd_trending`](#serializd-charts) | Finds a limited number of shows from Trending TV Shows. |
| [`serializd_popular`](#serializd-charts) | Finds a limited number of shows from Popular TV Shows. |
| [`serializd_featured`](#serializd-charts) | Finds a limited number of shows from Featured Shows. |

These builders do not scrape Serializd web pages. Private or otherwise API-inaccessible content produces a builder error.

## Serializd Charts — `serializd_trending`, `serializd_popular`, `serializd_featured` {#serializd-charts}

The Serializd chart builders retrieve the homepage's ordered show charts through its JSON API. Each builder value is the maximum number of shows to return.

| Builder | Homepage chart |
| ------- | -------------- |
| `serializd_trending` | Trending TV Shows |
| `serializd_popular` | Popular TV Shows |
| `serializd_featured` | Featured Shows |

```yaml
collections:
  Trending TV Shows:
    serializd_trending: 10
    collection_order: custom
    sync_mode: sync

  Popular TV Shows:
    serializd_popular: 10
    collection_order: custom
    sync_mode: sync

  Featured Shows:
    serializd_featured: 10
    collection_order: custom
    sync_mode: sync
```

The value must be an integer greater than `0`.

## Serializd List — `serializd_list` {#serializd-list}

The `serializd_list` builder finds every show in a public Serializd list.

```yaml
collections:
  Live Action Ranked:
    serializd_list: https://www.serializd.com/list/live-action-ranked-662885
    collection_order: custom
    sync_mode: sync
```

Multiple list URLs can be supplied as a YAML list. Items retain the order returned by Serializd.

## Serializd Watchlist — `serializd_watchlist` {#serializd-watchlist}

The `serializd_watchlist` builder finds every show in a Serializd watchlist using its JSON API.

Use `me` for the account authenticated in `config.yml`:

```yaml
collections:
  My Serializd Watchlist:
    serializd_watchlist: me
    collection_order: custom
    sync_mode: sync
```

Use a username or complete watchlist URL for another public user:

```yaml
collections:
  Someone Else's Watchlist:
    serializd_watchlist: somebodys_username
```

```yaml
collections:
  Noah's Serializd Watchlist:
    serializd_watchlist: https://www.serializd.com/user/somebodys_username/watchlist
```
