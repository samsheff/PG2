# ShadowBroker Frontend

Next.js 16 dashboard with MapLibre GL, Cesium, and Framer Motion.

## Development

```bash
npm install
npm run dev        # http://localhost:3000
```

## API URL Configuration

Browser API calls use relative `/api/*` paths. The catch-all route handler at
`src/app/api/[...path]/route.ts` proxies those requests to the backend using the
runtime `BACKEND_URL` environment variable.

Common deployments:

| Scenario | Action needed |
| --- | --- |
| Local dev (`localhost:3000` + `localhost:8000`) | None |
| Docker Compose | `BACKEND_URL=http://backend:8000` is set by Compose |
| Cloudflare/Nginx overlay | Route all traffic to the frontend; keep `BACKEND_URL=http://backend:8000` |
| Backend on another host | Set runtime `BACKEND_URL=http://backend-host:8000` |

Do not route `/api/*` around the frontend in production. The Next.js proxy adds
runtime backend routing, admin/session handling, and Wormhole-sensitive path
behavior before forwarding requests to FastAPI.

## Theming

Dark mode is the default. A light/dark toggle is available in the left panel toolbar.
Theme preference is persisted in `localStorage` as `sb-theme` and applied via
`data-theme` attribute on `<html>`. CSS variables in `globals.css` define all
structural colors for both themes.
