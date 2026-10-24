# Lidarr builders

Lidarr builders create artist collections from artists already tracked in Lidarr. They require a configured Lidarr connection and a Plex music library.

Kometa first matches each Lidarr artist's MusicBrainz artist ID to a Plex `mbid://` GUID. If the ID cannot identify one artist, it accepts an exact, case-insensitive Lidarr artist-name match only when it is unique in Plex. Artists without a unique match are reported as missing and are not added to the collection.

- [All](#lidarr-all) includes every Lidarr artist.
- [Taglist](#lidarr-taglist) includes artists with specified Lidarr tags.

## Lidarr All — `lidarr_all` {#lidarr-all}

`lidarr_all` includes every artist currently tracked in Lidarr.

Kometa matches the Lidarr MusicBrainz artist ID to a Plex artist GUID first. If the ID cannot identify one Plex artist, it uses the Lidarr artist name only when that name matches exactly one Plex artist, ignoring case.

```yaml
collections:
  All Lidarr Artists:
    lidarr_all: true
    sync_mode: sync
```

## Lidarr Taglist — `lidarr_taglist` {#lidarr-taglist}

`lidarr_taglist` includes Lidarr artists that have every supplied tag. Leave the value blank to include untagged artists.

```yaml
collections:
  Kometa Artists:
    lidarr_taglist: kometa, favorites

  Untagged Lidarr Artists:
    lidarr_taglist:
```
