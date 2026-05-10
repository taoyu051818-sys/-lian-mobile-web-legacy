# public/ File Layout

All files under `public/` are served as static assets. The server uses `public/` as the site root.

## Application scripts

These are classic (non-module) scripts loaded in order by `index.html`. Each exposes its API on `window`.

| File | Responsibility |
| --- | --- |
| `app-state.js` | Global state, geo data, configuration constants |
| `app-utils.js` | Shared helpers: `api` fetch wrapper, `displayImageUrl`, `uploadImage` |
| `app-auth-avatar.js` | Authentication and avatar management |
| `app-feed.js` | Home feed rendering and interaction |
| `app-legacy-map.js` | Legacy illustrated map runtime |
| `app-ai-publish.js` | AI-assisted publish flow |
| `publish-page.js` | Publish page UI and form handling |
| `app-messages-profile.js` | Messages and profile pages |
| `reply-form-click-guard.js` | Click guard for reply forms |
| `explore-preload.js` | Explore/map preload behavior (consumes `window.api`, `window.displayImageUrl`) |
| `map-v2.js` | Map V2 with Leaflet-based interactive map |
| `app.js` | Main application entry, bootstraps all modules |

## HTML entry

| File | Purpose |
| --- | --- |
| `index.html` | Main SPA entry point |
| `ops.html` | Operations/observability page |
| `menu-prototype.html` | Menu prototype (legacy) |
| `menu-prototype-v2.html` | Menu prototype v2 (legacy) |

## Stylesheets

| File | Purpose |
| --- | --- |
| `styles.css` | Main application styles |
| `glass-ui.css` | Glass-effect UI component styles |
| `lian-tokens.css` | Design tokens (colors, spacing, typography) |
| `menu-prototype.css` | Menu prototype styles |
| `menu-prototype-v2.css` | Menu prototype v2 styles |

## Data files

| File | Purpose |
| --- | --- |
| `menu-data.json` | Menu structure data |
| `assets/road-network-preview.json` | Road network GeoJSON preview |

## Operations scripts

| File | Purpose |
| --- | --- |
| `ops.js` | Operations page logic |
| `ops-observability.js` | Observability helpers |

## Assets

`assets/` contains images and static resources:

- Campus map images (`campus-base-map.png`, `lian-illustrated-map.webp`)
- Location marker images (`library.png`, `bupt-sport.png`, `lian-academy.png`, `life-zone-*.png`, `shuttle-cart.png`, etc.)
- Transparent variants of markers (`*-transparent.png`)
- Avatar aliases (`assets/aliases/*.svg`): `curious-passenger`, `evening-recorder`, `island-anonymous`, `morning-breeze`, `night-owl`, `quiet-observer`

## Internal tools

`tools/` contains developer/internal pages:

| File | Purpose |
| --- | --- |
| `tools/task-board.html` | Legacy task board viewer (historical, not live dashboard) |
| `tools/task-board.js` | Task board logic |
| `tools/task-board.css` | Task board styles |
| `tools/map-v2-editor.html` | Map V2 coordinate editor |
| `tools/map-v2-editor.js` | Map editor logic |
| `tools/map-v2-editor.css` | Map editor styles |
| `tools/map-georef.html` | Map georeferencing tool |
| `tools/map-coastline-align.html` | Coastline alignment tool |
