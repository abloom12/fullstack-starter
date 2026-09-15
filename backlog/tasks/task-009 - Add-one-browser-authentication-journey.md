---
id: TASK-009
title: Add one browser authentication journey
status: To Do
assignee: []
created_date: '2026-09-15 02:33'
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
The starter has no browser-level proof that its frontend, Better Auth routes, cookies, protected navigation, and PostgreSQL schema work together. Add one intentionally narrow Playwright journey for the agreed core authentication contract. Avoid broad UI coverage or application-feature tests.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 Playwright is installed as development-only test tooling with one Chromium project.
- [ ] #2 Browser test configuration starts or connects to the API and web applications with explicit test environment values.
- [ ] #3 The test setup uses a disposable PostgreSQL database and never inherits the normal developer database implicitly.
- [ ] #4 The journey creates a unique user through the signup page.
- [ ] #5 Successful signup reaches the protected settings page.
- [ ] #6 The journey logs out and confirms protected navigation redirects to login.
- [ ] #7 The journey logs in again with the created credentials and regains protected access.
- [ ] #8 The browser journey runs serially in CI and cleans up owned application processes.
- [ ] #9 Playwright configuration and test source are included in TypeScript checking.
- [ ] #10 Root and web package commands expose the browser test for reuse by CI.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria are met
- [ ] #2 Relevant tests and quality checks pass
- [ ] #3 Documentation is updated when behavior or setup changes (if documentation exists)
<!-- DOD:END -->
