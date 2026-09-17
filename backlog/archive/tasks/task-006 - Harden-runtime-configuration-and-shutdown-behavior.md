---
id: TASK-006
title: 'Fix production logging, shutdown, and env validation'
status: To Do
assignee: []
created_date: '2026-09-15 02:32'
updated_date: '2026-09-15 13:04'
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
Fix the runtime problems already found in the API and web apps. Production must not load pino-pretty, the PostgreSQL pool must close with Fastify, and shutdown should finish normally instead of immediately calling process.exit.

Also validate VITE_API_URL before the web app uses it and reject the example auth secret when the server runs in production.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 Development uses pino-pretty, tests can disable logging, and production writes JSON logs without loading pino-pretty.
- [ ] #2 The validated server config exposes whether it is running in development, test, or production.
- [ ] #3 createDB returns a close function for its PostgreSQL pool, and the Fastify onClose hook awaits it.
- [ ] #4 SIGINT and SIGTERM close the server once, and a successful shutdown does not call process.exit immediately.
- [ ] #5 The web app reports a clear startup or build error when VITE_API_URL is missing or invalid.
- [ ] #6 The server refuses to start in production with the example BETTER_AUTH_SECRET.
- [ ] #7 pnpm format, pnpm lint, pnpm typecheck, and pnpm build pass.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria are met
- [ ] #2 Relevant tests and quality checks pass
- [ ] #3 Documentation is updated when behavior or setup changes (if documentation exists)
<!-- DOD:END -->
