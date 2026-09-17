---
id: TASK-008
title: Add API tests and a production startup smoke test
status: To Do
assignee: []
created_date: '2026-09-15 02:32'
updated_date: '2026-09-15 13:04'
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
Add a small test suite for the API behavior we keep and a script that catches production-only startup failures. Use Node test through tsx; we do not need a separate test framework or mocks.

The production check must use a production dependency tree, start the built API, call health.ping, send SIGTERM, and confirm a clean exit.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 The Fastify app can be created for tests without opening a network port.
- [ ] #2 A Node test checks the successful health.ping response.
- [ ] #3 A Node test checks that health.me returns UNAUTHORIZED without a session.
- [ ] #4 Tests always close Fastify and PostgreSQL resources.
- [ ] #5 Server tests are typechecked but are not emitted in the production build.
- [ ] #6 The production smoke uses the built server with production dependencies and does not rely on pino-pretty.
- [ ] #7 The smoke waits for health.ping, sends SIGTERM, confirms exit code 0, and cleans up the child process when it fails.
- [ ] #8 Root scripts expose the server tests and production smoke command.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria are met
- [ ] #2 Relevant tests and quality checks pass
- [ ] #3 Documentation is updated when behavior or setup changes (if documentation exists)
<!-- DOD:END -->
