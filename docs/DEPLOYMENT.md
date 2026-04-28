# Deployment Guide

## Local Development Deployment

1. Copy env file:

```bash
cp .env.example .env
```

2. Build and run:

```bash
docker compose up --build
```

3. Validate:
- Dashboard: http://localhost:8080
- API docs: http://localhost:8000/docs
- Health: http://localhost:8000/health

## Production Deployment (Container Platforms)

Use images built from:
- `backend/Dockerfile`
- `frontend/Dockerfile`

Recommended runtime shape:
- Frontend container exposed publicly
- Backend container private behind ingress/proxy
- HTTPS termination at gateway/load balancer

## GitHub Container Registry Release

Release workflow (`.github/workflows/release.yml`) publishes tagged images:
- `ghcr.io/<owner>/drift-watch-backend:<tag>`
- `ghcr.io/<owner>/drift-watch-frontend:<tag>`

Tag convention:

```bash
git tag v0.1.0
git push origin v0.1.0
```

## GitHub Pages Deployment

Pages workflow builds and deploys frontend static output.

Important note:
- GitHub Pages hosts static assets only.
- Backend API must be hosted separately and configured via `VITE_API_BASE_URL`.

## Environment Variables

Backend:
- `DRIFT_ENV`
- `DRIFT_ALLOWED_HOSTS`
- `DRIFT_CORS_ORIGINS`
- `DRIFT_MAX_PAYLOAD_BYTES`
- `DRIFT_GZIP_MINIMUM_SIZE`
- `DRIFT_ENABLE_HSTS`
- `DRIFT_PORT`

Frontend:
- `VITE_API_BASE_URL`
