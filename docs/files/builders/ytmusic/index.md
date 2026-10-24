# YouTube Music Builders

Configure the [service connection](../../../config/ytmusic.md) before using these builders.

Choose a builder below. Each section includes its supported inputs and a configuration example.

| Builder reference |
| --- |
| [YouTube Music Dynamic Charts](#youtube-music-dynamic-charts) |
| [YouTube Music List Builder](#youtube-music-list-builder) |
| [YouTube Music Top Artists Builder](#youtube-music-top-artists-builder) |

## YouTube Music dynamic charts — `ytmusic_video_charts`, `ytmusic_genre_charts`, `ytmusic_list` {#youtube-music-dynamic-charts}

Use `dynamic_collections` to create track collections from YouTube Music charts. Kometa creates a collection for each chart available in the selected section and country. No sign-in or YouTube Music setup is needed.

```yaml title="Collection file"
dynamic_collections:
  YouTube Music Genre Charts:
    type: ytmusic_genre_charts
    data:
      country: US
      limit: 50
```

Choose `ytmusic_video_charts` or `ytmusic_genre_charts` for video or genre charts. `data.country` is optional and defaults to worldwide charts; enter a two-letter code such as `US` for a specific country. `data.limit` can cap the number of tracks in each collection. You can also use options such as `include`, `exclude`, `title_format`, and `sync`. To build a collection from one playlist, use its link or ID with [`ytmusic_list`](#youtube-music-list-builder).

For example, `ytmusic_video_charts` can create collections such as “Top 100 Music Videos United States” and “Top 100 Shorts United States.” `ytmusic_genre_charts` can create collections such as “Top 50 Pop Music Videos United States” and “Top 50 Rock Music Videos United States.” The charts shown in YouTube Music may vary from those available to Kometa, and only available charts become collections.

On each run, Kometa logs every genre key as `<playlist ID> | <genre name>`. Use either value in `exclude` to skip a genre:

```yaml
dynamic_collections:
  YouTube Music Genre Charts:
    type: ytmusic_genre_charts
    data:
      country: US
      limit: 50
    exclude:
      - PL4fGSI1pDJn77aK7sAW2AT0oOzo5inWY8 # Pop playlist key
      - Rock # Or exclude by displayed genre name
```

Kometa keeps each chart's track order. It can use the chart description and cover when available; details you set for a collection take priority. Available chart sections and names vary by country.

### Supported countries {#supported-countries}

These country codes are currently available. The list may change, and every chart type may not be available in every country. Use `global` for worldwide charts:

```text
AE, AR, AT, AU, BE, BO, BR, CA, CH, CL, CO, CR, CZ, DE, DK, DO, EC, EE, EG, ES, FI, FR, GB
GT, HK, HN, HU, ID, IE, IL, IN, IS, IT, JP, KE, KR, LU, MX, MY, NG, NI, NL, NO, NZ, PA, PE
PH, PL, PT, PY, RO, RS, RU, SA, SE, SG, SV, TH, TR, TW, TZ, UA, UG, US, UY, VN, ZA, ZW, ZZ
```

## YouTube Music list builder — `ytmusic_list` {#youtube-music-list-builder}

`ytmusic_list` creates a collection from a public YouTube Music playlist. Paste the playlist link, or use its playlist ID. No sign-in or YouTube Music setup is needed for public playlists.

This builder uses the playlist you choose, so it has no country setting. For top artists by country, use [`ytmusic_top_artists`](#youtube-music-top-artists-builder). For chart playlists by country, use [dynamic charts](#youtube-music-dynamic-charts).

```yaml title="Collection file"
collections:
  My YouTube Music Playlist:
    ytmusic_list: https://music.youtube.com/playlist?list=PLC7LNuBoMA-o
    collection_order: custom
    sync_mode: sync
```

You can also provide just the playlist ID, or a list of playlist links and IDs. Set `collection_order: custom` to keep the playlist order. If the same Plex track appears more than once, it is included once at its first position.

To include at most 50 tracks, use `ytmusic_list: {playlist: PLC7LNuBoMA-o, limit: 50}`. Kometa can also use the playlist description and cover when available. Details you set for the collection take priority.

Kometa matches playlist tracks to your Plex library using the artist and track name, and checks the duration and album when available. Tracks it cannot match appear in the missing-tracks log and report. Versions with similar names and lengths may occasionally be confused, so review the collection if the exact recording matters.

## YouTube Music top artists builder — `ytmusic_top_artists` {#youtube-music-top-artists-builder}

`ytmusic_top_artists` creates an artist collection from YouTube Music's top artists chart. You can use worldwide or country-specific charts. No sign-in is needed; see [YouTube Music settings](../../../config/ytmusic.md).

```yaml title="Collection file"
collections:
  Global Top Artists:
    ytmusic_top_artists: true
    collection_order: custom

  US Top Artists:
    ytmusic_top_artists:
      country: US
    collection_order: custom
```

`country` is optional and defaults to `global`. Use a two-letter country code such as `US`, or enter `global`. Set `collection_order: custom` to keep the chart order. Kometa matches artists by name; artists that are missing from Plex or have an ambiguous match appear in the missing-artists report.

### Supported countries {#youtube-music-top-artists-builder-supported-countries}

These country codes are currently available. You can also use `global` for worldwide charts. Availability may change over time:

```text
AE, AR, AT, AU, BE, BO, BR, CA, CH, CL, CO, CR, CZ, DE, DK, DO, EC, EE, EG, ES, FI, FR, GB
GT, HK, HN, HU, ID, IE, IL, IN, IS, IT, JP, KE, KR, LU, MX, MY, NG, NI, NL, NO, NZ, PA, PE
PH, PL, PT, PY, RO, RS, RU, SA, SE, SG, SV, TH, TR, TW, TZ, UA, UG, US, UY, VN, ZA, ZW, ZZ
```
