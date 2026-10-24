# TMDb People

Choose a builder below. Each section includes its supported inputs and a configuration example.

| Builder reference |
| --- |
| [TMDb Actor](#tmdb-actor) |
| [TMDb Crew](#tmdb-crew) |
| [TMDb Director](#tmdb-director) |
| [TMDb Producer](#tmdb-producer) |
| [TMDb Writer](#tmdb-writer) |

## TMDb actor — `tmdb_actor`, `tmdb_actor_details` {#tmdb-actor}

???+ tip "People Collections"

    As Plex does not allow People to be part of Collections, Kometa will instead add any media that the person is associated with based om the Builder criteria.

    You can not have a Collection of "Top 10 Actors" for example, as Plex does not allow this.

Finds every item in the TMDb Person's Actor Credits.

### Example TMDb actor builder(s) {#example-tmdb-actor-builders}

```yaml title="Press the + icon to learn more"
collections:
  Robin Williams:
    tmdb_actor: 2157 #(1)!
  Hemsworth Brothers:
    tmdb_actor_details: #(2)!
      - 74568 #(3)!
      - 96066
      - 216986
```

1.  https://www.themoviedb.org/person/2157-robin-williams also accepted
2.  You can replace `tmdb_actor` with `tmdb_actor_details` if you would like to fetch and use the TMDb Person's biography and profile from the list
3.  You can specify multiple people in `tmdb_actor_details` but it will only use the first one to update the collection details

## TMDb crew — `tmdb_crew`, `tmdb_crew_details` {#tmdb-crew}

Finds every item in the TMDb Person's Crew Credits.

### Example TMDb crew builder(s) {#example-tmdb-crew-builders}

```yaml title="Press the + icon to learn more"
collections:
  Quentin Tarantino:
    tmdb_crew: 138 #(1)!
  The Skarsgards Family:
    tmdb_crew_details: #(2)!
      - 28846 #(3)!
      - 137905
      - 63764
      - 1640
      - 1281937
      - 2367741
```

1.  https://www.themoviedb.org/person/138-quentin-tarantino also accepted
2.  You can replace `tmdb_crew` with `tmdb_crew_details` if you would like to fetch and use the TMDb Person's biography and profile from the list
3.  You can specify multiple people in `tmdb_crew_details` but it will only use the first one to update the collection details

## TMDb director — `tmdb_director`, `tmdb_director_details` {#tmdb-director}

Finds every item in the TMDb Person's Director Credits.

### Example TMDb director builder(s) {#example-tmdb-director-builders}

```yaml title="Press the + icon to learn more"
collections:
  Steven Spielberg:
    tmdb_director: 488 #(1)!
  The Russo Brothers:
    tmdb_director_details: #(2)!
      - 19271 #(3)!
      - 19272
```

1.  https://www.themoviedb.org/person/488-steven-spielberg also accepted
1.  You can replace `tmdb_director` with `tmdb_director_details` if you would like to fetch and use the TMDb Person's biography and profile from the list
3.  You can specify multiple people in `tmdb_director_details` but it will only use the first one to update the collection details

## TMDb producer — `tmdb_producer`, `tmdb_producer_details` {#tmdb-producer}

Finds every item in the TMDb Person's Producer Credits.

### Example TMDb producer builder(s) {#example-tmdb-producer-builders}

```yaml title="Press the + icon to learn more"
collections:
  Adam Sandler:
    tmdb_producer: 19292 #(3)! 
  The Wachowskis:
    tmdb_producer_details: #(1)!
      - 9339 #(2)!
      - 9340
```

1.  You can replace `tmdb_producer` with `tmdb_producer_details` if you would like to fetch and use the TMDb collection's summary, poster, and background from the list
2.  You can specify multiple producers in `tmdb_producer_details` but it will only use the first one to update the collection details
3.  https://www.themoviedb.org/person/19292-adam-sandler also accepted

## TMDb writer — `tmdb_writer`, `tmdb_writer_details` {#tmdb-writer}

Finds every item in the TMDb Person's Writer Credits.

### Example TMDb writer builder(s) {#example-tmdb-writer-builders}

```yaml title="Press the + icon to learn more"
collections:
  Woody Allen:
    tmdb_writer: 
        - 1243 #(3)!
  The Daniels:
    tmdb_writer_details: #(1)!
      - 1383612 #(2)!
      - https://www.themoviedb.org/person/1317730
```

1.  You can replace `tmdb_writer` with `tmdb_writer_details` if you would like to fetch and use the TMDb collection's summary, poster, and background from the list
2.  You can specify multiple people in `tmdb_writer_details` but it will only use the first one to update the collection details
3.  https://www.themoviedb.org/person/1243-woody-allen also accepted
