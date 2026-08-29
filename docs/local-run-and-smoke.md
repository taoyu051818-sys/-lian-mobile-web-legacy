# Local Run and Smoke Test

## Start the server

```bash
npm start
```

This runs `scripts/serve-frontend-static-rehearsal.js` and starts the static server at `http://127.0.0.1:4300`.

The `npm run serve` command is an alias for the same script.

## Environment variables

| Variable | Default | Description |
| --- | --- | --- |
| `FRONTEND_PORT` | `4300` | Port the static server listens on |
| `LIAN_BACKEND_BASE_URL` | `http://127.0.0.1:4200` | Backend API base URL for `/api/*` proxy |
| `LIAN_IMAGE_PROXY_BASE_URL` | `http://127.0.0.1:4201` | Image proxy base URL for `/api/image-proxy` |
| `LIAN_PUBLIC_PROTO` | (auto-detected) | Force `http` or `https` for forwarded proto header |

All URL variables must be absolute (`https://...`) if set. The server rejects relative values at startup.

## Run the smoke test

In a separate terminal while the server is running:

```bash
npm test
```

This runs `scripts/smoke-frontend.js` against `http://127.0.0.1:4300`.

You can also pass a custom URL:

```bash
node scripts/smoke-frontend.js http://localhost:4300
```

## What the smoke test checks

The smoke test runs these categories:

1. **Homepage HTML** -- verifies `<title>`, `<main class="app-shell">`, script tags present and in order.
2. **Static JS reachability** -- HTTP GET for each script file returns 200.
3. **API endpoints** -- `/api/feed` and `/api/map/v2/items` return valid JSON (skipped if backend is unavailable, unless `LIAN_SMOKE_REQUIRE_API=1`).
4. **Syntax check** -- `node --check` on all frontend JS files (runs even without a server).
5. **Helper contract** -- verifies `app-utils.js` exposes shared helpers with correct credentials policy.
6. **CSS reachability** -- `GET /styles.css` returns 200.

## Smoke test environment variables

| Variable | Default | Description |
| --- | --- | --- |
| `LIAN_SMOKE_REQUIRE_API` | (unset) | Set to `1` to fail instead of skip when backend is unavailable |

## Syntax-only check (no server needed)

To validate JS file syntax without starting the server:

```bash
node --check scripts/serve-frontend-static-rehearsal.js
node --check scripts/smoke-frontend.js
```

The smoke test also runs syntax checks on all `public/*.js` files as part of its offline pass.
