---
id: TASK-007
title: Fix database setup and commit the initial migration
status: To Do
assignee: []
created_date: '2026-09-15 02:32'
updated_date: '2026-09-15 13:04'
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
Make database setup work from a fresh clone. Fix the root database commands and Docker Compose setup, then regenerate the final auth schema with the pinned Better Auth CLI and commit one initial Drizzle migration.

This is the database pass we intentionally saved until auth and dependency work were finished.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 Root db commands work without a separate dotenv executable, and an explicitly supplied DATABASE_URL wins over apps/server/.env.
- [ ] #2 Docker Compose maps DB_PORT to container port 5432, uses starter-neutral names, and waits for a passing pg_isready healthcheck.
- [ ] #3 Empty migrate, seed, and settings schema files are deleted.
- [ ] #4 The pinned Better Auth command replaces auth-schema.ts and fails if it produces an empty or missing file.
- [ ] #5 The generated schema contains only the user, session, account, and verification tables and their required relations.
- [ ] #6 No admin, organization, invitation, member, two-factor, ban, role, impersonation, or active-organization fields remain.
- [ ] #7 One reviewed initial Drizzle migration and its metadata are committed.
- [ ] #8 pnpm db:migrate succeeds twice against a new PostgreSQL 17 database.
- [ ] #9 pnpm format, pnpm lint, pnpm typecheck, and pnpm build pass.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria are met
- [ ] #2 Relevant tests and quality checks pass
- [ ] #3 Documentation is updated when behavior or setup changes (if documentation exists)
<!-- DOD:END -->
