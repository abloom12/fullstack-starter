---
id: TASK-019
title: Enforce starter contracts in CI
status: To Do
assignee: []
created_date: '2026-09-17 00:35'
labels: []
dependencies:
  - TASK-017
  - TASK-018
documentation:
  - doc-001
ordinal: 19000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Enforce dependency, quality, database, API, browser, production, and security contracts from a clean checkout using the repository-pinned toolchain.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 CI runs for pull requests and pushes to main with pinned Node and pnpm versions.
- [ ] #2 CI starts healthy PostgreSQL 17 with test-only credentials.
- [ ] #3 CI supplies all environment values without ignored local files.
- [ ] #4 CI performs frozen install, format, lint, typecheck, and build.
- [ ] #5 CI fails on high or critical production advisories.
- [ ] #6 CI initializes a fresh database and verifies migration rerun safety.
- [ ] #7 CI runs API tests, production startup and shutdown smoke, and the browser authentication journey.
- [ ] #8 The workflow contains no placeholders and requires no pre-existing Turbo cache.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria are met
- [ ] #2 Relevant tests and quality checks pass
- [ ] #3 Documentation is updated when behavior or setup changes (if documentation exists)
<!-- DOD:END -->
