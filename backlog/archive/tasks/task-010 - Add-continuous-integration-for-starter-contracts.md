---
id: TASK-010
title: Add GitHub Actions CI
status: To Do
assignee: []
created_date: '2026-09-15 02:33'
updated_date: '2026-09-15 13:04'
labels: []
dependencies:
  - TASK-008
  - TASK-009
references:
  - docs/simplification-plan.md
modified_files:
  - .github/workflows/ci.yml
  - package.json
  - turbo.json
priority: high
type: chore
ordinal: 10000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Add one GitHub Actions workflow that runs the checks and tests created by the earlier tasks. It should prove the starter works from a clean checkout with a fresh PostgreSQL database.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 CI runs on pull requests and pushes to main using the Node and pnpm versions pinned in the repo.
- [ ] #2 CI starts a healthy PostgreSQL 17 service with test-only credentials.
- [ ] #3 CI runs pnpm install --frozen-lockfile, format, lint, typecheck, and build.
- [ ] #4 CI fails on high or critical production dependency advisories.
- [ ] #5 CI runs the migration check, API tests, production startup smoke, and Playwright auth test.
- [ ] #6 All test environment variables are set in the workflow; ignored local env files are not required.
- [ ] #7 The workflow contains no placeholder commands and passes without relying on an existing Turbo cache.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria are met
- [ ] #2 Relevant tests and quality checks pass
- [ ] #3 Documentation is updated when behavior or setup changes (if documentation exists)
<!-- DOD:END -->
