---
id: TASK-006
title: Harden runtime configuration and shutdown behavior
status: To Do
assignee: []
created_date: '2026-09-15 02:32'
labels: []
dependencies:
  - TASK-005
references:
  - docs/simplification-plan.md
modified_files:
  - apps/server/src/server.ts
  - apps/server/src/app.ts
  - apps/server/src/env.ts
  - apps/server/.env.example
  - packages/db/src/index.ts
  - apps/web/src/lib/auth-client.ts
  - apps/web/src/lib/trpc.ts
  - apps/web/src/env.ts
  - apps/web/vite.config.ts
  - apps/web/.env.example
priority: high
type: chore
ordinal: 6000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
The production API currently attempts to load a development-only pretty logger, retains no handle for closing the PostgreSQL pool, and exits the process immediately after Fastify closes. Browser configuration can also construct an invalid API URL silently, while the public example auth secret is accepted in production. Establish explicit environment-specific runtime behavior before creating the final database baseline and automated smoke tests.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 Development logging remains human-readable through the development-only pretty transport.
- [ ] #2 Production logging emits structured JSON without resolving pino-pretty.
- [ ] #3 Test logging can be disabled or controlled without selecting the development transport.
- [ ] #4 The validated server configuration exposes the active environment explicitly.
- [ ] #5 The database factory retains the PostgreSQL pool and exposes an asynchronous close operation.
- [ ] #6 Fastify shutdown hooks await PostgreSQL pool closure.
- [ ] #7 SIGINT and SIGTERM initiate shutdown once and successful shutdown does not call process.exit immediately.
- [ ] #8 A missing or invalid VITE_API_URL fails with a clear configuration error before API requests are attempted.
- [ ] #9 Production startup rejects the public example Better Auth secret.
- [ ] #10 Format, lint, typecheck, and build gates remain green.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria are met
- [ ] #2 Relevant tests and quality checks pass
- [ ] #3 Documentation is updated when behavior or setup changes (if documentation exists)
<!-- DOD:END -->
