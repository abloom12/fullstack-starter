---
id: TASK-001
title: Strip auth down to email and password
status: To Do
assignee: []
created_date: '2026-09-15 02:07'
updated_date: '2026-09-15 12:54'
labels: []
dependencies: []
references:
  - docs/simplification-plan.md
modified_files:
  - packages/auth/src/index.ts
  - apps/server/src/env.ts
  - apps/server/src/app.ts
  - apps/server/.env.example
  - apps/web/src/lib/auth-client.ts
  - README.md
priority: high
type: chore
ordinal: 1000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
We only want basic email/password auth in this starter. Right now Better Auth also enables admin tools, organizations, two-factor auth, OpenAPI, the Have I Been Pwned password check, and optional Google login. None of those features has a complete workflow, so remove them from the server and browser setup.

Keep signup, login, sessions, logout, profile updates, and password changes. Do not regenerate the auth schema or create migrations in this task; that will happen after the Better Auth upgrade in TASK-004 and during the database work in TASK-007.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 packages/auth/src/index.ts contains no advanced plugins, Google provider, or plugin-specific synthetic user fields.
- [ ] #2 createAuth only requires the database, app origin, auth URL, and secret.
- [ ] #3 Google credentials and wiring are removed from server configuration and apps/server/.env.example.
- [ ] #4 apps/web/src/lib/auth-client.ts contains only the core auth client and its Session and User types; plugin clients and unused error-code scaffolding are gone.
- [ ] #5 The README no longer tells users how to configure Google or claims advanced auth support.
- [ ] #6 Existing signup, login, logout, profile-update, and password-change route code still compiles.
- [ ] #7 pnpm build passes.
- [ ] #8 The database schema and migrations are unchanged by this task.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria are met
- [ ] #2 Relevant tests and quality checks pass
- [ ] #3 Documentation is updated when behavior or setup changes (if documentation exists)
<!-- DOD:END -->
