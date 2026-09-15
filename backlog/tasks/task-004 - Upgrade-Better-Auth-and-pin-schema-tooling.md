---
id: TASK-004
title: Upgrade Better Auth and pin its schema generator
status: To Do
assignee: []
created_date: '2026-09-15 02:32'
updated_date: '2026-09-15 13:04'
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
Upgrade Better Auth to a patched version and stop generating schemas with auth@latest. The runtime and generator should use the same pinned version.

Add the CLI config needed to generate our email/password schema, but generate only a temporary file for verification. TASK-007 will replace the real schema and create the migration.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 better-auth and the auth CLI use the same reviewed, lockfile-pinned version.
- [ ] #2 No auth command uses pnpm dlx or an @latest version.
- [ ] #3 The generator uses an explicit CLI config containing only the email/password auth options.
- [ ] #4 The CLI config does not need a database connection or production environment values.
- [ ] #5 The CLI config is included in typechecking and excluded from the auth package build.
- [ ] #6 The pinned command generates a non-empty PostgreSQL schema to a temporary location.
- [ ] #7 packages/db/src/schemas/auth-schema.ts and the migrations directory are unchanged by this task.
- [ ] #8 pnpm install --frozen-lockfile, pnpm typecheck, and pnpm build pass.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria are met
- [ ] #2 Relevant tests and quality checks pass
- [ ] #3 Documentation is updated when behavior or setup changes (if documentation exists)
<!-- DOD:END -->
