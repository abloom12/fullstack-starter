---
id: TASK-009
title: Add one Playwright auth test
status: To Do
assignee: []
created_date: '2026-09-15 02:33'
updated_date: '2026-09-15 13:04'
labels: []
dependencies:
  - TASK-007
references:
  - docs/simplification-plan.md
modified_files:
  - apps/web/package.json
  - apps/web/playwright.config.ts
  - apps/web/e2e
  - apps/web/tsconfig.test.json
  - package.json
  - pnpm-lock.yaml
priority: high
type: task
ordinal: 9000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Add one browser test for the auth flow we plan to keep. It should prove that the web app, API, cookies, and database work together without growing into a full UI test suite.

The test should sign up, open settings, log out, verify the protected redirect, and log back in.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 Playwright is installed as a development dependency and configured to run Chromium.
- [ ] #2 The test uses explicit test environment values and a disposable PostgreSQL database, not the normal local env files.
- [ ] #3 The test signs up a unique user and reaches the protected settings page.
- [ ] #4 The test logs out and confirms that opening settings redirects to login.
- [ ] #5 The test logs in with the same account and reaches settings again.
- [ ] #6 Playwright config and test files are typechecked.
- [ ] #7 The test runs serially in CI and shuts down app processes when it finishes or fails.
- [ ] #8 Root and web package scripts expose the Playwright test command.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria are met
- [ ] #2 Relevant tests and quality checks pass
- [ ] #3 Documentation is updated when behavior or setup changes (if documentation exists)
<!-- DOD:END -->
