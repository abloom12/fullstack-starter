---
id: TASK-005
title: Upgrade dependencies and remove unused packages
status: To Do
assignee: []
created_date: '2026-09-15 02:32'
updated_date: '2026-09-15 13:04'
labels: []
dependencies:
  - TASK-004
references:
  - docs/simplification-plan.md
modified_files:
  - package.json
  - pnpm-workspace.yaml
  - pnpm-lock.yaml
  - apps/server/package.json
  - apps/web/package.json
  - packages/api/package.json
  - packages/auth/package.json
  - packages/db/package.json
priority: high
type: chore
ordinal: 5000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Update the remaining vulnerable packages and remove dependencies left behind by the auth and frontend cleanup. This includes Fastify and its plugins, Vite, Turbo, duplicate Better Auth adapters, unused UI packages, and unused devtools.

Keep the changes in the normal dependency graph. Do not use forced audit fixes or broad overrides to hide advisories.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 Fastify, its plugins, Vite, Turbo, and other direct dependencies with available security fixes are upgraded to compatible versions.
- [ ] #2 Duplicate Better Auth adapter packages and packages no longer imported by the app are removed.
- [ ] #3 Development-only build and test tools are not listed as production dependencies.
- [ ] #4 Every internal workspace package has private: true.
- [ ] #5 The lockfile is updated without audit --fix --force or broad dependency overrides.
- [ ] #6 pnpm install --frozen-lockfile succeeds.
- [ ] #7 pnpm audit --prod --audit-level high reports no high or critical vulnerabilities.
- [ ] #8 pnpm format, pnpm lint, pnpm typecheck, and pnpm build pass.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria are met
- [ ] #2 Relevant tests and quality checks pass
- [ ] #3 Documentation is updated when behavior or setup changes (if documentation exists)
<!-- DOD:END -->
