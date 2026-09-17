---
id: TASK-016
title: Establish the reproducible authentication database baseline
status: To Do
assignee: []
created_date: '2026-09-17 00:34'
labels: []
dependencies:
  - TASK-015
documentation:
  - doc-001
ordinal: 16000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Make local database setup reproducible and commit the migration baseline for core email/password authentication. This is the first task allowed to replace the final auth schema and establish migration history.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 Root database commands work without a separate standalone dotenv executable.
- [ ] #2 Explicit DATABASE_URL values take precedence over local environment files.
- [ ] #3 Local startup uses PostgreSQL 17, maps the configured host port to container port 5432, uses neutral resource names, and reports readiness through pg_isready.
- [ ] #4 Root Compose interpolation values remain distinct from the server runtime DATABASE_URL.
- [ ] #5 Database credentials and URLs are runtime inputs rather than image contents.
- [ ] #6 Local environment files remain excluded from Docker build contexts, and build-context configuration contains no stale application references.
- [ ] #7 Empty or misleading migration, seed, settings, and schema modules are absent.
- [ ] #8 Pinned schema generation fails for missing or empty output.
- [ ] #9 The final schema contains only user, session, account, verification, and their required relations.
- [ ] #10 Advanced-auth tables and fields are absent.
- [ ] #11 One reviewed initial migration and its metadata establish the baseline for future incremental migrations.
- [ ] #12 A fresh PostgreSQL 17 database accepts the migration, and running it again is safe.
- [ ] #13 Format, lint, typecheck, and build pass.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria are met
- [ ] #2 Relevant tests and quality checks pass
- [ ] #3 Documentation is updated when behavior or setup changes (if documentation exists)
<!-- DOD:END -->
