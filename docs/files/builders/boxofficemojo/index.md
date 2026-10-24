# BoxOfficeMojo Builders

You can find items using the lists on [boxofficemojo.com](https://www.boxofficemojo.com/) (BoxOfficeMojo). 


| Builder                                | Description                        |             Works with Movies              |             Works with Shows             |    Works with Playlists and Custom Sort    |
|:---------------------------------------|:-----------------------------------|:------------------------------------------:|:----------------------------------------:|:------------------------------------------:|
| [`mojo_domestic`](#boxofficemojo-domestic)           | Uses the Domestic Box Office.      | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .red } | :fontawesome-solid-circle-check:{ .green } |
| [`mojo_international`](#boxofficemojo-international) | Uses the International Box Office. | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .red } | :fontawesome-solid-circle-check:{ .green } |
| [`mojo_world`](#boxofficemojo-worldwide)                 | Uses the Worldwide Box Office.     | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .red } | :fontawesome-solid-circle-check:{ .green } |
| [`mojo_all_time`](#boxofficemojo-all-time)           | Uses the All Time lists.           | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .red } | :fontawesome-solid-circle-check:{ .green } |
| [`mojo_never`](#boxofficemojo-never-hit)                 | Uses the Never Hit lists.          | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .red } | :fontawesome-solid-circle-check:{ .green } |
| [`mojo_record`](#boxofficemojo-other-records)               | Uses other Record lists.           | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .red } | :fontawesome-solid-circle-check:{ .green } |

## BoxOfficeMojo all time — `mojo_all_time` {#boxofficemojo-all-time}

Uses the [All Time Lists](https://www.boxofficemojo.com/charts/overall/) to collect items.

**Builder Attribute:** `mojo_all_time`  

**Builder Value:** Dictionary :material-information-outline:{ data-tooltip data-tooltip-id="tippy-yaml-dictionaries" } of Attributes

### Builder attributes {#builder-attributes}
    
| Attribute               | Description                                                                                                                     |
|-------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| `chart`                 | Determines the chart you want to use.<br>**Allowed Values:** `domestic` or `worldwide`                                          |
| `content_rating_filter` | Determines the content rating chart to use.<br>**Allowed Values:** `g`, `g/pg`, `pg`, `pg-13`, `r`, or `nc-17`                  |
| `limit`                 | The maximum number of results to return.<br>**Default Value:** Returns all results<br>**Allowed Values:** Number greater than 0 |

### Example Mojo all time builder(s) {#example-mojo-all-time-builders}
    
```yaml
collections:

  Top 100 Domestic All Time Grosses:
    mojo_all_time:
      chart: domestic
      limit: 100

  Top 100 Worldwide All Time Grosses:
    mojo_all_time:
      chart: worldwide
      limit: 100

  Top 10 Domestic All Time G Movie Grosses:
    mojo_all_time:
      chart: domestic
      content_rating_filter: g
      limit: 10
```

## BoxOfficeMojo domestic — `mojo_domestic` {#boxofficemojo-domestic}

Uses the Domestic Box Office to collect items.

**Builder Attribute:** `mojo_domestic`  

**Builder Value:** Dictionary :material-information-outline:{ data-tooltip data-tooltip-id="tippy-yaml-dictionaries" } of Attributes

### Builder attributes {#boxofficemojo-domestic-builder-attributes}
    
| Attribute    | Description                                                                                                                                                                                                                           |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `range`      | Determines the type of time range of the Box Office.<br>**Allowed Values:** `daily`, `weekend`, `weekly`, `monthly`, `quarterly`, `yearly`, `season`, or `holiday`                                                                    |
| `year`       | Determines the year of the Box Office. This attribute is ignored for the `daily` range.<br>**Default Value:** `current`<br>**Allowed Values:** Number between 1977 and the current year, `current`, or relative current (`current-#`) |
| `range_data` | Determines the actual time range of the Box Office. The input changes depending on the value of `range`.<br>**Required:** Yes, except for `yearly` range                                                                              |
| `limit`      | The maximum number of results to return.<br>**Default Value:** Returns all results<br>**Allowed Values:** Number greater than 0                                                                                                       |

### Allowed values for `range_data` {#allowed-values-for-range_data}

| Range       | Allowed Values                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|-------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `daily`     | Date in the format `MM-DD-YYYY`, `current`, or relative (`current-#`) where `#` is days before current                                                                                                                                                                                                                                                                                                                                                                                 |
| `weekend`   | Week number (1–53), `current`, or relative (`current-#`) where `#` is days before current                                                                                                                                                                                                                                                                                                                                                                                              |
| `weekly`    | Week number (1–53), `current`, or relative (`current-#`) where `#` is days before current                                                                                                                                                                                                                                                                                                                                                                                              |
| `monthly`   | `january`, `february`, ..., `december`, `current`, or relative (`current-#`) where `#` is days before current                                                                                                                                                                                                                                                                                                                                                                          |
| `quarterly` | `q1`, `q2`, `q3`, `q4`, `current`, or relative (`current-#`) where `#` is days before current                                                                                                                                                                                                                                                                                                                                                                                          |
| `season`    | `winter`, `spring`, `summer`, `fall`, `holiday`, or `current`                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `holiday`   | `new_years_day`, `new_year_weekend`, `mlk_day`, `mlk_day_weekend`, `presidents_day`, `presidents_day_weekend`, `easter`, `easter_weekend`, `memorial_day`, `memorial_day_weekend`, `independence_day`, `independence_day_weekend`, `labor_day`, `labor_day_weekend`, `indigenous_day`, `indigenous_day_weekend`, `halloween`, `thanksgiving`, `thanksgiving_3`, `thanksgiving_4`, `thanksgiving_5`, `post_thanksgiving_weekend`, `christmas_day`, `christmas_weekend`, `new_years_eve` |
    
### Example Mojo domestic builder(s) {#example-mojo-domestic-builders}
    
```yaml
collections:
  Current Domestic Box Office:
    mojo_domestic:
      range: yearly
      year: current

  Last Year's Domestic Box Office:
    mojo_domestic:
      range: yearly
      year: current-1

  Last Month's Top 10 Domestic Box Office:
    mojo_domestic:
      range: monthly
      range_data: current
      year: current-1
      limit: 10
```

## BoxOfficeMojo international — `mojo_international` {#boxofficemojo-international}
    
Uses the International Box Office to collect items.

**Builder Attribute:** `mojo_international`  

**Builder Value:** Dictionary :material-information-outline:{ data-tooltip data-tooltip-id="tippy-yaml-dictionaries" } of Attributes

### Builder attributes {#boxofficemojo-international-builder-attributes}
    
| Attribute    | Description                                                                                                                                                                          |
|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `range`      | Determines the type of time range of the Box Office.<br>**Allowed Values:** `weekend`, `monthly`, `quarterly`, or `yearly`                                                           |
| `chart`      | Determines the chart you want to use.<br>**Default Value:** `international`<br>**Allowed Values:** Item in the dropdown found [here](https://www.boxofficemojo.com/intl/)            |
| `year`       | Determines the year of the Box Office.<br>**Default Value:** `current`<br>**Allowed Values:** Number between 1977 and the current year, `current`, or relative current (`current-#`) |
| `range_data` | Determines the actual time range of the Box Office. Required for all ranges except `yearly`. Input depends on the `range` selected.                                                  |
| `limit`      | The maximum number of results to return.<br>**Default Value:** Returns all results<br>**Allowed Values:** Number greater than 0                                                      |

### Allowed values for `range_data` {#boxofficemojo-international-allowed-values-for-range_data}
    
| Range       | Allowed Values                                                                                                |
|-------------|---------------------------------------------------------------------------------------------------------------|
| `weekend`   | Week number (1–53), `current`, or relative (`current-#`) where `#` is days before current                     |
| `monthly`   | `january`, `february`, ..., `december`, `current`, or relative (`current-#`) where `#` is days before current |
| `quarterly` | `q1`, `q2`, `q3`, `q4`, `current`, or relative (`current-#`) where `#` is days before current                 |
    
### Example Mojo international builder(s) {#example-mojo-international-builders}
    
```yaml
collections:

  Current International Box Office:
    mojo_international:
      range: yearly
      year: current

  Last Year's International Box Office:
    mojo_international:
      range: yearly
      year: current-1

  Last Month's Top 10 German Box Office:
    mojo_international:
      range: monthly
      range_data: current
      chart: germany
      year: current-1
      limit: 10
```

## BoxOfficeMojo never hit" — `mojo_never` {#boxofficemojo-never-hit}

Uses the [Never Hit Lists](https://www.boxofficemojo.com/charts/overall/) (Bottom Section) to collect items.

**Builder Attribute:** `mojo_never`  

**Builder Value:** Dictionary :material-information-outline:{ data-tooltip data-tooltip-id="tippy-yaml-dictionaries" } of Attributes

### Builder attributes {#boxofficemojo-never-hit-builder-attributes}

| Attribute | Description                                                                                                                                   |
|-----------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| `chart`   | Determines the chart you want to use.<br>**Allowed Values:** Item in the dropdown found [here](https://www.boxofficemojo.com/charts/overall/) |
| `never`   | Determines the never filter to use.<br>**Default Value:** `1`<br>**Allowed Values:** `1`, `5`, or `10`                                        |
| `limit`   | The maximum number of results to return.<br>**Default Value:** Returns all results<br>**Allowed Values:** Number greater than 0               |
    
### Example Mojo never hit builder(s) {#example-mojo-never-hit-builders}

```yaml
collections:

  "Top 100 Domestic Never #1":
    mojo_never:
      chart: domestic
      limit: 100

  "Top 100 Domestic Never #10":
    mojo_never:
      chart: domestic
      never: 10
      limit: 100

  "Top 100 German Never #1":
    mojo_never:
      chart: germany
      limit: 100
```

## BoxOfficeMojo other records — `mojo_record` {#boxofficemojo-other-records}

Uses the [Weekend Records](https://www.boxofficemojo.com/charts/weekend/), [Daily Records](https://www.boxofficemojo.com/charts/daily/),
and [Miscellaneous Records](https://www.boxofficemojo.com/charts/misc/) to collect items.

**Builder Attribute:** `mojo_record`

**Builder Value:** Dictionary :material-information-outline:{ data-tooltip data-tooltip-id="tippy-yaml-dictionaries" } of Attributes

### Builder attributes {#boxofficemojo-other-records-builder-attributes}

| Attribute | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|-----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `chart`   | Determines the record you want to use.<br>**Allowed Values:**<br>`second_weekend_drop`, `post_thanksgiving_weekend_drop`, `top_opening_weekend`, `worst_opening_weekend_theater_avg`, `mlk_opening`, `easter_opening`, `memorial_opening`, `labor_opening`, `president_opening`, `thanksgiving_3_opening`, `thanksgiving_5_opening`, `mlk`, `easter`, `4th`, `memorial`, `labor`, `president`, `thanksgiving_3`, `thanksgiving_5`, `january`, `february`, `march`, `april`, `may`, `june`, `july`, `august`, `september`, `october`, `november`, `december`, `spring`, `summer`, `fall`, `holiday_season`, `winter`, `g`, `g/pg`, `pg`, `pg-13`, `r`, `nc-17`, `top_opening_weekend_theater_avg_all`, `top_opening_weekend_theater_avg_wide`, `opening_day`, `single_day_grosses`, `christmas_day_gross`, `new_years_day_gross`, `friday`, `saturday`, `sunday`, `monday`, `tuesday`, `wednesday`, `thursday`, `friday_non_opening`, `saturday_non_opening`, `sunday_non_opening`, `monday_non_opening`, `tuesday_non_opening`, `wednesday_non_opening`, `thursday_non_opening`, `biggest_theater_drop`, `opening_week` |
| `limit`   | The maximum number of results to return.<br>**Default Value:** Returns all results<br>**Allowed Values:** Number greater than 0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |

### Example Mojo other records builder(s) {#example-mojo-other-records-builders}

```yaml
collections:

  Top 10 Biggest Opening Weekends:
    mojo_record:
      chart: top_opening_weekend
      limit: 10

  Top 10 Biggest Opening Day:
    mojo_record:
      chart: opening_day
      limit: 10

  Top 10 Biggest Opening Weeks:
    mojo_record:
      chart: opening_week
      limit: 10
```

## BoxOfficeMojo worldwide — `mojo_world` {#boxofficemojo-worldwide}
    
Uses the [Worldwide Box Office](https://www.boxofficemojo.com/year/world/) to collect items.

**Builder Attribute:** `mojo_world`  

**Builder Value:** Dictionary :material-information-outline:{ data-tooltip data-tooltip-id="tippy-yaml-dictionaries" } of Attributes

### Builder attributes {#boxofficemojo-worldwide-builder-attributes}

| Attribute | Description                                                                                                                                                                                              |
|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `year`    | The year of the [Worldwide Box Office](https://www.boxofficemojo.com/year/world/) to pull.<br>**Allowed Values:** Number between 1977 and the current year, `current`, or relative current (`current-#`) |
| `limit`   | The maximum number of results to return.<br>**Default Value:** Returns all results<br>**Allowed Values:** Number greater than 0                                                                          |

### Example Mojo worldwide builder(s) {#example-mojo-worldwide-builders}
    
```yaml
collections:

  Current Worldwide Box Office:
    mojo_world:
      year: current

  Last Year's Worldwide Box Office:
    mojo_world:
      year: current-1

  2020 Top 10 Worldwide Box Office:
    mojo_world:
      year: 2020
      limit: 10
```
