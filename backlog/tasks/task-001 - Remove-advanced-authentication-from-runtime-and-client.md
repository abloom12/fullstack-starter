---
id: TASK-001
title: Remove advanced authentication from runtime and client
status: To Do
assignee: []
created_date: '2026-09-15 02:07'
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
The starter currently exposes unfinished Better Auth capabilities without supported UI or authorization coverage, increasing endpoint, configuration, client-type, and security surface beyond the agreed email/password scaffold.

Reduce active authentication to the supported core flow. Database schema regeneration and migration creation are deliberately deferred until Better Auth and the remaining dependencies have been upgraded. Package-manifest and lockfile pruning are also handled by the later dependency task.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 Server authentication supports email/password signup and login, sessions, logout, profile updates, and password changes.
- [ ] #2 Admin, organization, two-factor, OpenAPI, HIBP, and social-provider plugins are absent from runtime configuration.
- [ ] #3 The createAuth contract no longer accepts plugin-specific or Google-specific options.
- [ ] #4 Server environment parsing and configuration no longer accept or expose Google credentials.
- [ ] #5 The server environment example no longer contains Google variables.
- [ ] #6 The browser auth client has no advanced client plugins.
- [ ] #7 Unused auth error mapping and autocomplete-dump scaffolding are removed.
- [ ] #8 Session and User client types remain available to routes.
- [ ] #9 Active setup documentation no longer claims Google or advanced auth support.
- [ ] #10 Auth, API, server, and web packages build successfully.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria are met
- [ ] #2 Relevant tests and quality checks pass
- [ ] #3 Documentation is updated when behavior or setup changes (if documentation exists)
<!-- DOD:END -->
