# Last.fm builders

Configure the [service connection](../../../config/lastfm.md) before using these builders.

Choose a builder below. Each section includes its supported inputs and a configuration example.

| Builder reference |
| --- |
| [Last.fm Global Charts Builders](#lastfm-global-charts-builders) |
| [Last.fm Tag Charts Builder](#lastfm-tag-charts-builder) |
| [Last.fm User Loved Tracks Builder](#lastfm-user-loved-tracks-builder) |
| [Last.fm User Recent Tracks Builder](#lastfm-user-recent-tracks-builder) |
| [Last.fm User Tags Builder](#lastfm-user-tags-builder) |
| [Last.fm User Top Albums Builder](#lastfm-user-top-albums-builder) |
| [Last.fm User Top Artists Builder](#lastfm-user-top-artists-builder) |
| [Last.fm User Top Tracks Builder](#lastfm-user-top-tracks-builder) |

## Last.fm Global Charts Builders — `lastfm_chart_top_artists`, `lastfm_chart_top_tracks` {#lastfm-global-charts-builders}

`lastfm_chart_top_artists` and `lastfm_chart_top_tracks` use Last.fm's documented global chart API methods. They require a [Last.fm connection](../../../config/lastfm.md) and default to artist- and track-level collections respectively.

```yaml title="Collection file"
collections:
  Global Top Artists:
    lastfm_chart_top_artists: 50
    collection_order: custom
    sync_mode: sync
  Global Top Tracks:
    lastfm_chart_top_tracks:
      limit: 50
    collection_order: custom
    sync_mode: sync
```

The value is a result limit from 1 through 1000, either directly or as `limit` in a dictionary. `collection_order: custom` preserves order after matching to Plex. Artists use MusicBrainz IDs and unique name matching. Tracks use the [track matching hierarchy](#lastfm-user-top-tracks-builder), including its uncertainty around track versions. Missing items use the usual music reports.

???+ note "API charts and the website"

    These builders use `chart.getTopArtists` and `chart.getTopTracks`. Their rankings may differ from the live [Last.fm charts page](https://www.last.fm/charts). Last.fm does not document API chart methods for that page's **Top New Releases** or **Most Loved** sections, so those sections are not available through these builders.

## Last.fm Tag Charts Builder — `lastfm_tag_charts` {#lastfm-tag-charts-builder}

`lastfm_tag_charts` builds a Plex music collection from Last.fm's top artists, albums, or tracks for a tag. It defaults to artist level. Set `builder_level: album` or `builder_level: track` for the other levels. It requires a [Last.fm connection](../../../config/lastfm.md).

```yaml title="Collection file"
collections:
  Top Dance Tracks:
    builder_level: track
    lastfm_tag_charts:
      tag: dance
      limit: 50
    collection_order: custom
    sync_mode: sync
```

You can use the tag name alone, such as `lastfm_tag_charts: dance`, or a dictionary with `tag` and `limit`. `limit` defaults to 50 and accepts 1–1000. A list of tags or dictionaries combines their results. `collection_order: custom` preserves the order returned by Last.fm. Kometa matches MusicBrainz IDs first, then unique names using the [shared music matching rules](#lastfm-user-top-tracks-builder). Unmatched items use the usual missing artist, album, or track reporting.

## Last.fm User Loved Tracks Builder — `lastfm_user_loved_tracks` {#lastfm-user-loved-tracks-builder}

`lastfm_user_loved_tracks` creates a track-level collection from a user's loved tracks, newest loved first. It defaults to track level and requires a [Last.fm connection](../../../config/lastfm.md).

???+ warning "Track matching can be uncertain"

    Last.fm supplies at most one album for a track, even when that recording appears on several releases, and its album data may be missing or point to a different release from the one in Plex. When a MusicBrainz track ID is unavailable, Kometa relies on the artist, title, and a close duration, then tries that single album. A unique match can still be the wrong version if releases share those details. Check the resulting collection when different recordings or editions matter.

```yaml title="Collection file"
collections:
  My Loved Tracks:
    lastfm_user_loved_tracks:
      username: YOUR_LASTFM_USERNAME
      limit: 50
    collection_order: custom
    sync_mode: sync
```

A username alone selects the latest 50 loved tracks. `limit` accepts 1–1000 and counts Last.fm results before duplicate tracks are removed. `collection_order: custom` preserves newest-first order. The builder uses the same [track matching and missing-item reporting](#lastfm-user-top-tracks-builder) as `lastfm_user_top_tracks`. Last.fm loved tracks may lack a MusicBrainz ID or album, so review the matching warning on that page.

## Last.fm User Recent Tracks Builder — `lastfm_user_recent_tracks` {#lastfm-user-recent-tracks-builder}

`lastfm_user_recent_tracks` creates a track-level collection from a user's recent scrobbles, newest play first. It defaults to track level and requires a [Last.fm connection](../../../config/lastfm.md).

```yaml title="Collection file"
collections:
  Recently Played Tracks:
    lastfm_user_recent_tracks:
      username: YOUR_LASTFM_USERNAME
      limit: 50
    collection_order: custom
    sync_mode: sync
```

A username alone selects the latest 50 completed scrobbles; a currently playing track is excluded. `limit` accepts 1–1000 and counts scrobbles before duplicate tracks are removed. Optional `from` and `to` values are Unix timestamps in seconds (UTC) that restrict the play-time range; `from` must not be later than `to`. `collection_order: custom` preserves newest-first order after duplicates are removed.

The builder uses the same [track matching and missing-item reporting](#lastfm-user-top-tracks-builder) as `lastfm_user_top_tracks`. It tries the album recorded with the scrobble after MusicBrainz ID and duration matching. Review the matching warning on that page if different versions of a track matter.

## Last.fm User Tags Builder — `lastfm_user_tags` {#lastfm-user-tags-builder}

`lastfm_user_tags` builds a Plex music collection from the artists, albums, or tracks a Last.fm user has personally tagged. It defaults to artist level. Set `builder_level: album` or `builder_level: track` for the other levels. It requires a [Last.fm connection](../../../config/lastfm.md).

```yaml title="Collection file"
collections:
  My Tagged Albums:
    builder_level: album
    lastfm_user_tags:
      username: YOUR_LASTFM_USERNAME
      tag: favourites
      limit: 50
    sync_mode: sync
```

Both `username` and `tag` are required. `limit` defaults to 50 and accepts 1–1000. You can supply a list of user/tag dictionaries to combine them. `builder_level` determines whether Kometa requests the user's tagged artists, albums, or tracks; a collection contains one level. Kometa matches MusicBrainz IDs first, then unique names using the [shared music matching rules](#lastfm-user-top-tracks-builder). Unmatched items use the usual missing artist, album, or track reporting.

## Last.fm User Top Albums Builder — `lastfm_user_top_albums` {#lastfm-user-top-albums-builder}

`lastfm_user_top_albums` creates an album-level collection in a Plex music library from a Last.fm user's most-played albums. It defaults to album level; `builder_level: album` is optional. It requires a [Last.fm connection](../../../config/lastfm.md).

```yaml title="Collection file"
collections:
  My Most Played Albums:
    lastfm_user_top_albums:
      username: YOUR_LASTFM_USERNAME
      period: overall
      limit: 50
    collection_order: custom
    sync_mode: sync
```

A username alone selects the overall top 50 albums. You can also supply a list of usernames or dictionaries. `period` accepts `overall`, `7day`, `1month`, `3month`, `6month`, or `12month`; `limit` accepts 1–1000. `collection_order: custom` keeps Last.fm's ranking.

Kometa first matches the Last.fm album MusicBrainz ID against Plex album GUIDs. If the ID has no Plex match or Last.fm supplies no valid ID, Kometa accepts a unique artist and album title match, ignoring case and typographic dash differences. This also handles cases where Last.fm identifies a particular release while Plex identifies its release group. Ambiguous or unmatched albums are skipped and shown under **Missing Albums from Library** when `show_missing` is enabled. With `save_report`, they appear in the library report under **Albums Missing**.

## Last.fm User Top Artists Builder — `lastfm_user_top_artists` {#lastfm-user-top-artists-builder}

`lastfm_user_top_artists` creates an artist collection in a Plex music library from a Last.fm user's most-played artists. It requires a [Last.fm connection](../../../config/lastfm.md). The Last.fm account can be public; no account login is required.

```yaml title="Collection file"
collections:
  My Most Played Artists:
    lastfm_user_top_artists:
      username: YOUR_LASTFM_USERNAME
      period: 1month
      limit: 50
    collection_order: custom
```

A username alone selects the overall top 50 artists. You can also provide a list of usernames or dictionaries to combine charts.

Set `collection_order: custom` to keep the Last.fm ranking in the Plex collection. If multiple charts are provided, artists appear in chart order for each chart, with duplicates included only at their first position.

| Option | Description | Default |
| --- | --- | --- |
| `username` | Last.fm username. | Required |
| `period` | `overall`, `7day`, `1month`, `3month`, `6month`, or `12month`. | `overall` |
| `limit` | Maximum artists from the chart, from 1 to 1000. | `50` |

Kometa first matches a valid MusicBrainz artist ID from Last.fm to the artist's `mbid://` Plex GUID. If the ID has no Plex match or Last.fm supplies no valid ID, it accepts a unique artist-name match, ignoring case and typographic dash differences. Ambiguous matches are skipped. Matching does not require Lidarr. Retrieving MusicBrainz IDs can require a separate Last.fm API call for each chart artist, so large limits take longer.

Unmatched artists appear together under **Missing Artists from Library** when `show_missing` is enabled. With `save_report`, Kometa saves their names and available MusicBrainz IDs in the library report, like missing movies and shows. Ambiguous Plex name matches are marked in the log and skipped.

## Last.fm User Top Tracks Builder — `lastfm_user_top_tracks` {#lastfm-user-top-tracks-builder}

`lastfm_user_top_tracks` creates a track-level collection in a Plex music library from a Last.fm user's most-played tracks. It defaults to track level; `builder_level: track` is optional. It requires a [Last.fm connection](../../../config/lastfm.md).

```yaml title="Collection file"
collections:
  My Most Played Tracks:
    lastfm_user_top_tracks:
      username: YOUR_LASTFM_USERNAME
      period: overall
      limit: 50
    collection_order: custom
    sync_mode: sync
```

A username alone selects the overall top 50 tracks. You can also supply a list of usernames or dictionaries. `period` accepts `overall`, `7day`, `1month`, `3month`, `6month`, or `12month`; `limit` accepts 1–1000. `collection_order: custom` keeps Last.fm's ranking.

Kometa matches a MusicBrainz track ID to a Plex track GUID first. If that does not identify one Plex track, it matches an artist and track title with duration within two seconds, requiring exactly one Plex track. If that fails, it uses the album returned by Last.fm and accepts an artist, album, and track title match only if it is unique in Plex. Name comparisons ignore case and treat typographic dashes like regular hyphens. Last.fm's chart response includes neither album nor duration; track details may omit either. Tracks without enough information or with ambiguous Plex matches are skipped and appear under **Missing Tracks from Library** when `show_missing` is enabled. With `save_report`, they appear in the library report under **Tracks Missing**.
