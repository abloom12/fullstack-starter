---
id: TASK-008
title: Add server integration and production startup tests
status: To Do
assignee: []
created_date: '2026-09-15 02:32'
labels: []
dependencies:
  - TASK-007
references:
  - docs/simplification-plan.md
modified_files:
  - apps/server/src
  - apps/server/test
  - apps/server/package.json
  - apps/server/tsconfig.json
  - apps/server/tsconfig.test.json
  - package.json
  - turbo.json
  - scripts
priority: high
type: task
ordinal: 8000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
The API, auth adapter, resource cleanup, and production-only startup path currently have no automated coverage. Add a small server-focused suite that exercises Fastify without opening a normal test port and a smoke check that proves the built API runs with production dependencies, answers health requests, and terminates cleanly. This is verification infrastructure, not a hosting or container recipe.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 Server tests use the Node test runner through the existing TypeScript execution tooling without adding a mocking framework.
- [ ] #2 Application construction is testable independently from network listening.
- [ ] #3 A test verifies the public health.ping procedure succeeds with the expected response.
- [ ] #4 A test verifies anonymous access to health.me returns an unauthorized tRPC response.
- [ ] #5 Server tests close Fastify and all PostgreSQL resources even when an assertion fails.
- [ ] #6 Test source is included in typechecking but excluded from the production server build.
- [ ] #7 An automated smoke command creates or installs a production dependency tree without relying on development dependencies.
- [ ] #8 The production smoke starts the built API with NODE_ENV=production and waits for a successful health response.
- [ ] #9 The production smoke sends SIGTERM, observes a clean exit, and always cleans up its child process on failure.
- [ ] #10 Production smoke output uses structured logging and contains no pino-pretty resolution failure.
- [ ] #11 Root commands expose the server test and production smoke checks for reuse by CI.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria are met
- [ ] #2 Relevant tests and quality checks pass
- [ ] #3 Documentation is updated when behavior or setup changes (if documentation exists)
<!-- DOD:END -->
