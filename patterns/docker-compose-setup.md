# 🐳 Docker Compose in 4 Services

> Small stack (nginx + backend + PostgreSQL + Redis) with local–prod parity and a focus on the why, not just the YAML.

---

## What it solves

- Parity: same topology locally and in production to reproduce bugs fast.
- Order: nginx in front, app in the middle, data at the back; a single internal network.
- Reliability: health checks before booting dependencies; defensive restart policy.
- Safe data: named volumes so sessions and tables survive restarts.
- Operable: wait/migration scripts included.

## Quick map

```
┌─────────────────────────────────────────────┐
│           Docker Network (bridge)           │
│                                             │
│  ┌─────────┐  ┌─────────┐  ┌───────────┐    │
│  │  Nginx  │  │ Backend │  │ PostgreSQL│    │
│  │  :80    │──│  :3000  │──│  :5432    │    │
│  └─────────┘  └─────────┘  └───────────┘    │
│                     │                       │
│                ┌─────────┐                  │
│                │  Redis  │                  │
│                │  :6379  │                  │
│                └─────────┘                  │
└─────────────────────────────────────────────┘

```

## Design (why this way)

- nginx: serves static assets and proxies API, keeps URLs clean.
- backend: only starts after DB and Redis are healthy; runs migrations before serving.
- postgres: `pgdata` volume, health check via `pg_isready`, no secrets baked into YAML.
- redis: cache/sessions with AOF on; health check via `redis-cli ping`.

## Minimum env (.env.production)

```bash
NODE_ENV=production
PG_HOST=postgres
PG_USER=myuser
PG_PASSWORD=securepassword
PG_DBNAME=mydb
REDIS_HOST=redis
SESSION_SECRET=generated-64-bytes
CSRF_SECRET_KEY=generated-64-bytes
```

## Essential Compose (trimmed)

```yaml
version: '3.8'

services:
  backend:
    build: .
    depends_on:
      postgres:
        condition: service_healthy
      redis:
        condition: service_healthy
    environment:
      PGHOST: postgres
      REDIS_HOST: redis
    command: >
      sh -c "sh ./scripts/deploy/wait-for-db.sh postgres 5432 \
      && sh ./scripts/deploy/run-migrations.sh \
      && node ./server/app.mjs --environment=production"
    restart: unless-stopped

  postgres:
    image: postgres:15-alpine
    volumes:
      - pgdata:/var/lib/postgresql/data
    healthcheck:
      test: ['CMD-SHELL', 'pg_isready -U ${PG_USER} -d ${PG_DBNAME}']

  redis:
    image: redis:7-alpine
    command: redis-server --appendonly yes
    healthcheck:
      test: ['CMD', 'redis-cli', 'ping']

volumes:
  pgdata:
  redis_data:
```

> The full YAML lives in the repo; this keeps the intent clear: wait for dependencies, migrate before serving, and persist data.

## Handy scripts

- `wait-for-db.sh`: blocks until PostgreSQL responds (avoids slow-start failures).
- `run-migrations.sh`: applies SQL in order; assumes idempotent migrations. See [database-migrations.md](database-migrations.md#-best-practices) for details.

## Production notes

- Use non-root users in images and `no-new-privileges` where it applies.
- Inject secrets via env/secret managers in CI/CD, not in the repo.
- Add CPU/RAM limits if the host is shared.
- Backups: `pg_dumpall` from the container and Redis AOF/RDB.

## Related

- [redis-session-strategy.md](redis-session-strategy.md)
- [database-migrations.md](database-migrations.md)

<p align="center">
  <i>Containerized for consistency, orchestrated for reliability</i>
</p>
