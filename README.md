# Idleview Web

The Idleview screen: the clock, date, weather and photo page. The same page runs in two
places, and this repo is the one copy of it.

- **The desktop app** ([Idleview](https://github.com/raduandreigorcea/Idleview)) bundles
  `page/` and draws it in its window. Rust decides what the screen shows.
- **The web version** is `page/` served by Idleview's photo Worker, for devices that
  cannot run the app: Android TV, tablets, a Pi Zero 2 W in a browser. The Worker
  computes the screen from the visitor's location and local time.

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

Everything in `page/` is shipped as-is: bundled into the app and uploaded to the Worker.
Keep other files out of it.

## Tests

```
npm install
npm test
```
