# Idleview Web

The Idleview screen: the clock, date, weather and photo page. The same page runs in two
places, and this repo is the one copy of it.

- **The desktop app** ([Idleview](https://github.com/raduandreigorcea/Idleview)) bundles
  `page/` and draws it in its window. Rust decides what the screen shows.
- **The web version** is `page/` on GitHub Pages, for devices that cannot run the app:
  Android TV, tablets, a Pi Zero 2 W in a browser. Idleview's photo Worker computes
  the screen from the visitor's location and local time (`GET /api/view`).

  Live at **https://raduandreigorcea.github.io/Idleview-Web/**. Every push to `main`
  publishes `page/` (`.github/workflows/pages.yml`).

Idleview includes this repo as the `web` submodule.

## Layout

| Path | What it is |
|---|---|
| `page/index.html`, `page/styles.css`, `page/assets/` | The screen |
| `page/render.js` | Draws a view. Everything arrives formatted; it only places it |
| `page/main.js` | Picks the glue: `tauri.js` inside the app, `web.js` in a browser |
| `page/tauri.js` | App: listens for the `view` event, shows the pairing card |
| `page/web.js` | Browser: fetches `/api/view` on the minute, pings Unsplash attribution |
| `test/` | Renderer tests (jsdom) |

Everything in `page/` is shipped as-is: bundled into the app and published to Pages.
Keep other files out of it, and keep paths relative - Pages serves the site under
`/Idleview-Web/`, not at the root.

If the page moves to another address, add that origin to `WEB_ORIGINS` in the Worker
(Idleview's `proxy/src/worker.js`), or it will not be allowed to read `/api/view`.

## Tests

```
npm install
npm test
```
