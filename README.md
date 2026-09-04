# Where's it dark?

An interactive 3D globe for seeing, at a glance, **where it's night and where it's day right now** — and what the local time and weather are anywhere you click.

Everything lives in a single file: [`index.html`](index.html). No build step, no server.

## Run it

Open `index.html` in a modern browser (Chrome, Edge, Firefox, Safari).

An internet connection is required — the page pulls libraries, map textures and
live weather from CDNs and public APIs at runtime:

| What | Source |
| --- | --- |
| 3D engine | `three` + `globe.gl` (esm.sh) |
| Earth / cloud / water textures | jsDelivr + unpkg |
| Country borders | Natural Earth (`nvkelso/natural-earth-vector`, via jsDelivr) |
| Weather, timezone & local time | [Open-Meteo](https://open-meteo.com) (no API key) |

Capital coordinates are embedded in the file, so the globe and the day/night
view still work if the border/texture CDNs are unreachable.

## Features

- **Real-time day/night terminator** computed from the astronomical subsolar
  point (updates every minute). The ☀️ marker shows where the Sun is directly
  overhead; the shadowed hemisphere is night.
- **4K "Blue Marble" globe** with an optional drifting cloud layer, ocean
  sun-glint, atmospheric rim, anisotropic filtering and antialiasing.
- **Click anywhere** — a capital, a country, or open ocean — to fly there and
  open a panel with the **live local time** (correct timezone/DST), a
  day/night badge, and current **weather**: temperature, feels-like, condition,
  humidity, wind and precipitation.
- **Animated weather scene** in the panel (sun/moon, drifting clouds, rain,
  snow, fog, lightning) driven by the WMO weather code.
- **Weather map** (on by default) — one batched Open-Meteo call fetches the
  current conditions for ~195 capitals and shows a floating condition icon over
  each one on the globe, with animated rain/snow falling onto the surface,
  storm-icon flicker, a HUD tally, and dot colouring when the icons are off.
  Icons fade near the globe's edge and shrink where they crowd together.
- **Search** any capital from the HUD box — live results as you type
  (accent-insensitive), arrow keys / Enter / click to fly there.
- **Toggles** for auto-rotate, clouds (off by default) and the weather map.
- **UTC clock** and a running count of how many capitals are in night vs.
  daylight.

## Tech notes

- Custom GLSL shader blends day and night Earth textures across the terminator
  and adds the ocean specular highlight and atmospheric rim.
- On-globe weather markers/particles are plain `three` objects added to the
  scene, positioned with the same polar→cartesian mapping `three-globe` uses so
  they sit exactly on the capitals.
- No bundler, no dependencies checked in — it's ~1200 lines of HTML + CSS + one
  ES-module `<script>`.

## License

_To be decided._
