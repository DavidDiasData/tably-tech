# Tably Developer Tools

Build music discovery, sheet-music and learning experiences with **Tably.es**.

Tably is a licensed sheet music and tablature marketplace that connects music discovery with learning. This repository contains examples, integrations and reusable components that developers can use to build products on top of Tably's technology and catalog.

The goal is simple:

**Help users move from discovering a song to actually playing it.**

Developers can use the examples in this repository to experiment with:

- Sheet-music discovery
- Radio-to-sheet-music experiences
- Spotify and YouTube playlist integrations
- Tably catalog matching
- Music metadata normalization
- Instrument and difficulty metadata
- Webflow CMS integrations
- Embeddable music widgets
- AI and agent integrations
- Public APIs and MCP-compatible tools

Visit Tably:

https://www.tably.es/


## Radio + Sheet Music

One of the main experiments available in this repository connects **live radio broadcasts with the Tably sheet-music catalog**.

Traditional online radio players answer one question:

> What am I listening to?

Tably adds a second one:

> Can I learn to play it?


### How it works

A Tably radio integration combines three different data sources:

```text
Live radio stream
        +
Now-playing metadata
        +
Tably sheet-music catalog
        ↓
Identify the current song
        ↓
Normalize title + artist
        ↓
Search Tably
        ↓
Return matching sheet music
```

The result is a radio player where listeners can hear a song and immediately discover whether sheet music or tablature is available for it.


## Example

Imagine that a radio station is currently playing:

```text
Eight Days a Week
The Beatles
```

The radio metadata endpoint may return:

```json
{
  "title": "Eight days a week",
  "artist": "The Beatles",
  "album": "Beatles for sale"
}
```

Tably normalizes that information and searches its catalog.

If matching sheet music exists, the API can return:

```json
{
  "nowPlaying": {
    "title": "Eight Days a Week",
    "artist": "The Beatles"
  },
  "sheets": [
    {
      "title": "Eight Days a Week",
      "artist": "The Beatles",
      "instrument": "Piano",
      "difficulty": "Beginner",
      "url": "https://www.tably.es/free-sheets/..."
    }
  ]
}
```

The user can then move directly from:

**listening → discovering → learning**.


# Radio architecture

Different radio networks expose their live metadata in different ways.

The integrations in this repository normalize those different systems into a common Tably structure.

Examples may include:

```text
Triton Digital
Radio France LiveMeta
StreamTheWorld
Supla / Nelonen Media
Planet Radio
laut.fm
station-specific JSON APIs
ICY stream metadata
```

A station-specific adapter is responsible for turning the broadcaster's response into:

```json
{
  "title": "Song Title",
  "artist": "Artist Name",
  "album": "Album Name",
  "artwork": "https://...",
  "trackId": "...",
  "source": "metadata-provider"
}
```

Everything after that can use the same Tably matching system.


# Example integration flow

```text
Radio station
     │
     ├── Audio stream
     │
     └── Now-playing endpoint
              │
              ▼
       Tably radio adapter
              │
              ▼
       Normalize metadata
              │
              ▼
       Current song
       + current artist
              │
              ▼
       Tably catalog matcher
              │
              ▼
       Matching sheet music
              │
              ▼
       Radio player / API
```

This separation is intentional.

The radio-provider implementation can change without requiring developers to rewrite the Tably catalog-matching logic.


# Metadata normalization

Radio metadata is rarely consistent.

For example, the same song might appear as:

```text
The Beatles - Eight Days A Week
Eight days a week
Eight Days A Week - Remastered 2009
Eight Days A Week (Remastered)
```

Artist metadata may also contain:

```text
Artist A feat. Artist B
Artist A ft. Artist B
Artist A & Artist B
Artist A, Artist B
```

Tably therefore normalizes metadata before attempting a catalog match.

Normalization can include:

- Lowercasing
- Removing accents
- Removing punctuation
- Normalizing `&` and `and`
- Handling `feat.`, `ft.` and `featuring`
- Removing labels such as `remastered`, `live`, `edit`, `mix` or `version`
- Splitting multiple artists
- Comparing title tokens
- Comparing artist tokens


# Matching sheet music

The matching system evaluates the radio track against Tably catalog entries.

A simplified scoring model looks like:

```text
Exact title
    → strongest signal

Partial/contained title
    → strong signal

Token similarity
    → fallback title signal

Exact artist
    → additional confidence

Partial artist
    → additional confidence

Wrong artist + identical title
    → penalty
```

Only candidates above the configured matching threshold are returned.

Instrument and difficulty are descriptive metadata and do not determine whether two songs match.


# Instrument metadata

A matching score can expose the instrument available on Tably, for example:

```text
Piano
Acoustic Guitar
Electric Guitar
Bass Guitar
Drums
Violin
Saxophone
Flute
Cello
Trumpet
Trombone
French Horn
Clarinet
Ukulele
Accordion
Harmonica
Harp
Choir
Synthesizer
Recorder
Tabla
```

This lets a radio experience answer more than:

> Is sheet music available?

It can answer:

> Is sheet music available for the instrument I play?


# Difficulty metadata

Where available, Tably can also expose learning difficulty:

```text
Beginner
Intermediate
Advanced
```

A result might therefore look like:

```text
Eight Days a Week
The Beatles

Piano · Beginner
```

This makes radio discovery more useful for music learners rather than simply linking to generic search results.


# API pattern

A typical Tably radio endpoint follows:

```text
GET /api/radio/{station}
```

Example:

```text
GET /api/radio/fip-rock
```

A normalized response can look like:

```json
{
  "station": "FIP Rock",
  "country": "FR",
  "live": true,
  "streamUrl": "https://...",
  "nowPlaying": {
    "title": "Eight Days a Week",
    "artist": "The Beatles",
    "album": "Beatles for Sale",
    "artwork": "https://...",
    "source": "radio-france-livemeta"
  },
  "sheets": [
    {
      "title": "Eight Days a Week",
      "artist": "The Beatles",
      "instrument": "Piano",
      "difficulty": "Beginner",
      "url": "https://www.tably.es/free-sheets/..."
    }
  ]
}
```


# Embeddable player

The API can also power an embeddable player:

```text
GET /radio/{station}
```

The player can provide:

- Play / pause
- Live station stream
- Current song
- Current artist
- Album artwork
- Matching Tably sheet music
- Instrument
- Difficulty
- Link to the sheet-music page
- Link to the wider Tably catalog


# Why combine radio and sheet music?

Music discovery and music learning usually happen in separate products.

A listener discovers a song on:

```text
Radio
Spotify
YouTube
```

and later has to manually search:

```text
Song name
+
artist
+
sheet music
+
instrument
```

Tably experiments with removing that friction.

The product flow becomes:

```text
Hear a song
     ↓
Recognize the song automatically
     ↓
Check whether Tably has the score
     ↓
Choose an available instrument
     ↓
Start learning
```

The same concept can extend beyond radio to playlists, streaming services, music-identification tools and AI assistants.


# Existing Tably radio experiences

Tably already applies this concept to multiple radio experiences, including stations such as:

- BBC Radio 2
- LOS40 Classic
- Radio Paradise
- Radio Veronica

Each integration can use a different metadata provider while exposing a consistent experience to the user.


# Building a new radio adapter

To add another station, developers generally need:

```text
1. Station name
2. Country
3. Public audio stream
4. Public or accessible now-playing metadata source
5. Parser for the station's metadata format
```

The adapter should normalize the result into:

```javascript
{
  title,
  artist,
  album,
  artwork,
  trackId,
  source
}
```

Once normalized, the existing Tably catalog matcher can handle the rest.


# Public endpoint considerations

Radio metadata sources vary considerably.

Some are documented public APIs.

Others are endpoints used by public web players, streaming platforms or broadcaster applications.

Developers should:

- Respect broadcaster terms
- Avoid aggressive polling
- Cache metadata
- Prefer server-side requests
- Handle endpoint failures gracefully
- Avoid assuming undocumented endpoints will remain stable forever

Tably radio examples generally place the external metadata request behind a Tably server endpoint rather than exposing provider-specific logic directly to the browser.


# Caching

Recommended approximate caching:

```text
Radio metadata:
10–30 seconds

Tably catalog:
5 minutes or more
```

This prevents every embedded player from independently requesting the broadcaster API or the Webflow catalog.

