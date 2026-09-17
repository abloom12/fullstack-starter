---
id: TASK-015
title: Produce a secure reproducible dependency graph
status: To Do
assignee: []
created_date: '2026-09-17 00:34'
labels: []
dependencies:
  - TASK-014
documentation:
  - doc-001
ordinal: 15000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Pin compatible authentication tooling, upgrade vulnerable dependencies, and remove packages belonging only to unsupported product features without pruning the reusable UI inventory or retained development overlays.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 Better Auth runtime and schema tooling use the same reviewed, lockfile-pinned version.
- [ ] #2 Authentication schema generation uses explicit email/password-only configuration and no unpinned or @latest invocation.
- [ ] #3 The authentication CLI configuration requires no database or production values, is typechecked, and is excluded from production package output.
- [ ] #4 The pinned generator produces a non-empty PostgreSQL schema in a disposable location.
- [ ] #5 Direct dependencies with applicable security fixes use compatible reviewed versions.
- [ ] #6 Duplicate adapters and dependencies belonging only to removed authentication or product features are absent.
- [ ] #7 Every reusable component and retained development overlay continues to resolve its required dependencies.
- [ ] #8 Development-only build and test tools are not production dependencies.
- [ ] #9 Every internal workspace package is private.
- [ ] #10 Frozen-lockfile installation succeeds.
- [ ] #11 Production audit reports no high or critical advisories.
- [ ] #12 No forced audit fix or broad override conceals advisories.
- [ ] #13 Format, lint, typecheck, and build pass.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria are met
- [ ] #2 Relevant tests and quality checks pass
- [ ] #3 Documentation is updated when behavior or setup changes (if documentation exists)
<!-- DOD:END -->
