---
search:
  boost: 4
---
# Help & Troubleshooting

Find answers to frequently asked questions (FAQ), diagnose errors, update Kometa, undo changes, or migrate from Plex Meta Manager (PMM).

<span id="basic-log-file-troubleshooting"></span>

## Start here

1. Open the latest `meta.log` and note the Kometa version and installation method.
2. Check `[CRITICAL]` messages first, then `[ERROR]` messages and their surrounding context.
3. Use the sections below to identify the cause. If you need help, provide the complete log using the support guidance at the end of this page.


<span id="log-files-and-where-to-find-them"></span>

## Find and read your logs

### Log locations and rotation {#locating-log-files}

The meta.log file can be found within the `logs` folder of your Kometa config folder [right next to `config.yml`].

`meta.log` is the most recent run of Kometa.

As new log files are created, the old ones get a numeric suffix added: `meta-1.log`. **The most recent is always the one without a number at the end.**

`meta-1.log` is the previous run, `meta-2.log` is the run before that, so on and so forth.

???+ info "Old Naming Convention"

    In an older release of Kometa, prevous run logs followed the naming pattern of `meta.log.1`, `meta.log.2` etc. These files can safely be renamed if you no longer require them.

### Checking your version {#checking-kometa-version}

Your installed version appears near the beginning and end of `meta.log`. A `Newest Version` line indicates that an update is available. See [Update Kometa or switch branches](#update-kometa-or-switch-branches).

### Understanding message levels {#understanding-log-file-event-types}

There are five main event types that you need to be aware of when understanding the log files, detailed below:

| Type       | Short Info      | Description                                                              | Recommendation                                                                                        |
|:-----------|:----------------|:-------------------------------------------------------------------------|:------------------------------------------------------------------------------------------------------|
| `INFO`     | Information log | Informational message that does not require much attention               | No action required                                                                                    |
| `DEBUG`    | Debug Log       | Debug log message that does not require much attention                   | No action required                                                                                    |
| `WARNING`  | Warning Log     | Warning message that may require your attention                          | Read the warning and determine if this is something you need to take action on or not                 |
| `ERROR`    | Error Log       | Error message that in MOST cases requires action on your part to resolve | Read the error message, look for the message below and try recommendations                            |
| `CRITICAL` | Critical Log    | Critical message requiring you to fix it for Kometa to run properly      | Read the critical message and take appropriate action. look for message below and try recommendations |

## Fix common problems

<span id="other-troubleshooting-examples"></span>

### Startup and configuration errors

The Log files will contain a great deal of detail about what exactly is happening and why. Generally speaking, if you're having a problem with Kometa the answer will be found here. 
These logs can of course be quite technical, but often the error can be relatively clear:

Something's missing from the format of the file:

```
| Loading Collection File: config/TV Shows.yml                                                       |
|                                                                                                    |
| YAML Error: metadata, collections, or dynamic_collections attribute is required                    |
```

The problem in that case was:

```yaml
templates:
  Collection:
    cache_builders: 30
    sync_mode: sync
    sort_title: ZZZ-<<source>>-<<collection_name>>

collections:   <<< THIS LINE WAS MISSING
  Cached for 30 Days:
    template: {name: Collection, source: Looper}
    summary: ""
    mdblist_list: mdblist_list: https://mdblist.com/lists/stealthgyro/marvel-cinematic-universe-mcu
```

YAML doesn't allow duplicate keys:

```
| Loading Collection File: config/Anime.yml                                                          |
|                                                                                                    |
| YAML Error: while constructing a mapping
|   in "<unicode string>", line 27, column 5:
|         mal_favorite: 50
|         ^ (line: 27)
| found duplicate key "collection_order" with value "custom" (original value: "custom")
|   in "<unicode string>", line 32, column 5:
|         collection_order: custom
|         ^ (line: 32)
```

The problem there was something like this:

```yaml
templates:
  Collection:
    cache_builders: 30
    sync_mode: sync
    sort_title: ZZZ-<<source>>-<<collection_name>>

collections:   <<< THIS LINE WAS MISSING
  Cached for 30 Days:
    template: {name: Collection, source: Looper}
    collection_order: custom                         <<<<  THIS KEY
    summary: ""
    collection_order: custom                         <<<<  DUPLICATED HERE
    mdblist_list: mdblist_list: https://mdblist.com/lists/stealthgyro/marvel-cinematic-universe-mcu
```

File is not where Kometa expects it:

```
| Loading Collection File: config/Movies.yml                                              |
| YAML Error: File Error: File does not exist /Users/Lucky/Kometa/config/Movies.yml       |
```

### Connection and authentication problems

Confirm the connection details for the service named in the error. See [Service connections](../config/plex.md). For MyAnimeList, use [Kometa Utilities Authentication](../config/authentication.md).

### Common log messages {#common-log-file-messages}

This section aims to explain some commonly seen event messages that are produced in the logs.

#### CRITICAL

This table details examples of the most commonly-seen `[CRITICAL]` events and what they mean for the user.

<table>
    <thead>
        <th>Type</th>
        <th>Short Info</th>
    </thead>
    <tr>
        <td><code>CRITICAL</code></td>
        <td><code>Failed to Connect to https://api.themoviedb.org/</code></td>
    </tr>
    <tr>
        <td colspan="2"><strong>Description:</strong> Current step Kometa was on made an API call to TMDb, but it aborted and moved on<br><strong>Recommendation:</strong> Determine if TMDb was offline and not replying to API requests. Try again and see if it fails again or not.</td>
    </tr>
</table>

#### ERROR

This table details examples of the most commonly-seen `[ERROR]` events and what they mean for the user.

<table>
    <thead>
        <th>Type</th>
        <th>Short Info</th>
    </thead>
	<tr>
		<td><code>ERROR</code></td>
		<td><code>Playlist Error: Library: XYZ not defined</code></td>
	</tr>
	<tr>
		<td colspan="2"><strong>Description:</strong> Plex library XYZ is not found<br><strong>Recommendation:</strong> Ensure that your config file has defined the proper library name as found in Plex</td>
	</tr>
	<tr>
		<td><code>ERROR</code></td>
		<td><code>Plex Error: resolution: No matches found with regex pattern XYZ</code></td>
	</tr>
	<tr>
		<td colspan="2"><strong>Description:</strong> While looking for a pattern in Plex, this one was not found<br><strong>Recommendation:</strong> This may be normal and require 0 actions. However, if you expect that Plex should have returned records, check the pattern to ensure it is working properly</td>
	</tr>
	<tr>
		<td><code>ERROR</code></td>
		<td><code>Plex Error: No Items found in Plex</code></td>
	</tr>
	<tr>
		<td colspan="2"><strong>Description:</strong> While using the Kometa Builder, no items with that criteria were returned from Plex<br><strong>Recommendation:</strong> This may be normal and require 0 actions. However, if you expect that Plex should have returned records, check the Builder to ensure it is working properly</td>
	</tr>
	<tr>
		<td><code>ERROR</code></td>
		<td><code>IMDb Error: Failed to parse URL:</code></td>
	</tr>
	<tr>
		<td colspan="2"><strong>Description:</strong> While using the Kometa Builder, url does not exist<br><strong>Recommendation:</strong> This may be normal and require 0 actions. However, if you expect that the URL should have returned records, check the url in your browser to ensure it is working properly</td>
	</tr>
	<tr>
		<td><code>ERROR</code></td>
		<td><code>MDBList Error: No TVDb ID found for Nightfall (2022)</code></td>
	</tr>
	<tr>
		<td colspan="2"><strong>Description:</strong> Online sources are missing information<br><strong>Recommendation:</strong> These sorts of errors indicate that the thing can't be cross-referenced between sites.</br>For example, at the time of that error, the MDBList record for "Nightfall (2022)" didn't contain a TVDb ID.</br>This could be because the record just hasn't been updated, or because "Nightfall (2022)" is not listed on TVDb.</br>The fix is for someone [like you, perhaps] to go to the relevant site and fill in the missing data.</td>
	</tr>
	<tr>
		<td><code>ERROR</code></td>
		<td><code>MDBList Error: Not Found</code></td>
	</tr>
	<tr>
		<td colspan="2"><strong>Description:</strong> Online sources are missing information<br><strong>Recommendation:</strong> These sorts of errors indicate that the thing can't be cross-referenced between sites. For example, at the time of that error, the MDBList record was trying to get a rating for a media item and could not find it.</td>
	</tr>
	<tr>
		<td><code>ERROR</code></td>
		<td><code>Plex Error: actor: Mel B not found</code></td>
	</tr>
	<tr>
		<td colspan="2"><strong>Description:</strong> Actor not found and hence unable to create the collection<br><strong>Recommendation:</strong> Report error in #kometa-help channel and see if there is a fix.</td>
	</tr>
	<tr>
		<td><code>ERROR</code></td>
		<td><code>Input Failed</code></td>
	</tr>
	<tr>
		<td colspan="2"><strong>Description:</strong> A token or password is no longer valid for an online source of information<br><strong>Recommendation:</strong> Review the meta.log for more information</td>
	</tr>
	<tr>
		<td colspan="2"><strong>Description:</strong> You are using a builder that has not been configured yet.<br><strong>Recommendation:</strong> Review the meta.log for more information on what went wrong. Refer to the wiki for details on how to set this up</td>
	</tr>
</table>

#### WARNING

This table details examples of the most commonly-seen `[WARNING]` events and what they mean for the user.

<table>
	<thead>
		<th>Type</th>
		<th>Short Info</th>
	</thead>
	<tr>
		<td><code>WARNING</code></td>
		<td><code>Convert Warning: No TVDb ID Found for TMDb ID: 15733</code></td>
	</tr>
	<tr>
		<td colspan="2"><strong>Description:</strong> Online sources are missing information<br><strong>Recommendation:</strong> These sorts of errors indicate that the thing can't be cross-referenced between sites. For example, at the time of that error, the TMDb record for "The Two Mrs. Grenvilles" [ID 15733] didn't contain a TVDb ID. This could be because the record just hasn't been updated, or because "The Two Mrs. Grenvilles" is not listed on TVDB. The fix is for someone [like you, perhaps] to go to the relevant site and fill in the missing data.</td>
	</tr>
	<tr>
		<td><code>WARNING</code></td>
		<td><code>Convert Warning: AniDB ID not found for AniList ID: 21400</code></td>
	</tr>
	<tr>
		<td colspan="2"><strong>Description:</strong> Online sources are missing information<br><strong>Recommendation:</strong> These sorts of errors indicate that the thing can't be cross-referenced between sites. The fix is for someone [like you, perhaps] to go to the relevant site and fill in the missing data.</td>
	</tr>
	<tr>
		<td><code>WARNING</code></td>
		<td><code>Convert Warning: No TVDb ID or IMDb ID found for AniDB ID: 14719</code></td>
	</tr>
	<tr>
		<td colspan="2"><strong>Description:</strong> Online sources are missing information<br><strong>Recommendation:</strong> These sorts of errors indicate that the thing can't be cross-referenced between sites. The fix is for someone [like you, perhaps] to go to the relevant site and fill in the missing data.</td>
	</tr>
	<tr>
		<td><code>WARNING</code></td>
		<td><code>Convert Warning: AniDB ID not found for MyAnimeList ID: 36838</code></td>
	</tr>
	<tr>
		<td colspan="2"><strong>Description:</strong> Online sources are missing information<br><strong>Recommendation:</strong> These sorts of errors indicate that the thing can't be cross-referenced between sites. The fix is for someone [like you, perhaps] to go to the relevant site and fill in the missing data.</td>
	</tr>
</table>
#### INFO

This table details examples of the most commonly-seen `[INFO]` events and what they mean for the user.

<table>
	<thead>
		<th>Type</th>
		<th>Short Info</th>
	</thead>
	<tr>
		<td><code>INFO</code></td>
		<td><code>Detail: TMDb_person updated poster to [URL]</code></td>
	</tr>
	<tr>
		<td colspan="2"><strong>Description:</strong> Person image was downloaded from TMDb<br><strong>Recommendation:</strong> May require you to update the people poster image to your style or request it in the style of the Kometa defaults people posters</td>
	</tr>
</table>

### Plex errors and image uploads

A 500 Internal Server Error happens when the server has an unexpected error when responding to an API request.

There could be any number of reasons why this happens and it depends on what server Kometa is talking to although it's most likely coming from your Plex Server.

Most of the time these errors need to be resolved by changing something specific to your set up but some do come up that can be fixed 
(i.e. Plex throws one if you upload a photo larger than 10 MB)

Many Appbox Setups will throw this error when too many requests are sent, or if the central metadata repository 
is not properly configured to allow users to upload custom posters.

Take a look at the following logs:

:one: Settings | Manage | Console -> then filter on Error and Warning to see what might be going on

:two: Check the plex logs (container or other) for the "Busy DB Sleeping for 200ms)

There is nothing that Kometa or our support staff can really do to resolve a 500 error.

#### Temporary Plex image upload errors

Kometa retries poster, background, logo, and square-art uploads when Plex returns HTTP 502, 503, or 504. It makes at most three upload attempts, waiting 2 seconds before the second attempt and 5 seconds before the third. If all three attempts receive these errors, Kometa logs the item, image, and final HTTP status, skips that image update, and continues the run without a traceback. This also applies to artwork resets, overlay application, and overlay removal. Failed overlay removal keeps the overlay label and original poster backup so removal can be retried. Retry messages identify the item and image.

A gateway error does not establish that the image is missing. URL uploads still make these three attempts even if the source URL is permanently broken; this can add 7 seconds for that image on each run. Failed uploads are not cached as successes. Source URL validation and fallback are separate from these Plex retries. Other errors retain their existing handling and diagnostic details.

### Source integrity

Source integrity is checked alongside the startup system information, with a maximum wait of 30 seconds for both cached file checking and baseline retrieval. The log reports `Source Integrity: Verified`, `Source Integrity: MODIFIED`, or `Source Integrity: Check unavailable` with a reason and an explanation that local files were not verified. If the startup time limit is reached, Kometa continues with `Source Integrity: Check unavailable (startup time limit reached; local files were not verified)`. There is no later integrity result during library processing. The end-of-run `Source Integrity Summary (startup check)` repeats the startup result without waiting for or adopting a late result. A timeout in this summary describes the startup check, not a detected file change. Modified installations list changed, missing, and added files. An unavailable check means the comparison could not be completed; it does not indicate detected file changes. Only `MODIFIED` reports confirmed differences. This is a support diagnostic and never prevents Kometa from running.

The diagnostic is enabled by default. Use `--no-source-integrity` or set `KOMETA_SOURCE_INTEGRITY=false` to disable it, including file checks and network requests. Use `--source-integrity` or `KOMETA_SOURCE_INTEGRITY=true` to enable it. As with other runtime options, environment variables take precedence over CLI flags. Disabled checks report `Source Integrity: Disabled (source-integrity option)` in the startup header and end-of-run summary.

The baseline comes from official upstream source pinned to the installed commit. It is cached under `.source-integrity/` in the active config directory for subsequent offline checks. After a new cache is successfully saved, Kometa retains it and the two most recently written other caches for the same repository and installation profile. This limits storage growth while allowing installations at different commits to share a config directory without evicting each other on every update. Downloads use temporary disk files. Upstream retrieval has a separate 180-second deadline, so a slow download can continue after the 30-second startup wait. If the process remains running and retrieval completes within that deadline, the worker can silently save the baseline for a later run; it does not log another result or change the startup result repeated in the summary. Scheduled starts for the same installation, config directory, and profile reuse an active check rather than launching another download. Each start still has its own 30-second wait and saved startup result. The worker is a daemon: if Kometa exits before retrieval completes, no baseline is saved and the next run retries.

Runtime config, logs, virtual environments, compiled Python files, desktop metadata, and integrity metadata are excluded. Differences consisting only of Windows versus Unix line endings are tolerated in known text files; binary files require exact bytes. Docker checks Kometa-owned files and directories rather than the container operating system. Repository-only CI/test files excluded from upstream source archives are outside the comparison.

Git installs use the installation's HEAD; Docker builds carry `KOMETA_GIT_SHA` when provided; `.kometa_sha` is an identity hint when present. The candidate commit must belong to an official upstream branch before a baseline is cached. PR and test images whose commits are outside official upstream history report Check unavailable. Older images or installations without exact commit metadata also report Check unavailable; recreate the container with an image containing that metadata. Cache corruption, unavailable upstream data, and inspection errors report Check unavailable. The diagnostic cannot protect against deliberate replacement of its own implementation or provenance metadata.

## Performance and scheduling

### Improving performance

Enable [Kometa caching](../config/settings.md) where appropriate and schedule runs outside Plex scheduled maintenance. Limit expensive operations and episode overlays to the libraries that need them.

### Slow runs

Every time an item (media, collection, overlay) needs to be updated, Kometa needs to send the request to Plex, and then receive confirmation back from Plex 
that the action has been completed. This can take anywhere from seconds to minutes depending on when Plex provides a response. Given that the typical run can 
update hundreds or even thousands of items, this can quickly add up to a lot of time. If "Mass Update" operations are used, then every single item in the library
needs to go through this process, which can be lengthy. 

Overlays can be particularly cumbersome as Kometa needs to perform the following actions for each of the items that need to have an overlay applied:

- Check which overlays are applicable (this will take more time depending on how many overlays you are applying)
    - Compare the current poster to confirm what overlays are already applied, if changes are needed then continue with the following steps
    - Grab source image from Plex and save it to disk
    - Draw each overlay image on top of the source image
    - save final image to disk
    - Tell Plex to apply new image to the item
    - Wait for Plex to respond confirming that the change has been made

The above two points can be greatly exacerbated if Kometa has to update every episode within a Show library rather than just the Shows themselves, 
as there can often be hundreds of thousands of episodes to be updated with mass operations or overlays.

Additionally, some collections require a lot of computing resources to determine the critera of the collections that are to be made. This is commonly seen in the Defaults 
files for Actor/Director/Producer/Writer which need to get the crew information for each of the movies/shows within your library, and then calculate which ones appear the
most to find out which are the most popular. The larger your library, the longer this process will take.

### Scheduling different tasks

Yes, the recommended approach is to set up a new library for the Operations/Overlays, mapping it back to the original library, 
and then scheduling the library, as outlined below

```yaml
libraries:
  Movie Operations:           # NAME DOESN'T MATTER BUT MUST BE UNIQUE
    library_name: Movies      # THIS MUST MATCH A LIBRARY IN PLEX
    schedule: weekly(monday)
    operations:
      split_duplicates: true
    overlay_files:
      - default: resolution
```

See [Scheduling runs](guides/scheduling.md) and [Schedule syntax](../config/schedule.md) for the complete procedure.

## Update Kometa or switch branches

Back up your configuration before updating. For a local Git installation, inspect `git status` and preserve any local changes before pulling updates or switching branches. Do not discard a stash or reset modified files as a routine update step.

- **Local installation:** follow the update and branch-switching instructions in the [local walkthrough](install/index.md#path-local). Use `master` for stable releases or `develop` for the public beta, and install the dependencies required by that checkout in its virtual environment.
- **Docker:** pull the desired `kometateam/kometa` image and recreate the container while retaining the configuration volume. Use `latest` for stable releases or `develop` for the public beta. Follow the [Docker walkthrough](install/index.md#path-docker) or your platform's walkthrough; see [Docker images](install/images.md) for available tags.
- **Downloaded archive:** follow the local installation instructions for the new release and retain your configuration and asset files.


## Undo changes and recover


There is no global "undo everything Kometa ever did" *after the fact* since no history is kept.

The only "totally undo everything Kometa has ever done to this Plex server" process is to restore your Plex appdata from the backup you took prior to using Kometa. 

### Collections

You can delete the collections that Kometa has created either by telling Kometa to do so or manually in the UI.

If Kometa has deleted collections that you created outside of Kometa [something you would have explicitly told it to do], they cannot be restored.

### Playlists

You can delete the playlists that Kometa created manually in the UI.

### Overlays

You can tell Kometa to remove overlays, which will restore the clean posters that the overlays were applied to.

### Metadata

If you have not created a metadata backup in advance, there is probably no way to restore things that Kometa has changed.

Kometa can make a [metadata backup](../config/operations.md#mass-metadata-update) for you. This backup is a YAML file that contains things like ratings, titles, summaries, etc. 
You can use this backup to revert changes that Kometa has made.

Chazlarson has created a [metadata backup script](https://github.com/chazlarson/Media-Scripts/blob/main/Kometa/README.md#metadata-extractorpy) that backs up more metadata than Kometa does, 
including artwork. This script can be used to create a backup that can be used to revert changes that Kometa has made.

Both of these backups are only useful if you have created them before you need them.

The remarks that follow apply in the absence of a metadata backup.

#### Posters and backgrounds

If you have used Kometa to set artwork based on URLs or local files, there is no way to restore what was there before Kometa changed it. No history of what was there before is kept.

#### Mass updates

If you have made mass updates to things like genres, ratings, and the like, what was there before is gone for good *unless* what was there is the default Plex value. 
You can generally use Kometa to reset those values and let Plex fill them back in.

This is not always the case, however. If you had assigned user ratings to everything prior to using Kometa and then you told 
Kometa to update the user rating with some other rating [say TMDB or the like], all your user ratings are lost with no backup.

#### Other metadata

If you have used Kometa to change titles, summaries, years, artwork, etc. with a Metadata File[all things you would have explicitly told it to do] 
there is no way to restore what was there before Kometa changed it.

## Migration and older configurations

These notes describe historical changes. Follow them only when migrating an older working configuration, then check the current reference for supported settings.

### Plex meta manager → Kometa

??? info "Historical PMM migration instructions"

    You're using Plex-Meta-Manager now and need to switch to Kometa? Here's what you have to do:

    ???+ danger "Important"

        These instructions are assuming that your existing config file is working with a recent [say 1.19 or newer] pre-rebrand Plex-Meta-Manager release.

    #### If you are using Git:

    1. cd into the directory where you installed Plex-Meta-Manager
    2. retrieve the new code and reinstall requirements [see below for commands]. This is the same thing you'd do with any upgrade.
    3. change `plex_meta_manager.py` in any run command you use to `kometa.py`. For example: `python kometa.py --run`.
    4. You're done.

    Before updating, preserve any changes reported by `git status`; do not discard them. The commands for step 2 are:

    ```
        git status
        git pull
        # activate your venv here if you use one and it is not already active
        python -m pip install -r requirements.txt
    ```

    #### If you are using Docker:

    1. change the image you are using from `meisnate12/plex-meta-manager:SOME_TAG` to `kometateam/kometa`, 
    You'll change this wherever it's specified in your situation, a `docker run` command, a docker compose file, some field in a NAS UI, wherever.
    2. If needed, rebuild the container however that happens in your context. `docker compose up -d`, clicking a button, whatever.
    3. You're done.

    #### If you downloaded it as a zip file:

    1. uncompress the zip file
    2. cd into that directory and do the same setup you did initially (create a virtual environment, maybe, then install requirements. 
    There's no way for us to know what you did when you set it up, so we can't give more specific instructions than that)
    3. copy the config directory from your Plex-Meta-Manager dir into this directory.
    4. change `plex_meta_manager.py` in any run command you use to `kometa.py`. For example: `python kometa.py --run`.
    5. You're done.

    #### Other things you can do if you wish:

    Neither of these two things are required.

    1. change `- pmm:` in the `config.yml` file to `- default:`; the docs now use `- default:`, but either will work for the foreseeable future, 
    so you do not **need** to do this. You may *want* to, and if so go ahead, but you do not *have* to.
    2. change the name of any directories you are using to "kometa". The app does not care about that part of the path. It only cares about the contents of the config directory, but it can be 
    located anywhere. You do not **have* to change `/some/path/to/Plex-Meta-Manager` to `/some/path/to/Kometa`. Again, you may *want* to, and if so go ahead, but you do not *have* to.

    For example, this:

    ```yaml
    libraries:
      Movies:
        remove_overlays: false
        collection_files:
          - pmm: basic
          - pmm: imdb
    ```

    Could, but does not have to, become:

    ```yaml
    libraries:
      Movies:
        remove_overlays: false
        collection_files:
          - default: basic
          - default: imdb
    ```

### Removed services and builders

In September 2026, Trakt blocked API access for third-party services including MDBList and SIMKL with no prior notice.

Trakt's new draft API Use Policy also prohibits using Trakt as an upstream data provider for another service and continuously synchronizing Trakt account data into a separate tracking or list platform. The restrictions were introduced with little or no advance notice to affected services. [Trakt API discussion](https://github.com/trakt/trakt-api/issues/933) · [Proposed API Use Policy](https://github.com/trakt/trakt-api/pull/941)

In light of the above, and following a pattern of changes by Trakt (which you can read about [here](https://www.reddit.com/r/Simkl/comments/1wjv7i1/the_end_of_trakt_as_we_know_it_trakt_has/)), Kometa has decided to remove Trakt support in version 2.4.9. This includes the Trakt connection, builders, collection and playlist synchronization, artwork, ratings, operations, overlays, defaults, and related configuration attributes.

Kometa logs the following error when it finds Trakt configuration and continues with the rest of the run:

> Trakt is no longer supported, please see the Announcements channel in the Kometa Discord server for further information

We suggest users remove Trakt from configuration files and instead use supported alternatives such as TMDb, IMDb, MDBList, SIMKL, FlickList, and other available builders where appropriate.

### Legacy file and overlay settings

With the release of Kometa 1.20, several changes have been made. Please read the document below thoroughly!

??? blank "`metadata_path` and `overlay_path` are now legacy attributes (Click to Expand).<a class="headerlink" href="#metadata-overlay-path" title="Permanent link">¶</a>"

    <div id="metadata-overlay-path" />

    The attributes `metadata_path` and `overlay_path` are now legacy, and will likely produce an error `metadata attribute is required` when running Kometa.

    We have new attributes: `collection_files`, `overlay_files` and `metadata_files` which you can read more about on the 
    [Libraries Attributes page](../config/libraries.md#attributes)

    Whilst this error can be ignored, we strongly advise you to move over to the new attributes, which can be done following this guidance:

    :fontawesome-solid-1: If your YAML file creates collections or is a Kometa Defaults Collection File then it belongs under `collection_files`. 
    
    :fontawesome-solid-2: If your YAML file creates overlays or is a Kometa Defaults Overlay File then it belongs under `overlay_files`
    
    :fontawesome-solid-3: If your YAML file edits item metadata ([see this example](../files/metadata.md#movies)) then it belongs under `metadata_files`
    
    If your file creates collections AND edits item metadata, then it should go in both `collection_files` and `metadata_files`
    
    If you are unsure on the above, the majority of `metadata_path` files  will now fall under `collection_files`, and all `overlay_path` files will now fall under `overlay_files`.

    If you require any assistance with this, please visit our Discord Server where we can assist you.

    Below is an example of the new attributes in use:

    ```yaml
    libraries:
      Movies:
        collection_files: #(1)!
          - file: config/Movies.yml #(2)!
          - default: imdb #(2)!
        metadata_files: #(3)!
          - file: config/MetadataEdits.yml #(4)!
        overlay_files: #(5)!
          - file: config/Overlays.yml #(6)!
          - default: audio_codec #(6)!
    ```

    1. This attribute used to be `metadata_path` and defines files that will relate to Collections
    2. These files are placed within `collection_files` because they define how Collections are built/maintained.
    3. This attribute used to be `metadata_path` and defines files that will relate to Metadata Edits
    4. These files are placed within `metadata_files` because they define Metadata Edits rather than collections.
    5. This attribute used to be `overlay_path` and defines files that will relate to Overlays
    6. These files are placed within `overlay_files` because they define how Overlays are built/maintained.

??? blank "`remove_` `reset_` `reapply_` and `schedule_` attributes for `overlays` are now Library Attributes (Click to Expand).<a class="headerlink" href="#overlay-library-attributes" title="Permanent link">¶</a>"

    <div id="overlay-library-attributes" />

    The attributes `remove_overlays`, `reset_overlays`, `reapply_overlays` and `schedule_overlays` are now Library Attributes
    and are called at the library level rather than within `overlay_path`.

    This change has been made to make these attributes consistent with other attributes of a similar nature.

    Whilst the previous method still works, we strongly advise you to move over to the new attributes, which can be done by looking at the following sample YAML:

    ```yaml
    libraries:
      Movies:
        remove_overlays: false
        reapply_overlays: false #(1)!
        # reset_overlays: plex #(2)!
        schedule_overlays: daily
        overlay_files:
          - default: audio_codec
    ```

    1. We strongly advise never setting this to `true` as it can cause [Image Bloat](scripts/imagemaid.md)
    2. This is purely an example, you do not need to specify `reset_overlays` or any of these attributes unless you specifically need to use them.

??? blank "`imdb_list` no longer works for Title or Keyword search URLs (Click to Expand).<a class="headerlink" href="#imdb-search" title="Permanent link">¶</a>"

    <div id="imdb-search" />

    As a result of IMDb changing their back-end code, `imdb_list` can no longer be used for URLs which start with 
    `https://www.imdb.com/search/title/` or `https://www.imdb.com/search/keyword/`

    All URLs used with `imdb_list` **must** start with `https://www.imdb.com/list/`

    We have introduced the [IMDb Search Builder](../files/builders/imdb/search.md) which replaces the functionality that
    `search/title/` and `search/keyword/` used to provide.

    As an example, the `imdb_search` Builder for `https://www.imdb.com/search/keyword/?keywords=christmas-movie` would be:

    ```yaml
    collections:
      Christmas Movies:
        imdb_search:
          keyword: christmas movie
    ```

    And the `imdb_search` Builder for `https://www.imdb.com/search/title/?title_type=feature,tv_movie,tv_special,video&num_votes=100,&keywords=spy,espionage` would be:

    ```yaml
    collections:
      Spy Movies:
        imdb_search:
          type: movie, tv_movie, tv_special, video
          votes.gte: 100
          keyword.any: spy, espionage
    ```

??? blank "FlixPatrol Default Files and Builders have been removed (Click to Expand).<a class="headerlink" href="#flixpatrol" title="Permanent link">¶</a>"

    <div id="flixpatrol" />

    Due to FlixPatrol moving a lot of their data behind a paywall and them reworking their pages to remove IMDb IDs and 
    TMDb IDs the flixpatrol builders and default files have been removed. There currently are no plans to re-add them.

??? blank "Kometa Default `other_award` replaced with individual Award files (Click to Expand).<a class="headerlink" href="#awards" title="Permanent link">¶</a>"

    <div id="awards" />

    The Kometa Default file `other_award` is now deprecated and will no longer function.

    Individual Kometa Default files have been introduced for several Awards, see the [Awards List](../defaults/award/separator.md)
    for more information on the new options.

<span id="providing-log-files-on-discord"></span>

## Get further help

You can drag-and-drop your meta.log file directly into [Discord](https://wiki.kometa.team/discord/), 
you do not need to upload it to a third-party site unless it exceeds the 50mb size limit.

Please DO NOT manually extract, copy and paste text from your log files directly into Discord as the formatting 
can be difficult to read and can often redact parts of the log file that are important for full context.

Include your installation method, Kometa version, what you expected, and what happened. Review logs for private information before sharing. For support and project links, see [Community & credits](acknowledgements.md).




