---
id: TASK-012
title: Reduce authentication to email and password
status: To Do
assignee: []
created_date: '2026-09-17 00:34'
labels: []
dependencies: []
documentation:
  - doc-001
ordinal: 12000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Remove unsupported authentication capabilities while preserving core account and session flows. The final database schema and migration baseline are intentionally handled by the database-baseline task.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 Server authentication enables only email/password authentication and sessions.
- [ ] #2 Google OAuth and the admin, organization, two-factor, OpenAPI, and breached-password plugins are absent.
- [ ] #3 Authentication configuration requires only the database, application origin, authentication URL, and secret.
- [ ] #4 Plugin-specific synthetic fields and unused authentication error scaffolding are absent.
- [ ] #5 The browser authentication client exposes only core behavior and its session and user types.
- [ ] #6 Google credentials and application wiring are absent.
- [ ] #7 Signup, login, logout, profile-update, and password-change routes retain their supported behavior.
- [ ] #8 Email verification and password-reset workflows are not exposed.
- [ ] #9 The application builds without changing the final database schema or migration history.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria are met
- [ ] #2 Relevant tests and quality checks pass
- [ ] #3 Documentation is updated when behavior or setup changes (if documentation exists)
<!-- DOD:END -->
