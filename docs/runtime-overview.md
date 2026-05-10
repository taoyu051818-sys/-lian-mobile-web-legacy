# Legacy Static Runtime Overview

This repository (`-lian-mobile-web-legacy`) is the archived home of the LIAN legacy static web runtime. It was migrated from [taoyu051818-sys/lian-mobile-web](https://github.com/taoyu051818-sys/lian-mobile-web) when active development moved to a Vue 3 + Vite architecture.

**This runtime is archived.** Active LIAN frontend development continues in the Vue/Vite repository.

## What it is

A zero-build-step static web server that serves vanilla JavaScript files from `public/` and proxies API requests to a backend service. The frontend is plain HTML + CSS + classic (non-module) scripts loaded in a specific order via `<script>` tags in `index.html`.

## How it works

1. `scripts/serve-frontend-static-rehearsal.js` starts an HTTP server on port 4300.
2. It serves files from `public/` as the site root.
3. For `/api/*` requests, it proxies to `LIAN_BACKEND_BASE_URL` (default `http://127.0.0.1:4200`).
4. For `/api/image-proxy` requests, it proxies to `LIAN_IMAGE_PROXY_BASE_URL` (default `http://127.0.0.1:4201`).
5. On HTML responses, it injects a runtime config `<script>` into `<head>` that sets `window.LIAN_API_BASE_URL`, `window.LIAN_IMAGE_PROXY_BASE_URL`, and `window.LIAN_STATIC_REHEARSAL`.
6. SPA-style fallback: requests for paths without a file extension serve `index.html`.

## Script loading contract

The frontend loads scripts in a fixed order. This order is validated by the smoke test:

1. `/map-v2.js`
2. `/app-state.js`
3. `/app-utils.js`
4. `/app-auth-avatar.js`
5. `/app-feed.js`
6. `/app-legacy-map.js`
7. `/app-ai-publish.js`
8. `/publish-page.js`
9. `/app-messages-profile.js`
10. `/reply-form-click-guard.js`
11. `/explore-preload.js`
12. `/app.js`

Each script exposes its public API on `window` for downstream scripts to consume (e.g., `window.api`, `window.displayImageUrl`).

## Shared helpers

`public/app-utils.js` provides shared utilities exposed via `Object.assign(window, ...)`:

- `api` -- fetch wrapper with `credentials: "include"` by default
- `displayImageUrl` -- image URL resolution through the proxy
- `uploadImage` -- image upload via `/api/upload/image`

Other scripts consume these through `window.api` and `window.displayImageUrl` rather than reimplementing the logic.

## Historical context

Before migration, lian-mobile-web ran a dual-lane frontend:

- **Port 4300** -- Legacy/static rehearsal (this runtime)
- **Port 4301** -- Vue canary preview (Vite dev/preview server)

A supervisor script started both lanes. The legacy runtime was the student-facing default; the Vue canary was used for incremental feature migration. After PR #282 in lian-mobile-web removed the legacy static runtime from that repo, it was archived here.

## Node version

Requires Node >= 22 < 23 and npm >= 10.
