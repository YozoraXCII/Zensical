# Apple Music and iTunes builders

The Apple Music and iTunes chart builders match ranked chart entries to exact artist and title values in a Plex Music library.

| Builder | Description | Works with Music | Works with Playlists and Custom Sort |
|:--|:--|:--:|:--:|
| [`apple_chart`](#apple-music-and-itunes-charts) | Gets ranked songs or albums from Apple Music country charts | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
| [`itunes_chart`](#apple-music-and-itunes-charts) | Gets ranked songs or albums from iTunes country charts | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |

Both builders accept US, UK, JP, DE, FR, IT, and RU. France, Italy, and Russia use EU chart pages. They default to songs and can use `type: album` for album-level collections. Rows without a positive integer rank for the selected country are skipped. Use `collection_order: custom` to keep the country's chart rank order.

See [Apple Music and iTunes Charts](#apple-music-and-itunes-charts) for configuration examples and source page details.

## Apple Music and iTunes Charts — `apple_chart` {#apple-music-and-itunes-charts}

`apple_chart` and `itunes_chart` build track-level collections from country charts. Use `type: album` to build an album-level collection; the level defaults to tracks for songs and albums for the album chart. Kometa keeps only rows with a positive integer in the selected country's column, sorts those rows by that rank, then matches exact artist and title values in Plex. When multiple track matches exist, the earliest known album release is selected. Unmatched chart items are skipped.

```yaml title="Apple Music collection"
collections:
  UK Apple Songs:
    apple_chart:
      country: UK
    collection_order: custom

  France Apple Albums:
    apple_chart:
      country: FR
      type: album
    collection_order: custom
```

```yaml title="iTunes collection"
collections:
  US iTunes Songs:
    itunes_chart:
      country: US
    collection_order: custom
```

`country` accepts the following codes. France, Italy, and Russia use EU chart pages.

| Shortcode | Country |
|:--|:--|
| US | United States |
| UK | United Kingdom |
| JP | Japan |
| DE | Germany |
| FR | France |
| IT | Italy |
| RU | Russia |

`type` accepts `track`, `song`, or `album` and defaults to `track`. For `apple_chart`, songs use `apple_songs` and albums use `apple_albums`; for `itunes_chart`, songs use `ww`/`eu` and albums use `aww`/`eua`. Set `collection_order: custom` to order Plex matches by the selected country's chart rank.
