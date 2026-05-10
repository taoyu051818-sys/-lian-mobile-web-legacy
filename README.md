# LIAN Mobile Web Legacy

Archived legacy static web runtime for LIAN, migrated from [taoyu051818-sys/lian-mobile-web](https://github.com/taoyu051818-sys/lian-mobile-web). Active LIAN frontend development has moved to the Vue 3 + Vite architecture in that repository.

**This repository is read-only archived code.** It preserves the legacy static runtime for historical reference and legacy smoke validation. Do not submit feature PRs here.

## Quick start

```bash
npm start          # starts static server at http://127.0.0.1:4300
npm test           # runs smoke test against the running server
```

## Environment variables

| Variable | Default | Description |
| --- | --- | --- |
| `FRONTEND_PORT` | `4300` | Server port |
| `LIAN_BACKEND_BASE_URL` | `http://127.0.0.1:4200` | Backend API proxy target |
| `LIAN_IMAGE_PROXY_BASE_URL` | `http://127.0.0.1:4201` | Image proxy target |

## Documentation

- [Runtime Overview](docs/runtime-overview.md) -- architecture, script loading, shared helpers
- [Local Run and Smoke Test](docs/local-run-and-smoke.md) -- env vars, running the server and tests
- [public/ File Layout](docs/public-file-layout.md) -- what each file in `public/` does
- [Migration Notes](docs/migration-notes.md) -- why this repo exists and migration history

## Node version

Requires Node >= 22 < 23 and npm >= 10.
