# Contributing to drift-watch

## Setup

1. Install Docker Desktop (or compatible runtime).
2. Clone repository.
3. Copy `.env.example` to `.env`.
4. Run `docker compose up --build`.

## Local Development

- Backend: `cd backend ; uvicorn app.main:app --reload --host 0.0.0.0 --port 8000`
- Frontend: `cd frontend ; npm install ; npm run dev -- --host`

## Testing

- Backend tests: `cd backend ; pytest -q`
- Frontend build check: `cd frontend ; npm run build`

## Pull Request Requirements

- Include test evidence for modified code paths.
- Document configuration or API contract changes.
- Keep changes scoped and atomic.
- Add comments for non-obvious logic decisions.

## Commit Message Convention

Use conventional commits:
- `feat:` new behavior
- `fix:` bug fix
- `docs:` documentation update
- `chore:` maintenance or tooling
- `ci:` pipeline/workflow changes
