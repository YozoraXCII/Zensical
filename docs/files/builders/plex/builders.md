# Plex Builders

Plex Builders utilize media that already exists within your Plex library to place them into a Collection.

Plex has two categories of Collections - Smart and Manual. The same search criteria can be used to build a Smart or Manual collection in most instances. 

To keep things simple we will use the term Smart Builders and Manual Builders, which refers to the criteria that is used to build the Collection.

Smart Builders use filters (rules) to build collections that match the criteria of the Builder. When new media is added to your library, or if metadata of any item in your library changes to match the Builder's rules, the media is automatically included in the collection without the need to run Kometa again. 

Manual (also known as Dumb or non-Smart) Builders are static in nature and will not dynamically update as new media is added/metadata criteria changes across your library - you will have to run Kometa any time you want the Builder to re-run.

Smart Builders are usually the recommended approach as they are lightweight and faster to process than Dumb Builders

## Understanding smart vs manual collections

There are some key differences that you should understand before choosing if you want to use a Smart or Manual Builder, this table shows you the key differences between the Collections that are built from each type of Builder.

| Feature                                          | **Smart Collection**                                                                       | **Manual (Dumb) Collection**                                              |
|--------------------------------------------------|--------------------------------------------------------------------------------------------|---------------------------------------------------------------------------|
| Automation                                       | Automatically includes or removes items as your library changes                            | Requires manual updates—items must be added or removed by hand            |
| Use Case                                         | Great for auto-generating groups like “Movies Released This Year” or “Top-Rated Thrillers” | Ideal for curated lists like “My Favorites” or “Family Movie Night Picks” |
| Customization                                    | Built using Plex’s filter system; limited to available filter options                      | Fully customizable—any item from the library can be included              |
| Accuracy                                         | Always reflects real-time library data based on filter criteria                            | Remains the same unless manually edited                                   |
| Icon                                             | Identified with a gear icon in the Plex UI (⚙️)                                            | No special icon—just a standard collection                                |
| Behavior After Library Scan                      | Automatically refreshes based on updated metadata                                          | No change unless edited manually                                          |
| Editing                                          | Filters can be edited to change which items are included                                   | Items must be individually added/removed                                  |
| Metadata Changes (via Refresh or Kometa updates) | Filters remain intact; collection contents may shift as metadata changes                   | Content stays fixed unless explicitly modified by scripts or user         |

There are some exceptions to the above when using a Smart Builder (namely when using a [Smart Label Definition](../../settings.md#smart-label-definitions)), but the above should offer a basic understanding of the key differences.

## Builder attributes

The majority of Smart and Manual Builders utilize the same Builder Attributes. Any deviation from this will be highlighted against the specific Builder.

| Attribute  | Description & Values                                                                                                                                                                                                                               |
|:-----------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `limit`    | **Description:** The max number of item for the filter.<br>**Default:** `all`<br>**Values:** `all` or a number greater than 0                                                                                                                      |
| `sort_by`  | **Description:** This will control how the filter is sorted in your library. You can do a multi-level sort using a list.<br>**Default:** `random`<br>**Values:** Any sort options for your filter type in the [Sorts Options Table](#plex-sort-options) |
| `validate` | **Description:** Determines if a collection will fail on a validation error<br>**Default:** `true`<br>**Values**: `true` or `false`                                                                                                                |

## Plex builder types

| Builder                                    | Description                                                                                                                                                  |             Works with Movies              |              Works with Shows              |    Works with Playlists and Custom Sort    |
|:-------------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------|:------------------------------------------:|:------------------------------------------:|:------------------------------------------:|
| [`smart_filter`](smart-filter.md)          | use Plex's [Advanced Filters](https://support.plex.tv/articles/201273953-collections/) to create a smart collection based on the filter parameters provided. | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
| [`plex_all`](#plex-all)                       | Gets every movie/show in your library. Useful with [Filters](../../filters.md)                                                                               | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
| [`plex_id`](#plex-id)                         | Gets items using Plex metadata IDs or full Plex GUIDs                                                                                                         | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
| [`plex_rating_key`](#plex-rating-key)         | Gets items using numeric Plex rating keys                                                                                                                     | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
| [`plex_search`](search.md)                 | Gets every movie/show based on the search parameters provided                                                                                                | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
| [`plex_watchlist`](#plex-watchlist)           | Gets every movie/show in your Watchlist.                                                                                                                     | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
| [`plex_pilots`](#plex-pilots)                 | Gets the first episode of every show in your library                                                                                                         |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
| [`plex_collectionless`](#plex-collectionless) | Gets every movie/show that is not in a collection                                                                                                            | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |


{%
    include-markdown "./search-options.md"
  start="<!--shared-content-start-->"
%}

{%
    include-markdown "./sort-options.md"
  start="<!--shared-content-start-->"
%}

## Plex all — `plex_all` {#plex-all}

Finds every item in your library. Useful with [Filters](../../filters.md).

The expected input is either true or false.

See the shared [sort options](#plex-sort-options) above.

### Example Plex all builder(s) {#example-plex-all-builders}

```yaml
collections:
  9.0 Movies:
    plex_all: true
    filters:
      user_rating.gte: 9
```

## Plex collectionless — `plex_collectionless` {#plex-collectionless}

**This is not needed if you're using [Smart Label Collections](../../settings.md#smart-label-definitions).**

Finds every item that is not in a collection unless the collection is in the exclusion list. This is a special 
collection type to help keep your library looking correct. When items in your library are in multiple collections it 
can mess up how they're displayed in your library.

For Example, if you have a `Marvel Cinematic Universe` Collection set to `Show this collection and its items` and an 
`Iron Man` Collection set to `Hide items in this collection` what happens is the show overrides the hide, and you end 
up with both the collections and the 3 Iron Man movies all displaying.

Alternatively, if you set the `Marvel Cinematic Universe` Collection to `Hide items in this collection` then movies 
without a collection like `The Incredible Hulk` will be hidden from the library view.

To combat the problem above you set all collections to `Hide items in this collection` then create a collection set to 
`Hide collection` and put every movie that you still want to display in that collection. 

With the variability of collections generated by the Kometa maintaining a collection like this becomes very difficult, 
so in order to automate it, you can use `plex_collectionless`. You just have to tell it what collections to exclude or 
what collection prefixes to exclude.

There are two attributes for `plex_collectionless`:

* `exclude`: Exclude these Collections from being considered for collectionless. 
* `exclude_prefix` Exclude Collections whose title or sort title starts with a prefix from being considered for 
collectionless. 
 
**At least one exclusion is required.**

### Example Plex collectionless builder(s) {#example-plex-collectionless-builders}

```yaml
collections:
  Collectionless:
    plex_collectionless:
      exclude_prefix:
        - "!"
        - "+"
        - "~"
      exclude: 
        - Marvel Cinematic Universe
    sort_title: ~_Collectionless
    collection_order: alpha
    collection_mode: hide
```

* Both `exclude` and `exclude_prefix` can take multiple values as a List.
* This is a known issue with Plex Collection and there is a [Feature Suggestion](https://forums.plex.tv/t/collection-display-issue/305406) detailing the issue more on their 
forms.

## Plex ID — `plex_id` {#plex-id}

The `plex_id` builder finds items already in Plex using their Plex metadata ID. It accepts a single ID or a list of IDs. Each value can be either a bare 24-character metadata ID or a complete `plex://` GUID.

```yaml
collections:
  Selected Plex Movies:
    plex_id:
      - 5d7768243c3c2a001fbca85b
      - plex://movie/5d776824880197001ec901ab
```

For show-part collections, episode GUIDs such as `plex://episode/63e3eedd166819851638a317` are also supported. Values that do not exist in the configured library are skipped with a warning.

This builder does not guarantee that the resulting collection follows the order of the configured IDs.

## Plex pilots — `plex_pilots` {#plex-pilots}

Gets the first episode of every show in your library. This only works with `builder_level: episode`

See the shared [sort options](#plex-sort-options) above.

### Example Plex pilots builder(s) {#example-plex-pilots-builders}

```yaml
collections:
  Pilots:
    builder_level: episode
    plex_pilots: true
```

## Plex rating key — `plex_rating_key` {#plex-rating-key}

The `plex_rating_key` builder finds items already in Plex using their numeric Plex rating key. It accepts a single rating key or a list.

```yaml
collections:
  Selected Plex Movies:
    plex_rating_key:
      - 123
      - 456
```

Rating keys are local to a Plex server and can change if a library is rebuilt. Use [`plex_id`](#plex-id) when a stable Plex metadata identifier is available.

This builder does not guarantee that the resulting collection follows the order of the configured rating keys.

## Plex watchlist — `plex_watchlist` {#plex-watchlist}

Finds every item in your Watchlist.

The expected input is the sort you want returned. It defaults to `added.asc`.

### Watchlist sort options {#watchlist-sort-options}

| Sort Option                                 | Description                                 |
|:--------------------------------------------|:--------------------------------------------|
| `title.asc`<br>`title.desc`                 | Sort by Title                               |
| `release.asc`<br>`release.desc`             | Sort by Release Date (Originally Available) |
| `critic_rating.asc`<br>`critic_rating.desc` | Sort by Critic Rating                       |
| `added.asc`<br>`added.desc`                 | Sort by Date Added to your Watchlist        |

The `sync_mode: sync` and `collection_order: custom` Setting are recommended.

### Example Plex watchlist builder(s) {#example-plex-watchlist-builders}

```yaml
collections:
  My Watchlist:
    plex_watchlist: critic_rating.desc
    collection_order: custom
    sync_mode: sync
```

## More Plex references

- [Search](search.md)
- [Smart filters](smart-filter.md)
