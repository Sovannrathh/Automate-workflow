# Automate-workflow

Self-hosted n8n backend + a customizable n8n editor-ui frontend, wired to
talk to each other locally.

## Quickstart

```
cd backend
cp .env.example .env   # fill in secrets
docker compose -f n8n.yaml -f facebook.yaml up -d
```

```
cd frontend/editor-ui
pnpm install
pnpm serve
```

- Backend REST API: http://localhost:5678
- Frontend dev server: http://localhost:8080

See `backend/README.md` for the CORS/env wiring between the two.
