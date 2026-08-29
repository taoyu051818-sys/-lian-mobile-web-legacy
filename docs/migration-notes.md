# Migration Notes

## Why this repo exists

The LIAN frontend originally lived entirely in [taoyu051818-sys/lian-mobile-web](https://github.com/taoyu051818-sys/lian-mobile-web). That repo contained both the legacy static runtime (port 4300) and an in-development Vue 3 + Vite shell (port 4301) running side by side in a dual-lane configuration.

When the Vue/Vite shell reached sufficient maturity, the legacy static runtime was extracted into this repository to:

- Keep archived legacy code with its own history and scripts.
- Prevent stale legacy guidance from appearing in the active repo's docs.
- Allow the active repo to clean up legacy-specific references (PR #301).

## Migration timeline

- **li-mobile-web PR #282** -- Removed the legacy static runtime files from the active repository.
- **li-mobile-web PR #301** -- Cleaned stale legacy references from active repo documentation.
- **This repo** -- Houses the archived runtime with its own scripts, docs, and smoke test.

## What was migrated

The following were preserved in this repository:

- All `public/` application scripts, HTML, CSS, assets, and tools.
- `scripts/serve-frontend-static-rehearsal.js` (static server).
- `scripts/smoke-frontend.js` (smoke test).
- `package.json` with `start`, `serve`, and `test` scripts.

## What was not migrated

The following remain in the active repo or were intentionally excluded:

- Vue 3 + Vite shell (`src/`, `vite.config.ts`, root `index.html`).
- CI workflow files (`.github/workflows/`).
- Backend code (`lian-platform-server`).
- Agent task boards, handoff documents, and dated override snapshots.
- `node_modules` and lockfile (this repo has no dependencies).

## Historical dual-lane model

Before migration, `lian-mobile-web` ran two frontend runtimes:

| Lane | Port | Role |
| --- | --- | --- |
| Legacy/static rehearsal | 4300 | Student-facing default; served `public/` files |
| Vue canary preview | 4301 | In-development Vue shell for incremental migration |

A supervisor script (`scripts/serve-frontend-runtimes.js`) started both. The legacy runtime was the product default; Vue canary was used only for validating migrated pages.

Key migration guardrails from the active repo:

- Vue canary was never the default product entrypoint during migration.
- A page could move from canary to default only after its legacy feature parity was complete.
- A failed early Vue migration attempt (2026-05-05) where Vue became the default prematurely was rolled back, reinforcing these rules.

## Relationship to active repo

This repo is read-only archived code. Active LIAN frontend development uses the Vue 3 + Vite architecture in `lian-mobile-web`. Do not submit feature PRs here; this repo exists for historical reference and legacy smoke validation only.
