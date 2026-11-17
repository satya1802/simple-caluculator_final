# Developer Guide

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start status -->
_Up to date._
<!-- sdlc:auto:end status -->

<!-- sdlc:auto:start source -->
Generated from commit `e2f3485` · model `claude-sonnet-5`
<!-- sdlc:auto:end source -->

<!-- sdlc:auto:start overview -->
simple_caluculator is a generated two-app repository from the Quorq AI SDLC platform. The frontend/ is an approved Vite + React 19 single-page app whose screens were reviewed and run on seeded sample data (not yet wired to a real API). The backend/ is a FastAPI 0.115 service scaffolded from an API spec that had no approved architecture at generation time, so it currently exposes only a /health liveness endpoint, with SQLAlchemy models, Pydantic schemas, and a router package ready for future endpoints. The backend defaults to a local SQLite file so it runs with no external database, while docker-compose.yml provides an optional PostgreSQL 16 service for when DATABASE_URL is pointed at it.
<!-- sdlc:auto:end overview -->

<!-- sdlc:auto:start prerequisites -->
- Node.js (for the frontend, Vite 6 / React 19 toolchain)
- npm
- Python 3.12
- pip
- Docker and Docker Compose (optional, for the PostgreSQL service in docker-compose.yml)
<!-- sdlc:auto:end prerequisites -->

<!-- sdlc:auto:start setup -->
1. Clone the repository and cd into it
2. cd backend
3. pip install -r requirements.txt
4. (optional) set DATABASE_URL to point at a real database; otherwise a local sqlite:///./app.db file is used automatically
5. uvicorn app.main:app --reload   # starts the API on http://localhost:8000 and creates tables on startup
6. cd ../frontend
7. npm install
8. (optional) create a .env based on .env.example and set VITE_API_BASE_URL / VITE_API_SECRET_KEY if pointing the frontend at a real backend
9. npm run dev   # starts the Vite dev server on http://localhost:5173
<!-- sdlc:auto:end setup -->

<!-- sdlc:auto:start run -->
| Name | Command | Description |
|---|---|---|
| backend dev server | `uvicorn app.main:app --reload` | Runs the FastAPI app with auto-reload (from backend/) |
| frontend dev server | `npm run dev` | Starts the Vite dev server for the SPA (from frontend/) |
| frontend build | `npm run build` | Bundles the app with Vite; does not typecheck |
| frontend preview | `npm run preview` | Serves the production build locally |
| db via compose | `docker-compose up db` | Starts the optional PostgreSQL 16 container defined in docker-compose.yml |
<!-- sdlc:auto:end run -->

<!-- sdlc:auto:start structure -->
| Path | Purpose |
|---|---|
| `backend/app` | FastAPI application: main.py (entrypoint, CORS, /health), database.py (engine/session), models.py (SQLAlchemy models, currently empty), schemas.py (Pydantic models, incl. StubResponse), routers/ (one router per architecture component, currently empty) |
| `backend/tests` | Pytest suite: unit/ and integration/ tests (integration/test_health.py exercises the health endpoint) |
| `frontend/src` | React app source: main.tsx (app bootstrap/router), lib/ (api.ts client, ui.tsx, icons.tsx, navigate.ts), index.css (brand/theme tokens) |
| `frontend/e2e` | Playwright end-to-end specs (e.g. example.spec.ts) and support helpers (support/admin.ts) |
| `.devcontainer` | VS Code devcontainer configuration for a consistent development environment |
| `.quorq` | Platform metadata (handoff.json) used by the Quorq AI SDLC platform |
| `docker-compose.yml` | Optional PostgreSQL 16 service definition for local development against a real database |
<!-- sdlc:auto:end structure -->

<!-- sdlc:auto:start conventions -->
- Backend routes are organized as one router per architecture component under app/routers/, registered in main.py
- Generated/unimplemented endpoints return a typed StubResponse (schemas.py) rather than raising, keeping the OpenAPI spec complete before handlers exist
- SQLAlchemy models all inherit from the shared Base in app/database.py; tables are created on app startup via Base.metadata.create_all, with no migration tool yet in place
- Database connection is configured via the DATABASE_URL env var, defaulting to a local SQLite file for zero-dependency local runs
- CORS allowed origins are configured via the ALLOWED_ORIGINS env var (comma-separated), falling back to the Vite dev server origins in development
- Frontend screens live under src/screens/ (one module per approved screen) and currently render seeded sample data rather than calling the API
- frontend/src/lib/api.ts is the single seam for backend calls: apiFetch() attaches a bearer token (session token if present, else VITE_API_SECRET_KEY) and is the intended place to wire screens to real endpoints
- Frontend uses path alias @/ mapped to src/ (see tsconfig.json and vite.config.ts)
- Vitest component tests live beside the components they test under src/; Playwright e2e specs live separately under e2e/
<!-- sdlc:auto:end conventions -->

<!-- sdlc:auto:start testing -->
| Name | Command | Description |
|---|---|---|
| backend tests | `pytest` | Runs backend unit and integration tests (from backend/); pythonpath is set via pytest.ini |
| backend lint | `ruff check .` | Lints the backend Python code |
| backend format | `ruff format .` | Formats the backend Python code |
| frontend unit tests | `npm run test` | Runs Vitest component tests under src/ |
| frontend lint | `npm run lint` | Runs ESLint over the frontend app |
| frontend typecheck | `npm run typecheck` | Runs tsc --noEmit (not run by npm run build) |
| frontend e2e install | `npm run test:e2e:install` | Installs the Chromium browser needed for Playwright |
| frontend e2e tests | `npm run test:e2e` | Runs Playwright specs from e2e/; without E2E_BASE_URL it boots the backend and a production build of the frontend locally |
<!-- sdlc:auto:end testing -->

<!-- sdlc:auto:start troubleshooting -->
| Problem | Solution |
|---|---|
| Frontend dev server calls to the backend are blocked by the browser (CORS error) | Ensure the backend is running and, if the frontend origin differs from http://localhost:5173 or http://127.0.0.1:5173, set the ALLOWED_ORIGINS env var on the backend to include it |
| `pytest` run from backend/ fails to import app | Run pytest from the backend/ directory so pytest.ini's `pythonpath = .` applies, or run `cd backend && pytest` |
| Playwright e2e tests fail to start the backend | The webServer config expects backend/.venv/bin/python with dependencies installed; create that venv and `pip install -r requirements.txt` inside backend/.venv before running npm run test:e2e |
| `npm run build` succeeds but the app is broken at deploy time | Run `npm run typecheck` separately, since build does not run tsc and generated screens can have type errors it would catch |
| Backend fails to connect to a database | Unset DATABASE_URL to fall back to the local SQLite file, or start the Postgres service with `docker-compose up db` and set DATABASE_URL to match its credentials before running uvicorn |
<!-- sdlc:auto:end troubleshooting -->
