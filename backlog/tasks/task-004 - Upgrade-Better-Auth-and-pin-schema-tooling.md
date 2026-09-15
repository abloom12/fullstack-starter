---
id: TASK-004
title: Upgrade Better Auth and pin schema tooling
status: To Do
assignee: []
created_date: '2026-09-15 02:32'
labels: []
dependencies:
  - TASK-003
references:
  - docs/simplification-plan.md
modified_files:
  - pnpm-workspace.yaml
  - pnpm-lock.yaml
  - packages/auth/package.json
  - packages/auth/auth.cli.ts
  - packages/auth/src/index.ts
  - packages/auth/tsconfig.json
  - packages/auth/tsconfig.build.json
priority: high
type: chore
ordinal: 4000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Better Auth is pinned to a vulnerable runtime release while schema generation invokes an arbitrary latest CLI without a loadable explicit configuration. Upgrade the runtime and schema tooling together so the final core schema can later be regenerated reproducibly. The committed database schema and migration remain deferred to the database-baseline task.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 Better Auth runtime packages use one reviewed compatible version across the workspace.
- [ ] #2 The Better Auth schema CLI is a lockfile-pinned development dependency compatible with the runtime version.
- [ ] #3 No schema-generation command uses pnpm dlx, latest, or another unpinned executable.
- [ ] #4 Schema generation uses an explicit CLI-only auth configuration containing only the accepted core auth options.
- [ ] #5 The CLI-only configuration requires no live PostgreSQL connection or production secret.
- [ ] #6 The CLI-only configuration is typechecked but excluded from the runtime library build.
- [ ] #7 The pinned CLI successfully generates a non-empty core PostgreSQL schema to a disposable output location.
- [ ] #8 No final auth schema or Drizzle migration is committed by this task.
- [ ] #9 Frozen installation and all existing quality gates pass after the upgrade.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria are met
- [ ] #2 Relevant tests and quality checks pass
- [ ] #3 Documentation is updated when behavior or setup changes (if documentation exists)
<!-- DOD:END -->
