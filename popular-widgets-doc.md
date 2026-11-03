# Popular Sheet Music Widget

Embed popular sheet music from **Tably.es** directly into your website.

The Popular Sheet Music Widget is a lightweight HTML widget that lets developers display popular Tably sheet music for a specific instrument without building their own catalog integration.

Choose an instrument, define how many results you want to display, and embed the resulting URL in your website.

Tably handles:

- Sheet-music data
- Instrument filtering
- Ranking
- Song and artist information
- Links to sheet music
- Instrument category links
- Widget styling
- Catalog updates

The widget is generated dynamically from Tably's sheet-music marketplace.

Tably is a licensed sheet music and tablature marketplace for music learners, professional editors and transcribers, teachers, music schools, artists, labels and rights holders.


# Live example

The base endpoint is:

```text
https://tably-two.vercel.app/api/widgets/popular
```

Use URL parameters to select the instrument and number of results:

```text
https://tably-two.vercel.app/api/widgets/popular?instrument=piano&limit=10
```

A widget can display:

```text
Popular Piano Sheet Music

1. Song title — Artist
2. Song title — Artist
3. Song title — Artist
...

See all Piano sheet music →
```

Each result links directly to the corresponding sheet-music page on Tably.


# Parameters

The endpoint currently accepts two main parameters.

## `instrument`

Defines which instrument should be shown.

Example:

```text
instrument=piano
```

## `limit`

Defines the maximum number of sheet-music results displayed.

Example:

```text
limit=10
```

If `limit` is omitted, the widget uses a smaller default result set.

For example:

```text
https://tably-two.vercel.app/api/widgets/popular?instrument=piano
```

currently displays three Piano results.

Use values between `1` and `10` when integrating the widget.


# Complete URL structure

```text
https://tably-two.vercel.app/api/widgets/popular?instrument={instrument}&limit={limit}
```

Example:

```text
https://tably-two.vercel.app/api/widgets/popular?instrument=electric-guitar&limit=10
```


# Verified instrument examples

## Piano

```text
https://tably-two.vercel.app/api/widgets/popular?instrument=piano&limit=10
```

The current widget displays Piano sheet music and links every item directly to Tably.


## Electric Guitar

```text
https://tably-two.vercel.app/api/widgets/popular?instrument=electric-guitar&limit=10
```

Example songs currently returned include tracks by Elvis Presley, Alice Cooper, Bob Dylan, Green Day and other artists.


## Acoustic Guitar

```text
https://tably-two.vercel.app/api/widgets/popular?instrument=acoustic-guitar&limit=10
```

The widget currently exposes Acoustic Guitar material from artists including Bob Dylan, Beyoncé, Ben E. King, Alanis Morissette and ABBA.


## Bass Guitar

```text
https://tably-two.vercel.app/api/widgets/popular?instrument=bass-guitar&limit=10
```

Current results include music associated with artists such as Al Green, Michael Jackson, Oasis, Green Day and Chuck Berry.


## Drums

Use the `drum-kit` slug:

```text
https://tably-two.vercel.app/api/widgets/popular?instrument=drum-kit&limit=10
```

The widget renders the user-facing instrument name as **Drums**.


## Saxophone

```text
https://tably-two.vercel.app/api/widgets/popular?instrument=saxophone&limit=10
```

The endpoint returns up to the requested limit, but it does not invent results.

If fewer matching sheet-music items exist in Tably, only the available items are displayed.

For example, the current Saxophone widget returns two available scores even with `limit=10`.


# How to embed the widget

The easiest integration is an `iframe`.

## Piano example

```html
<iframe
  src="https://tably-two.vercel.app/api/widgets/popular?instrument=piano&limit=10"
  title="Popular Piano Sheet Music on Tably"
  width="100%"
  height="720"
  loading="lazy"
  style="
    width: 100%;
    border: 0;
    border-radius: 12px;
    overflow: hidden;
  "
></iframe>
```

That's enough to add the widget to a normal HTML website.


# Electric Guitar example

```html
<iframe
  src="https://tably-two.vercel.app/api/widgets/popular?instrument=electric-guitar&limit=10"
  title="Popular Electric Guitar Sheet Music on Tably"
  width="100%"
  height="720"
  loading="lazy"
  style="
    width: 100%;
    border: 0;
    border-radius: 12px;
    overflow: hidden;
  "
></iframe>
```


# Drum example

```html
<iframe
  src="https://tably-two.vercel.app/api/widgets/popular?instrument=drum-kit&limit=10"
  title="Popular Drum Sheet Music on Tably"
  width="100%"
  height="720"
  loading="lazy"
  style="
    width: 100%;
    border: 0;
    border-radius: 12px;
    overflow: hidden;
  "
></iframe>
```


# Smaller widgets

You do not need to show ten results.

For a sidebar or article block, use a smaller limit.

Example:

```text
https://tably-two.vercel.app/api/widgets/popular?instrument=piano&limit=3
```

Embed:

```html
<iframe
  src="https://tably-two.vercel.app/api/widgets/popular?instrument=piano&limit=3"
  title="Popular Piano Sheet Music"
  width="100%"
  height="360"
  loading="lazy"
  style="
    width: 100%;
    border: 0;
    border-radius: 12px;
  "
></iframe>
```

This format can work well inside:

- Music blogs
- Instrument-learning websites
- Teacher websites
- Music-school websites
- Lesson pages
- Artist websites
- Educational resources
- Music communities


# Responsive integration

The widget itself is designed as web content, while the surrounding website controls the available iframe space.

A simple responsive wrapper is:

```html
<div
  style="
    width: 100%;
    max-width: 560px;
    margin: 0 auto;
  "
>
  <iframe
    src="https://tably-two.vercel.app/api/widgets/popular?instrument=piano&limit=10"
    title="Popular Piano Sheet Music on Tably"
    width="100%"
    height="720"
    loading="lazy"
    style="
      display: block;
      width: 100%;
      border: 0;
      border-radius: 12px;
    "
  ></iframe>
</div>
```

Adjust the iframe height according to the number of results you choose to display.


# Webflow integration

The widget can also be embedded in Webflow.

1. Open the Webflow Designer.
2. Add an **Embed** element.
3. Paste the iframe HTML.
4. Change the `instrument` and `limit` parameters.
5. Set the wrapper width you want.
6. Publish the page.

Example:

```html
<iframe
  src="https://tably-two.vercel.app/api/widgets/popular?instrument=acoustic-guitar&limit=10"
  title="Popular Acoustic Guitar Sheet Music on Tably"
  width="100%"
  height="720"
  loading="lazy"
  style="border:0;width:100%;"
></iframe>
```


# WordPress integration

Add a Custom HTML block and paste:

```html
<iframe
  src="https://tably-two.vercel.app/api/widgets/popular?instrument=saxophone&limit=10"
  title="Popular Saxophone Sheet Music on Tably"
  width="100%"
  height="720"
  loading="lazy"
  style="border:0;width:100%;"
></iframe>
```

No WordPress plugin is required.


# React / Next.js example

The endpoint can also be embedded from a React application:

```jsx
export default function PopularPianoSheetMusic() {
  return (
    <iframe
      src="https://tably-two.vercel.app/api/widgets/popular?instrument=piano&limit=10"
      title="Popular Piano Sheet Music on Tably"
      loading="lazy"
      style={{
        width: "100%",
        height: "720px",
        border: 0,
        borderRadius: "12px",
      }}
    />
  );
}
```


# Dynamic instrument example

Developers can construct the widget URL dynamically.

```javascript
function getTablyWidgetUrl(instrument, limit = 3) {
  const url = new URL(
    "https://tably-two.vercel.app/api/widgets/popular"
  );

  url.searchParams.set(
    "instrument",
    instrument
  );

  url.searchParams.set(
    "limit",
    String(limit)
  );

  return url.toString();
}
```

Usage:

```javascript
const widgetUrl =
  getTablyWidgetUrl(
    "bass-guitar",
    10
  );
```

Result:

```text
https://tably-two.vercel.app/api/widgets/popular?instrument=bass-guitar&limit=10
```


# Switching instruments dynamically

A website can let users choose an instrument and update the widget.

```html
<select id="instrument">
  <option value="piano">Piano</option>
  <option value="electric-guitar">Electric Guitar</option>
  <option value="acoustic-guitar">Acoustic Guitar</option>
  <option value="bass-guitar">Bass Guitar</option>
  <option value="drum-kit">Drums</option>
  <option value="saxophone">Saxophone</option>
</select>

<iframe
  id="tably-widget"
  title="Popular Sheet Music on Tably"
  width="100%"
  height="720"
  style="border:0;width:100%;"
></iframe>

<script>
  const selector =
    document.getElementById(
      "instrument"
    );

  const widget =
    document.getElementById(
      "tably-widget"
    );

  function updateWidget() {
    widget.src =
      "https://tably-two.vercel.app/api/widgets/popular" +
      "?instrument=" +
      encodeURIComponent(
        selector.value
      ) +
      "&limit=10";
  }

  selector.addEventListener(
    "change",
    updateWidget
  );

  updateWidget();
</script>
```


# How the widget was built

The Popular Sheet Music Widget is intentionally simple from the developer's point of view.

Behind the endpoint, Tably handles the catalog logic.

The high-level architecture is:

```text
Developer website
        │
        ▼
Tably widget endpoint
        │
        ▼
instrument=piano
limit=10
        │
        ▼
Tably backend
        │
        ▼
Tably live sheet-music catalog
        │
        ▼
Filter by instrument
        │
        ▼
Apply current widget ordering
        │
        ▼
Render HTML
        │
        ▼
Developer website
```

The public `instrument` parameter uses human-readable slugs such as:

```text
piano
electric-guitar
acoustic-guitar
bass-guitar
drum-kit
saxophone
```

Internally, Tably maps those slugs to the corresponding instrument references in its live sheet-music catalog.

This means developers do not need to know Tably's internal CMS IDs.


# Catalog filtering

Tably's catalog stores sheet music with metadata including information such as:

```text
Song
Artist
Instrument
Difficulty
Availability
Canonical sheet-music URL
```

Tably also exposes a machine-readable catalog as part of its developer/search infrastructure.

For the Popular Widget, the requested instrument is resolved internally and only matching sheet music is considered.

Conceptually:

```javascript
const instrument =
  request.query.instrument;

const limit =
  request.query.limit;

const sheets =
  catalog
    .filter(
      sheet =>
        sheet.instrument ===
        requestedInstrument
    )
    .slice(
      0,
      limit
    );
```

The real implementation uses Tably's internal instrument references rather than relying only on display text.


# Server-rendered HTML

The endpoint returns **HTML**, not a JSON data object.

That decision makes the integration extremely lightweight.

Developers do not need to:

- Request JSON
- Build a UI
- Recreate Tably styles
- Parse catalog data
- Build links
- Maintain instrument mappings
- React to catalog changes

They simply embed:

```html
<iframe
  src="https://tably-two.vercel.app/api/widgets/popular?instrument=piano&limit=10"
></iframe>
```

and Tably handles the rest.


# What the widget renders

A current widget includes:

- A “Popular” label
- Instrument-specific heading
- Short discovery description
- Ranked sheet-music results
- Song title
- Artist
- Link to each Tably sheet
- “See all” link for the selected instrument

For example, the live Piano widget currently renders the heading **Popular Piano Sheet Music**, followed by individual Tably results and a link to see all Piano sheet music.


# Why use an iframe?

An iframe keeps the integration isolated.

Tably controls:

```text
Catalog
Ranking
Links
Markup
Styles
Updates
```

while the host website controls:

```text
Placement
Width
Height
Surrounding content
```

Changes to Tably's catalog can therefore appear in the widget without requiring the developer to update their website.


# No authentication required

The widget is intended as a public discovery component.

A basic embed does not require the developer to expose:

- A Tably API token
- Webflow credentials
- User authentication
- Private catalog IDs

The integration is simply the public widget URL.


# Example use cases

## Music teacher

A piano teacher can add:

```text
Popular Piano Sheet Music
```

to their resource page and help students discover new repertoire.


## Guitar website

A guitar-learning website can show:

```text
Popular Electric Guitar Sheet Music
```

next to lessons or equipment guides.


## Music school

A school can create different sections:

```text
Piano
Electric Guitar
Bass Guitar
Drums
Saxophone
```

each powered by the same endpoint with a different `instrument` parameter.


## Music blog

An article about bass playing could embed:

```text
https://tably-two.vercel.app/api/widgets/popular?instrument=bass-guitar&limit=3
```

to surface relevant playable repertoire.


## Artist or music community

Communities can use the widget as an additional discovery surface and direct users to playable sheet music without maintaining their own notation database.


# Current examples

### Piano

```text
https://tably-two.vercel.app/api/widgets/popular?instrument=piano&limit=10
```

### Electric Guitar

```text
https://tably-two.vercel.app/api/widgets/popular?instrument=electric-guitar&limit=10
```

### Acoustic Guitar

```text
https://tably-two.vercel.app/api/widgets/popular?instrument=acoustic-guitar&limit=10
```

### Bass Guitar

```text
https://tably-two.vercel.app/api/widgets/popular?instrument=bass-guitar&limit=10
```

### Drums

```text
https://tably-two.vercel.app/api/widgets/popular?instrument=drum-kit&limit=10
```

### Saxophone

```text
https://tably-two.vercel.app/api/widgets/popular?instrument=saxophone&limit=10
```


# Important behavior

`limit` means:

> Return up to this number of results.

It does not guarantee that this number of scores exists for every instrument.

For example:

```text
instrument=saxophone
limit=10
```

currently returns fewer than ten results because the live Tably Saxophone inventory available to this widget is smaller.

This behavior keeps the widget connected to real catalog availability rather than filling empty positions with unrelated content.


# Recommended integration

For most sites:

```html
<iframe
  src="https://tably-two.vercel.app/api/widgets/popular?instrument=piano&limit=10"
  title="Popular Piano Sheet Music on Tably"
  width="100%"
  height="720"
  loading="lazy"
  style="
    display:block;
    width:100%;
    border:0;
  "
></iframe>
```

For compact placements:

```html
<iframe
  src="https://tably-two.vercel.app/api/widgets/popular?instrument=piano&limit=3"
  title="Popular Piano Sheet Music on Tably"
  width="100%"
  height="360"
  loading="lazy"
  style="
    display:block;
    width:100%;
    border:0;
  "
></iframe>
```


# Building with Tably

The Popular Sheet Music Widget is one of the simplest ways to add Tably's music-discovery technology to another website.

The broader developer ecosystem can combine it with other Tably ideas such as:

- Radio → sheet music
- Spotify playlist → sheet music
- YouTube → sheet music
- Instrument-specific discovery
- Music-learning tools
- Catalog search
- AI assistants
- MCP integrations
- Educational resources

The underlying principle is the same:

**Turn music discovery into something playable.**

Tably  
https://www.tably.es/
