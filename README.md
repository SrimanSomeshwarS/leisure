# Leisure backend: Batch 1 (foundation + authentication)

Python 3.12 - FastAPI - MySQL 8 - SQLAlchemy 2 - Alembic - Argon2id. Phase 1 modules arrive in later batches.
Read `docs/decisions.md` first (commercial rules, cash payments, domain limitation).

## Run locally (needs Docker Desktop)
```bash
cp .env.example .env            # then edit every CHANGE_ME (SECRET_KEY: python -c "import secrets; print(secrets.token_urlsafe(48))")
docker compose up --build       # API http://localhost:8000/api/v1/docs  |  inbox http://localhost:8025
docker compose run --rm api pytest      # tests run against a separate MySQL database: leisure_test
docker compose exec api python -m scripts.create_manager --email you@yourdomain --name "Your Name"
```
Daily maintenance: `python -m scripts.housekeeping`.

## What exists in Batch 1
Register (customer/host), email verification, login/logout/logout-all, password reset + change (single-use expiring
tokens, sessions revoked), MySQL-backed rate limits, CSRF + Origin checks, strict CORS, role guards, audit log,
feature flags (`GET /api/v1/features`), 503/501 stubs for shared cab and parcels, health checks, JSON logs with redaction.

## Not built yet
Listings, availability, discovery, bookings, cash flow, commission ledger, manager endpoints, photo upload
(Batches 2-6), cab and parcel modules (Phase 2/3). Nothing here is production-ready until the launch checklist (Batch 7).
