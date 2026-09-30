# Backend

Self-hosted n8n (with Postgres) plus a Facebook App/webhook config overlay.

## Run

```
cp .env.example .env   # fill in real secrets
docker compose -f n8n.yaml -f facebook.yaml up -d
```

n8n will be available at http://localhost:5678.

- `n8n.yaml` — base stack: n8n + Postgres.
- `facebook.yaml` — overlay that injects `FB_*` env vars into the n8n
  container for use in workflows (`{{$env.FB_PAGE_ACCESS_TOKEN}}`, etc.)
  and documents the Meta webhook setup.

## Connecting the frontend

`N8N_CORS_ALLOW_ORIGIN` (default `http://localhost:8080`) allows the
`frontend/editor-ui` dev server to call this instance's REST API
cross-origin. With the backend running, start the frontend:

```
cd ../frontend/editor-ui
pnpm install
pnpm serve   # already targets http://localhost:5678/ by default
```

Then open http://localhost:8080 — it talks to the REST API on
http://localhost:5678 served by this stack. If you change `N8N_PORT` or
the frontend's dev port, update `N8N_CORS_ALLOW_ORIGIN` and the
frontend's `VUE_APP_URL_BASE_API` (see `editor-ui/package.json`'s
`serve` script) to match.
