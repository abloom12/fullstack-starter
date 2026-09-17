---
id: TASK-018
title: Verify the browser authentication journey
status: To Do
assignee: []
created_date: '2026-09-17 00:35'
labels: []
dependencies:
  - TASK-016
documentation:
  - doc-001
ordinal: 18000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Prove through one browser journey that the web app, API, cookies, authentication runtime, and database work together for the supported account flow.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 Playwright is a development-only dependency configured for Chromium.
- [ ] #2 Playwright configuration and tests are typechecked without entering production output.
- [ ] #3 Tests use explicit values and a disposable PostgreSQL database rather than normal local environment files.
- [ ] #4 A unique user signs up and reaches protected settings.
- [ ] #5 The user logs out, and direct settings access redirects to login.
- [ ] #6 The same account logs back in and reaches settings.
- [ ] #7 The journey runs serially in CI.
- [ ] #8 Application processes stop on success and failure.
- [ ] #9 Root and web commands expose the browser test.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria are met
- [ ] #2 Relevant tests and quality checks pass
- [ ] #3 Documentation is updated when behavior or setup changes (if documentation exists)
<!-- DOD:END -->
