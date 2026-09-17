---
id: TASK-017
title: Make the API lifecycle production-safe
status: To Do
assignee: []
created_date: '2026-09-17 00:35'
labels: []
dependencies:
  - TASK-016
documentation:
  - doc-001
ordinal: 17000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Make configuration, logging, database ownership, startup, and shutdown safe across development, test, and production, with automated verification through Fastify and the built server process.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 Development logging is readable, tests can disable logging, and production emits JSON without loading pino-pretty.
- [ ] #2 Validated server configuration distinguishes development, test, and production.
- [ ] #3 Missing or invalid browser API URL configuration produces a clear startup or build failure.
- [ ] #4 Production rejects the public example authentication secret.
- [ ] #5 Closing Fastify waits for PostgreSQL resources to close.
- [ ] #6 SIGINT and SIGTERM initiate shutdown no more than once without immediate successful-path process.exit().
- [ ] #7 Fastify can be constructed for tests without opening a port.
- [ ] #8 Node tests verify successful health.ping and anonymous health.me authorization failure.
- [ ] #9 Tests close all Fastify and PostgreSQL resources, are typechecked, and are excluded from production output.
- [ ] #10 Root commands expose the API tests and production smoke check.
- [ ] #11 The production smoke uses the built server and production dependencies, waits for health, sends SIGTERM, and requires exit code 0.
- [ ] #12 The production smoke does not rely on pino-pretty and cleans up on failure.
- [ ] #13 Format, lint, typecheck, and build pass.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria are met
- [ ] #2 Relevant tests and quality checks pass
- [ ] #3 Documentation is updated when behavior or setup changes (if documentation exists)
<!-- DOD:END -->
