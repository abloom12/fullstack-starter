---
id: TASK-007
title: Create the final reproducible database baseline
status: To Do
assignee: []
created_date: '2026-09-15 02:32'
labels: []
dependencies:
  - TASK-006
references:
  - docs/simplification-plan.md
modified_files:
  - package.json
  - docker-compose.yml
  - packages/auth/package.json
  - packages/auth/auth.cli.ts
  - packages/db/package.json
  - packages/db/drizzle.config.ts
  - packages/db/src/schema.ts
  - packages/db/src/schemas/auth-schema.ts
  - packages/db/src/migrations
  - packages/db/src/migrate.ts
  - packages/db/src/seed.ts
  - packages/db/src/schemas/settings.ts
priority: high
type: chore
ordinal: 7000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
A fresh clone cannot currently initialize PostgreSQL because no migration is committed, root database commands invoke a missing dotenv executable, and local Compose configuration has incorrect port and stale naming behavior. With auth scope and dependency versions finalized, regenerate the core Better Auth schema and commit one reviewed initial migration that makes database setup deterministic.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 Root database commands work without requiring a standalone dotenv executable.
- [ ] #2 An injected DATABASE_URL takes precedence and loading apps/server/.env remains optional for local commands.
- [ ] #3 Docker Compose maps the configured host port to PostgreSQL container port 5432.
- [ ] #4 Docker Compose uses starter-neutral database and volume naming.
- [ ] #5 PostgreSQL has a pg_isready healthcheck and the documented startup command waits for readiness.
- [ ] #6 Empty or misleading migrate, seed, and settings schema modules are removed.
- [ ] #7 The pinned Better Auth generator reproducibly replaces the final auth schema and fails when it produces no output.
- [ ] #8 The final auth schema contains only the core user, session, account, and verification model required by accepted authentication scope.
- [ ] #9 The final auth schema contains no advanced-plugin tables, relations, or columns.
- [ ] #10 One reviewed initial Drizzle migration and its metadata are committed.
- [ ] #11 The migration succeeds against an empty PostgreSQL 17 database.
- [ ] #12 Running the migration command a second time succeeds without pending changes.
- [ ] #13 Format, lint, typecheck, and build gates remain green.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria are met
- [ ] #2 Relevant tests and quality checks pass
- [ ] #3 Documentation is updated when behavior or setup changes (if documentation exists)
<!-- DOD:END -->
