# AniDB Builders

You can find anime using the features of [AniDB.net](https://anidb.net/) (AniDB).

| Builder                         | Description                                                                                     |             Works with Movies              |              Works with Shows              |    Works with Playlists and Custom Sort    |
|:--------------------------------|:------------------------------------------------------------------------------------------------|:------------------------------------------:|:------------------------------------------:|:------------------------------------------:|
| [`anidb_id`](#anidb-id)             | Finds the anime specified by the AniDB ID.                                                      | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
| [`anidb_relation`](#anidb-relation) | Finds all anime in the relation graph of the specified AniDB ID.                                | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
| [`anidb_tag`](#anidb-tag)           | Finds anime with a specific AniDB tag ID.                                                        | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
| [`anidb_tag_name`](#anidb-tag-name) | Finds anime with specific AniDB tag names (supports multiple tags).                             | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |

## AniDB ID — `anidb_id` {#anidb-id}

Finds the anime specified by the AniDB ID.

The expected input is an AniDB ID or AniDB Anime URL. Multiple values are supported as either a list :material-information-outline:{ data-tooltip data-tooltip-id="tippy-yaml-lists" } or a comma-separated string.

### Example AniDB ID builder(s) {#example-anidb-id-builders}

```yaml
collections:
  Sword Art Online Shows:
    anidb_id: 8692, 8691, 13494
```
```yaml
collections:
  Sword Art Online Shows:
    anidb_id: 
     - 8692
     - 8691
     - 13494
```
```yaml
collections:
  Sword Art Online Shows:
    anidb_id: https://anidb.net/anime/8692, https://anidb.net/anime/8691, https://anidb.net/anime/13494
```

## AniDB relation — `anidb_relation` {#anidb-relation}

Finds all anime in the relation graph of the specified AniDB ID.

To see the relation graph of an anime use: `https://anidb.net/anime/<ANIDB_ID>/relation/graph` but replace `<ANIDB_ID>` with the AniDB ID you want to see the relations for.

**Value:** The expected input is an AniDB ID, AniDB Anime URL, or AniDB Anime Relation URL. Multiple values are supported as either a list :material-information-outline:{ data-tooltip data-tooltip-id="tippy-yaml-lists" } or a comma-separated string.

### Example AniDB relation builder(s) {#example-anidb-relation-builders}

```yaml
collections:
  All Sword Art Online:
    anidb_relation: 8692
```
```yaml
collections:
  All Sword Art Online:
    anidb_relation: https://anidb.net/anime/8692
```
```yaml
collections:
  All Sword Art Online:
    anidb_relation: https://anidb.net/anime/8692/relation/graph
```

## AniDB tag — `anidb_tag` {#anidb-tag}

Finds anime with a specific AniDB tag ID.

The expected input is an AniDB tag ID with an optional `limit` parameter.

You can find tag IDs by browsing tags at [https://utilities.kometa.wiki/anidb-service/tags](https://utilities.kometa.wiki/anidb-service/tags).

### Example AniDB tag builder(s) {#example-anidb-tag-builders}

```yaml
collections:
  Military Anime:
    anidb_tag: 36
    collection_order: custom
    sync_mode: sync
```
```yaml
collections:
  Top 10 Military Anime:
    anidb_tag:
      tag_id: 36
      limit: 10
    collection_order: custom
    sync_mode: sync
```
```yaml
collections:
  Future Setting:
    anidb_tag:
      tag_id: 2626
      limit: 50
    collection_order: custom
    sync_mode: sync
```

### Tag ID examples {#tag-id-examples}

| Tag Name | Tag ID |
|:---------|-------:|
| Military | 36     |
| Future   | 2626   |
| Comedy   | 2853   |
| Action   | 2604   |
| Fantasy  | 2849   |
| Sci-Fi   | 2846   |

### Attributes {#attributes}

| Attribute | Description                                          | Required |
|:----------|:-----------------------------------------------------|:--------:|
| `tag_id`  | AniDB Tag ID                                         | Yes      |
| `limit`   | Maximum number of anime to return (default: 1000)    | No       |

**Note:** The `mature` setting from your AniDB configuration controls whether mature/adult anime are included in the results.

## AniDB tag name — `anidb_tag_name` {#anidb-tag-name}

Finds anime with specific AniDB tag names. This builder supports multiple tags and searches by tag name (e.g., "action", "comedy") rather than tag ID.

The expected input is either a single tag name, a list of tag names, or a dictionary with `tags` and optional `min_weight` parameters.

Multiple tags can be specified to find anime that match all of the given tags. Tag names are case-insensitive.

### Example AniDB tag name builder(s) {#example-anidb-tag-name-builders}

```yaml
collections:
  Action Anime:
    anidb_tag_name: action
    collection_order: custom
    sync_mode: sync
```
```yaml
collections:
  Action Comedy Anime:
    anidb_tag_name:
      - action
      - comedy
    collection_order: custom
    sync_mode: sync
```
```yaml
collections:
  High-Weight Action Anime:
    anidb_tag_name:
      tags: action
      min_weight: 300
    collection_order: custom
    sync_mode: sync
```
```yaml
collections:
  Action Comedy (High Weight):
    anidb_tag_name:
      tags:
        - action
        - comedy
      min_weight: 400
    collection_order: custom
    sync_mode: sync
```

### Tag weight {#tag-weight}

Tag weights in AniDB indicate how strongly a tag applies to an anime:

- **600+**: Core theme/element
- **400-599**: Significant element
- **200-399**: Notable element  
- **0-199**: Minor element

Using `min_weight` filters results to only include anime where the tag(s) meet the minimum weight threshold.

### Common tag names {#common-tag-names}

| Tag Name      | Description                      |
|:--------------|:---------------------------------|
| action        | Action-oriented content          |
| adventure     | Adventure themes                 |
| comedy        | Comedic content                  |
| drama         | Dramatic storytelling            |
| fantasy       | Fantasy settings/elements        |
| horror        | Horror themes                    |
| mecha         | Giant robots/mechanical themes   |
| military      | Military themes                  |
| mystery       | Mystery/detective themes         |
| romance       | Romantic relationships           |
| sci-fi        | Science fiction themes           |
| slice of life | Everyday life scenarios          |
| sports        | Sports-related content           |
| supernatural  | Supernatural elements            |
| thriller      | Thriller/suspense themes         |

### Attributes {#anidb-tag-name-attributes}

| Attribute    | Description                                          | Required |
|:-------------|:-----------------------------------------------------|:--------:|
| `tags`       | Single tag name or list of tag names                 | Yes      |
| `min_weight` | Minimum tag weight (0-1000, default: 0)              | No       |

**Note:** The `mature` setting from your AniDB configuration controls whether mature/adult anime are included in the results.
